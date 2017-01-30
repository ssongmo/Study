#Activity LifeCycle

https://kairo96.gitbooks.io/android/content/pic2/2-4-1-1.jpg

* ��Ƽ��Ƽ �����ֱ�� onCreate() -> onStart() -> onResume() -> onPause() -> onStop() -> onDestory()������ ����Ǹ�, ��쿡 ���� onRestart() �޼ҵ尡 ȣ��Ǳ⵵ �Ѵ�. 

* ��Ƽ��Ƽ�� 4���� ����

- (��) Active : ���� Ȱ��ȭ�ǰ� �ִ� â�̴�.�� ��Ƽ��Ƽ�� Ȱ��ȭ�Ǹ� ������ Ȱ���� ��Ƽ��Ƽ�� Pause�� �ȴ�.
- (��) Pause : ������ ��Ƽ��Ƽ�� Ȱ��ȭ�� ��Ƽ��Ƽ�� ������ ��Ƽ��Ƽ�� �Ϻ� ������ �����̴�. ��Ƽ��Ƽ�� ������ �������� �Ǹ� ������ ��Ƽ��Ƽ�� Stop ���°� �ȴ�.
- (��) Stop : ȭ�鿡 ��Ÿ���� �ʴ� ��Ƽ��Ƽ�̴�. ��Ƽ��Ƽ�� ȭ�� ������ �����ų� ������ ���� �� ��Ƽ��Ƽ�� Inactive�� �ȴ�.
- (��) Inactive : activity stack���� ���ŵ� �����̴�. �ٽ� ȭ�鿡 ��Ÿ���� ���ؼ��� ����۵Ǿ�� �Ѵ�.

#App Architecture

���ø����̼� ��Ű��ó�� ���ø��ɼ��� �����ϰ� �����ϴ� �۾��� ǥ��ȭ �� ���̴�. ǥ��ȭ�� �۾��� ���ø����̼� �����ֱ⸦ �����Ű�� �ٸ� ���� �ڵ�͵� �����ϴ� ���� �����ϴ�. ��Ű��ó ���� �߿� ���� ���� ���Ǵ� ���� MVC �����̴�.

MVC�� ��, ��, ��Ʈ�ѷ��� �ǹ��Ѵ�.
```
�� : ���ø����̼ǿ� ���Ǵ� �������� �Ϲ����� ����
�� : ����ڿ��� �����͸� ��Ÿ����.
��Ʈ�ѷ� : ���ø����̼��� �̺�Ʈ�� ���� ó���� �𵨰� �� ���̿��� ����� ������ �����̴�.
MVC ��Ű��ó�� ������ �� Ŭ�������� ������ �и��� ���ǵǾ��ֱ� ������ ���� �׽�Ʈ�� ������ ���� �ڵ带 ������ �� �ִ�.
```

##Ŀ���� ������(WebView)

Ŀ���� �������� ���������� ���ο� ȭ������ ��ȯ���� �ʰ� ȭ�� ������� ����Ǵ� ���� ���Ѵ�.

1. ���ͳ� ���� �ֱ�

http://cfile27.uf.tistory.com/image/215D0C3D543D0A0E141370

2. .xml�� ���� �׸���

```
<WebView

        android:id="@+id/WebView1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_alignParentLeft="true"
        android:layout_alignParentTop="true" />
```

3. ainActivity.java ���Ͽ� ���並 �ҷ��������� �ҽ��� �Է�

```
private WebView mWebView;    // ���� ����
private WebSettings mWebSettings; //���� ����
```

```
@Override

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        WebView = (WebView) findViewById(R.id.WebView);
        WebView.setWebViewClient(new WishWebViewClient());  //���� ��â �ȶ߰� ����.       
        WebSettings = mWebView.getSettings();
        
        WebSettings.setJavaScriptEnabled(true);             // �ڹ� ��ũ��Ʈ ���.  
        WebView.loadUrl( "http://google.com/" );            // ���信�� �ҷ��� URL �Է�
        webView.setWebViewClient(new Web)

    }
```
