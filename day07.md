# Day07

### 상속
>' is a' 관계

~~~java
public class Employee extends Person{
	int salary;

}

public class Student extends Person{
	int score;
}

public class Person{
	String name;
	int age;
	public void wakeup(){

	}
}
~~~



### 오버라이딩
> 부모클래스가 정의한 멤버 변수, 함수를 자식이 다시 또 만드는 것

~~~java
class Parent{
	int data=100;

//	public Parent() {
//		System.out.println("나는 parent 생성자");
//		
//	}

	public Parent(String msg) {
		System.out.println(msg+"를 출력하는 생성자");
	}
	public void print() {
		System.out.println("Parent의 data: "+data);
	}
}

class Child extends Parent{
	int data =200;

	public Child() {
//		자식클래스가 객체화 될때 부모클래스의 기본 생성자 '묵시적'으로 호출
		super("hello");  //부모클래스의 기본생성자가 없는 경우 '명시적'으로 부모클래스의 생성자 호출
		System.out.println("나는  Child의 생성자");

	}
	public void print() {
		int data = 300;
		System.out.println("Child의 data: "+ data);
		System.out.println("this.data: "+ this.data);
		System.out.println("super.data: "+ super.data);
	}
}
public class Test {
	public static void main(String[] args) {
		Child c = new Child();
		c.print();
	}
}
~~~

> 부모 클래스의 private 멤버는 자식이 접근 할 수 없음

### 패키지

- 하나의 패키지에 같은 이름의 클래스 X .

* 이클립스에서는 파일구조처럼 사용하므로 하나의 자바파일에 하나의 클래스를 넣는 것이 좋음

- 다른 패키지의 클래스를 사용하려면 1. 풀네임으로 부르거나 2. import문 사용


SimpleDateFormat : 문자열과 Date 사이 변환


#### StringTokenizer 클래스
문자열을 분석하여 토큰으로 분리시켜주는 기능을 제공
- boolean hasMoreTokens() : 다음 토큰 가지는지
- String nextToken() : 다음 토큰 반환
- String nextToken(String delim) : 다음토큰 반화하고, 분리자 delim으로 설정


~~~ java
import java.util.StringTokenizer;

public class StringTest {
	public static void main(String[] args) {
		StringTokenizer st = new StringTokenizer("Will Java change my life?"," ");
		while(st.hasMoreTokens()) {
			System.out.println(st.nextToken());
		}
	}
}
~~~
실행 결과
~~~
Will
Java
change
my
life?
~~~
