# Day14
\\\\70.12.112.50
### 레코드 삽입, 수정, 삭제
**DML 명령어: insert, upadate, delete, select**
#### 레코드 삽입
>insert into 테이블이름values(값, 값, ...)<br>

*필드순서 모를때*
~~~sql
insert into multi(name, address, age) values('김나나', 'bb', 30);
~~~

#### 레코드 수정
>update 테이블이름
set 컬럼명=변경값, 컬럼명=변경값, 컬럼명=변경값, .....
[ where 조건식]

ex)

-- pay300 이하인 사람들의 급여에 5% 인상
~~~sql
update professor set pay=pay*1.05 where pay<300;
~~~
-- homepage 없는 교수들 출력해서 null표시 삭제
~~~sql
select * from professor where hpage is not null; -- hpage가 있는 교수들 출력하기
select * from professor where hpage IS NULL;
update professor set hpage= ' ' where hpage IS NULL;
select * from professor where hpage is null or hpage = ' '; -- 수정 후에 홈페이지 없는 사람들 찾기
-- hpage = null (X) hpage is null (O)
~~~
-- bonus 에서 null처리 되어있는 분들 0으로표시
~~~sql
update professor set bonus=0 where bonus IS NULL;
~~~
~~~sql
update professor set bonus =nvl(bonus,0) where bonus is null;
~~~
*nvl(값, 대치값) -값에null이있으면대치값으로변경한다.*

-- emp2테이블에서 이씨 성 가진 사람들 중에 계약직인 사람들 인턴직으로 승진
~~~sql
update emp2 set emp_type='인턴직' where name like '이%' AND emp_type like '계약직';
~~~

*실행취소*
~~~sql
rollback;
--rollback은 DML명령어에서만 적용됨(select, insert, delete, update)
~~~
*실행완료*
~~~sql
commit;
~~~

#### 레코드 삭제
delete 테이블 이름 (조건식);

truncate table 테이블 이름; (레코드 전체삭제, 구조는 남음)

*테이블 자체 없애기 - drop table 테이블 이름*

ex)

-- 계약직인 직원 찾아서 삭제하기
~~~sql
select * from emp2 where emp_type ='계약직';
delete emp2 where emp_type ='계약직';
~~~

***

####  연산자
-- 컬럼명 in(값, 값, ...)

~~~sql
-- 1,2,3 학년인 학생 찾기
select * from student where grade=1 or grade=2 or grade=3;
select * from  student where grade in(1,2,3);
~~~
-- between a and b (a이상 b이하)

~~~sql
select * from student where weight between 40 and 60;
~~~

***
####  함수

집합함수(그룹함수) - 여러 개의 데이터에 대해 하나의 값을 만들어냄

-- 컬럼의 합과 평균: sum(칼럼명) , avg(칼럼명)
~~~sql
select sum(weight) as "몸무게의 합", avg(weight) as "몸무게의 평균" from student;
~~~

-- 최대값과 최소값 max(칼럼명) , min(칼럼명)
~~~sql
select max(pay), min(pay) from professor;
~~~
*그룹필드와 일반 필드 함께 쓸 수 없음. <br>
함께 쓰려면 그룹화해야함 :
**group by***

 ex) 학생 테이블에서 학년 별로 몸무게와 키의 합
~~~sql
select sum(weight), sum(height)
  from student
  group by grade; --일반 컬럼명은 group by에 넣어줘야 함
~~~
 그룹별로 출력됨
***
#### JOIN
> 두 개 이상의 테이블 들을 연결 또는 결합하여 데이터를 출력하는 것
(primary, foreign key 관계만 )

** inner join **
~~~sql
select ename, job, sal, d.deptno, dname, loc
  from emp e join dept d  
  on e.deptno = d.deptno; --일차하는 경우 출력
~~~
** outer join **
