# Day12

employee 프로그램
~~~java
~~~

### 입출력
입출력: 우리 프로세스 밖의 누군가와 데이터 주고받는 것<br>
스트림: 순서가 있는 데이터의 연속적인 흐름.<br>

파일은 프로세스 밖의 존재.

##### 스트림
스트림의 분류:<br>
입출력의 단위에 따라 바이트스트림, 문자스트림으로 나뉨

파일에 쓰기
~~~java
package fileio;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileStreamTest {
	public static void main(String[] args) {

//		1.FileOutputStream 객체 생성
//		 2.출력하고자 하는 데이터 바이트배열로 준비
//		 3.write메소드를 통해 데이터 출력
//		 4.스트림 닫기!!!

		FileOutputStream fo = null;

		try {
			fo = new FileOutputStream("myfile.txt");	//목적지지정

			for(int i=65;i<123;i++) {
				fo.write(i);
			}
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		finally {
			try {	//스트림 닫기

				if(fo!=null)
					fo.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}
}
~~~

파일 읽기
~~~java
package fileio;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class FileStreamTest1 {
	public static void main(String[] args) {
		FileInputStream fi = null;
		try {
			fi = new FileInputStream("myfile.txt");
			int data;
			while((data = fi.read())!=-1) {
				System.out.println(data);
			}
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		finally {
			try {

				if(fi!=null)
					fi.close();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
	}
}

~~~
