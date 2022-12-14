# 데이터 입출력 구현

## 논리 데이터 저장소 확인 - 예상문제

### 01. 괄호 안의 용어

- 논리 데이터 모델링의 속성은 ( `개체` ), 속성, ( `관계` )로 구성된다

---

### 02. 해당하는 데이터 모델

- 현실 세계에 존재하는 데이터와 그들 간의 관계를 사람이 이해할 수 있는 형태로 명확하게 표현하기 위해서 가장 널리 사용되고 있는 모델이다.
- 요구사항으로부터 얻어낸 정보들을 개체, 속성, 관계로 기술한 모델이다.
  - `개체-관계(E-R) 모델`

---

### 03. 개체-관계 다이어그램

|구성|기호||
|:--:|:--:|--|
|개체|⬜️|(사각형)|
|( `관계` )|◇|(마름모)|
|( `속성` )|○|(타원)|
|다중 값 속성|◎|(이중타원)|
|관계-속성 연결|ㅡ|(선)|
||||

---

### 04. 설명하는 데이터베이스 기법

- 관계형 데이터 모델에서 데이터의 중복성을 제거하여 이상 현상을 방지하고,
- 데이터의 일관성과 정확성을 유지하기 위해 무손실 분해하는 과정이다.
  - `정규화`

>- 정규화는 함수적 종속성을 이용해서 연관성 있는 속성들을 분류하고, 각 릴레이션의 이상 현상이 생기지 않도록 하는 과정이다.

---

### 05. 데이터베이스 정규화 단계

- `2NF(2정규화)`

>- 부분 관계인 <서비스 이름, 서비스 가격> 관계를 별도의 테이블로 두면 부분함수 종속 관계가 제거 되어 2차 정규화를 만족한다

---

### 06. 서술

- 데이터베이스 이상 현상을 서술
  - `데이터의 중복성으로 인해 릴레이션을 조작할 때 발생하는 비합리적 현상`

---

### 07. 개념 서술

- 정규화 단계 중 BCNF의 개념 서술
  - `모든 결정자가 후보 키가 되도록 하여 결정자 함수 종속성을 제거하는 단계`

>- BCNF
>- 3차 정규형을 만족하면서 모든 결정자가 후보 키 집합에 속한 정규형
>- 3차 정규형으로 해결할 수 없는 이상 현상을 해결할 수 있다.
