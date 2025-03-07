# 데이터베이스 시스템

## 02. DB 모델링

- 컴퓨터 과학과 정재화

### (1) 데이터베이스 모델링의 이해

- 데이터베이스 모델링의 정의
    - 데이터의 의미를 파악하고 데이터와 관여하는 업무 프로세스를 개념적으로 정의하고 분석하는 작업
    - 데이터 베이스 모델링의 단계
        1. 사용자 요구사항 분석
        2. 개념적 데이터 모델링
            - 요구사항을 바탕으로 추상화하고 해석 오류를 방지
            - 실세계의 데이터를 개념적으로 일반화시켜 데이터 타입, 속성, 관계, 제약조건등을 이끌어내는 과정
        3. 논리적 데이터 모델링
            - DBMS의 구현 모델에 맞춰 데이터의 구조를 표현
            - 데이터 정의 언어로 기술된 스키마(schema) 생성
        4. 물리적 데이터 모델링
            - 데이터베이스 파일의 내부 저장구조, 파일 구성, 인덱스, 접근 경로 등을 결정하는 과정
        5. 내부 스키마

- 데이터 모델
    - 데이터의 의미, 데이터 타입, 연산 등을 명시하기 위해 사용할 수 있는 개념(표기법)의 집합
- 데이터 모델링
    - 데이터에 대한 요구사항을 분석하여 추상화하는 과정
    - 실세계의 일부분을 DBMS가 지원하는 데이터 모델의 형태로 나타내는 과정

### (2) 사용자 요구사항 분석

- 사용자 요구사항 분석 과정
    1. 제안 요청서
    2. 요구사항 도출
    3. 요구사항 명세서
    4. 요구사항 분석
    5. 요구사항 정의서
    6. 요구사항 기록

### (3) ER 모델

- ER 모델의 개념
    - 개념적 데이터 모델링 단계에서 사용되는 모델
    - 실세계의 속성들로 이루어진 개체(entity)와 개체 사이의 관계 (relationship)를 정형화시킨 모델
    - 데이터 구조와 관계를 ER 다이어그램(ERD)으로 표현
    - 1976년 카네기 멜론 대학의 P.Chen 박사 제안
    - 구성 요소
        - 개체 집합, 관계 집합, 속성
        - 제약 조건
        - 특수 속성과 특수 관계
- 개체(entity)
    - 실세계에 존재하는 다른 객체와 구별되는 유무형의 사물
    - 개체를 설명하는 여러 속성들로 구성
- 개체 집합(entity set)
    - 같은 속성을 공유하는 개체들의 모임

- 속성
    - 개체를 구체적으로 설명하는 특성으로 개체 집합은 속성의 집합
    - 속성 값의 특성에 따라 여러 종류로 구분
    - 속성의 종류
        - 단순 속성과 복합 속성
            - 단순 속성
                - 더 작은 구성 요소로 나눌 수 없는 속성 (ex. 학생이름, 성별, 나이)
            - 복합 속성
                - 더 작은 구성요소로 나눌 수 있는 속성 (ex. 생년월일)
        - 단일값 속성과 다중값 속성
            - 단일값 속성
                - 한 개체에 대해 단 하나의 속성 값만을 갖는 속성
            - 다중값 속성
                - 한 개체에 대해 여러 개의 속성 값을 같는 속성
        - 유도 속성과 저장 속성
            - 유도 속성
                - 다른 속성의 값으로부터 값이 유추될 수 있는 속성
            - 저장 속성
                - 실제 값을 저장해야하는 속성, 유도 속성을 위해 사용
- 키(key) 속성
    - 각 개체를 구별하는데 사용되는 유일한 값을 가지는 속성의 집합
        - 개체를 고유하게 구분하는 역할
        - 관계 집합의 특정 관계를 찾는 역할

### # 주요 용어

- 사용자 요구사항 분석
    - 사용자가 원하는 애플리케이션 프로그램의 요구사항을 만족하는 데이터 베이스를 모델링하기 위해 실제 업무에서 사용되는 데이터의 종류와 특징을 폭넓게 파악하는 과정
- 개념적 데이터 모델링
    - 실세계의 데이터를 개념적으로 일반화시켜 데이터 구조, 데이터 타입, 속성, 관계, 제약조건등을 이끌어내는 과정
- ER 모델
    - 실세계의 속성들로 이루어진 개체(entity)와 개체 사이의 관계(relationship)를 정형화시킨 모델
- 개체 집합
    - 실세계에 존재하는 다른 객체 와 구별되는 유무형의 사물의 집합
- 관계 집합
    - 개체 집합 간의 연결 관계
- 스키마
    - 어떤 물건들을 적재하기 위한 효율적인 구조