# Day16
### JDBC

#### JDBC 연결하기
1.드라이브 로드
~~~
Class.forName("oracle.jdbc.driver.OracleDriver");
~~~
C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib\ojdbc6.jar 을 jar lib에 넣어줌  

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
        //방법1
		// String sql = "insert into gift values("+11+",'"+"아이패드"+"',"+1000+","+100000+")";
		// sql문 문자열 취급

        //방법2. 여러 값을 넣을 때 메인에 입력해주는 방법도 있음 (run as configuration 에서 실행)
		//String sql = "insert into gift values(" + args[0] + ",'" + args[1] + "'," + args[2] + "," + args[3] + ")";

        //방법3.
        String sql = "insert into gift values(" + scan.nextInt() + ",'" + scan.next() + "'," + scan.nextInt() + "," + scan.nextInt() + ")";

		System.out.println(sql.toString());
		int result = stmt.executeUpdate(sql); // 실제 명령 실행
		System.out.println(result + "데이터 추가 성공함");

	}
}

~~~
***
\* 반복적인 문장 구현하지 않도록 클래스를 만들자

connection 관련 클래스
~~~java
package dbConn.util;

import java.sql.*;
//반복적인 것 구현하지 않도록
public class ConnectionHelper {

	public static Connection getConnection(String dsn) {
		Connection conn = null;

		try {
			if(dsn.equals("mysql")) {
				Class.forName("com.mysql.jdbc.Driver");
				conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/sampleDB",
						"suhyun", "oracle");
			}else if(dsn.equals("oracle")) {
				Class.forName("oracle.jdbc.OracleDriver");
				conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:XE",
						"suhyun", "oracle");
			}

		} catch (Exception e) {
			e.printStackTrace();
		} finally {

			return conn;
		}

	}

	public static Connection getConnection(String dsn, String userid, String pwd) {
		Connection conn = null;

		try {
			if(dsn.equals("mysql")) {
				Class.forName("com.mysql.jdbc.Driver");
				conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/sampleDB",
						userid, pwd);
			}else if(dsn.equals("oracle")) {
				Class.forName("oracle.jdbc.OracleDriver");
				conn = DriverManager.getConnection("jdbc:oracle:thin:@127.0.0.1:1521:XE",
						userid, pwd);
			}

		} catch (Exception e) {
			e.printStackTrace();
		} finally {

			return conn;
		}
	}

}
~~~
close 관련 클래스
~~~java
package dbConn.util;

import java.sql.*;

public class CloseHelper {

	public static void close(Connection conn) {
		if(conn!=null)
			try {
				conn.close();
			} catch (Exception e) {
				e.printStackTrace();

			}
	}
	public static void close(Statement stmt ) {
		if(stmt!=null)
			try {
				stmt.close();
			} catch (Exception e) {
				e.printStackTrace();

			}
	}

	public static void close(ResultSet rs) {
		if(rs!=null)
			try {
				rs.close();
			} catch (Exception e) {
				e.printStackTrace();

			}
	}
	public static void close(PreparedStatement pstmt) {
		if(pstmt!=null)
			try {
				pstmt.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
	}
}
~~~
***
- update

~~~java
public class GiftUpdate {
	public static void main(String[] args) throws Exception{ //예외처리위임

		Connection conn = ConnectionHelper.getConnection("oracle");
		//3. dml - update 사용
		Statement stmt = conn.createStatement();
		PreparedStatement pstmt = null;
		ResultSet rs = stmt.executeQuery("SELECT * FROM GIFT");

		System.out.println("상품번호\t상품명\t최저가\t최고가");
		while(rs.next()) {		//다음칸으로 내림
			int gno = rs.getInt(1);
			String name = rs.getString("gname"); //2
			int g_s = rs.getInt("g_start");
			int g_e = rs.getInt("g_end");

			System.out.println(gno+"\t"+name+"\t"+g_s+"\t"+g_e);
		}

		//레코드 업데이트
		System.out.println("\n목록에서 update할 번호");
		int num = new Scanner(System.in).nextInt();

		System.out.println("gno를 몇번으로 바꾸시겠습니까");
		int gno = new Scanner(System.in).nextInt();

		pstmt = conn.prepareStatement("update gift set gno = ? where gno="+num);

		pstmt.setInt(1, gno);
		pstmt.executeUpdate();

		System.out.println(gno+" 수정이 완료되었습니다.");

	}
}
~~~
\* 다양한 update문 사용 예

~~~java
pstmt = conn.prepareStatement(
"update gift set gno = ?, gname = ? where gno=?");

System.out.println("\n목록에서 update할 번호");
int num = new Scanner(System.in).nextInt();
pstmt.setInt(3, num); //3번쨰 물음표

System.out.println("gno 변경: ");
pstmt.setInt(1, new Scanner(System.in).nextInt()); //1번째 물음표

System.out.println("gname 변경:");
pstmt.setString(2, new Scanner(System.in).next());  //2번째 물음표

pstmt.executeUpdate();
~~~
- delete

~~~java
public class GiftDelete {
	public static void main(String[] args) throws Exception{

		Connection conn = ConnectionHelper.getConnection("oracle");


		PreparedStatement pstmt = null;
		// 3. dml - delete 사용

		pstmt = conn.prepareStatement("delete gift where gname = ?");

		System.out.println("변경할 상품명: ");
		String name = new Scanner(System.in).next();
		pstmt.setString(1, name);

		int result  = pstmt.executeUpdate();

		System.out.println(result+" 제거되었습니다");

		CloseHelper.close(conn);
		CloseHelper.close(pstmt);
	}
}
~~~
