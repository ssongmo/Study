# Layout의 종류
* 안드로이드 Layout 클래스는 View 위젯들을 화면에 배치하는 과정에서, 위젯의 위치를 정렬하거나, 연관된 위젯들을 그룹화하는 역할을 수행한다. 
즉, Layout 클래스는 View 위젯들을 그룹화하여 배치하기 위한 용도로 사용되는 ViewGroup이다.

###LinearLayout

* stack 처럼 쌓는다. (horizontal, vertical) / 각 구성요소들을 비율로 나타낼 때 사용한다.

###GridLayout

* 구성요소(텍스트, 버튼 등)들을 2차원 배열의 테이블 형식으로 나타낼 때 사용한다.


###Constrained Layout

* Constrained Layout은 화면에 나타나는 뷰에서 각 아이템들이 서로간에 위치를 잡는 것을 정의한다. 
즉 어떤 아이템이 위치를 잡을 때 다른 아이템과의 거리나 다른 조건들도 고려해서 배치된다는 말이다. 여기서 말하는 Constraint는 다음 3가지다.


#버튼 사용하기
하나의 뷰를 사용하기 위해선 절차를 거쳐야 하는데 기본적인 순서는 대부분 동일하지만 리스너를 구성하는 방식이 조금씩 다르다. 
먼저 간단한 버튼을 안드로이드에 적용해보자.

1.변수 선언
```
Button btn0;
```

2.선언된 변수와 안드로이드 버튼을 연결.
```
btn0 = (Button)findViewById(R.id.btn0);
```

3. 리스너
.xml에서 화면 구성을 하고나서 각 아이템들을 유저가 눌렀을 때, 반응하도록 하는 것이 리스너이다. 

```
btn0.setOnClickListener(this);
```



#액티비티 불러오기

액티비티(Activity)는 사용자에게 UI가 있는 화면을 제공하는 앱 컴포넌트이다. 다시 말해서, 폰 다이얼러 화면, 카메라 촬영 화면, 
이메일 쓰기 화면, 지도 보기 화면 등과 같이 사용자들이 뭔가 하기 위해 상호작용을 할 수 있는 화면을 제공한다는 것이다. 액티비티를
불러오는 방식은 다음과 같다.
```

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    // 위젯을 선언한다
    Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 선언한 위젯을 id와 연동.
        btn = (Button)findViewById(R.id.btnClick);

        // 위젯에 onClickListener
        btn.setOnClickListener(this);
    }


    @Override
    public void onClick(View view) {

        // view 의 id를 기준으로 경우의 수를 나눈다.
        switch (view.getId()) {

            // id가 btnClick일 때
            case R.id.btnClick :

                // MainActivity 에서 SecondActivity 컴포넌트를 소환하는 Intent 선언
                Intent i = new Intent(MainActivity.this, SecondActivity.class); //(context, 사용할 클래스)

                // Intent 시작
                startActivity(i);
        }
    }
}
```
