# 데이터 입출력 구현

## 논리 데이터 저장소 확인 - 기출문제

### 01. 데이터 모델링 절차

- 요구 사항 분석 -> ( `개념적 데이터 모델` ) -> ( `논리적 데이터 모델` ) -> ( `물리적 데이터 모델` )

>- 요개논물

---

### 02. DB 설계 절차

- ( `물리적 설계` )는 특정 DBMS의 특성 및 성능을 고려하여 데이터베이스 저장 구조로 변환하는 과정으로 결과로 나오는 명세서는 테이블 정의서 등이 있다
- ( `개념적 설계` )는 현실 세계에 대한 인식을 추상적, 개념적으로 표현하여 개념적 구조를 도출하는 과정으로 주요 산출물에는 E-R 다이어그램이 있다.
- ( `논리적 설계` )는 목표 DBMS에 맞는 스키마 설계, 트랜잭션 인터페이스를 설계하는 정규화 과정을 수행한다

|||
|--|--|
|요구사항 분석|- 사용자에게서 데이터베이스를 사용하는 용도를 파악함</br>- 다양한 요구사항을 수집하는 단계로 요구사항 명세서를 작성함|
|개념적 설계|- 요구사항 명세서를 기반으로 개념적 데이터 모델을 표현하며 E-R다이어그램으로 표현할 수 있음|
|논리적 설계|- 목표 DBMS에 맞는 스키마 설꼐 트랜젝션 인터페이스를 설계하는 정규화 과정을 수행함|
|물리적 설계|- 특정 DBMS의 특성 및 성능을 고려하여 데이터베이스 저장 구조로 변환하는 과정을 결과로 나오는 명세서는 테이블 정의서 등이 있음|
|구현|- SQL문을 실행하여 데이터베이스를 실제로 생성함|
|||

---

### 03. 데이터 모델의 구성요소

- 개체 데이터 모델에서는 ( `연산` )을 이용하여 실제 데이터를 처리하는 작업에 대한 명세를 나타내는데 논리 데이터 모델에서는 ( `구조` )를 어떻게 나타낼 것인지 표현한다

|||
|--|--|
|연산</br>(Operation)|- 데이터베이스에 저장된 실제 데이터를 처리하는 작업에 대한 명세</br>- 릴레이션을 조작하기 위한 관계 연산을 나타냄(SELECT, PROJECT, JOIN, DIVISION)|
|구조</br>(Structure)|- 데이터베이스에 논리적으로 표현될 대상으로서의 개체 타입과 개체 타입들 간의 관계</br>- 데이터 구조 및 정적 성질을 표현하는 요소|
|제약 조건</br>(Constraint)|- 데이터베이스에 저장될 수 있는 실제 데이터의 논리적인 제약 조건</br>- 데이터 무결성 유지를 위한 DB의 보편적 방법</br>- 릴레이션의 특정 칼럼에 설정하는 제약을 의미(개체무결성, 참조 무결성 등)|
|||

---

### 04. Cardinality, Degree 구하기

- Cardinality: `5`
- Degree: `4`

|학번|이름|학년|학과|
|--|--|--|--|
|202101||||
|202102||||
|202103||||
|202104||||
|202105||||
|||||

---

### 05. 정규형

- 부분 함수 종속성을 제거하여 완전 함수 종속을 만족하는 ( `2` )정규형이다

- 데이터베이스 정규화 단계 (원부이 결다조)
  - 원자화 (1NF)
  - 부분함수 종속 제거 (2NF)
  - 이행함수 종속 제거 (3NF)
  - 결정자 함수 종속 제거(BCNF)
  - 다치 종속 제거 (4NF)
  - 조인 종속 제거 (5NF)

---

### 06. 해당 데이터 모델링 기법

- 정규화된 엔터티, 속성, 관계에 대해 성능 향상과 개발 운영의 단순화를 위해 중복, 통합, 분리 등을 수행하는 데이터 모델링의 기법은?
  - `반 정규화`

- 테이블
  - 테이블 병합
    - 1:1 관계, 1:M 관계를 통합하여 조인 횟수를 줄여 성능을 향상
    - 슈퍼타입/서브타입 테이블 통합 통해 성능 향상
  - 테이블 분할
    - 테이블을 수직 또는 수평으로 분할하는 것으로 파티셔닝이라고 함
      - 수평 분할
        - 테이블 분할에 레코드를 기준으로 활용
      - 수직 분할
        - 하나의 테이블이 가지는 컬럼의 개수가 증가하는 경우 활용
        - 갱신 위주의 속성 분할, 자주 조회되는 속성 분할, 크기가 큰 속성 분할, 보안을 적용해야 하는 속성 분할
  - 중복 테이블 추가
    - 대량의 데이터들에 대한 집계함수(GROUP BY, SUM등)를 사용하여 실시간 통계정보를 계산하는 경우에 효과적인 수행을 위해 별도의 통게 테이블을 두거나 중복 테이블을 추가
      - 집게 테이블
        - 집계 데이터를 위한 테이블을 생성하고 각 원본 테이블에 트리거를 설정하여 사용하는 것으로 트리거의 오버헤드에 유의 필요
      - 진행 테이블 추가
        - 이력 관리 등의 목적으로 추가하는 테이블로, 적절한 데이터양의 유지와 활용도를 높이기 위해 기본키를 적절히 설정
      - 특정 부분만을 포함하는 테이블 추가
        - 데이터가 많은 테이블의 특정 부분만을 사용하는 경우 해당 부분만으로 새로운 테이블을 생성
- 컬럼
  - 컬럼 중복화
    - 조인 성능 향상을 위한 중복 허용
- 관계
  - 중복 관계 추가
    - 데이터를 처리하기 위한 여러 경로를 거쳐 재ㅗ인이 가능하지만, 이때 발생할 수 있는 성능 저하를 예방하기 위해 추가적 관계를 맺는 방법

---

### 07. 관계 대수

- 릴레이션 A, B가 있을 때 릴레이션 B 조건에 맞는 것들만 릴레이션 A에서 튜플을 꺼내 프로젝션하는 관계 대수는?
  - `디비전`

- 관계 대수 연산자 중 순수 관계 연산자

|연산자|기호|표현|설명|
|:--:|:--:|:--:|:--|
|셀렉트</br>(Select)| σ | σ(조건)(R) |릴레이션 R에서 조건을 만족하는 튜플 반환|
|프로젝트</br>(Project)| π | π(속성 리스트)(R) |릴레이션 R에서 주어진 속성들의 값으로만 구성된 튜플 반환|
|조인</br>(Join)| ▷◁ | R▷◁S |공통 속성을 이용해 R과 S의 튜플들을 연결해 만들어진 튜플 반환|
|디비전</br>(Division)| ÷ | R ÷ S |릴레이션 S의 모든 튜플과 관련 있는 R의 튜플 반환|
|||||

---

### 08. 이상 현상의 종류

- 이상 현상 종류 (삽삭갱)
  - `삽입 이상`
  - `삭제 이상`
  - `갱신 이상`

---

### 09. 개념 쓰기

- 비 정규화(De-Normalization)의 개념을 쓰시오
  - `정규화된 엔터티, 속성, 관계에 대해 성능 향상과 개발 운영의 단순화를 위해 중복, 통합, 분리 등을 수행하는 데이터 모델링 기법이다`

---

### 10. 용어

- 데이터베이스에서 자료 저장의 형태가 2차원 구조의 표 또는 테이블로 표현되는 관계 데이터 모델의 용어를 쓰시오
  - `릴레이션(Relation)`

---

### 11. 용어

- 관계 데이터 모델의 구성 요소 중 ( `스키마` )는 데이터베이스의 구조, 제약 조건 등의 정보를 담고 있는 기본적인 구조이고, ( `인스턴스` )는 정의된 ( `스키마` )에 따라 생성된 테이블에 실제 저장된 데이터의 집합이다

- 관계 데이터 모델의 구성요소

|||
|--|--|
|릴레이션(Relation)|행(Row)과 열(Column)로 구성된 테이블|
|튜플(Tuple)|릴레이션의 행(Row)에 해당되는 요소|
|속성(Attribute)|릴레이션의 열(Column)에 해당되는 요소|
|카디널리티(Cardinality)|튜플(Tuple)의 수|
|차수(Degree)|속성(Attribute)의 수|
|스키마(Schema)|데이터베이스의 구조, 제약 조건 등의 정보를 담고 있는 기본적인 구조|
|인스턴스(Instance)|정의된 스키마에 따라 생성된 테이블에 실제 저장된 데이터의 집합|
|||

---

### 12. 용어

- 데이터베이스에서 관계형 데이터 모델은 데이터를 테이블 구조로 표현하는 논리적 데이터 모델이다. 관계형 데이터 모델에서는 데이터를 원자값으로 갖는 이차원 테이블로 표현하는데, 이를 ( `릴레이션` )이라고 한다. ( `릴레이션` )의 구조는 물리적인 저장 구조를 나타내는 것이 아닌 논리적 구조이므로 다양한 정렬 기준을 통하여 표현할 수 있다. ( `릴레이션` )의 열을 속성이라 하고, 행을 튜플이라고 하며, 하나의 속성이 취할 수 있는 같은 타입의 원자값들의 집합을 ( `도메인` )이라고 한다.

---

### 13. 괄호 안의 용어

- ( `카티션 프로덕트` )는 모든 튜플들을 대응시켜 새로운 릴레이션을 만드는 연산으로, 연산의 결과 차수는 두 릴레이션의 차수를 합한 것과 같고 튜플은 두 릴레이션의 튜플 수를 곱한 것과 같다.
- ( `셀렉트` )는 릴레이션에 존재하는 튜플들 중에서 특정 조건을 만족하는 튜플을 구하는 연산으로 수평 연산이라고도 한다. 기호는 σ를 사용한다

>- 관계 대수 연산자 중 일반 집합 연산자

|연산자|기호|표현|설명|
|:--:|:--:|:--:|:--|
|합집합</br>(Union)|∪|R∪S|합병 가능한 두 릴레이션 R과 S의 합집합|
|교집합</br>(Intersection)|∩|R∩S|릴레이션 R과 S에 속하는 모든 튜플로 결과 릴레이션 구성|
|차집합</br>(Difference)|-|R-S|R에 존재하고 S에 미 존재하는 튜플로 결과 릴레이션 구성|
|카티션 프로덕트</br>(CARTESIAN Product)|×|RxS|R과 S에 속한 모든 튜플을 연결해 만들어진 새로운 튜플로 릴레이션 구성|
|||||

>- 관계 대수 연산자 중 순수 관계 연산자

|연산자|기호|표현|설명|
|:--:|:--:|:--:|:--|
|셀렉트</br>(Select)| σ | σ(조건)(R) |릴레이션 R에서 조건을 만족하는 튜플 반환|
|프로젝트</br>(Project)| π | π(속성 리스트)(R) |릴레이션 R에서 주어진 속성들의 값으로만 구성된 튜플 반환|
|조인</br>(Join)| ▷◁ | R▷◁S |공통 속성을 이용해 R과 S의 튜플들을 연결해 만들어진 튜플 반환|
|디비전</br>(Division)| ÷ | R ÷ S |릴레이션 S의 모든 튜플과 관련 있는 R의 튜플 반환|
|||||

---

### 14. 괄호 안의 용어

- 순수 관계 연산자 중에서 ( `셀렉트` )는 릴레이션 R에서 조건을 만족하는 튜플을 반환하는 연산자이고,
- ( `프로젝트` )는 릴레이션 R에서 주어진 속성들의 값으로만 구성된 튜플을 반환하는 연산자이다

---

### 15. 괄호 안의 용어

- ( `관계 대수` )는 기본 연산과 집합 연산을 이용하여 관계형 데이터베이스에서 원하는 정보와 그 정보를 어떻게 유도하는가를 기술하는 절차적 언어이다

>- 관계 해석은 튜플 관계 해석과 도메인 관계 해석을 하는 비절차적 언어이다

---

### 16. 괄호 안의 용어 - 정규화

- 제 1 정규형은 테이블 R에 속한 모든 속성의 도메인이 원자 값만으로 되어 있는 정규형이다 즉, 테이블의 모든 속성 값이 원자 값으로만 되어 있는 정규형이다. 제 1 정규형에서는 ( `부분 함수 종속` )이 있는 애트리뷰트가 존재하므로 이상이 발생한다
- 제 3정규형은 테이블 R이 제 2 정규형이고, ( `이행 함수 종속` )을 만족하지 않는 정규형이다

---

### 17. 괄호 안의 용어

- 제 2 정규형은 테이블 R이 제 1 정규형이고, ( `완전 함수 종속` )을 만족하는 정규형이다
- BCNF는 테이블 R에서 모든 결정자가 ( `후보키` )인 정규형이다 일반적으로 제 3 정규형에 ( `후보키` )가 여러개 존재하고, 이러한 ( `후보키` )들이 서로 중첩되어 나타나는 경우에 적용 가능하다

---

### 18. 괄호 안의 용어

- ( `2NF` )는 완전 함수 종속성을 만족하는 정규형이다
- ( `3NF` )는 이행 함수적 종속을 만족하지 않는 정규형이다

---

### 19. 정규화

- 이행 함수 종속성은 A->B이고, B->C일 때 ( `A->C` )를 만족하는 관계이다
- BCNF는 테이블에서 모든 결정자가 ( `후보키` )인 정규형이다

---

### 20. 정규화

- 정규화의 목적은 가능한 중복을 제거하여 삽입, 삭제, 갱신 ( `이상` )의 발생 가능성을 줄이는 것이다
- ( `이상` ) 현상은 데이터의 중복성으로 인해 릴레이션을 조작할 때 발생하는 비합리적 현상이다

---

### 21. 괄호 안의 용어

- 기존의 테이블에서 부분 함수적 종속을 제거하여 완전 함수적 종속을 만족하는 정규화 단계는 ( `2정규화(2NF)` )이다
