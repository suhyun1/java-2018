# Day09
### 인터페이스
>추상 클래스를 모아둠

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

	public void move() {
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
#### 내부클래스

### 예외처리
~~~
try{
  예외가 발생할 수 있는 코드
} catch{
  예외 발생시 실행하는 코드
}
~~~
