# Day13

### 설치하기
- oracle Database 11g
- sql developer (압축풀기)

##### Run SQL Command Line<br>
*서비스가 실행되지 않은 경우 작업관리자->서비스 Oracle Agent 시작 시킴 (service, Agent,Listener 모두 실행되어 있는지 확인)*

###### 계정만들기
최고관리자인 system 계정으로 접속하여 만듦
>①계정만들기 <br>
create user 계정명identified by 비밀번호; <br>
②만든계정의lock 풀기 <br>
alter user 계정명account unlock; <br>
③기본권한설정<br>
grant connect, resource to 계정명; <br>
④권한주기(특정권한부여)<br>
grant create session, create table, create view,
create sequence, create procedure
to 계정명;

<hr>
#### 테이블 생성

ex) CREATE TABLE userlist(<br>
id VARCHAR2(10) CONSTRAINT id_pk PRIMARY key, <br>
name varchar2(10) not null <br>
)
