# 데이터 입출력 구현

## 물리 데이터 저장소 설계 - 기출문제

### 01. 괄호 안의 용어

- ( `참조 무결성` ) = 외래키 값이 NULL이거나 참조 릴레이션의 기본키 값과 동일해야 한다는 규정이다
- ( `개체 무결성` ) = 기본 릴레이션의 기본키를 구성하는 어떤 속성도 NULL일 수 없다는 규정이다

- 데이터베이스 무결성의 종류

|||
|--|--|
|개체 무결성|한 엔터티에서 같은 기본 키(PK)를 가질 수 없거나, 기본 키(PK)의 속성이 NULL을 허용할 수 없는 제약조건|
|참조 무결성|외래 키가 참조하는 다른 개체의 기본 키에 해당하는 값이 기본 키 값이나 NULL이어야 하는 제약조건|
|속성 무결성|속성의 값은 기본값, NULL 여부, 도메인(데이터 타입, 길이)이 지정된 규칙을 준수해야 하는 제약 조건|
|사용자 무결성|사용자의 의미적 요구사항을 준수해야 하는 제약조건|
|키 무결성|한 릴레이션에 같은 키 값을 가진 튜플들을 허용할 수 없는 제약조건|
|||

---

### 02. 괄호 안의 용어

- 키의 종류

|||
|:--:|--|
|기본 키</br>(Primary Key)|- 테이블의 각 튜플들을 고유하게 식별하는 컬럼|
|대체 키</br>(Alternate Key)|- 후보 키 중에서 기본 키로 선택되지 않은 키|
|( `후보 키` )</br>(Candidate Key)|- 테이블에서 각 튜플들을 구별하는데 기준이 되는 컬럼</br>- 기본 키와 대체 키를 합친 키|
|슈퍼 키</br>(Super Key)|- 릴레이션을 구성하는 모든 튜플에 대해 유일성을 만족하지만, 최소성을 만족하지 못하는 키|
|( `외래 키` )</br>(=참조 키)</br>(Foreign Key)|- 테이블 간의 참조 데이터 무결성을 위한 제약 조건</br>- 한 릴레이션의 칼럼이 다른 릴레이션의 기본 키로 이용되는 키|
|||
