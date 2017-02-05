##Runtime Permission
---------
�ȵ���̵�� 6.0���� �۹̼� ���� ��������� �����Ͽ���. �������� ��ġ ������ �� �� �� ������� �㰡�� �޾����� ������ �����߿� Ư�� ����� ����� ������ ������� �㰡�� ������ �޾ƾ� �Ѵ�.

###�۹̼� ����

![](https://developer.android.com/reference/android/Manifest.permission.html)
---------

�ȵ���̵� 6.0�� �۹̼� ���� ������ ���� ��ô ��ٷο�����. �̷� ��Ȳ���� ���� �۹̼� ������ �ִ��� ���������� �Ͽ� ������� ������ ���߾�� �Ѵ�.
1. �ʿ��� �۹̼��� �ּ�ȭ�Ѵ�.
2. �۹̼� ��û�� ������ �ʰ� �Ѵ�.
3. ������ ª�� �ٽ������� �ۼ��Ѵ�.

- ��ȿ�� üũ
- ������ �ʿ��� ��� ó��
- ���� ȹ���� ���� API
- ��� ó�� onRequestPermissionResult(����, ���п� ���� ������ ����ִ�.

Permission Source Code

*���� üũ

``` 
private final int REQ_CODE = 100;

        // 1. ����üũ
        @TargetApi(Build.VERSION_CODES.M) // Target ���� �ֳ����̼�
        private void checkPermission () {
            // 1.1 ��Ÿ�� ����üũ
            if (checkSelfPermission(Manifest.permission.WRITE_EXTERNAL_STORAGE)
                    != PackageManager.PERMISSION_GRANTED
                    ) {
                // 1.2 ��û�� ���� ��� �ۼ�
                String permArr[] = {Manifest.permission.WRITE_EXTERNAL_STORAGE};
                // 1.3 �ý��ۿ� ���ѿ�û
                requestPermissions(permArr, REQ_CODE);
            } else {
                working();
            }
        }

```

*Ȯ�� �� �ý����� ȣ���ϴ� �Լ�
```
	// 2. ����üũ �� �ݹ� < ����ڰ� Ȯ���� �ý����� ȣ���ϴ� �Լ�
        @Override
        public void onRequestPermissionsResult ( int requestCode, @NonNull String[] permissions,
        @NonNull int[] grantResults){
            super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            if (requestCode == REQ_CODE) {
                // 2.1 �迭�� �ѱ� ��Ÿ�ӱ����� üũ�ؼ� ������ ������
                if (grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    // 2.2 ���α׷� ����
                    working();
                } else {
                    Toast.makeText(this, "������ ������� �����ø� ���α׷��� ������ �� �����ϴ�.", Toast.LENGTH_LONG).show();
                    // ���� : 1 ����, 2 ����üũ �ٽ� �����
                    finish();
                }
            }
        }
```


