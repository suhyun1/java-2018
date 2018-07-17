# Day10

## 예외처리

~~~java
public class CheckingExceptionTest {
	public static void main(String[] args) {

		try {
			doSomething();
		} catch (InterruptedException e) {
		}
	}

	public static void doSomething() throws InterruptedException {
  //throws 사용하면 예외를 상위 메소드로 전달
		for (int i = 10; i > 0; i--) {
			Thread.sleep(1000); //1000ms (1초)

			if (i == 3)
				System.out.println(i);
		}
	}
}
~~~

사용자 정의 함수 사용하기
~~~java
//사용자 정의 예외
public class DivideByZeroException extends ArithmeticException {

	public DivideByZeroException() {
		super("0으로 나눌수는 없음");	//부모 클래스의 생성자
	}

	public void doSomething() {
		System.out.println("0으로 나눴으니 이런거해야겠다");
	}
}

public class ExceptionTest {
	public static void main(String[] args) {
		double result;
		try {
			result = quotient(1,0);

		}catch (DivideByZeroException e){
			System.out.println(e.toString());
			e.doSomething();	//예외의 경우 수행할 동작

		}
	}
	public static double quotient (int n, int d) throws DivideByZeroException{

		if(d==0) {
			throw new DivideByZeroException();
      //throw 키워드는 실제로 예외를 동작시키게함
		}
		return (double) n/d;
	}
}
~~~

## 스레드
프로세스는 프로그램의 실행단위. 프로세스는 최소하나의 스레드를 가짐. 이것을 메인 스레드라고 함.<br> 메인스레드 종료=> 프로세스 종료

컴퓨터에서 병렬처리 구현하는 방법
1. 멀티프로세서   
각 프로레서가 별도의 메모리 공간 가짐. 어떻게 데이터 공유할지
2. 멀티스레드<br>
여러개의 명령 흐름이 하나의 메모리 공간을 공유함. 어떻게 교통정리할지

명령처리 흐름이 Thread라는 객체로 표현됨

명령흐름이 대기해야됨에도 불구하고 동시에 다른 작업을 하고 싶을 때 스레드 사용

멀티스레드 사용하는 방법<br>
thread 상속하여 run함수를 오버라이드하거나
Runnable 인터페이스 상속<br>
 파생스레드가 수행할 동작을 run함수에 정의하고, 스레드 객체의 start호출

~~~java
public class MyRunnable implements Runnable {

	String myName;
	public MyRunnable(String name) {
		myName = name;
	}

	@Override
	public void run() {
		for(int i=0;i<10;i++) {
			System.out.println(myName +i);
		}
	}
}

public class TestThread {
	public static void main(String[] args) {
		Thread t1 = new Thread(new MyRunnable("First Thread"));
		Thread t2 = new Thread(new MyRunnable("Second Thread"));
		t1.start();
		t2.start();
	}
}
~~~

동기화 방법 - synchronized: 한순간에 하나의 스레드만을 허용함
~~~java
public class BankAccount {
	int balance;
	public synchronized void deposit(int amount) {
		balance += amount;

	}
	public synchronized void withdraw(int amount) {
		balance -= amount;

	}
	public synchronized int getBalance() {
		return balance;
	}
}
~~~
