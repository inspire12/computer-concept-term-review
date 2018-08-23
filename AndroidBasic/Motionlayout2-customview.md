# 개인정리 : MotionLayout 2 - Custom View 에 적용 

## CoordinatorLaylout 과 함께 쓰는 MotionLayout

##


### 참고 
#### JvmOverloads 
만약 java와 연계해서 사용한다면 @JvmOverloads 을 이용하여 디폴트 인자로 처리된 부분을 오버로딩 함수로 자동으로 생성되게끔 해줄수도 있습니다.<br>

// Android 에서 커스텀 뷰를 만든다고 한다면 아래 3가지 생성자를 구현해야 하지만,
```
class CustomView : View {
    constructor(context: Context) : this(context, null)
    constructor(context: Context, attrs: AttributeSet?) : this(context, attrs, 0)
    constructor(context: Context, attrs: AttributeSet?, defStyleAttr: Int) : super(context, attrs, defStyleAttr)
}
```
// @JvmOverloads 를 이용해서 코드를 더 간결하게 만들 수 있다.
```
class CustomView @JvmOverloads constructor(context: Context
                            , attrs: AttributeSet? = null
                            , defStyleAttr: Int = 0
                            ) : View(context, attrs, defStyleAttr) {
}
```
### 참고자료 
- [Introduction to MotionLayout (part III)](https://medium.com/google-developers/introduction-to-motionlayout-part-iii-47cd64d51a5)

- [Kotlin 코딩 팁](https://cchcc.github.io/blog/Kotlin-%EC%BD%94%EB%94%A9-%ED%8C%81/)