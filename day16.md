# Day16
### JDBC

#### JDBC 연결하기
1.드라이브 로드
~~~
Class.forName("oracle.jdbc.driver.OracleDriver");
~~~

2.연결
~~~
Connection conn = DriverManager.getConnection(url, user, pw);
//연결객체
~~~
3.sql명령어 사용
~~~
statement stat = conn.createStatement("select * from gift");
result rs = connn. stat.executeQuery(); //반환 값이 있는 경우

stat.excuteUpdate(sql); //반환 값이 없는 경우
~~~
4.닫기
~~~
rs.close();
stat.close();
conn.close();
~~~
