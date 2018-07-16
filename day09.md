# Day09
### 인터페이스
>추상 클래스를 모아둠. (일반 메소드 또는 멤버 변수 가질 수 없음)
독립적인 프로그래밍이 가능해짐


  #### 의존성 주입
~~~java
public class Taekwon extends Robot {
	//private PunchAttack attack = new PunchAttack();
	//Taekwon이 PunchAttack에 의존함. 객체만들면서, 타입만들면서 의존

	//private Attack attack = new PunchAttack(); //느슨하게 의존 (Attack에 의존)
	//PunchAttack 만들어야하나?-> setter를 통해 누군가 대신 만들어주면? (의존성 주입)


	private Attack attack;
	public void setAttack(Attack attack) {
		this.attack = attack;
	}
	//의존관계 역전
	//누군가 punchAttack을 만들어서 내 setAttack에 넣어줘야
}
~~~
그래서.. Move와 Attack Interface를 만들고, 각각의 attack들과 move들 클래스에서 인터페이스를 상속 받고 기능을 구현한다.

~~~java

public class Robot {

	private Attack attack;
	private Move move;

	public void setAttack(Attack attack) {
		this.attack = attack;
	}
	public void setMove(Move move) {
		this.move = move;
	}

	pub lic void move() {
		move.move();
	}
	public void attack() {
		attack.attack();
	}
	public void fight() {
		move();
		attack();
		move();
	}
}
~~~

~~~java
public class RobotTest {

	public static void main(String[] args) {
		PunchAttack pa = new PunchAttack();
		MissileAttack ma = new MissileAttack();
		WalkingMove wm = new WalkingMove();
		FlyingMove fm = new FlyingMove();

		Robot taekwon = new Robot();
		taekwon.setAttack(pa);
		taekwon.setMove(fm);

		Robot mazinga = new Robot();
		mazinga.setAttack(ma);
		mazinga.setMove(wm);

		taekwon.fight();
		mazinga.fight();
	}
}
~~~
#### 내부클래스
>내부클래스에서 외부 클래스의 멤버들을 쉽게 접근할 수 있음



### 예외처리
~~~
try{
  예외가 발생할 수 있는 코드
} catch{
  예외 발생시 실행하는 코드
} finally{
  오류 발생과 상관없이 항상 실행되어야 하는 코드
}
~~~
여러 종류의 catch를 넣을 수 있움<br>
catch도 위부터 읽음

##### 에러의 종류

자바에서는 예외도 객체로 처리됨. 이 예외를 만들기 위한 클래스들도 상속계층 구조 가짐<br>
IOException - 필수적 예외처리<br>
RuntimeException - 선택적 예외처리<br>
Error - 예외처리 대상 아님
