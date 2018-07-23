# Day15
#### 테이블 복사,  레코드 복사  
~~~sql
create table 복사할 테이블명;
  as select 복사할 필드명,... from 테이블명
~~~
ex) 전체 복사
~~~sql
create table c_emp
  as select * from emp;
~~~
ex) 부분 복사, 조건 붙음
~~~sql
-- deptno가 20인 테이블에서 ename, job, deptno 필드만 복사
create table c_emp_20
  as select ename, job, deptno from emp where deptno=20;
~~~

\* 구조물만 복사하길 원할때
~~~sql
create table c_emp2
  as
  select * from emp where 1=0; -- 조건에 맞지 않게 지정
~~~

***
**order by**
>해당 컬럼을 오름차순으로 정렬하여 결과를 출력한다. <br>두 개의 컬럼을 지정할 경우는 첫 컬럼별로 정렬 후, 다시 두번째 컬럼으로 정렬한다.

~~~sql
select * from emp order by ename desc;
select * from emp order by 2 desc; --필드명 대신 번호(칼럼 순서)도 가능
~~~
***
#### union
> 2개 테이블의 레코드 합침

union
~~~sql
select * from emp
  union --중복 제거
   select * from c_emp;
~~~
union all
~~~sql
select * from emp
  union all --중복 포함
  select * from c_emp;
~~~


 ** 필드 개수와 data type 일치시켜야 함
~~~sql
select empno, ename, job, sal  from emp
union
select * from c_emp3;
~~~
***
\* cast 함수 - 데이터 형식 변환 함수
~~~sql
cast(sal *1.15 as int)
-- sal 1.15배하고 정수형으로
~~~
#### subquery
> 메인 쿼리 안에서 또 다른 쿼리문이 있는 것. 반드시 서브쿼리를 괄호로 묶는다.

ex) 평균 급여보다 적게 받는 사람들 출력
~~~sql
select avg(pay) from emp2;
select * from emp2 where pay< (select avg(pay) from emp2);
~~~
ex) 이윤나 학생과 동일한 전공을 가지는 사람들 출력
~~~sql
select name, deptno1 from student
where deptno1=( select deptno1 from student where name like '이윤나');
~~~
#### View
>가상의 테이블. 보안을 위해 사용함.<br>
원본이 사라지면 가상의 테이블도 사라짐

view 생성
~~~sql
create view v_emp
as
select job "직위", ename "이름", sal "급여" from emp where deptno=30;
~~~
view 삭제
~~~sql
drop view v_emp;
~~~
ex) 그룹함수로 view만들기
~~~sql
create view d
as
select  max(sal) 최대급여, min(sal) 최소급여, round(avg(sal)) 급여평균 from EMP;
--그룹함수가 필드명이 될 수 없어 별칭 넣어줘야함
~~~
*having* 이용해 조건 넣기
~~~sql
create view v_student_grade
as
select grade 학년, avg(height) 평균키, round(avg(weight),1) 평균몸무게
from student
group by grade
having avg(height) >=165 and avg(weight)>=60;
~~~

#### SEQUENCE
> - 유일한 값을 생성해주는 오라클 객체이다.
- 시퀀스를 생성하면 기본키와 같이 순차적으로 증가하는 컬럼을 자동적으로 생성 할 수 있다.

~~~sql
CREATE SEQUENCE seq_name
  START WITH 10 --시퀀스의 시작 값
  INCREMENT BY 10; --시퀀스의 증가 값
  ~~~
