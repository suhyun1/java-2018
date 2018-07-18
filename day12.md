# Day12
~~~java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class EmployeeManager {
	private static List<Employee> employeeList= new ArrayList<>();
	static Scanner scan = new Scanner(System.in);


	public static void main(String[] args) {
		int userSel=-1;
		while(true) {
			System.out.println("메뉴를 선택하세요");
			System.out.println("1. 직원등록");
			System.out.println("2. 급여가 제일 많은 직원");
			System.out.println("3. 전체 직원 평균 급여");
			System.out.println("0. 종료");

			userSel = Integer.parseInt(scan.nextLine());

			if(userSel==1) {
				System.out.println("이름을 입력하세요");
				String name = scan.nextLine();

				System.out.println("나이를 입력하세요");
				int age = Integer.parseInt(scan.nextLine());

				System.out.println("급여(단위:만)를 입력하세요");
				int salary = Integer.parseInt(scan.nextLine());

				Employee employee = new Employee(name, age, salary);
				employeeList.add(employee);

				System.out.println("등록되었습니다");
			}

			else if(userSel ==2) {
				int max=0;
				int index=-1;
				for(int i=0;i<employeeList.size();i++) {
					if(max<employeeList.get(i).getSalary()) {
						max=employeeList.get(i).getSalary();
						index = i;
					}
				}

				System.out.println("급여가 제일 많은 직원은 "+employeeList.get(index).getName()+"입니다");

			}
			else if(userSel==3) {

				int sum =0;

				for(int i=0;i<employeeList.size();i++) {
					sum += employeeList.get(i).getSalary();
				}
				int aver = sum/employeeList.size();

				System.out.println("전체 직원의 평균 급여는 "+aver+"만원입니다");
			}
			else if(userSel==0)
				break;

		}
		System.out.println("프로그램을 종료하였습니다");
	}


}

~~~
