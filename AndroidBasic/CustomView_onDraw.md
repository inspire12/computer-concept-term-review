# View를 상속받아 CustomView 만들어보기 (기본기)
<img width="50%" src = "https://cdn-images-1.medium.com/max/800/1*abc0UlGj1myFD0eph4pZjQ.png"></img>

크기를 안 뒤에 좌표를 설정하고 그림을 그린다. <br>
Constructor -> OnAttach -> (measure -> onMeasure())-> (layout -> onLayout) -> OnDraw

## measure() -> View 크기
```
View.measure() >> View.onMeasure() >> View.setMeasuredDimesion()
```
View가 wrap_content 인지, match_constraint, 값으로 박아넣었는지에 따라 달라지는 View 크기를 측정한다.<br>
CustomView에선 setMeasuredDimension() 을 호출해 줘서 mMeasuredWidth / mMeasuredHeight 을 설정해야 한다.

## layout() -> View 좌표
```
ViewGroup.layout() >> View.layout() >> View.onLayout() : empty >> ViewGroup.onLayout() : empty >> inherited class' onLayout()
```
* gravity 값에 따라 위치변화 
* ViewGroup의 child View 구역 처리

## draw() 
Paint 객체를 이용해 내부에 그림을 그려줌 

### Reference
- [Medium Proandroiddev Roman Danylyk Posting](https://proandroiddev.com/android-draw-a-custom-view-ef79fe2ff54b)
- [Android 의 View 에서 onMeasure 와 onLayout 의 의미 ](http://i5on9i.blogspot.com/2013/05/android-view-onmeasure-onlayout.html)