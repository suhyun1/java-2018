# Day11
## 지네릭스
객체를 생성할 때 다룰 객체의 타입을 미리 명시해줌으로써 형변환을 줄여준다

~~~java
class Box<T>{
	T data;
	public void setData(T data) {
		this.data = data;
	}
	public Object getData() {
		return data;
	}
}
public class Test {
	public static void main(String[] args) {
		Box<String> b = new Box<String>();

		b.setData("???");
		System.out.println(b.getData());
	}
}
~~~

## 컬렉션 프레임웤
컬렉션은 자바에서 자료구조를 구현한 클래스<br>
자료구조로는 리스트, 스택, 큐, 집합(set), 해쉬 테이블 등이 있다.
- List:
 순서가 있는 데이터 모임. 각각의 데이터는 순서(인덱스)로 구분
- Set:
순서가 없는 데이터 모임. 각각의 데이터 구분이 안됨. 중복이 없음!
- Map:
 이름이 있는 데이터 모임. (key, value) 형태의 데이터 모임

위의 내용 중요하다!

### List
가변길이 배열에 쓸 수 있음
##### Array List
~~~java
import java.util.ArrayList;

public class ListTest {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<String>();

		list.add("MILK");
		list.add("BREAD");
		list.add("BUTTER");
		list.add(1,"APPLE");
		list.set(2, "GRAPE");
		list.remove(3);

		for(int i=0;i<list.size();i++)
			System.out.println(list.get(i));
	}
}
~~~

##### Linked List
~~~java
import java.util.LinkedList;

public class ListTest {
	public static void main(String[] args) {
		LinkedList<String> list = new LinkedList<String>();

		list.add("MILK");
		list.add("BREAD");
		list.add("BUTTER");
		list.add(1,"APPLE");
		list.set(2, "GRAPE");
		list.remove(3);

		for(int i=0;i<list.size();i++)
			System.out.println(list.get(i));
	}
}
~~~
출력 결과는 같음

ArrayList: 읽기 빠르지만 추가/삭제는 느림(순차적인 추가삭제는 더 빠름)<br>
LinkedList: 읽기는 느리지만 추가/삭제 빠름()

### Set
~~~java
import java.util.HashSet;

public class ArrayListTest {
	public static void main(String[] args) {
		HashSet<String> set = new HashSet<String>();

		set.add("Milk");
		set.add("Bread");
		set.add("Butter");
		set.add("Cheese");
		set.add("Ham");
		set.add("Ham");


		System.out.println(set);
	}
}
~~~
출력결과
~~~
[Ham, Butter, Cheese, Milk, Bread]
~~~
- Set은 중복안됨
- 순서가 없음

원소 하나씩 접근하기
- 반복자(iterator): 컬렉션의 원소들을 하나씩 처리하는데 사용

~~~java
//중복검사
import java.util.HashSet;
import java.util.Set;

public class FindDupplication {

	public static void main(String[] args) {
		Set<String> s = new HashSet<String>();

		String[] sample = {"단어", "중복","구절","중복"};
		for(String a : sample)
			if(!s.add(a))
      	//추가가 안되었을 때 (add()는 추가결과 알려줌)
				System.out.println("중복된 단어: "+a);

		System.out.println(s.size()+" 중복되지 않은 단어: "+s);
	}

}
~~~

### Map
~~~java

class Student{
	int number;
	String name;
	public Student(int number, String name) {
		this.number= number;
		this.name=name;
	}
	@Override
	public String toString() {
		return name;
	}
}
~~~
~~~java
import java.util.HashMap;
import java.util.Map;
public class MapTest{
	public static void main(String[] args) {
		Map<String, Student> st = new HashMap<String, Student>();
		st.put("20090001", new Student(20090001,"구준표"));
		st.put("20090002", new Student(20090002,"금잔디"));
		st.put("20090003", new Student(20090003,"윤지후"));

		System.out.println(st);

		//Map 탐색 1 Entry단위로 탐색
		for(Map.Entry<String, Student> s : st.entrySet()) {
//			s.getKey();
//			s.getValue();
			System.out.println(s.getValue());
		}
		//Map에서 데이터 가져올땐 키 값으로 질의
		System.out.println(st.get("20090001"));

		//Map 탐색2. key로 접근
		for(String k : st.keySet())
			System.out.println(st.get(k));
	}

}
~~~
