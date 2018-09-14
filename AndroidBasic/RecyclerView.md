# Recycler View 
Viewholder 패턴을 강제해 뷰를 재사용하는 리스트 
목차 
1. 기본틀과 구성요소
2. 크기 설정 
3. listener 설정 
4.

## 기본 틀 
### Activity : RecylcerView를 attach 하는 곳 
    1. RecylcerView 레이아웃을 findViewById 
    2. 리스트 형식을 (vertical, horizon, grid) 지정 
    // setHasFixedSize(true)는 값이 없어도 리스트 공간을 유지하게 하는 설정
    ```
        rvTable1.apply{
                setHasFixedSize(true)
                layoutManager = GridLayoutManager(baseContext, 7)
                adapter = RecylerAdapter(data, baseContext)
            }
    ```
### Adapter : 데이터를 통해 RecyclerView의 내용을 정하는 곳 
    ```
class RecylerAdapter(val items : ArrayList<String>, val context: Context) : RecyclerView.Adapter<ViewHolder>(){

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val v = LayoutInflater.from(context).inflate(R.layout.holder_card, parent, false)
        return ViewHolder(v)
    }

    override fun getItemCount(): Int {
        return items.size
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        holder.tvTitle.setText(items[position])
    }
}
    ```

    1. override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder 
     
     inflater를 통해 layout view를 viewholder로 객체화 시키는 부분 
     class viewholder 이 부분에서 구현이 힘든 부분을 여기서 처리해도 된다.  

    2. override fun onBindViewHolder(holder: ViewHolder, position: Int) 
     각 아이템 순서에 따라 달라지는 부분의 데이터를 바꿔주는 부분, view가 재사용 될 때 이 부분을 계속 거치기 때문에 성능에 부담이 갈 수 있다.  
> 기존 list adapter의 getView()를 onCreateViewHolder와 onBindViewHolder로 분리해서 반복되는 부분 처리 

#### getViewType
 다른 레이아웃이 필요할 때 override 해서 View Type을 지정해 적용할 수 있다.

### Viewholder : 재사용되는 View 부분

    주로 findViewById 같이 같은 행동을 반복하는 초기화 과정을 여기서 함, 추가적으로 부작용이 없다면, 이곳에서 지정하는 게 효과가 좋음

#### RecyclerView Scroll 정보 형태에서 재사용되는 시점 
<img src="https://t1.daumcdn.net/cfile/tistory/21140B4E57352A810B">
- 검은색 : RecyclerView 전체 영역 
- 파란색 : computeVerticalScrollRange 값, Window에 할당된 영역으로 onBindViewHolder를 부른 상태 (getView)
- 녹색 : computeVerticalScrollOffset 값, 스크롤 상단에서 어느 정도 움직였는지 알려주는 Offset 값 (상단이 0에서 시작, -1을 곱해서 사용)

## How to set Height onBindViewHolder for RecyclerView [Programatically]
```
val params:LinearLayout.LayoutParams = 
                        LinearLayout.LayoutParams(ViewGroup.LayoutParams.WRAP_CONTENT,
                        ViewGroup.LayoutParams.WRAP_CONTENT);
                // Set the height by params
                params.height=1700;
                // set height of RecyclerView
                holder.recyclerViewList.setLayoutParams(params);
```

## Event Lisnter 처리 
context가 있어야 터치가 일어났을 때 처리가 가능 

## List Header 


## Drag selection 
- ItemTouchListener
- GestureDetector 

1. ViewHolder에서 onLongPress()안에 GestureDetector를 사용<br>
2. ACTION_MOVE
3. 

### 참고 자료 
[RecyclerView 사용이 이유와 재사용 원리](http://dudmy.net/android/2017/06/23/consider-of-recyclerview/)
[](http://gogorchg.tistory.com/entry/Android-RecyclerView-%EC%97%90%EC%84%9C-Scroll-%EC%A0%95%EB%B3%B4-%ED%98%95%ED%83%9C)

[Drag selection of RecyclerView items, Nikola Despotoski](https://medium.com/@nullthemall/drag-selection-of-recyclerview-items-7072678e9900)