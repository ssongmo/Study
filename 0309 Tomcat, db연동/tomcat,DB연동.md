
## Tomcat & Database 연동하기


####  1. Tomcat Setting
```
$ tar xvfz apache-tomcat-8.0.30.tar.gz
$ sudo mkdir -p /usr/local
$ sudo mv ~/Downloads/apache-tomcat-8.0.30 /usr/local
$ sudo rm -f /Library/Tomcat         (기존 링크가 있다면 제거하자)
$ sudo ln -s /usr/local/apache-tomcat-8.0.30 /Library/Tomcat
$ sudo chown -R <사용자계정> /Library/Tomcat
$ sudo chmod +x /Library/Tomcat/bin/*.sh
```

*  Tomcat이 설정된 후 start.sh를 통해 시작해줘야 서버가 열린다. (종료시 shutdown.sh)

#### 2. .jsp 파일 생성
database를 배우면서 eclipse를 통해 사용했던 예제이다. 이 예제를 jsp파일로 변환한 소스이다.

```
//언어, 언어타입, 인코딩 타입을 설정해준다.
<%@ page language = "java" contentType = "application/json; charset=UTF-8" pageEncoding = "UTF-8"%>
//java에 import되어있는 것들을 한꺼번에 처리할 수 있다.
<%@ page import = "java.sql.*" %>

<%
		//이 공간이 서버영역.
		String id = "root";  //mysql id
		String pw = "1234";  //mysql root pw
		String dbName = "test1"; // db name
		String url = "jdbc:mysql://localhost:3306/"+dbName;

		Class.forName("com.mysql.jdbc.Driver");
		//동적으로 클래스를 로드 한다(new와 다른방식). 서버에 이런식으로 올라가서 식별자가 없는형태로 메모리에 올린다. 버전이 달라도 사용가능.
		Connection conn = DriverManager.getConnection(url, id, pw);

		//--------------------end Connection
		String parameter = request.getParameter("param");
		//query작성.
		String sql = "select * from bbs3 where title like '%"+parameter+"%';";

		//데이터베이스에 쓰기 위한 한개의 실행단위.
		Statement stmt = conn.createStatement();
		//쿼리 실행후 결과셋을 변수에 전달.
		ResultSet rs = stmt.executeQuery(sql);

//변수에 담긴 결과셋을 반복문을 돌면서 화면에 출력.

		//제이슨 만들기
		out.print("{");
		out.print("\"root\" :[");

		while(rs.next()){ //데이터셋이 있을때까지 반복.
				out.print("{");
	      int bbsno = rs.getInt("bbsno");
				String title = rs.getString("title");
				String content = rs.getString("content");
				String date = rs.getString("nDate");
				out.print("\"bsno\": "+ bbsno + ", \"title\": \"" +title+ "\", \"content\" :\"" +content+"\" ,\"date\" :\"" +date+ "\"");
				out.print("}");

				if(rs.next()){
						out.print(", ");
				}
				rs.previous();
		}

		out.print("] }");
    conn.close();
%>
```

#### 3. 주소창에 보이기
http://localhost:8080/dbconnect.jsp?param=rename:999 아래와 같은 식으로 parameter값을 select 할수 있다.
