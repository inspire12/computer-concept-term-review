# ViewModel 
## 개요
화면 전환 같은 구성변경에 대응하는 모델입니다. <br>
안드로이드 생명주기 때문에 여러 진입 케이스에 따른 복잡성이 많은데 특히 런타임 중 화면 회전 같이 화면 구성이 변경될 경우 엑티비티를 종료하고 메모리에서 제거 후 다시 생성하는 과정을 거쳐 종속된 UI데이터를 유지하는 것이 손이 많이 갔습니다. <br>

### 화면 회전에 대한 이전 해결책 
1. onSaveInstanceState() 콜백 이용
 - 직렬화 할 수 없는 객체는 저장이 불가능 (애초에 큰 데이터용으로 설계 된게 아님)
2. fragment 하나를 UI 없는 워커 fragment로 setRetainInstance(true)로 
 - 엣지케이스 처리 문제

## ViewModel 
 
액티비티와 프래그먼트에서 사용되는 UI 관련 데이터를 보관하고, 관리하기 위해 설계<br>

### 장점
1. 액티비티가 재생성 되는 상황에서도 ViewModel 인스턴스를 유지하며 데이터를 안전하게 다룸
2. 데이터 소유권을 액티비티와 프래그먼트로부터 분리해 컴포넌트들은 UI 업데이트하는데 역할을 집중 
3. ViewModel 을 싱글톤 객체처럼 사용하여 데이터 공유 중간자 역할 가능

### 사용
ViewModelProvider를 통해 객체를 생성해야 HolderFragment에 의해 ViewModel이 관리된다. 
```
class ChronometerViewModel : ViewModel() {
    override fun onCleared() {
        // Do somthing to clean up
        ...
    }
}
```
```
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {        
        val chronometerModel = ViewModelProviders.of(this).get(ChronometerViewModel::class.java)
        ...
    }
}
``` 
또 ViewModel은 Factory 패턴을 강제한다
```
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        val factory = ChronometerViewModelFactory(SystemClock.elapsedRealtime())
        val chronometerModel = ViewModelProviders.of(this, factory).get(ChronometerViewModel::class.java)
        ...
    }
}
```
### 사용시 주의점 
1. ViewModel 사용 시 ViewModel에 액티비티, 프래그먼트, 뷰의 컨텍스트를 저장해선 안됩니다. ViewModel은 엑티비티 수명 주기 외부에 존재하기 때문에 엑티비티가 재생성 되도 ViewModel의 기존 Context는 JVM이 처리하지 않아서 메모리 릭이 발생하게 된다. 
 - 단, Application 컨텍스트는 전체 앱의 수명주기이기 때문에 메모리 릭에 영향을 주지 않습니다. 
2. ViewModel은 구성 변경일 때 (Configuration Changes) 됐을 때만 유지되니 사용자가 앱을 종료하거나 엑티비를 종료할 때는 메모리에 유지가 되지 않습니다. 

### 참고문헌 
[안드로이드 아키텍처 컴포넌트, ViewModel 이해하기](https://medium.com/@jungil.han/%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-viewmodel-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-2e4d136d28d2)