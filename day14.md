# Day14

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
select * from professor where hpage IS NULL;
update professor set hpage= ' ' where hpage IS NULL;
~~~
-- bonus 에서 null처리 되어있는 분들 0으로표시
~~~sql
update professor set bonus=0 where bonus IS NULL;
~~~
-- emp2테이블에서 이씨 성 가진 사람들 중에 계약직인 사람들 인턴직으로 승진
~~~sql
update emp2 set emp_type='인턴직' where name like '이%' AND emp_type like '계약직';
~~~
