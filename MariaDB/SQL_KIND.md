# 6.1.4 SQL 분류

> SQL문은 크게 DML, DDL, DCL로 분류된다.



## DML

> Data Manipulation Language(데이터 조작 언어)는 데이터를 조작(선택, 삽입, 수정, 삭제)하는데 사용된다.

* DML 구문이 사용되는 대상은 테이블의 행이다.
* 따라서 DML 사용하기 위해서는 테이블이 정의되어 있어야 한다.

* DELETE, INSERT, SELECT, UPDATE, 트랜잭션이 발생하는 SQL

* 트랜잭션 : 테이블의 데이터를 변경(입력/삭제/수정)할 때 실제 테이블에 완전히 적용하지 않고, 임시로 적용하는 것을 말한다. 실수가 있을 때 임시로 적용한 것을 취소할 수 있다.



## DDL

> Data Definition Language(데이터 정의 언어)는 데이터베이스, 테이블, 뷰, 인덱스 등의 데이터베이스 개체를 생성/삭제/변경하는 역할을 한다. 

* 자주사용하는 DDL은 CREATE, DROP, ALTER 등이다.
* 트랜잭션을 발생시키지 않는다. 즉, ROLLBACK, COMMIT을 시킬 수 없다.
* 실행 즉시 MariaDB에 적용된다.



## DCL

> Data Control Language(데이터 제어 언어)는 사용자에게 어떤 권한을 부여하거나 빼앗을 떄 주로 사용하는 구문이다.

* GRANT, REVOKE, DENY 등이 이에 해당한다.

