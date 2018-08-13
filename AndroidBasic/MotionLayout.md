# MotionLayout 

사용자가 앱과 소통하는 느낌을 주는 퀄리티 있는 앱을 위해 자연스러운 애니메이션은 필수입니다. <br>
인드로이드에서 기본적으로 제공하는 기존의 애니메이션 처리 방법들을 사용자에게 익숙한 방식으로 간단하게 구현할 수 있습니다.<br>
하지만 기존의 처리 방법에서 아쉬운 부분을 느꼈는데 AnimationUtils 를 이용하면 Animation 중간에 끊는 처리가 어색해집니다.
 만약 제공되지 않는 복잡한 방식의 애니메이션을 구현하려면 onDraw 메소드와 interpolate 메소드 그리고 수학적 계산을 통해 구현해야하는 복잡함이 있습니다. <br>

이번에 2018년 구글 IO 키노트에서 발표한 가장 최근에 나온 MotionLayout 방식은 기존 제공하던 방법들의 장점을 합쳐 이와 같은 단점을 해결하고 훨씬 편하고 간단하게 구현이 가능합니다.


## 기존 안드로이드 애니메이션들 
* Animated Vector Drawable
* Property Animation framework
* LayoutTransition animations
* Layout transitions with TransitionManager
* CoordinatorLayout

## 왜 MotionLayout?
 Constraint layout의 subclass <br>
 layout transitions 과 complex motion handling 의 차이를 이어주기 위해 만들어짐 <br>
 => <strong>property animation framework 와 transitionManager, CoordinatorLayout의 혼합! </strong>

 1. 2가지 레이아웃을 통해 묘사 (tranisitionManager 적인 요소) 
 2. property로 처리가 가능함
 3. seekable transition을 지원 (touch나 transition의 위치를 반환)

MotionLayout 은 완전히 선언적 (xml 을 통해 표현)

## 사용법
### 추가 
```
dependencies {
    implementation 'com.android.support.constraint:constraint-layout:2.0.0-alpha1'
}
```

1. 엑티비티에 MotionLayout 설정(불러오는 부분)
```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.motion.MotionLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/motionLayout"
   
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <View
        android:id="@+id/button"
        android:background="@color/colorAccent"
        android:layout_width="64dp"
        android:layout_height="64dp"
        android:text="Button" />

</android.support.constraint.motion.MotionLayout>
```
 app:layoutDescription="@xml/scene_02" 이 부분이 res/xml 부분의 MotionScene과 연결 <br>
 <View> 가 애니메이션 적용 대상, MotionScenene 에서도 설정해줌 <br>
 추후에 <View>를 <ImageFilterView> 로 변경하여 이미지 애니메이션 설정도 가능 

2. MotionScene 설정 (ConstraintSet과 옵션) 
```
<?xml version="1.0" encoding="utf-8"?>
<MotionScene xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetStart="@+id/start"
        motion:constraintSetEnd="@+id/end"
        motion:duration="1000">
        <OnSwipe
            motion:touchAnchorId="@+id/button"
            motion:touchAnchorSide="right"
            motion:dragDirection="dragRight" />
    </Transition>

    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/button"
            android:layout_width="64dp"
            android:layout_height="64dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent" />
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/button"
            android:layout_width="64dp"
            android:layout_height="64dp"
            android:layout_marginEnd="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintEnd_toEndOf="parent"
            motion:layout_constraintTop_toTopOf="parent" />
    </ConstraintSet>
</MotionScene> 
```
<br>

* ConstraintSet android:id="@+id/start"  와 motion:constraintSetStart="@+id/start" 이 연결
* ConstraintSet android:id="@+id/end" 와 motion:constraintSetEnd="@+id/end" 이 연결
<img src = "https://cdn-images-1.medium.com/max/640/1*PYOByy271vItozskVYc0SQ.png">

3. OnSwipe 설정으로 애니메이션 trigger 설정 
OnSwipe Handler 
    * touchAnchorId : 애니메이션이 적용된 객체 id 
    * touchAnchorSide : 
    * dragDirection : 
    
    + Motion Layout 옵션 (Debugging 에 유용함) 
        * app:applyMotionScene="boolean"
        * app:showPaths="boolean"
        * app:progress="float"
        * app:currentState="reference"


4. KeyFrame
Transition 에 디테일한 이동경로를 설정 
```
<Transition>
    <KeyFrameSet>
            <KeyPosition
                motion:type="parentRelative"
                motion:percentY="0.25"
                motion:framePosition="50"
                motion:target="@+id/button"/>
        </KeyFrameSet>
</Transition>
```
<img src = "https://cdn-images-1.medium.com/max/640/1*jOmDbVPaNMiqZqCb9W6I3w.gif">

5. image filter 로 이미지 애니메이션 가능 
* 엑티비티에 대상 이미지를 적용
```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.motion.MotionLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/motionLayout"
    app:layoutDescription="@xml/scene_04"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <android.support.constraint.utils.ImageFilterView
        android:id="@+id/image"
        android:background="@color/colorAccent"
        android:src="@drawable/roard"
        app:altSrc="@drawable/hoford"
        android:layout_width="64dp"
        android:layout_height="64dp"/>

</android.support.constraint.motion.MotionLayout>
```
android:src="@drawable/roard" 여기서 이미지를 설정  <br>
* ConstraintSet 내부에서 변경점 적용
```
    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:id="@+id/image"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:layout_marginStart="8dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            motion:layout_constraintStart_toStartOf="parent"
            motion:layout_constraintTop_toTopOf="parent">
            <CustomAttribute
                motion:attributeName="crossfade"
                motion:customFloatValue="0" />
        </Constraint>
    </ConstraintSet>
```

```
 <CustomAttribute
                motion:attributeName="crossfade"
                motion:customFloatValue="0" />
```


### 참고문헌 
- [Introduction to MotionLayout (part I) - 기본적인 적용](https://medium.com/google-developers/introduction-to-motionlayout-part-i-29208674b10d)
- [Introduction to MotionLayout (part II) - ImageFilter와 Keyframe ](https://medium.com/google-developers/introduction-to-motionlayout-part-ii-a31acc084f59)
- [Creating Animations With MotionLayout for Android : 사용법](https://code.tutsplus.com/tutorials/creating-animations-with-motionlayout-for-android--cms-31497)