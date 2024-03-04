# SQL 응용

## # 응용 SQL - 기출문제

### 01. SQL 문 작성

- 아래 조건을 만족하면서 과목별 점수의 평균이 90 이상인, 과목이름, 최소점수, 최대점수를 구하는 SQL 작성

>- 대소문자를 구분하지 않습니다.
>- WHERE 구문을 사용하지 않습니다.
>- GROUP BY, HAVING 구문을 반드시 사용합니다.
>- 세미콜론(;)은 생략 가능합니다.
>- 별칭(AS)를 사용해야 합니다

- 성적 테이블

|과목코드|과목이름|학점|점수|
|:--:|:--:|:--:|:--:|
|1000|컴퓨터과학|A+|95|
|2000|운영체제|B+|85|
|1000|컴퓨터과학|B+|85|
|2000|운영체제|B|80|
|||||

- 결과

|과목이름|최소점수|최대점수|
|:--:|:--:|:--:|
|컴퓨터과학|85|95|
||||

- `SELECT 과목이름.MIN(점수) AS 최소점수.MAX(점수) AS 최대점수 FROM 성적 GROUP BY 과목이름 HAVING AVG(점수) >= 90;`

---

### 02. SQL문 작성

- 조건을 만족하면서 학과별로 튜플 수가 얼마인기 구하는 SQL문 작성

>- 대소문자를 구분하지 않습니다.
>- WHERE 구문을 사용하지 않습니다.
>- GROUP BY 사용합니다.
>- 세미콜론(;)은 생략 가능합니다.
>- 별칭(AS)를 사용해야 합니다
>- 집계 함수를 사용해야 합니다

- 학생 테이블

|학과|학생|
|:--:|:--:|
|전기|이순신|
|컴퓨터|안중근|
|컴퓨터|윤봉길|
|전자|이봉창|
|전자|강우규|
|||

- 결과 테이블

|학과|학과별튜플수|
|:--:|:--:|
|전기|1|
|전기|2|
|전자|2|
|||

- `SELECT 학과, COUNT(학과) AS 학과별튜플수 FROM 학생 GROUP BY 학과;`

---

### 03. SQL 실행시 결과를 숫자로 쓰기

- 급여 테이블

|EMPNO|SAL|
|:--:|:--:|
|100|1000|
|200|3000|
|300|1500|
|||

>- SELECT COUNT(*) FROM 급여</br>WHERE EMPNO > 100 AND SAL >= 3000 OR EMPNO = 200;

- `1`