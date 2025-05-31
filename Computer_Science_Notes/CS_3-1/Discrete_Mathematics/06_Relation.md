# # 이산수학

## 06. 관계

- 컴퓨터과학과 손진곤 교수님

### (1) 기본사항

- 관계
    - 집합 X에서 집합 Y로의 (이항)관계 ((binary) relation) R은 X x Y의 부분 집합

### (3) 관계의 성질

- 집합 A에서의 관계 R이
    - 반사적 (reflexive)
        - $\forall a \in A,\ (a, a) \in R$
    - 대칭적 (symmetric)
        - $\forall a, b \in A,\ (a, b) \in R \Rightarrow (b, a) \in R$
    - 추이적 (transitive)
        - $\forall a, b, c \in A,\ ((a, b) \in R \land (b, c) \in R) \Rightarrow (a, c) \in R$

### (4) 관계의 종류

- (1) 역관계
    - X,Y : 집합
    - R : X에서 Y로의 관계
    - R<sup>-1</sup> : R의 역관계(inverse relation)
    - $R^{-1} = \{(y, x) \mid (x, y) \in R \} \subset Y \times X$

- (2) 합성관계
    - A, B, C : 집합
    - R : A에서 B로의 관계, S:B 에서 C로의 관계
    - R과 S의 합성관계 (composition relation)
    - $S \circ R = \{(a, c) \mid a \in A,\, b \in B,\, c \in C,\ (a, b) \in R,\ (b, c) \in S \}$
    - $S \circ R \subset A \times C \quad (\text{A에서 C로의 관계})$

- (3) 동치관계 (equivalence relation)
    - R : 집합 A에서 관계
    - R이 반사적, 대칭적, 추이적이면 R을 동치관계라고 부른다

- (4) 동치류 (equivalence class)
    - A : 집합
    - R : A에서의 동치관계
    - A의 임의의 원소 a에 대해서
    - $[a] = \{ x \in A \mid (a, x) \in R \}$
    - 이를 $a$의 동치류라고 부른다.
