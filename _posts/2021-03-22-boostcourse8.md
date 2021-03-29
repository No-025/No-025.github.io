---
title: "DB와 SQL"
toc: tru
toc_label: "DB와 SQL"
categories:
  - DB
  - SQL
---

---

# 1. 데이터베이스(DB)

-   데이터의 집합 (a Set of Data)
-   여러 응용 시스템(프로그램)들의 통합된 정보들을 저장하여 운영할 수 있는 공용(share) 데이터의 집합
-   효율적으로 저장, 검색, 갱신할 수 있도록 데이터 집합들끼리 연관시키고 조직화


## - 데이터베이스의 4가지 특성


### 실시간 접근성(Real-time Accessability)  

사용자의 요구를 즉시 처리




### 계속적인 변화(Continuous Evolution)  

 정확한 값을 유지하고 데이터를 지속적으로 갱신




### 동시 공유성(Concurrent Sharing)  

 동시에 여러 사람이 동일한 데이터에 접근하고 이용가능
 


### 내용 참조(Content Reference)  

사용자가 요구하는 데이터의 내용, 즉 데이터 값에 따라 참조가능

---


# 2. 데이터베이스 관리 시스템 (DBMS)

-   데이터베이스를 관리하는 소프트웨어
-   여러 응용 소프트웨어(프로그램) 또는 시스템이 동시에 데이터베이스에 접근하여 사용가능
-   Oracle, SQL Server, MySQL, DB2 등의 상용 또는 공개 DBMS


## - DBMS 필수 3가지 기능

### 정의기능

데이터 베이스의 `논리적, 물리적 구조를 정의`  


### 조작기능
데이터를 `검색, 삭제, 갱신, 삽입, 삭제`하는 기능 

 
### 제어기능
데이터베이스의 내용 `정확성과 안전성을 유지`하도록 제어하는 기능


---


## - DBMS 장단점

### 장점  
- 데이터 중복이 최소화
- 데이터의 일관성 및 무결성 유지
- 데이터 보안 보장
    
    
  
### 단점
- 운영비가 비쌈
- 백업 및 복구에 대한 관리가 복잡
- 부분적 데이터베이스 손실이 전체 시스템을 정지

---

# 3. SQL(Structured Query Language)

-   데이터를 쉽게 검색하고 추가, 삭제, 수정 같은 조작을 할 수 있게 고안된 컴퓨터 언어
-   관계형 데이터베이스에서 `데이터를 조작하고 쿼리`하는 표준 수단

## - SQL 문법 3가지


### DML (Data Manipulation Language)

- `데이터를 조작`
- INSERT, UPDATE, DELETE, SELECT 등



### DDL (Data Definition Language)
- 데이터베이스의 `스키마를 정의하거나 조작`
- CREATE, DROP, ALTER 등


### DCL (Data Control Language)
- `데이터를 제어`
- 권한을 관리하고, 테이터의 보안, 무결성 등을 정의
- GRANT, REVOKE 등

---

## - MySQL Database 접속하기

```sql
mysql> –uroot  -p
```

관리자 계정인 root로 접속

*설치 시 입력했던 암호 입력



## - MySQL Database 생성하기


> mysql> **create** database DB이름;

```sql
mysql> create database connectdb;
```

## - MySQL 사용자 생성

> create user '아이디'@'%' identified by '비밀번호';
> 
> flush privileges;


- @’%’는 어떤 클라이언트에서든 접근 가능하다는 의미
- @’localhost’는 해당 컴퓨터에서만 접근 가능
- flush privileges는 DBMS에게 적용을 하라는 의미

```sql
create user 'connectuser'@'%' identified by 'connect123!@#';

flush privileges;
```


## - MySQL 사용자 권한

> **grant** all privileges on *.* to '아이디'@'%';
> 
> FLUSH PRIVILEGES;

```sql
grant all privileges on connectdb.* to 'connectuser'@'%';

flush privileges;
```

## - 생성한 Database에 접속하기

> mysql –h호스트명 –uDB계정명 –p 데이터베이스이름

```sql
mysql> mysql –h127.0.0.1 –uconnectuser –p connectdb [enter]
```


## - MySQL 연결끊기

> mysql> **QUIT**
> 
> mysql> **exit**


## - MySQL 버전과 현재 날짜 구하기

```sql
mysql> SELECT VERSION(), CURRENT_DATE;
```

## - 쿼리문

### 키워드는 대소문자를 구별하지 않음

> mysql> SELECT VERSION(), CURRENT_DATE;
  mysql> select version(), current_date;
  mysql> SeLeCt vErSiOn(), current_DATE;


모두 `같은 결과`


### 쿼리를 이용해서 계산식의 결과 구하기 

> mysql> SELECT SIN(PI()/4), (4+1)*5;



### 여러 문장을 한 줄에 연속으로 붙여서 실행하

> mysql> SELECT VERSION(); SELECT NOW();



### 하나의 SQL은 여러 줄로 입력하기

> mysql> SELECT
    -> USER()
    -> ,
    -> CURRENT_DATE;


### SQL을 입력하는 도중에 취소하기

> mysql> SELECT
    -> \c
  mysql>


### DBMS에 존재하는 데이터베이스 확인하기

> mysql> **show** databases;


### 사용중인 데이터베이스 전환하기

> mysql> **use** 데이터베이스명 ;


---


## - Table(테이블)

### 테이블(Table)
RDBMS의 기본적 저장구조 1개 이상의 `column`과 

0개 이상의 `row`로 구성


### 열(Column)
- 테이블 상에서의 `단일 종류의 데이터`
- 특정 데이터 타입 및 크기를 갖음

### 행(Row) 
- Column들의 값의 조합
- `레코드`라고 불림
- 기본키(PK)에 의해 구분
- `기본키는 중복을 허용하지 않음`


### Field
- Row와 Column의 교차점
- 데이터를 포함할 수 있고 없을 때는 NULL 값

---


## - 현재 데이터베이스에 존재하는 테이블 목록 확인하기

> mysql> **show** tables;



## - SQL파일로 테이블 생성 및 값 저장

터미널에서 `파일이 있는 폴더로 이동`


> mysql >  –uDB계정명 –p 데이터베이스이름   <  파일명.sql

```sql
mysql> -uconnectuser  -p  connectdb   <  examples.sql
```

## - 테이블 구조를 확인하기 위한 DESCRIBE 명령

> mysql> **desc** 테이블명;

```sql
mysql> desc employee;
```

---


# 4. DML(select, insert, update, delete)

-   SELECT – 검색
-   INSERT - 등록
-   UPDATE - 수정
-   DELETE - 삭제



## - SELECT

> **SELECT**(DISTINCT) 칼럼명(ALIAS) FROM 테이블명;

- SELECT: 검색하고자 하는 데이터(칼럼)
- DISTINCT: 중복행 제거
- ALIAS: 나타날 컬럼에 다른 이름 부여
- FROM: 선택한 칼럼이 있는 테이블 명시


### SELECT 전체 데이터 검색

> \*

```sql
SELECT * FROM  DEPARTMENT;
```



### SELECT 특정 컬럼 검색

> 콤마(,)

```msql
SELECT empno, name, job from employee;
```



### SELECT 컬럼에 Alias부여하기

> as

```sql
select empno as 사번, name as 이름, job as 직업 from employee;
```




### SELECT 컬럼의 합성(Concatenation)

> concat

```sql
SELECT concat( empno, '-', deptno) AS '사번-부서번호' 
FROM employee;
```




### SELECT 중복행의 제거

> DISTINCT

```sql
select distinct deptno from employee;
```




### SELECT  정렬하기

> 오름차순 ORDER BY

```sql
select empno as 사번, name as 이름, job as 직업 from employee order by 이름;
```

---

> 내림차순 desc

```sql
select empno, name, job from employee order by name desc;
```


### SELECT 특정 행 검색

>where

```sql
select name, hiredate from employee where hiredate < '1981-01-01';

select name, deptno from employee where deptno = 30;
```

---

>IN

```sql
select name, deptno from employee where deptno in (10, 30);
```

---

>like

```sql
select name, job from employee where name like '%A%';
```
-   % 는 0에서부터 여러 개의 문자열을 나타냄
-   _ 는 단 하나의 문자를 나타내는 와일드 카드



### SELECT 함수의 사용

> UCASE, UPPER: 대문자 변환
> 

```sql
mysql> SELECT UPPER('SEoul'), UCASE('seOUL');
```

---


> LCASE, LOWER: 소문자 변환
> 

```sql
mysql> SELECT LOWER('SEoul'), LCASE('seOUL');
```

---


> substring: 문자열 자르기
> 

```sql
mysql> SELECT SUBSTRING('Happy Day',3,2);
```

---


> LPAD, RPAD: 공백 채우기
> 

```sql
mysql> SELECT LPAD('hi',5,'?'),LPAD('joe',7,'*');
```

---



> TRIM, LTRIM, RTRIM: 공백 제거

```sql
mysql> SELECT LTRIM(' hello '), RTRIM(' hello ');
```

---


> ABS(x) : x의 절대값

```sql
mysql> SELECT ABS(2), ABS(-2);
```

---


> MOD(n,m) % : n을 m으로 나눈 나머지 값을 출력

```sql
mysql> SELECT MOD(234,10), 253 % 7, MOD(29,9);
```


### SELECT 함수

-   FLOOR(x): x보다 크지 않은 가장 큰 정수를 반환(BIGINT로 자동 변환)
-   CEILING(x) : x보다 작지 않은 가장 작은 정수를 반환
-   ROUND(x) : x에 가장 근접한 정수를 반환
-   POW(x,y) POWER(x,y) : x의 y 제곱 승을 반환
-   GREATEST(x,y,...) : 가장 큰 값을 반환
-   LEAST(x,y,...) : 가장 작은 값을 반환
-   CURDATE(),CURRENT_DATE : 오늘 날짜를 YYYY-MM-DD나 YYYYMMDD 형식으로 반환
-   CURTIME(), CURRENT_TIME : 현재 시각을 HH:MM:SS나 HHMMSS 형식으로 반환
-   NOW(), SYSDATE() , CURRENT_TIMESTAMP : 오늘 현시각을 YYYY-MM-DD HH:MM:SS나 YYYYMMDDHHMMSS 형식으로 반환
-   DATE_FORMAT(date,format) : 입력된 date를 format 형식으로 반환
-   PERIOD_DIFF(p1,p2) : YYMM이나 YYYYMM으로 표기되는 p1과 p2의 차이 개월을 반환



### SELECT 형변환

> CAST: 형변환

```sql
mysql> select cast(now() as date);
```



### SELECT 그룹함수

- SUM(expr): 그룹의 누적 합계를 반환
- AVG(expr): 그룹의 평균을 반환
- COUNT(expr): 그룹의 총 개수를 반환
- MAX(expr): 그룹의 최대값을 반환
- MIN(expr): 그룹의 최소값을 반환
- STDDEV(expr): 그룹의 표준편차를 반환
- VARIANCE(expr): 그룹의 분산을 반환

```sql
SELECT AVG(salary) , SUM(salary) FROM employee WHERE deptno = 30;
```

### SELECT groupby 절

> GROUP  BY 단순컬럼

```sql
SELECT deptno, AVG(salary) , SUM(salary) FROM employee group by deptno;
```

---

## - INSERT

>**INSERT** INTO 테이블명(필드1, 필드2, 필드3, 필드4, … ) 
>
>**VALUES** ( 필드1의 값, 필드2의 값, 필드3의 값, 필드4의 값, … )


```sql
insert into ROLE (role_id, description) 

values ( 200, 'CEO');
```


## - UPDATE

> **UPDATE**  테이블명 
> 
> **SET**  필드1=필드1의값, 필드2=필드2의값, 필드3=필드3의값, … 
> 
> **WHERE**  조건식


```sql
update ROLE

set description = 'CTO'

where role_id = 200;
```


## - DELETE

> **DELETE** FROM  테이블명 
> 
> **WHERE**  조건식

```sql
delete from ROLE 

where role_id = 200;
```




---


# 5. DDL(create, drop)


## - 테이블생성

> create table 테이블명(
>          필드명1 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT],
>           필드명2 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT],
>           필드명3 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT], 
>           ........... 
>           PRIMARY KEY(필드명) 
>           );

```sql
CREATE TABLE EMPLOYEE2(   
            empno      INTEGER NOT NULL PRIMARY KEY,  
           name       VARCHAR(10),   
           job        VARCHAR(9),   
           boss       INTEGER,   
           hiredate   VARCHAR(12),   
           salary     DECIMAL(7, 2),   
           comm       DECIMAL(7, 2),   
          deptno     INTEGER);
```


### 테이블 컬럼 추가


>**alter** table 테이블명
>
>**add**  필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];


```sql
alter table EMPLOYEE2

add birthdate varchar(12);
```


### 테이블 컬럼 삭제

>**alter** table 테이블명
>
>**drop**  필드명;

```sql
alter table EMPLOYEE2

drop birthdate;
```


### 테이블 컬럼 수정

> **alter** table  테이블명 
> 
> **change**  필드명  새필드명 타입 [NULL | NOT NULL][DEFAULT ][AUTO_INCREMENT];



```sql
alter table EMPLOYEE2

change deptno dept_no int(11);
```


### 테이블 이름 변경

>**alter** table  테이블명 
>
>**rename** 변경이름;

```sql
alter table EMPLOYEE2 

rename EMPLOYEE3;
```


## - 테이블 삭제

>**drop** table 테이블이름;

```sql
drop table EMPLOYEE2;
```




