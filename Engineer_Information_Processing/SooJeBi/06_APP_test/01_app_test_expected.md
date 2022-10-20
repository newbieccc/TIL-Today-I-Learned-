# 애플리케이션 테스트 관리

## # 애플리케이션 테스트 케이스 설계 - 예상문제

### 01. 서술

- 소프트웨어 테스트(Test) 개념에 대해서 서술하시오
  - `개발된 응용 애플리케이션이나 시스템이 사용자가 요구하는 기능과 성능, 사용성 안정성 등을 만족하는지 확인하고, 노출되지 않은 숨어 있는 소프트웨어의 결함을 찾아내는 활동이다`

---

### 02. 서술

- 소프트웨어 테스트의 원리 중 오류-부재의 궤변에 대해서 서술하시오
  - `요구사항을 충족시켜주지 못한다면, 결함이 없다고 해도 품질이 높다고 볼 수 없는 소프트웨어 테스트 원리이다`

---

### 03. 괄호안의 용어

- ( `결함 집중` ) = 적은 수의 모듈에서 대다수의 결함이 발견된다는 원리로 오류의 80%는 전체 모듈의 20% 내에서 발견
- ( `테스팅은 정황에 의존적` ) = 소프트웨어의 성격에 맞게 테스트 실시해야 한다는 원리로 정황과 비즈니스 도메인에 따라 테스트를 다르게 수행해야 함

---

### 04. 해당 설명하는 테스트 산출물

- 소프트웨어 테스트 산출물 중에서 애플리케이션의 테스트 되어야 할 기능 및 특징, 테스트가 필요한 상황을 작성한 문서는?
  - `테스트 시나리오(Test Scenario)`

---

### 05. 괄호안의 용어

|||
|--|--|
|( `테스트 수트` )</br>( `Test Suites` )|- Test Case를 실행환경에 따라 구분해 놓은 Test Case의 집합</br>- 시나리오가 포함되지 않은 단순한 테스트 케이스들의 모음|
|테스트 시나리오</br>(Test Scenario)|- 애플리케이션의 테스트 되어야 할 기능 및 특징, 테스트가 필요한 상황을 작성한 문서</br>- 하나의 단일 테스트 시나리오가 하나 또는 여러 개의 테스트 케이스들을 포함할 수 있음</br>- 테스트 시나리오가 테스트 케이스와 일 대 다의 관계를 가짐|
|( `테스트 스크립트` )</br>( `Test Script` )|- 테스트 케이스의 실행 순서(절차)를 작성한 문서</br>- 테스트 스텝(Test Step), 테스트 절차서(Test Procedure)라고도 함|
|||

---

### 06. 괄호안의 용어

|||
|:--:|--|
|정적 테스트|- 테스트 대상을 실행하지 않고 구조를 분석하여 논리성을 검증하는 테스트</br>- 리뷰, 정적 분석|
|( `동적 테스트` )|- 소프트웨어를 실행하는 방식으로 테스트를 수행하여 결함을 검출하는 테스트</br>- 화이트박스 테스트, 블랙박스 테스트, 경험 기반 테스트|
|||

---

### 07. 서술

- White-box Test란?
  - `각 응용 프로그램의 내부 구조와 동작을 검사하는 동적 소프트웨어 테스트이다`

---

### 08. 설명하는 테스트 커버리지는?

- 결정 포인트 내의 전체 조건식이 적어도 한 번은 참(T)과 거짓(F)의 결과를 수행하는 테스트 커버리지를 무엇이라고 하는가?
  - `결정 커버리지(선택 커버리지 or 분기 커버리지)`

---

### 09. 괄호안의 테스트 유형

|||
|:--:|--|
|( `다중 조건 커버리지` )|결정 조건 내 모든 개별 조건식의 모든 가능한 조합을 100% 보장하는 커버리지 테스트|
|( `데이터 흐름 테스트` )|제어 흐름 그래프에 데이터 사용현황을 추가한 그래프를 통해 테스트하는 기법|
|||

---

### 10. 해당 설명하는 테스트

- 프로그램 외부 사용자의 요구사항 명세를 보면서 수행하는 기능 테스트
- 소프트웨어의 특징, 요구사항, 설꼐 명세서 등에 초점을 맞춰 테스트가 이루어짐
- 기능 및 동작 위주의 테스트를 진행하기 때문에 내부 구조나 작동 원리를 알지 못해도 가능
  - `블랙박스 테스트`

---

### 11. 서술

- 블랙박스 테스트 유형 중에서 경계값 분석 테스트(Boundary Value Analysis Testing)란 무언인가?
  - `등가 분할 후 경계값 부분에서 오류 발생 확률이 높기 때문에 경계값을 포함하여 테스트 케이스를 설계하여 테스트하는 기법이다`

---

### 12. 괄호안의 용어

|||
|:--:|--|
|( `회복 테스트` )|시스템에 고의로 실패를 유도하고, 시스템의 정상적 복귀 여부를 테스트하는 기법|
|( `조건/결정 커버리지` )|전체 조건식뿐만 아니라 개별 조건식도 참 한 번, 거짓 한 번 결과가 되도록 수행하는 테스트 커버리지 기법|
|||

---

### 13. 올바르게 설명한 항목

- 애플리케이션 테스트에 대한 설명

1) 화이트박스 테스트가 끝난 후 더 나은 품질을 기대하기 위해서는 블랙박스 테스트를 실시해서 결함을 많이 검출해야 한다
2) 리그레션 테스트는 자동화에 적합한 테스트 타입이다
3) 디버깅은 테스트의 일종이 아니다
4) 타 시스템과 연동되는 테스트는 테스트 수행 단계에서 단위 테스트 단계에 속한다

- `2` / `3`

>- 화이트박스 테스트와 블랙박스 테스트의 수행 순서와 결함 검출률은 아무런 상관이 없다 독립적으로 수행하면 된다
>- 리그레션 테스트(회귀 테스트)는 반복적 성향이 강해서 자동화 테스트에 적합하다
>- 디버깅(Debugging)은 개발 활동이다
>- 타 시스템과 연동 테스트는 통합 테스트 단계에서 수행한다

---

### 14. 괄호안의 테스트 유형

- ( `인수 테스트` ) : 사용자가 실제로 사용될 환경에서 요구 사항들이 모두 충족되는지 사용자의 입장에서 확인하는 테스트로 알파, 베타 테스트가 있다
- ( `강도 테스트` ) : 시스템 처리 능력 이상의 부하, 즉 입계점 이상의 부하를 가하여 비정상적인 상황에서의 처리를 테스트하는 기법이다
- ( `회귀 테스트` ) : 오류를 제거하거나 수정한 시스템에서 오류 제거와 수정에 의해 새로이 유입된 오류가 없는지 확인하는 일종의 반복테스트 기법이다

---

### 15. 서술

- 상태 전이 테스트(State Transition Testing)란 무엇인지 서술하시오
  - `테스트 대상이 되는 시스템이나 객체의 상태를 구분하고, 이벤트에 의해 어느 한 상태에서 다른 상태로 전이되는 경우의 수를 수행하는 테스트 기법이다`

---

### 16. 괄호안의 테스트 유형

- ( `페어와이즈 테스트` ) : 테스트 데이터 값들 간에 최소한 한 번씩을 조합하는 방식이며, 이는 커버해야 할 기능적 범위를 모든 조합에 비해 상대적으로 적은 양의 테스트 세트를 구성하기 위한 테스트 기법
- ( `원인-결과 그래프 테스트` ) : 그래프를 활용하여 입력 데이터 간의 관계 및 출력에 미치는 영향을 분석하여 효용성이 높은 테스트 케이스를 선정하여 테스트하는 기법

---

### 17. 괄호안의 유형

|||
|:--:|--|
|( `부하 테스트` )|- 시스템에 사용량을 계속 증가시키면서 시스템의 임계점을 찾는 테스트</br>- 병목 지점을 찾아서 병목 현상을 제거하는 과정을 반복하여 성능 개선 가능|
|강도 테스트</br>(Stress Testing)|- 시스템 처리 능력 이상의 부하, 즉 입계점 이상의 부하를 가하여 비정상적인 상황에서의 처리를 테스트|
|( `스파이크 테스트` )|짧은 시간에 사용자가 몰릴 때 시스템의 반응 측정 테스트|
|||

---

### 18. 서술

- 리뷰의 유형 중 인스펙션(Inspection)은 무엇인지 서술하시오
  - `소프트웨어 요구, 설계, 원시 코드 등의 저작자 외의 다른 전문가 또는 팀이 검사하여 문제를 식별하고 문제에 대한 올바른 해결을 찾아내는 형식적인 검토 기법이다`

---

### 19. 구문 커버리지

- 프로그램 (소스 코드)

```code
입력값: X, Y, Z

1. IF ((X>2) AND (Y==2))
2.      Z = Z / X
    END
3. IF ((X==3) OR (Z>2))
4.      Z=Z+1
    END
```

- 구문 커버리지를 수행할 때 각각의 테스트 케이시는 몇 %를 만족하는지 쓰시오
  - 테스트 케이스 1: X=4, Y=1, Z=0 -> ( `50` )% 만족
  - 테스트 케이스 2: X=3, Y=2, Z=9 -> ( `100` )% 만족

---

### 20. 사용되는 테스트 케이스

```code
입력값: X, Y, Z

1. IF ((X>1) OR (Y>3))
2.      Z = Z * X
    END
3. IF ((X<2) AND (Y>1))
4.      Z=Z+1
    END
```

- 100% 조건/결정 커버리지를 만족하기 위해서 사용해야 하는 테스트 케이스를 모두 고르시오
  - 테스트 케이스 1: X=3, Y=0.5, Z=2
  - 테스트 케이스 2: X=1, Y=3, Z=3
  - 테스트 케이스 3: X=0.5, Y=4, Z=1

- `1`/ `2` / `3`

---

### 21. 테스트 케이스

- 아래의 명세 조건을 만족하는 경계값 분석의 테스트 케이스를 만들 수 있는 날짜를 모두 쓰시오.(2-Value 방식 기준)

>- 신규 출시된 예금 상품은 날짜에 따라서 이자가 아래와 같이 다르게 계산된다</br>- 1일~10일: 1,000원</br>- 11일~20일: 2,000원</br>- 21일~30일: 3,000원
>- 경계 설정: 1일, 11일, 21일, 30일

- `0일, 1일, 10일, 11일, 20일, 21일, 30일, 31일`

---

### 22. 괄호 안의 테스트 유형

- 경험 기반 테스트 유형에 대한 설명이다

- ( `오류 추정(Error Guessing)` )
  - 개발자가 범할 수 있는 실수를 추정하고 이에 따른 결함이 검출되도록 테스트 케이스를 설계하여 테스트하는 기법
  - 특정 테스트 대상이 주어지면 테스터의 경험과 직관을 바탕으로 개발자가 범할 수 있느 ㄴ실수들을 나열하고, 해당 실수에 따른 결함을 노출하는 테스트 수행

---

### 23. 서술

- 테스트 오라클(Test Oracle)이 무엇인지 서술하시오
  - `테스트의 결과가 참인지 거짓인지를 판단하기 위해서 사전에 정의된 참값을 입력하여 비교하는 기법이다`

---

### 24. 해당 테스트 레벨의 종류

- ( `단위 테스트` )
  - 사용자 요구사항에 대한 단위 모듈, 서브루틴 등을 테스트하는 단계
  - 인터페이스 테스트, 자료구조 테스트, 실행 경로 테스트, 오류 처리 테스트 등의 기법이 존재

---

### 25. 괄호 안의 구성요소

- ISO/IEC/IEEE 29119-3 표준 기반의 테스트 케이스 구성요소
  - 식별자, 테스트 항목, 입력 명세, 출력 명세, ( `환경 설정` ),  ( `특수절차요구` ), 의존성 기술

---

### 26. 테스트 레벨의 종류

- ( `시스템 테스트` ) : 통합된 단위 시스템의 기능이 시스템에서 정상적으로 수행되는지를 검증하는 테스트로 기능/비기능 요구사항 테스트 기법이 있다.
- ( `인수 테스트` ) : 최종 사용자와 업무의 이해관계자 등이 테스트를 수행함으로써 개발된 제품에 대해 운영 여부를 결정하는 테스트로 알파 테스트, 베타 테스트 기법이 있다.

---

### 27. 괄호안의 용어

- 테스트 케이스 작성 절차

1) 테스트 계획 검토 및 자료 확보
2) ( `위험` )평가 및 우선순위 결정
3) 테스트 요구사항 정의
4) 테스트 구조 설꼐 및 테스트 방법 결정
5) ( `테스트 케이스` )정의
6) 테스트 케이스 타당성 확인 및 유지보수