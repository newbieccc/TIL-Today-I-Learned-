# # 이산수학

## 04. 집합론

- 컴퓨터과학과 손진곤 교수님

### (1) 기본사항

- 기본사항
    - 논리학과 집합론
        - p(x) v g(x)
            - A U B
        - p(x) ∧ g(x)
            - A ∩ B
    - 집합과 원소
        - 무정의 용어
            - 정의 없이 사용하는 용어
            - 직관적으로 이해할 수 있으나 다른 용어로 정의하기 힘든 대상을 표현하기 위해 사용됨
    - 집합의 표시법
        - S가 하나의 집합리고 하면.
            - a를 S의 원소이고, b를 S의 원소가 아니라고 할 때
            - a ∈ S, b ∉ S
        - 집합의 표기 방법
            - S는 중괄호 ({, })로 표시함
                1. 원소나열법 -> S = {1, 2, 3}
                2. 조건나열법 -> S = {x | 0 < x < 4인 자연수}
            - 집합의 크기
                - |S| -> |S| = 3
            - 동일한 원소 사용 x, {} 기호 없으면 x
    - 부분집합
        - ~의 부분집합 (subset)
            - A의 모든 원소가 B의 원소이면 A는 B의 부분집합이라 하고
            - A ⊂ B 또는 A ⊆ B로 표기한다.
            - 즉, A ⊆ B <-> ∀x (x ∈ A -> x ∈ B)
        - 진부분집합 (proper subset)
            - A는 B의 진부분집합
                - A ⊆ B, B ⊊ A
                - A ⊆ B, A ≠ B
        - 상동 (equal)
            - A = B ↔ A ⊆ B and B ⊆ A
        - ∅ (공집합) ⊆ {1, 2, 3}은 참이다
    - 서로소 (disjoint)
        - 집합 A와 B는 서로소 ↔ A ∩ B = ∅
        - A와 B의 원소에 교칩합이 없다면 A와 B는 서로소이다.
    - 분할 (partition)
        - 집합 A를 `∅이 아닌 부분집합`들로 나눌 때 A의 모든 원소들이 각각 나누어진 부분집합들 중 하나에만 포함될 경우 이 부분집합들 전체의 집합을 `A의 분할`이라고 함
        - ex. {A1, A2, A3, A4, A5} ({} 기호가 있어야 함)
            - ∅ (공집합)은 분할에 들어가면 안됨 -> {{1, 2}, 3}
            - {{1, 2}, {2, 3}} -> 2의 원소가 교집합에 해당하여 안됨 -> {{1}, {2, 3}}
            - A = {1, 2, 3} 일 때 {{1}, {2}}는 안됨 -> {{1}, {2}, {3}}
        - A = {1, 2, 3}의 모든 분할은?
            - {{1}, {2}, {3}}
            - {{1, 2}, {3}}
            - {{1, 3}, {2}}
            - {{1}, {2, 3}}
            - {{1, 2, 3}}
        - 집합 기호
            - 자연수 집합 : ℕ
            - 정수 집합 : ℤ
            - 유리수 집합 : ℚ
            - 실수 집합 : ℝ
            - 복소수 집합 : ℂ
    - 멱집합 (power set)
        - 집합 A의 모든 부분집합들의 집합을 A의 멱집합이라고 하고, P(A)로 표기한다.
        - 멱집합의 원소 수
        - |S| = n -> |P(S)| = 2<sup>n</sup>
            - ex) 집합 S = {a, b, c} -> 3개
                - P(S) = {∅, {a}, {b}, {c}, {a,b}, {a,c}, {b,c}, {a,b,c}} -> 8개

### (2) 집합연산

- 집합연산
    - 합집합
        - A U B = {x ∈ U | x ∈ A V x ∈ B}
    - 교집합
        - A ∩ B = {x ∈ U | x ∈ A ∧ x ∈ B}
    - 차집합
        - A - B = {x ∈ U | x ∈ A ∧ x ∉ B}
    - 여집합
        - A<sup>c</sup> = U - A = {x ∈ U | x ∉ A}
    - 대칭차집합
        - A ⊕ B = {x ∈ U | x ∈ A U B ∧ x ∉ A ∩ B}

### (3) 집합의 대수법칙

- 집합의 대수법칙
    - 집합의 크기에 관한 성질
    - 포함관계 및 항등식
