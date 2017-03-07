

# Retrofit
Retrofit은 REST API 통신을 위한 라이브러리이다. RESTAPI를 이용해서 데이터를 가져올때 JSON을 내가 원하는 데이터로 수정하는 파싱작업의 귀찮음을 최소화 할 수 있고, 네트워크 비동기, 동기 통신 또한 매우 편하고 깔끔하게 구현 할 수 있도록 다양한 메소드를 제공한다.

*REST(Representational safe transfer) : 웹의 장점을 최대한 활용할 수 있는 네트워크 기반의 아키텍쳐*



## OkHttp
OkHttp : 데이터와 미디어를 교환할때 사용하는 HTTP 클라이언트.
```
- 지원을 통해 동일한 호스트에 대한 모든 요청이 소켓을 공유 할 수 있다.
- 연결 풀링은 요청 대기 시간을 줄인다.
- 응답 캐싱은 반복 요청에 대해 네트워크를 완전히 피한다.
```

![스크린샷 2017-03-08 오전 12.13.51](http://i.imgur.com/GIvkaRN.png)
* 서버에서 요청을 하면 필요한 것을 브라우저에서 받아온다. url을 넣어주는것이 서버에 요청하는 것이다.


정리하자면, OkHttp를 이용해서 Retrofit을 사용한다. retrofit은 외부 API를 연동해준다.
바로 소스 코드를 통해 보도록 하겠다. 먼저 OkHttp를 설정해준다.
*소스 참조 : square.github.io/okhttp/*

* 예제 소스코드는 구글 맵을 연동, 서울시 실시간 주차 현황을 확인해보는 소스이다.
먼저 서울시 실시간 주차 현황을 알기 위해선 오픈소스가 필요하다.
![스크린샷 2017-03-06 오후 2.18.43](http://i.imgur.com/zuuICzT.png)
이곳 데이터셋에서 '서울시 실시간 주차'라고 검색하면 open api를 제공해준다.

받은 소스를 아래와 같은 사이트에 붙여넣기를 하고 Beauty를 클릭하면 Json언어로 컨버트해준다.
![스크린샷 2017-03-06 오후 2.18.16](http://i.imgur.com/kIHa5Rj.jpg)

컨버트된 Json 소스를 아래와같이 넣어주면 안드로이드에서 사용할 Java Pojo Classes를 생성해준다.
![스크린샷 2017-03-06 오후 6.01.56](http://i.imgur.com/BQLLV7G.png)

Retrofit과 OkHttp를 사용하기 위해서 Gradle(App)에 추가해야 할 것이 있다.
```
 compile 'com.squareup.okhttp3:okhttp:3.6.0'
 compile 'com.squareup.retrofit2:retrofit:2.2.0'
 compile 'com.squareup.retrofit2:converter-gson:2.2.0'

 ```

컨버트된 소스들은 클래스별로 나누어져 있는데 이를 그대로 domain이라는 패키지를 생성 후 넣어준다.
![스크린샷 2017-03-08 오전 12.53.18](http://i.imgur.com/dhwiRMH.png)

상단에 사진에 보이듯이 retrofit를 사용하기 위해선 인터페이스가 필요하다.
```
package com.example.goodgoodman.remoteokhttp;
import com.example.goodgoodman.remoteokhttp.domain.Data;
import java.util.List;
import retrofit2.Call;
import retrofit2.http.GET;
import retrofit2.http.Path;

/**
 * Created by GoodGoodMan on 2017. 3. 7..
 */

public interface SeoulOpenService {
    @GET("4c425976676b6f643437665377554c/json/SearchParkingInfo/1/10/{gu}")
    //1은 시작 10은 끝 뒤에는 주소

    Call<Data> getData(@Path("gu") String value);
}
```

이해하기 쉽도록 OkHttp는 network에 접근하기 위해서 스레드를 사용해야 하므로 MainActivity에서 Asynktask를 사용했다.
* MainActivity.java

```
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // OkHttp 는 네트웍에 접근하기 위해서 새로운 Thread를 생성해서 처리해야한다
        // 1. Thread 생성방법 - AsyncTask
        new AsyncTask<Void,Void,Void>() {
            @Override
            public Void doInBackground(Void... params){
                try {
                    String result = getData("http://daum.net");
                    Log.i("OkHttp", "result=" + result);
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return null;
            }
        }.execute();

        // 2. new Thread
        new Thread(){
            @Override
            public void run(){
                try {
                    String result = getData("http://google.com");
                    Log.i("OkHttp", "result=" + result);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }.start();

    }

    private String getData(String url) throws IOException {
        // 1. OKHttp 인스턴스 생성
        OkHttpClient client = client = new OkHttpClient();

        // 2. request 개체 생성
        Request request = new Request.Builder()
                .url(url)
                .build();

        // 3. client 인스턴스에 request 를 담아 보낸다
        Response response = client.newCall(request).execute();
        // -> 서버측으로 요청

        return response.body().string();
    }
}
```

MapsActivity.java에서 레트로핏을 사용했다. 하나하나 살펴보면,
1. Override함수로 onCreate(), onMapReady(), convertDouble()를 생성하고, onMapReady()함수 안에는 onResponse(), onFailure()매소드가 Override되어있다.
![스크린샷 2017-03-08 오전 1.09.23](http://i.imgur.com/lt3fc5Q.png)

```
@Override
     public void onMapReady(GoogleMap googleMap) {
     mMap = googleMap;

     LatLng seoul = new LatLng(37.566696, 126.977942);
     mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(seoul,12));

     // 1. 레트로핏을 생성하고
     Retrofit retrofit = new Retrofit.Builder()
     .baseUrl("http://openapi.seoul.go.kr:8088/")
     .addConverterFactory(GsonConverterFactory.create())
     .build();

     // 2. 사용할 인터페이스를 설정한다
     SeoulOpenService service = retrofit.create(SeoulOpenService.class);

     // 3. 데이터를 가져온다
     Call<Data> result = service.getData("강남구");
```
2. 값이 정상적으로 리턴됬을 경우 원래 반환값인 jsonString 이 Data 클래스로 변환되어 리턴.
```
      result.enqueue(new Callback<Data>() {
        @Override
        public void onResponse(Call<Data> call, Response<Data> response) {
            // 값이 정상적으로 리턴됬을 경우
            if(response.isSuccessful()){
               Data data = response.body();
               // 원래 반환값인 jsonString 이 Data 클래스로 변환되어 리턴된다.
               for (Row row : data.getSearchParkingInfo().getRow()) {
                   LatLng parking = new LatLng( convertDouble(row.getLAT()),
                   convertDouble(row.getLNG()));
                   double capacity = convertDouble(row.getCAPACITY());
                   Marker marker = mMap.addMarker(new MarkerOptions().position
                   (parking).title(row.getPARKING_NAME()
                   +" 주차공간:" + capacity));

                   marker.showInfoWindow();
               }
             }else{
               Log.e("Retrofit", response.message());
               // 정상적이지 않을경우 message에 오류내용이 담겨 온다
            }
        }

        @Override
        public void onFailure(Call<Data> call, Throwable t) {
           Log.e("Retrofit", t.getMessage());
           }
      });
```

* MapsActivity.java 소스 전체
```
public class MapsActivity extends FragmentActivity implements OnMapReadyCallback {

    private GoogleMap mMap;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_maps);
        // Obtain the SupportMapFragment and get notified when the map is ready to be used.
        SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager()
                .findFragmentById(R.id.map);
        mapFragment.getMapAsync(this);
    }


     @Override
     public void onMapReady(GoogleMap googleMap) {
     mMap = googleMap;

     LatLng seoul = new LatLng(37.566696, 126.977942);
     mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(seoul,12));

     // 1. 레트로핏을 생성하고
     Retrofit retrofit = new Retrofit.Builder()
     .baseUrl("http://openapi.seoul.go.kr:8088/")
     .addConverterFactory(GsonConverterFactory.create())
     .build();

     // 2. 사용할 인터페이스를 설정한다
     SeoulOpenService service = retrofit.create(SeoulOpenService.class);

     // 3. 데이터를 가져온다
     Call<Data> result = service.getData("강남구");

     // 4. 데이터를 가져오는 부분은 네트웍을 통해서 오기 때문에 비동기 처리된다.
         result.enqueue(new Callback<Data>() {
             @Override
             public void onResponse(Call<Data> call, Response<Data> response) {
                 // 값이 정상적으로 리턴됬을 경우
                 if(response.isSuccessful()){
                    Data data = response.body();
                    // 원래 반환값인 jsonString 이 Data 클래스로 변환되어 리턴된다.
                    for (Row row : data.getSearchParkingInfo().getRow()) {
                        LatLng parking = new LatLng( convertDouble
                          (row.getLAT()), convertDouble(row.getLNG()));
                        double capacity = convertDouble(row.getCAPACITY());
                        Marker marker = mMap.addMarker(new MarkerOptions().
                        position(parking).title(row.getPARKING_NAME()
                        +" 주차공간:" + capacity));
                        marker.showInfoWindow();
                    }
                  }else{
                    Log.e("Retrofit", response.message());
                    // 정상적이지 않을경우 message에 오류내용이 담겨 온다
                 }
             }

             @Override
             public void onFailure(Call<Data> call, Throwable t) {
                Log.e("Retrofit", t.getMessage());
                }
         });
     }

     private double convertDouble(String value){
         double result = 0;
             try {
                result = Double.parseDouble(value);
             }catch(Exception e){

        }
        return result;
     }

     private int convertInt(String value){
        int result = 0;
         try {
             result = Integer.parseInt(value);
        }catch(Exception e){

         }
         return result;
     }

}
```
