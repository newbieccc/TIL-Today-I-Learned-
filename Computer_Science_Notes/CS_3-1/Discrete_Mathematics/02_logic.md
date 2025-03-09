# # 이산수학

## 02. 논리

- 컴퓨터과학과 손진곤 교수님

### (1) 명제

- 명제 (Proposition)
    - 참과 거짓을 구별할 수 있는 문장이나 수학적 식을 명제라고 한다.
    - 명제의 진리값 (truth value)
        - 참 (True), T : 명제가 타당한 경우
        - 거짓 (False), F : 명제가 타당하지 않는 경우
- 명제의 종류
    - 합성명제
    - 조건명제, 쌍조건 명제
    - 항진명제, 모순명제

### (2) 논리연산

- 논리연산자
    - 실수연산 : +, -, *, /
    - 논리연산 : ∨, ∧, ¬, ⊕, ∨
        - 논리합 (disjunction; or, ∨)
            - p ∨ q
            - 둘 중에 하나라도 True라면 True
        - 논리곱 (conjunction; and, ∧)
            - p ∧ q
            - 둘 다 모두 True여야 True
        - 부정 (negation; ~, ¬)
            - ~p
            - True는 False로, False는 True로 부정
        - 배타적 논리합 (exclusive or; xor, ⊕)
            - p⊕q = (p∧~q)∨(~p∧q)
            - 둘 다 True거나 False는 False
            - 하나만 True일 때만 True
- 합성명제 (compound proposition)
    - 하나 이상의 명제와 논리연산자 그리고괄호로 이루어진 명제

- 조건명제 (conditional proposition, →)
    - 명제 p와 q가 있을 때, 명제 p가 조건의 역할을 수행하고 명제 q가 결론의 역할을 수행하는 경우
    - p → q
        - p는 q의 충분조건
        - q는 p의 필요조건

- 쌍조건명제 (conditional proposition ,↔)
    - 명제 p와 q가 있을 때, 명제 p와 q가 조건의 역할과 결론의 역할을 동시에 수행하는 경우

- 논리적동치 (logical equivalence, ≡)
    - 두 명제 p와 q가 논리적으로 동등하면 논리적 동치라고 하고, p ≡ q로 표시한다
        - 논리적으로 동등하다는 말은 두 명제가 항상 동일한 진리값을 가진다는 의미
- 동치
    - 역, 이, 대우
        - 조건명제 p → q
            - 역(converse) : q → p
            - 이(inverse) : ~p → ~q
            - 대우(contrapositive) : ~q → ~p
- 논리적 동치법칙
    - 교환법칙(commutation law)
        - p ∨ q ≡ q ∨ p
        - p ∧ q ≡ q ∧ p
        - p ↔ q ≡ q ↔ p
    - 결합법칙(associative law)
        - (p ∨ q) ∨ r ≡ p ∨ (q ∨ r)
        - (p ∧ q) ∧ r ≡ p ∧ (q ∧ r)
    - 분배법칙(distributive law)
        - p ∨ (q ∧ r) ≡ (p ∨ q) ∧ (p ∨ r)
        - p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)
    - 항등법칙(identity law)
        - p ∨ F ≡ p
        - p ∧ T ≡ p
    - 지배법칙(domination law)
        - p ∨ T ≡ T
        - p ∧ F ≡ F
    - 부정법칙(negation law)
        - ~T ≡ F
        - ~F ≡ T
        - p ∨ (~p) ≡ T
        - p ∧ (~p) ≡ F
    - 이중 부정 법칙(double negation law)
        - ~(~p) ≡ p
    - 멱등법칙(idempotent law)
        - p ∨ p ≡ p
        - p ∧ p ≡ p
    - 드 모르간 법칙(de Morgan's law)
        - ~(p ∨ q) ≡ (~p) ∨ (~q)
        - ~(p ∧ q) ≡ (~p) ∧ (~q)
    - 흡수법칙(absorption law)
        - p ∨ (p ∧ q) ≡ p
        - p ∧ (p ∨ q) ≡ p
    - 함축법칙(implication law)
        - p → q ≡ ~p ∨ q
    - 대우법칙
        - p → q ≡ ~q ∨ ~p
- ex) 2.12 드 모르간 법칙을 사용해 다음 식의 부정을 나타내시오
    - -2 < x < 3
        - (-2 < x) ∧ (x < 3)
    - ~(-2 < x < 3)
        - ~((-2 < x) ∧ (x < 3))
        - ~(-2 < x) ∨ ~(x < 3)
        - (x ≤ -2) ∨ (x ≥ 3)
- 항진명제(tautology)와 모순명제(contradiction)
    - 합성명제를 구성하는 명제의 진리값과 상관없이
        1. 항상 참(T)인 명제를 항진명제라고 한다.
        2. 항상 거짓(F)인 명제를 모순명제라고 한다.

### (3) 술어논리

- 논리 (logic)
    - 명제논리(proposition logic)
        - 명제
    - 술어논리(predicate logic)
        - 명제함수(propositional function)
            - 변수의 값에 의해 함수의 진리값이 결정되는 문장이나 식
            - 변수의 명세
                - 변수의 값을 적시
                - 변수의 범위를 제시 (한정화 : ∀, ∃)
- 한정화 (quantification)
    - 전체한정자 (universal quantifier, ∀)
    - 존재한정자 (existential quantifier, ∃)
- 명제함수의 타당성
    - 벤 다이어그램(Venn diagram)
        - 한정자가 사용된 명제함수의 타당성을 직관적으로 검사함

### (4) 추론

- 추론(inference)
    - 참으로 알려진 명제를 기초로 하여 다른 명제를 유도해 내는 과정을 추론이라고 한다.
        1. 결론의 근거를 제공하는 알려진 명제를 전제(premise)라고 한다
        2. 새로 유도된 명제는 결론(conclusion)
    - 유효 추론
        - 유효추론은 전제를 참(T)이라고 가정하였을 때 결론이 항상 참(T)이 되는 추론
            - ((p → q) ∧ (q → r)) → (p → r)
    - 추론 규칙
        - 기본적인 추론규칙은 논리적 동치(항진명제)를 이용함
