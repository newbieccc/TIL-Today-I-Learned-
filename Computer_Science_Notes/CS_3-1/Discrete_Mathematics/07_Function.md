# # 이산수학

## 07. 함수

- 컴퓨터과학과 손진곤 교수님

### (1) 기본사항

- 함수
    - 집합 X의 각 원소에 대해 집합 Y의 원소를 유일하게 대응시키는 관계
    - 기호: 𝑓: X → Y
        - 상수 함수
            - 정의역의 모든 원소가 같은 값으로 대응됨 (항상 일정한 출력값)
        - 항등 함수
            - 모든 원소 x에 대해 𝑓(x) = x인 함수
            - 기호: id<sub>X</sub>(x) = x

### (2) 전사, 단사, 역함수

- 전사함수와 단사함수
    - 전사 함수(Surjective Function)
        - 공역 Y의 모든 원소가 정의역 X의 어떤 원소와 매핑됨
        - ∀y ∈ Y, ∃x ∈ X such that f(x) = y
    - 단사 함수(Injective Function)
        - 서로 다른 원소가 서로 다른 값으로 매핑됨
        - f(x₁) = f(x₂) ⟹ x₁ = x₂
    - 전단사 함수(Bijective Function)
        - 전사이면서 단사인 함수
        - 일대일 대응 (1:1 and onto)
- 역함수와 합성함수
    - 역함수
        - 함수 f:X -> Y가 전단사 함수일 때 f의 역관계 f<sup>-1</sup>를 f의 역함수(inverse function)
        - f(f⁻¹(y)) = y, f⁻¹(f(x)) = x
    - 합성 함수(Composition of Functions)
        - 두 함수 f: X → Y, g: Y → Z에 대해 (g ∘ f): X → Z 정의
        - (g ∘ f)(x) = g(f(x))

### (3) 함수의 종류

- 계승함수 (factorial)
- 바닥함수 (floor function)
    - 실수 x에 대해, x 보다 작거나 같으면서 가장 큰 정수를 구하는 함수
- 천장함수 (ceiling function)
    - 실수 x에 대해, x보다 크거나 같으면서 가장 작은 정수를 구하는 함수
- 나머지 함수
    - 정수 n 과 양의 정수 m에 대해 n을 m으로 나누었을 때의 나머지를 구하는 함수를
        - 나머지 함수(modulo function) [모듈로 함수 / mod 함수]
        - n mod m 으로 표기함
