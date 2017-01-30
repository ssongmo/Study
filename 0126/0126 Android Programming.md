#Activity LifeCycle

https://kairo96.gitbooks.io/android/content/pic2/2-4-1-1.jpg

* 액티비티 생명주기는 onCreate() -> onStart() -> onResume() -> onPause() -> onStop() -> onDestory()순으로 실행되며, 경우에 따라서 onRestart() 메소드가 호출되기도 한다. 

* 액티비티의 4가지 상태

- (가) Active : 현재 활성화되고 있는 창이다.이 액티비티가 활성화되면 기존의 활성된 액티비티는 Pause가 된다.
- (나) Pause : 투명한 액티비티나 활성화된 액티비티가 기존의 액티비티를 일부 가리는 상태이다. 액티비티가 완전히 가려지게 되면 가려진 액티비티는 Stop 상태가 된다.
- (다) Stop : 화면에 나타나지 않는 액티비티이다. 액티비티가 화면 밖으로 나가거나 닫히고 나면 그 액티비티는 Inactive가 된다.
- (라) Inactive : activity stack에서 제거된 상태이다. 다시 화면에 나타나기 위해서는 재시작되어야 한다.

#App Architecture

애플리케이션 아키텍처는 애플리케션을 설계하고 구축하는 작업을 표준화 한 것이다. 표준화된 작업은 애플리케이션 개발주기를 단축시키고 다른 앱의 코드와도 공유하는 것이 가능하다. 아키텍처 패턴 중에 가장 많이 사용되는 것이 MVC 패턴이다.

MVC는 모델, 뷰, 컨트롤러를 의미한다.
```
모델 : 애플리케이션에 사용되는 데이터의 일반적인 포맷
뷰 : 사용자에게 데이터를 나타낸다.
컨트롤러 : 애플리케이션의 이벤트에 관한 처리를 모델과 뷰 사이에서 명령을 내리는 역할이다.
MVC 아키텍처의 장점은 각 클래스마다 역할이 분명히 정의되어있기 때문에 앱의 테스트와 유지가 쉽고 코드를 재사용할 수 있다.
```

##커스텀 브라우저(WebView)

커스텀 브라우저는 웹브라우저가 새로운 화면으로 전환되지 않고 화면 가운데에서 실행되는 것을 말한다.

1. 인터넷 권한 넣기

http://cfile27.uf.tistory.com/image/215D0C3D543D0A0E141370

2. .xml에 웹뷰 그리기

```
<WebView

        android:id="@+id/WebView1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true" />
```

3. ainActivity.java 파일에 웹뷰를 불러오기위한 소스를 입력

```
private WebView mWebView;    // 웹뷰 선언
private WebSettings mWebSettings; //웹뷰 셋팅
```

```
@Override

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        WebView = (WebView) findViewById(R.id.WebView);
        WebView.setWebViewClient(new WishWebViewClient());  //웹뷰 새창 안뜨게 설정.       
        WebSettings = mWebView.getSettings();
        
        WebSettings.setJavaScriptEnabled(true);             // 자바 스크립트 허용.  
        WebView.loadUrl( "http://google.com/" );            // 웹뷰에서 불러올 URL 입력
        webView.setWebViewClient(new Web)

    }
```
