# 6.2.2 데이터의 수정 : UPDATE

> UPDATE 문에 대해서 알아본다.

* 기본 형식

  ```mariadb
  UPDATE 테이블이름
  	SET 열1=값1, 열2=값2 ...
  	WHERE 조건;
  ```

  * 여기서 WHERE절은 생략 가능하지만 생략하면 테이블 전체의 행이 변경된다.

* 예제

  ```mariadb
  UPDATE testtbl4
  	SET LNAME= '없음'
  	WHERE FNAME = 'Kyoichi'
  ```

