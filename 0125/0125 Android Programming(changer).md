#단위 변환 App 구현해보기 (미완)

이제 막 안드로이드를 시작 했기때문에 완변한 구현은 어려웠으나, 네이버 단위변환기를 카피해 구현해보았다.

![](https://github.com/ssongmo/Study/blob/master/0125/Screenshot_20170130-144535.png?raw=true)
<img width="" height=""></img>

### 1. 레이아웃 구성 (.xml)

LinearLayout(horizontal, vertical)을 반복적으로 사용해 전체적인 틀을 구성하였다.
![]( https://github.com/ssongmo/Study/blob/master/0125/xml%20image.jpg?raw=true)
<img width="" height=""></img>

### 2. ChangerActivity.java

* 스피너1,2를 구성하여 단위를 환산하고 싶었으나, 아직 설정이 어려워 스피터1을 mm로 고정시키고 스피너2를 변환했을때 값이 출력되도록 설계하였다.

```
package com.example.songmoo.changer;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.text.Editable;
import android.text.Layout;
import android.text.TextWatcher;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.LinearLayout;
import android.widget.Spinner;
import android.widget.TextView;
import android.widget.Toast;

import org.w3c.dom.Text;
import java.util.ArrayList;
import static android.R.id.edit;
```

* 사용 할 변수 선언

```
public class ChangerActivity extends AppCompatActivity implements View.OnClickListener{
    Button btnL;
    Button btnA;
    Button btnW;
    ArrayList arraylist;
    Spinner sp;
    Spinner sp2;
    String textData;
    TextView result;
    TextView mMm, mCm, mM, mKm, mInch, mFt, mYard, mMile;

    EditText editText;

    LinearLayout layoutL, layoutA, layoutW;

    float[]  ratio = { 1f, 0.1f, 0.001f, 1e-6f, 0.03937f, 0.003281f, 0.001094f, 6.2137e-7f};
```

* onCreate 부분(xml과 연결 + 리스너)

```
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_changer);


        btnL = (Button) findViewById(R.id.btnLength);
        btnA = (Button) findViewById(R.id.btnArea);
        btnW = (Button) findViewById(R.id.btnWeight);

        layoutL = (LinearLayout) findViewById(R.id.layoutLength);
        layoutA = (LinearLayout) findViewById(R.id.layoutArea);
        layoutW = (LinearLayout) findViewById(R.id.layoutWeight);

        mMm = (TextView) findViewById(R.id.mm);
        mCm = (TextView) findViewById(R.id.cm);
        mM = (TextView)findViewById(R.id.m);
        mKm = (TextView) findViewById(R.id.km);
        mInch = (TextView) findViewById(R.id.inch);
        mFt = (TextView) findViewById(R.id.ft);
        mYard = (TextView) findViewById(R.id.yard);
        mMile = (TextView) findViewById(R.id.mile);

        editText = (EditText)findViewById(R.id.editText);
        TextView result = (TextView)findViewById(R.id.resultView);
        textData = editText.getText().toString();



//리스너
        btnL.setOnClickListener(this);
        btnA.setOnClickListener(this);
        btnW.setOnClickListener(this);

        //Spinner arrayAdapter
        arraylist = new ArrayList<String>();
        arraylist.add("mm");    arraylist.add("cm");    arraylist.add("m");
        arraylist.add("km");    arraylist.add("inch");  arraylist.add("ft");
        arraylist.add("yard");  arraylist.add("mile");

        ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,android.R.layout.simple_spinner_dropdown_item, arraylist);
        sp = (Spinner) findViewById(R.id.spinner);
        sp.setAdapter(adapter);
        sp.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                switch (position) {
                    case 0:

                        calculateAll();
                        break;
                    default:
                        Toast.makeText(ChangerActivity.this, "not implemented.", Toast.LENGTH_SHORT).show();
                        break;
                }
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {

            }
        });
        sp2 = (Spinner) findViewById(R.id.spinner2);
        sp2.setAdapter(adapter);
        sp2.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {

            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {

            }
        });

```

* 하단부분의 자동 변환 기능 구현 +  레이아웃 리스너

```

//자동 갱신 onTextChanged
        editText.addTextChangedListener(new TextWatcher() {

            @Override
            public void onTextChanged(CharSequence s, int start, int before, int count) {
                // 입력되는 텍스트에 변화가 있을 때
                Toast.makeText(ChangerActivity.this, "뿅", Toast.LENGTH_SHORT).show();
                calculateAll();
            }

            @Override
            public void afterTextChanged(Editable arg0) {
                // 입력이 끝났을 때
            }

            @Override
            public void beforeTextChanged(CharSequence s, int start, int count, int after) {
                // 입력하기 전에
            }
        });

    }
    //레이아웃 리스너
    View.OnClickListener clickListener = new View.OnClickListener(){
        @Override
        public void onClick(View view) {
            switch (view.getId()){
                case R.id.btnLength:
                    layoutL.setVisibility(View.VISIBLE);
                    layoutA.setVisibility(View.GONE);
                    layoutW.setVisibility(View.GONE);
                    break;
                case R.id.btnArea:
                    layoutL.setVisibility(View.GONE);
                    layoutA.setVisibility(View.VISIBLE);
                    layoutW.setVisibility(View.GONE);
                    break;
                case R.id.btnWeight:
                    layoutL.setVisibility(View.GONE);
                    layoutA.setVisibility(View.GONE);
                    layoutW.setVisibility(View.VISIBLE);
            }
        }
    };
```

* 단위 변환을 위한 계산코드

```
    public void calculateAll() {
        //spinner1 spinner2
        //N * sp1R * sp2R
        //100 mm inch
        //
        float input;
        try {
            input = Float.valueOf(editText.getText().toString());
        } catch (NumberFormatException ex) {
            input = 0;
        }
        mMm.setText((input*1)+"mm");
        mCm.setText(String.valueOf(input*0.1)+"cm");
        mM.setText(String.valueOf(input*0.001)+"m");
        mKm.setText(String.valueOf(input*1e-6)+"km");
        mInch.setText(String.valueOf(input*0.03937)+"in");
        mFt.setText(String.valueOf(input*0.003281)+"ft");
        mYard.setText(String.valueOf(input*0.001094)+"yard");
        mMile.setText(String.valueOf(input*6.2137e-7)+"mile");

    }
```

* 섹션 구분하기

```
    @Override
    public void onClick(View view) {
        layoutL.setVisibility(View.GONE);
        layoutA.setVisibility(View.GONE);
        layoutW.setVisibility(View.GONE);

        switch (view.getId()){
            case R.id.btnLength:
                layoutL.setVisibility(View.VISIBLE);
                break;
            case R.id.btnArea:
                layoutA.setVisibility(View.VISIBLE);
                break;
            case R.id.btnWeight:
                layoutW.setVisibility(View.VISIBLE);
                break;

        }
    }
}
```
