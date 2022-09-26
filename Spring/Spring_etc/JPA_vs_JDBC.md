# JPA vs JDBC

## JDBC 특징

>1) sql문 작성
>2) connection 관리
>3) preparedstatement, reultset 객체

- connection 객체가 db와 app의 연결을 관리하고,
- preparedstatement가 sql을 전달하며,
- resultset 객체를 통해 결과값을 전달한다.

---

## JPA 장점

>1) slq문을 직접 java application 내에서 적을 경우가 적어진다.
>2) sql 구조를 java application 내에서 적용하지 않아도 된다.
