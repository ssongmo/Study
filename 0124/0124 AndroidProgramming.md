# Layout�� ����
* �ȵ���̵� Layout Ŭ������ View �������� ȭ�鿡 ��ġ�ϴ� ��������, ������ ��ġ�� �����ϰų�, ������ �������� �׷�ȭ�ϴ� ������ �����Ѵ�. 
��, Layout Ŭ������ View �������� �׷�ȭ�Ͽ� ��ġ�ϱ� ���� �뵵�� ���Ǵ� ViewGroup�̴�.

###LinearLayout

* stack ó�� �״´�. (horizontal, vertical) / �� ������ҵ��� ������ ��Ÿ�� �� ����Ѵ�.

###GridLayout

* �������(�ؽ�Ʈ, ��ư ��)���� 2���� �迭�� ���̺� �������� ��Ÿ�� �� ����Ѵ�.


###Constrained Layout

* Constrained Layout�� ȭ�鿡 ��Ÿ���� �信�� �� �����۵��� ���ΰ��� ��ġ�� ��� ���� �����Ѵ�. 
�� � �������� ��ġ�� ���� �� �ٸ� �����۰��� �Ÿ��� �ٸ� ���ǵ鵵 ����ؼ� ��ġ�ȴٴ� ���̴�. ���⼭ ���ϴ� Constraint�� ���� 3������.


#��ư ����ϱ�
�ϳ��� �並 ����ϱ� ���ؼ� ������ ���ľ� �ϴµ� �⺻���� ������ ��κ� ���������� �����ʸ� �����ϴ� ����� ���ݾ� �ٸ���. 
���� ������ ��ư�� �ȵ���̵忡 �����غ���.

1.���� ����
```
Button btn0;
```

2.����� ������ �ȵ���̵� ��ư�� ����.
```
btn0 = (Button)findViewById(R.id.btn0);
```

3. ������
.xml���� ȭ�� ������ �ϰ��� �� �����۵��� ������ ������ ��, �����ϵ��� �ϴ� ���� �������̴�. 

```
btn0.setOnClickListener(this);
```



#��Ƽ��Ƽ �ҷ�����

��Ƽ��Ƽ(Activity)�� ����ڿ��� UI�� �ִ� ȭ���� �����ϴ� �� ������Ʈ�̴�. �ٽ� ���ؼ�, �� ���̾� ȭ��, ī�޶� �Կ� ȭ��, 
�̸��� ���� ȭ��, ���� ���� ȭ�� ��� ���� ����ڵ��� ���� �ϱ� ���� ��ȣ�ۿ��� �� �� �ִ� ȭ���� �����Ѵٴ� ���̴�. ��Ƽ��Ƽ��
�ҷ����� ����� ������ ����.
```

public class MainActivity extends AppCompatActivity implements View.OnClickListener {
    // ������ �����Ѵ�
    Button btn;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // ������ ������ id�� ����.
        btn = (Button)findViewById(R.id.btnClick);

        // ������ onClickListener
        btn.setOnClickListener(this);
    }


    @Override
    public void onClick(View view) {

        // view �� id�� �������� ����� ���� ������.
        switch (view.getId()) {

            // id�� btnClick�� ��
            case R.id.btnClick :

                // MainActivity ���� SecondActivity ������Ʈ�� ��ȯ�ϴ� Intent ����
                Intent i = new Intent(MainActivity.this, SecondActivity.class); //(context, ����� Ŭ����)

                // Intent ����
                startActivity(i);
        }
    }
}
```
