# Custom View

1. res를 통해 Custom View 생성 
2. Paint 를 통해 뷰 그리기
3. onMeasure(), onLayout(), onDraw()
4. 애니메이션 ArgbEvaluator / AnimatorSet 
    - runnable 처리(애니메이션의 병렬처리)
    - ViewPropertyAnimator 
5. attributeSet
6. transformer적용 
7. cache manager 적용 

### onMeasure를 통해 뷰 크기 인지 
```
override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
        val widthMode = View.MeasureSpec.getMode(widthMeasureSpec)
        val heightMode = View.MeasureSpec.getMode(heightMeasureSpec)

        val widthSize = View.MeasureSpec.getSize(widthMeasureSpec)
        val heightSize = View.MeasureSpec.getSize(heightMeasureSpec)

        val width = when (widthMode) {
            View.MeasureSpec.EXACTLY -> widthSize
            View.MeasureSpec.AT_MOST -> defaultBarWidth
            View.MeasureSpec.UNSPECIFIED -> defaultBarWidth
            else -> defaultBarWidth
        }
        val height = when (heightMode) {
            View.MeasureSpec.EXACTLY -> heightSize
            View.MeasureSpec.AT_MOST -> defaultBarHeight
            View.MeasureSpec.UNSPECIFIED -> defaultBarHeight
            else -> defaultBarHeight
        }
        curLoc = height / 2
        interval = (width - height) / (visibleDot-1)

        setMeasuredDimension(width, height)
    }
```


### 애니메이션 적용 
invalidate()를 쓰면 onDraw를 다시 부름 -> view를 다시 받음

```
 fun  setAnimation(prevLoc:Int, nextLoc: Int) {
        // 이전 current VolumeLevel
        // 이후 volumeLeve

        var animator: ValueAnimator = ValueAnimator.ofInt(prevLoc, nextLoc)
        animator.setDuration(500)
        animator.addUpdateListener(object : ValueAnimator.AnimatorUpdateListener{
            override fun onAnimationUpdate(p0: ValueAnimator?) {
                curLoc = p0!!.getAnimatedValue() as Int
                invalidate()
            }
        })
        animator.start()
    }
```

### 참고사항 
[How to draw a custom view?](https://proandroiddev.com/how-to-draw-a-custom-view-9da8016fe94)
[Android Animation](http://blog.naver.com/PostView.nhn?blogId=xicnt&logNo=10152628778)

