# Day17

16일차 내용 dml명령어 합치기

deptCRUD.java
~~~java
package ex02.jdbc;
import java.sql.*;
import dbConn.util.*;
import java.util.Scanner;
public class deptCRUD {

	PreparedStatement pstmt = null;
	ResultSet rs = null;
	String sql;
	public Connection conn = null;
	Scanner scan = new Scanner(System.in);

	//연결
	public void connect() {
		conn = ConnectionHelper.getConnection("oracle");

	}

	//selectf
	public void selectAll() throws SQLException {
		pstmt = conn.prepareStatement("SELECT * FROM dept2");
		rs = pstmt.executeQuery();

		System.out.println("팀 번호\t부서이름\t부서번호\t지역");
		while(rs.next()) {
			String dcode = rs.getString(1);
			String dname = rs.getString(2);
			String pdept = rs.getString(3);
			String area = rs.getString(4);

			System.out.println(dcode+"\t"+dname+"\t"+pdept+"\t"+area );
		}

	}

	//insert
	public void insert() throws SQLException {

		pstmt = conn.prepareStatement("INSERT INTO DEPT2 VALUES(?,?,?,?)");

		System.out.println("팀번호, 부서 이름, 부서번호, 지역을 입력하세요");
		pstmt.setString(1,scan.next());
		pstmt.setString(2,scan.next());
		pstmt.setString(3,scan.next());
		pstmt.setString(4,scan.next());

		int result = pstmt.executeUpdate();
		System.out.println(result +" 행의 데이터가 추가되었습니다.");

		selectAll();
	}

	//update
	public void update() throws SQLException {
		selectAll();

		System.out.println("변경하고 싶은 팀의 번호를 입력하세요");
		String teamNum = scan.next();

		System.out.println("새로운 팀번호, 부서 이름, 부서번호, 지역을 입력하세요");


		pstmt = conn.prepareStatement("UPDATE DEPT2 SET DCODE=?, DNAME =?, PDEPT=?, AREA=? WHERE DCODE ="+teamNum);

		pstmt.setString(1,scan.next());
		pstmt.setString(2,scan.next());
		pstmt.setString(3,scan.next());
		pstmt.setString(4,scan.next());


		int result = pstmt.executeUpdate();
		System.out.println(result +" 행의 데이터가 수정되었습니다.");

		selectAll();
	}

	//delete
	public void delete() throws SQLException {

		selectAll();
		System.out.println("삭제하고 싶은 팀의 번호를 입력하세요");
		String teamNum = scan.next();

		pstmt = conn.prepareStatement("delete dept2 where dcode = "+teamNum);

		int result = pstmt.executeUpdate();
		System.out.println(result +" 행의 데이터가 삭제되었습니다.");

		selectAll();
	}

	//close (16일차에 작성한 dbConn 임포트함)
	public void close() {
		CloseHelper.close(conn);
		CloseHelper.close(rs);
		CloseHelper.close(pstmt);

	}
}
~~~
