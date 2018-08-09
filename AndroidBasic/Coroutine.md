# Coroutine 

코루틴은 “루틴" 상의 로컬 상태를 유지하면서 제어를 반환했다가(suspend), 제어권을 다시 획득했을 때(resume) 흐름을 이어갈 수 있다.
</br>
> 기존의 멀티테스킹 방식으론 버그 발생 여지가 많고 멀티쓰레드간 교착 상태 등 신경 쓸 부분이 많기 때문에 깔끔한 단일 쓰레드로 멀티테스킹을 구현한다 (멀티 쓰레드를 흉내)

> suspend / resume 이 가능하다. 함수가 call/return 되는 것과 비교해 일반화 된 형태 

## 어떻게 쓰레드를 사용하지 않고 멀티테스킹을 할까?
 코루틴 함수는 yield return 을 사용함으로써 위치를 기억하고 다음 호출 때 그곳에서 다음 실행을 할 수 있도록 한다. 따라서 여러 개 코루틴을 동작시키기고 다른 시점에 yield 가 반환되도록 하면 여러개 쓰레드가 돌아가며 동작하는 것과 같은 효과가 있다. <br>
 위에 말한 suspend와 resume 이 가능하단 의미는 종료할 때 완전히 삭제되는 게 아니라 현재 상태를 저장하고 있다는 얘기이다.  
 > suspend 될 때, 컨텍스트 객체에 다음 시작될 지점을 저장 
 > resume 될 때, 저장된 지점으로 점프 
```
 function co():
  <before>
  yield;
  <after>
// compile 후
function co(context):
  if (context.resumePoint == "L0") goto L0;
    <before>
    context.resumePoint = "L0";
    return;
  L0:
    <after>
```

## Enumerator 
일종의 코루틴 

## 코루틴의 종류 
* 대칭 : 코루틴 멈출 때 제어권을 넘겨받을 다른 코루틴 지정하는 방식 
* 비대칭 : 코루틴 멈추면 자동으로 코루틴에 제어권을 주었던 지점으로 되돌아 가는 방식 (좀 더 구조적 프로그래밍에 가깝)

> 대칭 코루틴 예제

```
var q := new queue
coroutine produce
    loop
        while q is not full
            create some new items
            add the items to q
        yield to consume
coroutine consume
    loop
        while q is not empty
            remove some items from q
            use the items
        yield to produce
```
> 비대칭 방식에 dispatch loop 를 더해 대칭 코루틴 모사 가능 
```
var q := new queue
generator produce
    loop
        while q is not full
            create some new items
            add the items to q
        yield consume
generator consume
    loop
        while q is not empty
            remove some items from q
            use the items
        yield produce
subroutine dispatcher
    var d := new dictionary(generator → iterator)
    d[produce] := start produce
    d[consume] := start consume
    var current := produce
    loop
        current := next d[current]
```

## 안드로이드 코틀린 코루틴 
kotlinx.coroutines 라이브러리에서 <strong>launch</strong> 이나 <strong>async</strong> 함수를 이용하야 새 동시 루틴을 시작할 수 있다. 
> launch 는 Job을 반환 (아무런 결과 값도 전달하지 않음)
> async는 Defered를 반환 (Defered는 <strong>.await()를 통해 최종 결과를 얻습니다</strong>.)
> + defered도 Job 이기 때문에 필요하면 취소할 수 있다. 

### 코루틴 Context 
* uiContext : 부모 코루틴은 Android 기본 UI 스레드로 실행 전달 
* bgContext : 자식 코루틴에서 쓰레드 풀로 실행 전달 
> 따라서 코루틴 작업이 예약되어도 모든 코어가 점유되면 대기열에 들어갑니다. 
>> newFixedPoolContext 또는 캐시 된 스레드 풀 구현을 고려할 수 있습니다. 

### 코루틴 실행 
* uiContext : UI Context -> launch를 통해 실행
* bgContext : CommonPool Context -> async를 통해 실행  
> 부모 코루틴은 항상 모든 하위 항목 완료를 기다립니다. 

#### 실행 pseudo 코드 
* Two tasks sequentially 
```
private fun loadData() = launch(uiContext) {
    view.showLoading() // ui thread
 
    // non ui thread, suspend until task is finished
    val result1 = async(bgContext) { dataProvider.loadData("Task 1") }.await()
 
    // non ui thread, suspend until task is finished
    val result2 = async(bgContext) { dataProvider.loadData("Task 2") }.await()
 
    val result = "$result1 $result2" // ui thread
 
    view.showData(result) // ui thread
}
```
* execute two tasks parallel
```
private fun loadData() = launch(uiContext) {
    view.showLoading() // ui thread
 
    val task1 = async(bgContext) { dataProvider.loadData("Task 1") }
    val task2 = async(bgContext) { dataProvider.loadData("Task 2") }
 
    val result = "${task1.await()} ${task2.await()}" // non ui thread, suspend until finished
 
    view.showData(result) // ui thread
}
```
* timeout 
```
private fun loadData() = launch(uiContext) {
    view.showLoading() // ui thread
 
    val task = async(bgContext) { dataProvider.loadData("Task") }
 
    // non ui thread, suspend until the task is finished or return null in 2 sec
    val result = withTimeoutOrNull(2, TimeUnit.SECONDS) { task.await() }
 
    view.showData(result) // ui thread
}
```
* cancel 
 취소 될수 있는 Job 객체를 반환한다.
 > 부모 코루틴이 취소되면 모든 자식도 재귀적으로 취소 
```
var job: Job? = null
 
fun startPresenting() {
    job = loadData()
}
 
fun stopPresenting() {
    job?.cancel()
}
 
private fun loadData() = launch(uiContext) {
    view.showLoading() // ui thread
 
    val task = async(bgContext) { dataProvider.loadData("Task") }
    val result = task.await() // non ui thread, suspend until finished
 
    view.showData(result) // ui thread
}
```
dataProvider.loadData가 아직 진행 중일 때 stopPresenting 함수가 호출 된 경우 view.showData 함수는 호출되지 않습니다



### Reference 
[Medium 한주영님 포스팅 - Coroutine이란](https://medium.com/@jooyunghan/%EC%BD%94%EB%A3%A8%ED%8B%B4-%EC%86%8C%EA%B0%9C-504cecc89407)
[Teddy 블로그](http://teddy.tistory.com/22)
[Medium 김태수님 포스팅 - Android Coroutine](https://medium.com/@kimtaesoo188/kotlin-weekly-63-android-coroutine-recipes-e077cb5f3d97)
[amuyu github 예제 소스](https://github.com/amuyu/SampleCoroutines)
