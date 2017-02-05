##Runtime Permission
---------
안드로이드는 6.0부터 퍼미션 모델을 대대적으로 수정하였다. 이전에는 설치 시점에 딱 한 번 사용자의 허가를 받았지만 이제는 실행중에 특정 기능을 사용할 때마다 사용자의 허가를 일일이 받아야 한다.

###퍼미션 종류

![](https://developer.android.com/reference/android/Manifest.permission.html)
---------

안드로이드 6.0의 퍼미션 모델은 이전에 비해 무척 까다로워졌다. 이런 상황에서 앱은 퍼미션 관리를 최대한 지능적으로 하여 사용자의 비위를 맞추어야 한다.
1. 필요한 퍼미션을 최소화한다.
2. 퍼미션 요청은 가급적 늦게 한다.
3. 설명은 짧고 핵심적으로 작성한다.

- 유효성 체크
- 설명이 필요한 경우 처리
- 권한 획득을 위한 API
- 결과 처리 onRequestPermissionResult(성공, 실패에 대한 정보가 들어있다.

Permission Source Code

*권한 체크

``` 
private final int REQ_CODE = 100;

        // 1. 권한체크
        @TargetApi(Build.VERSION_CODES.M) // Target 지정 애너테이션
        private void checkPermission () {
            // 1.1 런타임 권한체크
            if (checkSelfPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE)
                    != PackageManager.PERMISSION_GRANTED
                    ) {
                // 1.2 요청할 권한 목록 작성
                String permArr[] = {Manifest.permission.WRITE_EXTERNAL_STORAGE};
                // 1.3 시스템에 권한요청
                requestPermissions(permArr, REQ_CODE);
            } else {
                working();
            }
        }

```

*확인 후 시스템이 호출하는 함수
```
	// 2. 권한체크 후 콜백 < 사용자가 확인후 시스템이 호출하는 함수
        @Override
        public void onRequestPermissionsResult ( int requestCode, @NonNull String[] permissions,
        @NonNull int[] grantResults){
            super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            if (requestCode == REQ_CODE) {
                // 2.1 배열에 넘긴 런타임권한을 체크해서 승인이 됬으면
                if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    // 2.2 프로그램 실행
                    working();
                } else {
                    Toast.makeText(this, "권한을 허용하지 않으시면 프로그램을 실행할 수 없습니다.", Toast.LENGTH_LONG).show();
                    // 선택 : 1 종료, 2 권한체크 다시 물어보기
                    finish();
                }
            }
        }
```


