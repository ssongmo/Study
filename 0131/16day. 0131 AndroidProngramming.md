ListHolderView

ListView + Holder
각 view가 위젯 생성에 메모리를 낭비하는 것을 줄이기 위해 Holder를 합친 형태
사용 순서

1. ListView 위젯 id할당
2. BaseAdapter를 상속받은 커스텀 Adapter 생성
3. Adapter 세팅


###예제
```
MainActivity)
listView = (ListView)findViewById(R.id.listview);

CustomAdapter adapter = new CustomAdapter(자료, MainActivity.this);

listView.setAdapter(adapter);

CustomAdapter extends BaseAdapter)
자료형 data;
Context context;
LayoutInflater inflater;

public CustomAdapter(자료형 data, Context context) {
    this.data = data;
    this.context = context;
    inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
}

@Override
public int getCount() {
    return data.size();
}

@Override
public Object getItem(int i) {
    return data.get(i);
}

@Override
public long getItemId(int i) {
    return i;
}

@Override
public View getView(int i, View view, ViewGroup viewGroup) {
    Holder h;
    if(view==null) {
    view = inflater.inflate(R.layout.view아이템, null);
    h = new Holder();

    h.위젯1.id할당;
    h.위젯2.id할당;

    view.setTag(h);
    } else {
        h = (Holder)view.getTag();
    }

    자료형 data2 = data.get(i);

    h.위젯1.조작;
    h.위젯2.조작;

    return view;
}

public class Holder {
    자료형 위젯1;
    자료형 위젯2;
}
```

##RecyclerView

* Holder를 포함하고 각각의 View를 유기적으로 사용하기 편한 View

* 사용 순서

1. RecyclerView id 할당
2. RecyclerView.Adapter를 상속받는 커스텀 Adapter 생성
3. RecyclerView.ViewHolder를 상속받는 컴스텀 Holder 생성
4. RecyclerView.Adapter의 generic으로 Holder 삽입
5. Adapter 세팅
6. LayoutManger 세팅

###예제
```
MainActivity)
recyclerView = (RecyclerView)findViewById(R.id.recyclerView);

CustomRecyclerAdapter adapter = new CustomeRecyclerAdapter(자료, MainActivity.this);

recyclerView.setAdapter(adapter);

recyclerView.setLayoutManager(new LinearLayoutManager(MainActivity.this));
```

```
CustomRecyclerAdapter)
CustomRecyclerAdapter extends RecyclerView.Adapter<CustomRecyclerAdapter.RecyclerHolder> {

public CustomRecyclerAdapter(자료, Context context) {
        자료
        this.context = context;
    }

    @Override
    public RecyclerHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.view형식, parent, false);
        RecyclerHolder rh = new RecyclerHolder(view);
        return rh;
    }

    @Override
    public void onBindViewHolder(RecyclerHolder holder, int position) {
        자료형 data = 자료.get(position);

        holder.txId.setText(""+data.id);
        holder.txNm.setText(data.name);
        holder.txPn.setText(""+data.phoneNum);
    }


    @Override
    public int getItemCount() {
        return 자료.size();
    }

    public class RecyclerHolder extends RecyclerView.ViewHolder {

        자료형 위젯1;
        자료형 위젯2;

        public RecyclerHolder(View itemView) {
            super(itemView);
            위젯1 = (자료형)itemView.findViewById(R.id.아이디1);
            위젯2 = (자료형)itemView.findViewById(R.id.아이디2);
        }
    }
}
```


##CardView

* RecyclerView 의 각 view를 카드의 형태로 보여주는 view

선언을 통해 위젯처럼 사용한다

* 사용 시 유의점

- card_view의 속성을 사용하기 위해서는 xmlns:card_view="http://schemas.android.com/apk/res-auto" 를 선언하여 사용한다
- OnClickListener는 커스텀 Adapter내의 onBindViewHolder에서 처리한다


 RecyclerView의 커스텀 Adapter와 같은 모습이나 Holder에서 차이를 보인다

```
CustomCardAdapter)
public class CardHolder extends RecyclerView.ViewHolder {

    자료형 자료1;
    CardView 카드1;

    public CardHolder(View itemView) {
        super(itemView);
        자료1 = (자료형)itemView.findViewById(R.id.아이디1);
        카드1 = (CardView)itemView.findViewById(R.id.카드id);
}

```
##Animation

* view의 움직임을 만들어내는 메소드


```
커스텀 Adapter내의 onBindViewHolder에서 처리한다
Animation anime = AnimationUtils.loadAnimation(context, android.R.anim.slide_in_left);
anime.setStartOffset(100);
holder.카드.setAnimation(anime);
```