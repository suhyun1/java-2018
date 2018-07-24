# Day16
### JDBC

#### JDBC 연결하기
1.드라이브 로드
~~~
Class.forName("oracle.jdbc.driver.OracleDriver");
~~~
C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib\ojdbc6.jar  
2.연결
~~~
Connection conn = DriverManager.getConnection(url, user, pw);
//연결객체
~~~
3.sql명령어 사용
~~~
statement stat = conn.createStatement("select * from gift");
result rs = connn. stat.executeQuery(); //반환 값이 있는 경우

stat.executeUpdate(sql); //반환 값이 없는 경우(select문 제외한 dml 명령어)
~~~
4.닫기
~~~
rs.close();
stat.close();
conn.close();
~~~

#### 예제
- select문

~~~java
import java.sql.*;

public class GiftSelect {
	public static void main(String[] args) throws ClassNotFoundException, SQLException {
		// 1. 드라이버 로드
		Class.forName("oracle.jdbc.driver.OracleDriver");

		// 2. connection & open //driver@IP:portNumber:SID (or 전역데이터베이스명)
		String url = "jdbc:oracle:thin:@127.0.0.1:1521:XE";
		String user = "suhyun";
		String password = "oracle";
		Connection conn = DriverManager.getConnection(url, user, password);

		// 3. 사용(dml- select)
		Statement stmt = conn.createStatement();
		ResultSet rs = stmt.executeQuery("SELECT * FROM GIFT");

		System.out.println("상품번호\t상품명\t최저가\t최고가");
		while(rs.next()) {		//다음칸으로 내림
			int gno = rs.getInt(1);
			String name = rs.getString("gname"); //2
			int g_s = rs.getInt("g_start");
			int g_e = rs.getInt("g_end");

			System.out.println(gno+"\t"+name+"\t"+g_s+"\t"+g_e);
		}

		//4. 자원반환
		rs.close();
		stmt.close();
		conn.close();

	}
}
~~~

- insert문

~~~java
package ex03.jdbc;

import java.sql.*;

public class GiftInsert {
	public static void main(String[] args) throws ClassNotFoundException, SQLException {
		// 1. 드라이버 로드
		Class.forName("oracle.jdbc.driver.OracleDriver");

		// 2. connection & open //driver@IP:portNumber:SID (or 전역데이터베이스명)
		String url = "jdbc:oracle:thin:@127.0.0.1:1521:XE";
		String user = "suhyun";
		String password = "oracle";
		Connection conn = DriverManager.getConnection(url, user, password);

		// 3.
		Statement stmt = conn.createStatement();

		// insert into gift values(11,'아이패드',1000,100000); 이 문장 수행하려면
		// String sql = "insert into gift values("+11+",'"+"아이패드"+"',"+1000+","+100000+")";
		// sql문 문자열 취급

        //여러 값을 넣을 때 메인에 입력해주는 방법도 있음 (run as configuration 에서 실행)
		String sql = "insert into gift values(" + args[0] + ",'" + args[1] + "'," + args[2] + "," + args[3] + ")";

		System.out.println(sql.toString());
		int result = stmt.executeUpdate(sql); // 실제 명령 실행
		System.out.println(result + "데이터 추가 성공함");

	}
}

~~~

-
