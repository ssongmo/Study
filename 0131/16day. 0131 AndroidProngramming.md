ListHolderView

ListView + Holder
�� view�� ���� ������ �޸𸮸� �����ϴ� ���� ���̱� ���� Holder�� ��ģ ����
��� ����

1. ListView ���� id�Ҵ�
2. BaseAdapter�� ��ӹ��� Ŀ���� Adapter ����
3. Adapter ����


###����
```
MainActivity)
listView = (ListView)findViewById(R.id.listview);

CustomAdapter adapter = new CustomAdapter(�ڷ�, MainActivity.this);

listView.setAdapter(adapter);

CustomAdapter extends BaseAdapter)
�ڷ��� data;
Context context;
LayoutInflater inflater;

public CustomAdapter(�ڷ��� data, Context context) {
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
    view = inflater.inflate(R.layout.view������, null);
    h = new Holder();

    h.����1.id�Ҵ�;
    h.����2.id�Ҵ�;

    view.setTag(h);
    } else {
        h = (Holder)view.getTag();
    }

    �ڷ��� data2 = data.get(i);

    h.����1.����;
    h.����2.����;

    return view;
}

public class Holder {
    �ڷ��� ����1;
    �ڷ��� ����2;
}
```

##RecyclerView

* Holder�� �����ϰ� ������ View�� ���������� ����ϱ� ���� View

* ��� ����

1. RecyclerView id �Ҵ�
2. RecyclerView.Adapter�� ��ӹ޴� Ŀ���� Adapter ����
3. RecyclerView.ViewHolder�� ��ӹ޴� �Ľ��� Holder ����
4. RecyclerView.Adapter�� generic���� Holder ����
5. Adapter ����
6. LayoutManger ����

###����
```
MainActivity)
recyclerView = (RecyclerView)findViewById(R.id.recyclerView);

CustomRecyclerAdapter adapter = new CustomeRecyclerAdapter(�ڷ�, MainActivity.this);

recyclerView.setAdapter(adapter);

recyclerView.setLayoutManager(new LinearLayoutManager(MainActivity.this));
```

```
CustomRecyclerAdapter)
CustomRecyclerAdapter extends RecyclerView.Adapter<CustomRecyclerAdapter.RecyclerHolder> {

public CustomRecyclerAdapter(�ڷ�, Context context) {
        �ڷ�
        this.context = context;
    }

    @Override
    public RecyclerHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.view����, parent, false);
        RecyclerHolder rh = new RecyclerHolder(view);
        return rh;
    }

    @Override
    public void onBindViewHolder(RecyclerHolder holder, int position) {
        �ڷ��� data = �ڷ�.get(position);

        holder.txId.setText(""+data.id);
        holder.txNm.setText(data.name);
        holder.txPn.setText(""+data.phoneNum);
    }


    @Override
    public int getItemCount() {
        return �ڷ�.size();
    }

    public class RecyclerHolder extends RecyclerView.ViewHolder {

        �ڷ��� ����1;
        �ڷ��� ����2;

        public RecyclerHolder(View itemView) {
            super(itemView);
            ����1 = (�ڷ���)itemView.findViewById(R.id.���̵�1);
            ����2 = (�ڷ���)itemView.findViewById(R.id.���̵�2);
        }
    }
}
```


##CardView

* RecyclerView �� �� view�� ī���� ���·� �����ִ� view

������ ���� ����ó�� ����Ѵ�

* ��� �� ������

- card_view�� �Ӽ��� ����ϱ� ���ؼ��� xmlns:card_view="http://schemas.android.com/apk/res-auto" �� �����Ͽ� ����Ѵ�
- OnClickListener�� Ŀ���� Adapter���� onBindViewHolder���� ó���Ѵ�


 RecyclerView�� Ŀ���� Adapter�� ���� ����̳� Holder���� ���̸� ���δ�

```
CustomCardAdapter)
public class CardHolder extends RecyclerView.ViewHolder {

    �ڷ��� �ڷ�1;
    CardView ī��1;

    public CardHolder(View itemView) {
        super(itemView);
        �ڷ�1 = (�ڷ���)itemView.findViewById(R.id.���̵�1);
        ī��1 = (CardView)itemView.findViewById(R.id.ī��id);
}

```
##Animation

* view�� �������� ������ �޼ҵ�


```
Ŀ���� Adapter���� onBindViewHolder���� ó���Ѵ�
Animation anime = AnimationUtils.loadAnimation(context, android.R.anim.slide_in_left);
anime.setStartOffset(100);
holder.ī��.setAnimation(anime);
```