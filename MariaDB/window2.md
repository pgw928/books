# 7.2.2 윈도우 함수(2)

> 행과 행 사이의 관계를 쉽게 정의하기 위해 제공되는 함수다. 윈도우 함수를 잘 활용하면 복잡한 SQL을 쉽게 활용할 수 있다. 쉽게 생각해 `OVER`절이 들어간 하수라고 보면 된다.



## 분석 함수

> 비집계 함수 중 `CUME_DIST()`, `LEAD()`, `FIRST_VALUE()`, `LAG()`, `LAST_VALUE()`, `PERCENT_RANK()` 등을 분석 함수라 부른다. 이를 이용하면 이동 평균, 백분율, 누계 등의 결과를 계산할 수 있다.

* 예제 1 : 회원 테이블에서 키가 큰 순서로 정렬하고 다음 사람과 키 차이를 미리 알려면 `LEAD()` 함수를 사용할 수 있다.

  ```mariadb
  USE SQLDB;
  SELECT NAME, ADDR, HEIGHT AS '키', HEIGHT-LEAD(HEIGHT, 1) OVER(ORDER BY HEIGHT DESC) AS '다음 사람과 키 차이' FROM usertbl;
  ```

  ![image-20210316223839485](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20210316223839485.png)

  * `HEIGHT-LEAD(HEIGHT, 1)` : LEAD(HEIGHT, 1)을 사용하면 바로 다음사람의 키를 알 수 있다.

  * `LAG()`는 이전 행과의 차이를 구할 수 있다.

* 예제 2 : 지역별로 가장 키가 큰 사람과의 차이를 알고 싶다면 `FIRST_VALUE()`를 사용하면 된다.

  ```mariadb
  SELECT ADDR, NAME, HEIGHT AS '키', HEIGHT-FIRST_VALUE(HEIGHT) OVER (PARTITION BY ADDR ORDER BY HEIGHT DESC) FROM usertbl;
  ```

  ![image-20210316224348865](C:\Users\User\AppData\Roaming\Typora\typora-user-images\image-20210316224348865.png)

* 예제 3 : 누적 합계를 내본다. 예로 현 지역에서 자신보다 키가 크거나 큰 인원의 백분율을 구할 수 있다. `CUM_DIST()` 함수를 사용해 본다.

  ```mariadb
  SELECT addr, name, height AS '키',
  	CAST((CUME_DIST() OVER(PARTITION BY ADDR ORDER BY HEIGHT DESC))*100 AS INTEGER) AS '누적인원 백분율%' FROM usertbl;
  ```

  * `PERCENT_RANK()`도 `CUME_DIST()`와 유사한 기능을 한다.

