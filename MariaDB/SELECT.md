# 6.1 SELECT 문(1)

> 가장 기본적인 `SELECT 열이름 FROM 테이블이름 WHERE 조건` 에 살을 붙여가며 `SELECT`문을 정복한다.



## Use 구문

> 현재 사용하는 데이터베이스를 지정 또는 변경하는 구문 형식이다. `USE 데이터베이스_이름;` 형식으로 입력한다.

```mariadb
USE employees; -- 지금부터 employees를 사용하겠으니, 모든 쿼리는 employees에서 수행하라. 
```



## SELECT & FROM

```mariadb
SELECT * FROM titles ; -- titles 테이블에서 모든 열의 내용을 가져와라.
/* 영향 받은 행: 0  찾은 행: 443,308  경고: 0  지속 시간 1 쿼리: 0.000 초 (+ 0.266 초 네트워크) */
```

![image-20210113181606782](markdown-images/image-20210113181606782.png)

* 영향 받은 행(Affected rows) : 변경된 행의 개수를 나타낸다. `SELECT`문은 행을 변경하지 않는다.
* 찾은 행 : `SELECT`문은 조회된 행의 개수가 나온다.
* 경고 : 경고가 발생된 경우 경고의 개수가 나온다.
* 지속시간 1 쿼리 :  실행된 쿼리의 개수와 쿼리가 실행된 시간을 나타낸다.
* ( +  0.266 초 네트워크) : 네트워크 전송시간을 나타낸다.



* `*` : 모든 것 , 모든 열을 의미, 특정한 열을 얻으려면 이 위치에 얻고 싶은 열을 입력하면 된다.
* `FROM` :  다음으로 테이블/뷰 등의 항목이 나온다.



```mariadb
SELECT * FROM employees.titles;
```

테이블의 이름은 `emplyees.tiltes`로 원칙적으로 위와 같이 사용하여야 하지만 

이미 선택된 데이터베이스 이름이 자동으로 붙어 아래 두 쿼리는 동일하다.

```makefile
SELECT * FROM employees.titles;
SELECT * FROM titles ;
```



다음과 같이 입력하면 사원테이블(employees)의 이름만 가져올 수 있다.

```mariadb
SELELCT first_name FROM employees;
/* 영향 받은 행: 0  찾은 행: 300,024  경고: 0  지속 시간 1 쿼리: 0.000 초 (+ 0.063 초 네트워크) */
```

![image-20210113215130092](markdown-images/image-20210113215130092.png)



여러 개의 열을 가져오고 싶으면 `,`로 구분하면 된다.  순서는 사용자의 마음이다.

```mariadb
SELECT first_name, last_name FROM employees;
```

![image-20210113215241015](markdown-images/image-20210113215241015.png)



### 예제

> 데이터베이스 이름, 테이블 이름, 필드 이름이 정확히 기억나지 않을 때 조회하는 방법이다.

1. 현재 서버에 어떤 데이스베이스가 있는지 조회한다.

```mariadb
SHOW DATABASES;
```

![image-20210113215538805](markdown-images/image-20210113215538805.png)

2. 찾는 데이터 베이스를 지정한다.

```mariadb
USE employees
```

3. 현재 데이터베이스에 있는 테이블을 조회한다.

```mariadb
SHOW TABLE STATUS;
```

![image-20210113215911354](markdown-images/image-20210113215911354.png)

4. 위에서 `employees` 테이블 이름을 찾았으니 테이블 열을 조회한다.

```mariadb
DESCRIBE employees; -- DESC employees; 도 된다.
```

![image-20210113220042243](markdown-images/image-20210113220042243.png)

5. `first_name` 열과 `gender` 열을 조회한다.

```mariadb
SELECT first_name, gender FROM employees;
```

![image-20210113220345271](markdown-images/image-20210113220345271.png)





## 계속 사용할 데이터 베이스 만들어두기

```mariadb
DROP DATABASE IF EXISTS sqlDB;
CREATE DATABASE sqlDB;

USE SQLdb;
CREATE TABLE userTBL
(userID CHAR(8) NOT NULL PRIMARY KEY,
 NAME VARCHAR(10) NOT NULL,
 birthYear INT NOT NULL,
 addr CHAR(2) NOT NULL,
 mobile1 CHAR(3),
 mobile2 CHAR(8),
 height SMALLINT,
 mDate DATE 
);
CREATE TABLE buyTbl
(num INT AUTO_INCREMENT NOT NULL PRIMARY KEY,
 userID CHAR(8) NOT NULL,
 prodName CHAR(6) NOT NULL,
 groupName CHAR(4),
 price INT NOT NULL,
 amount SMALLINT NOT NULL,
 FOREIGN KEY (userID) REFERENCES userTBL(userID)
);

INSERT INTO usertbl VALUES('LSG', n'이승기', 1987, n'서울', '011', '11111111', 182, '2008-8-8');
INSERT INTO usertbl VALUES('KBS', n'김범수', 1979, n'경남', '011', '22222222', 173, '2012-4-4');
INSERT INTO usertbl VALUES('KKH', n'김경호', 1971, n'전남', '019', '33333333', 177, '2007-7-7');
INSERT INTO usertbl VALUES('JYP', n'조용필', 1950, n'경기', '011', '44444444', 166, '2009-4-4');
INSERT INTO usertbl VALUES('SSK', n'성시경', 1979, n'서울', NULL, NULL, 186, '2013-12-12');
INSERT INTO usertbl VALUES('LJB', n'임재범', 1963, n'서울', '016', '66666666', 182, '2009-9-9');
INSERT INTO usertbl VALUES('YJS', n'윤종신', 1969, n'경남', NULL, NULL, 170, '2005-5-5');
INSERT INTO usertbl VALUES('EJW', n'은지원', 1972, n'경북', '011', '88888888', 174, '2014-3-3');
INSERT INTO usertbl VALUES('JKW', n'조관우', 1965, n'경기', '018', '99999999', 172, '2012-10-10');
INSERT INTO usertbl VALUES('BBK', n'바비킴', 1973, n'서울', '010', '00000000', 176, '2013-5-5');
INSERT INTO buytbl VALUES(NULL, 'KBS', N'운동화', NULL,    30, 2);
INSERT INTO buytbl VALUES(NULL, 'KBS', N'노트북', N'전자', 1000, 1);
INSERT INTO buytbl VALUES(NULL, 'JYP', N'모니터', N'전자', 200, 1);
INSERT INTO buytbl VALUES(NULL, 'BBK', N'모니터', N'전자', 200, 5);
INSERT INTO buytbl VALUES(NULL, 'KBS', N'청바지', N'의류', 50, 3);
INSERT INTO buytbl VALUES(NULL, 'BBK', N'메모리', N'전자', 80, 10);
INSERT INTO buytbl VALUES(NULL, 'SSK', N'책',     N'서저', 15, 5);
INSERT INTO buytbl VALUES(NULL, 'EJW', N'책',     N'서적', 15, 2);
INSERT INTO buytbl VALUES(NULL, 'EJW', N'청바지', N'의류', 50, 1);
INSERT INTO buytbl VALUES(NULL, 'BBK', N'운동화', NULL,    30, 2);
INSERT INTO buytbl VALUES(NULL, 'EJW', N'책',     N'서적', 15, 1);
INSERT INTO buytbl VALUES(NULL, 'BBK', N'운동화', NULL,    30, 2);
```



