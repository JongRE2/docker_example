# 데이터 베이스

## 접속

root을 만든후에 mysql -u root -p명령을 쳐서 계정으로 접속 후, 아래 명령어 입력

```sql
show databases;
```

처음 설치 후 바로 확인하게 되면, 위와 같이 기본 데이터베이스들만 있습니다.

특별히 건드릴 필요는 없습니다.

## 생성

```sql
create database test_db;
```



test_db라는 데이터베이스를 생성한 후, 데이터베이스를 조회하게되면, 새로 생성된 것을 확인할 수 있습니다.

## 사용

여러 데이터베이스들 중에서 하나 선택해 사용합니다.

```sql
use mysql;
```

일단 위와 같이 use 를 사용하시면 MariaDB 에서는 아래와 같이 MariaDB[(none)] 부분이 MariaDB [mysql] 과 같이 변하는 것을 볼 수 있습니다.

변한 부분은 현재 사용중인 DB 를 나타냅니다.

데이터베이스에 들어있는 테이블을 조회해보도록 하겠습니다.

```sql
show tables;
```

mysql 데이터베이스를 사용하는 상태에서 table을 조회하게 되면, mysql 데이터베이스에 속해있는 테이블들을 조회할 수 있습니다.



## 삭제

```sql
drop database test_db;
```

test_db 데이터베이스를 삭제하고, 데이터베이스들의 목록을 조회해보면, test_db 데이터베이스가 삭제된 것을 확인할 수 있습니다.



# 테이블 생성 및 데이터 입력

이 테이블들을 본인의 데이터베이스에 넣어봅시다.



Sailors(sid: integer, sname: string, rating: integer, age: real)

Boat(bid: integer, bname: string, color: string)

Reserves(sid: integer, bid: integer, day: date)

## 테이블 생성하고 기본키/외래키 설정

1. Sailors(sid: integer, sname: string, rating: integer, age: real) 테이블을 생성해 봅시다.

   *** 기본키는 반드시 not null 선언 해주세요

   ```sql
   create table sailors
       -> (sid int not null primary key,
       -> sname varchar(10) not null,
       -> rating int not null,
       -> age real not null
       -> );
   ```

   

2. Boats(bid: integer, bname: string, color: string) 테이블을 생성해 봅시다. (오타는 의도한게 아니었어요..)

   ```sql
   create table boad
       -> (bid int not null primary key,
       -> bname varchar(10) not null,
       -> color varchar(10) not null
   		-> );
   ```

   

3. Reserves(sid: integer, bid: integer, day: date) 테이블을 생성해 봅시다.

   ```sql
   create table reserves 
       -> (sid int not null, 
       -> bid int not null, 
       -> day date not null, 
       -> constraint primary key(sid, bid, day));
   ```

   

## 데이터 타입(자료형)

- 크게 문자형, 숫자형, 날짜형, 선택형으로 나뉘어 집니다.

## 테이블 수정

### 테이블 이름 수정

```sql
rename table boad to boats;
```



### 테이블 속성 변경하기

이미 생성된 테이블에 기본키를 지정하고 싶을 때는 ALTER문으로 기본키 지정이 가능합니다.

```sql
DROP TABLE IF EXISTS userTBL;
CREATE TABLE userTBL 
( userID CHAR(8) NOT NULL,
name VARCHAR(10) NOT NULL, 
birthYear INT NOT NULL ); 

ALTER TABLE userTBL -- userTBL 테이블 변경 
	ADD CONSTRAINT PRIMARY KEY (userID); -- 추가 강제 기본키 (열이름)
```

### 테이블 속성 확인하기

```sql
desc [table_name];
```



## 테이블에 데이터 삽입 및 조회

### 데이터 삽입

```sql
INSERT INTO [table_name] ([column], [column], [column], [column] ) 
VALUE ([value], [value], [value], [value])

ex> insert into sailors (sid,sname,rating,age) value('22','Dustin','7','45.0');
```



### 데이터 조회

```sql
select [column] from [table_name];

# 원하는 테이블의 모든 컬럼 출력
select * from [table_name];
```



### 데이터 수정

```sql
update [table_name] set [column1] = 'value1';

# 테이블 데이터 전체 수정
update sailors set rating = '1';
# 테이블 데이터 일부 수정
update sailors set rating = '1' where sid = 22;
# 테이블 데이터 여러 열 수정
update sailors set rating = '1', sname = 'Destin' where sid = 22;
```

### 데이터 삭제

```sql
delete from [table_name] (where 조건);

# 테이블 데이터 전체 삭제
delete from sailors;
# 테이블 데이터 일부 삭제
delete sailors where id = 22;
```