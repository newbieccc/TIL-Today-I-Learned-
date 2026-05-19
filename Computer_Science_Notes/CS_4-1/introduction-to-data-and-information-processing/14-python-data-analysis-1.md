# 데이터정보처리입문

## 14. 파이썬을 활용한 자료분석 (1)

### 강의 목차

1. 파이썬 소개
2. 파이썬 설치
3. 파이썬 프로그래밍

---

## 1. 파이썬 소개

### 1.1 파이썬이란?

파이썬(Python)은 배우기 쉽고 다양한 분야에서 활용되는 프로그래밍 언어이다.

| 특징        | 설명                                      |
|-----------|-----------------------------------------|
| 플랫폼 독립성   | Windows, Unix, MacOS 등 다양한 운영체제에서 사용 가능 |
| 쉬운 설치와 사용 | 문법이 비교적 쉽고 배우기 쉬움                       |
| 확장성       | 다양한 라이브러리 패키지를 쉽게 추가 가능                 |
| 활용 분야     | 자료분석, 통계, 머신러닝, 웹 개발, 자동화 등             |

---

### 1.2 파이썬 개발자

파이썬의 개발자는 네덜란드 출신의 귀도 반 로섬(Guido van Rossum)이다.

| 항목  | 내용               |
|-----|------------------|
| 개발자 | Guido van Rossum |
| 출생  | 1956년 1월 31일     |
| 국적  | 네덜란드             |
| 의미  | 파이썬 언어를 만든 핵심 인물 |

---

### 1.3 파이썬과 자료분석

파이썬은 자료분석에 많이 활용된다.

특히 다음 라이브러리와 함께 사용하면 데이터 처리, 분석, 시각화가 가능하다.

| 라이브러리      | 활용            |
|------------|---------------|
| NumPy      | 배열 계산, 수치 연산  |
| pandas     | 데이터프레임, 자료 정리 |
| matplotlib | 그래프 작성        |
| tensorflow | 딥러닝, 머신러닝     |
| graphviz   | 그래프 구조 시각화    |

---

## 2. 파이썬 설치

### 2.1 Anaconda

아나콘다(Anaconda)는 파이썬과 자료분석에 필요한 여러 패키지를 함께 제공하는 배포판이다.

| 항목  | 설명                                              |
|-----|-------------------------------------------------|
| 사이트 | www.anaconda.com                                |
| 장점  | 파이썬, Jupyter Notebook, Spyder, 주요 데이터 분석 패키지 포함 |
| 대상  | 자료분석, 통계, 머신러닝 학습자                              |

---

### 2.2 Anaconda 설치

아나콘다는 공식 홈페이지에서 다운로드할 수 있다.

설치 사이트:

    www.anaconda.com

설치 후 사용할 수 있는 주요 프로그램은 다음과 같다.

- Anaconda Navigator
- Anaconda Prompt
- Jupyter Notebook
- Spyder

---

### 2.3 Path 설정

Windows에서 Anaconda 명령을 편리하게 사용하려면 환경변수 Path 설정을 할 수 있다.

설정 경로:

    Windows 시스템
    → 제어판
    → 시스템 및 보안
    → 시스템
    → 고급 시스템 설정
    → 환경변수
    → 시스템 변수에서 Path 편집
    → 새로 만들기

추가할 경로 예:

    C:\anaconda3\
    C:\anaconda3\Scripts
    C:\anaconda3\Library\bin

---

### 2.4 pip

`pip`는 Python 패키지를 설치하고 관리하는 프로그램이다.

예를 들어 DOS 창 또는 명령 프롬프트에서 다음과 같이 패키지를 설치할 수 있다.

    pip install mglearn
    pip install graphviz
    pip install pydot
    pip install pydotplus
    pip install tensorflow

시험에서는 `pip`가 파이썬 패키지 설치 및 관리 프로그램이라는 점을 기억한다.

---

### 2.5 Spyder 실행

Spyder는 파이썬 코드를 작성하고 실행할 수 있는 개발 환경이다.

예:

    print("Hello Python !")

실행 결과:

    Hello Python !

계산 예:

    3**2

실행 결과:

    9

---

### 2.6 Jupyter Notebook 실행

Jupyter Notebook은 웹 브라우저 기반으로 파이썬 코드를 실행할 수 있는 환경이다.

실행 방법 예:

    jupyter notebook

기본 사용 흐름:

1. Jupyter Notebook 실행
2. New 선택
3. Python 3 선택
4. 코드 셀 또는 Markdown 셀 작성
5. Run으로 실행

---

### 2.7 Markdown과 Code 셀

Jupyter Notebook에서는 Markdown 셀과 Code 셀을 구분하여 사용할 수 있다.

| 셀 종류     | 용도            |
|----------|---------------|
| Markdown | 설명, 제목, 문서 작성 |
| Code     | 파이썬 코드 실행     |

Markdown 예:

    # Hello

Code 예:

    print("Hello, World!")

---

### 2.8 Google Colab

Google Colab은 구글에서 제공하는 온라인 파이썬 실행 환경이다.

| 특징     | 설명                          |
|--------|-----------------------------|
| 설치 필요성 | 별도 설치 없이 웹에서 사용 가능          |
| 실행 환경  | 브라우저 기반                     |
| 활용     | 파이썬 실습, 데이터 분석, 머신러닝        |
| 장점     | 파일 업로드, 라이브러리 사용, 노트북 공유 가능 |

---

## 3. 파이썬 프로그래밍

## 3.1 산술연산

파이썬에서는 기본 산술연산을 바로 수행할 수 있다.

| 연산자 | 의미   | 예       | 결과  |
|-----|------|---------|-----|
| +   | 더하기  | 1 + 2   | 3   |
| -   | 빼기   | 1 - 2   | -1  |
| *   | 곱하기  | 4 * 5   | 20  |
| /   | 나누기  | 7 / 5   | 1.4 |
| **  | 거듭제곱 | 3 ** 2  | 9   |
| //  | 몫    | 17 // 4 | 4   |
| %   | 나머지  | 17 % 4  | 1   |

코드 예:

    1 - 2
    4 * 5
    7 / 5
    3 ** 2
    17 // 4
    17 % 4

---

## 3.2 자료형

파이썬의 기본 자료형은 다음과 같다.

| 자료형   | 의미  | 예           |
|-------|-----|-------------|
| int   | 정수  | 10          |
| float | 실수  | 2.710       |
| str   | 문자열 | "hello"     |
| bool  | 논리값 | True, False |

자료형 확인은 `type()` 함수를 사용한다.

    type(10)
    type(2.710)
    type("hello")

결과 예:

    int
    float
    str

---

## 3.3 변수

변수는 값을 저장하는 이름이다.

    x = 10
    print(x)

    y = 3.14
    x * y
    type(x * y)

해석:

- `x`에 10 저장
- `y`에 3.14 저장
- `x * y`는 31.4
- 정수와 실수를 곱하면 결과는 실수형이 된다.

---

## 3.4 리스트

### 3.4.1 리스트 생성

리스트는 여러 값을 순서대로 저장하는 자료형이다.

    a = [1, 2, 3, 4, 5]
    print(a)

결과:

    [1, 2, 3, 4, 5]

---

### 3.4.2 리스트 길이

리스트의 원소 개수는 `len()` 함수로 확인한다.

    len(a)

결과:

    5

---

### 3.4.3 리스트 인덱싱

파이썬의 인덱스는 0부터 시작한다.

    a[0]

결과:

    1

    a[4]

결과:

    5

---

### 3.4.4 리스트 값 변경

리스트의 특정 위치 값을 변경할 수 있다.

    a[4] = 99
    print(a)

결과:

    [1, 2, 3, 4, 99]

---

### 3.4.5 리스트 슬라이싱

리스트의 일부 구간을 가져올 수 있다.

    a[0:2]

결과:

    [1, 2]

    a[1:]

결과:

    [2, 3, 4, 99]

    a[:3]

결과:

    [1, 2, 3]

    a[:-1]

결과:

    [1, 2, 3, 4]

    a[:-2]

결과:

    [1, 2, 3]

시험에서는 파이썬 인덱스가 0부터 시작한다는 점을 반드시 기억한다.

---

## 3.5 딕셔너리

### 3.5.1 딕셔너리의 의미

딕셔너리(Dictionary)는 key와 value를 한 쌍으로 저장하는 자료형이다.

형식:

    {key: value}

예:

    me = {'height': 180, 'weight': 70}

---

### 3.5.2 딕셔너리 값 접근

    me['height']

결과:

    180

    me['weight']

결과:

    70

---

### 3.5.3 새 원소 추가

    me['age'] = 30
    print(me)

결과:

    {'height': 180, 'weight': 70, 'age': 30}

---

### 3.5.4 pandas 데이터프레임 예

딕셔너리와 pandas를 이용하여 데이터프레임을 만들 수 있다.

    import pandas as pd
    import numpy as np

    D = {
        'Name': pd.Series(['Tom', 'James', 'Ricky', 'Vin', 'Steve', 'Smith', 'Jack',
                           'Lee', 'David', 'Gasper', 'Betina', 'Andres']),
        'Age': pd.Series([25, 26, 25, 23, 30, 29, 23, 34, 40, 30, 51, 46]),
        'Rating': pd.Series([4.23, 3.24, 3.98, 2.56, 3.20, 4.63, 3.78, 2.98, 4.80, 4.10, 3.65])
    }

    df = pd.DataFrame(D)
    print(df)
    df.head()

해석:

- `pd.Series()`는 열 데이터를 만든다.
- `pd.DataFrame()`은 표 형태의 데이터프레임을 만든다.
- `df.head()`는 앞부분 자료를 보여준다.

---

## 3.6 bool

bool은 참과 거짓을 나타내는 자료형이다.

    hungry = True
    sleepy = False

    type(hungry)

결과:

    bool

---

### 3.6.1 논리연산

| 연산자 | 의미  |
|-----|-----|
| not | 부정  |
| and | 그리고 |
| or  | 또는  |

예:

    not hungry

결과:

    False

    hungry and sleepy

결과:

    False

    hungry or sleepy

결과:

    True

---

## 3.7 if 문

### 3.7.1 if 기본 구조

조건이 참일 때만 특정 코드를 실행한다.

    hungry = True

    if hungry:
        print("I'm hungry")

결과:

    I'm hungry

---

### 3.7.2 if-else 구조

조건이 참일 때와 거짓일 때 실행할 내용을 다르게 지정할 수 있다.

    hungry = False

    if hungry:
        print("I'm hungry")
    else:
        print("I'm not hungry")
        print("I'm sleepy")

결과:

    I'm not hungry
    I'm sleepy

시험에서는 파이썬이 들여쓰기로 코드 블록을 구분한다는 점을 기억한다.

---

## 3.8 for 반복문

### 3.8.1 리스트 반복

    for i in [1, 2, 3]:
        print(i)

결과:

    1
    2
    3

---

### 3.8.2 문자열 리스트 반복

    name = ['a', 'b', 'c', 'd', 'e']

    for i in name:
        print(i)

결과:

    a
    b
    c
    d
    e

---

### 3.8.3 range 반복

`range(10)`은 0부터 9까지의 값을 만든다.

    sum = 0

    for i in range(10):
        sum = sum + i

    print(sum)

결과:

    45

주의:

    range(10)은 0부터 10까지가 아니라 0부터 9까지이다.

---

## 3.9 함수

### 3.9.1 함수 정의

함수는 `def`를 사용하여 정의한다.

    def hello():
        print("Hello World !")
        print("Welcome to Python class !")

    hello()

결과:

    Hello World !
    Welcome to Python class !

---

### 3.9.2 매개변수가 있는 함수

    def hello2(object):
        print("Hello " + object + " !")

    hello2("Jang")

결과:

    Hello Jang !

---

## 3.10 클래스

### 3.10.1 클래스의 의미

클래스는 객체를 만들기 위한 틀이다.

객체 안에는 속성과 기능을 함께 담을 수 있다.

---

### 3.10.2 클래스 예: Man

    class Man:
        def __init__(self, name):
            self.name = name
            print("Initialized !")

        def hello(self):
            print("Hello " + self.name + " !")

        def goodbye(self):
            print("Good-bye " + self.name + " !")

    m = Man("David")

결과:

    Initialized !

    m.hello()

결과:

    Hello David !

    m.goodbye()

결과:

    Good-bye David !

---

### 3.10.3 클래스 예: Person

    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def disp(self):
            print(self.name)
            print(self.age)

    p1 = Person('홍길동', 22)
    p2 = Person('철수', 35)

    p1.disp()

결과:

    홍길동
    22

    p2.disp()

결과:

    철수
    35

---

### 3.10.4 입력을 받는 클래스 예

    class Person2:
        def __init__(self):
            self.name = input('Name:')
            self.age = int(input('Age:'))

        def disprint(self):
            print('Name = ', self.name)
            print('Age = ', self.age)

    customer = []

    for i in range(5):
        customer.append(Person2())

    customer[0].disprint()
    customer[1].disprint()

해석:

- `input()`은 사용자 입력을 받는다.
- `int()`는 입력값을 정수로 변환한다.
- `customer` 리스트에 Person2 객체를 저장한다.

---

## 3.11 NumPy 가져오기

### 3.11.1 NumPy 배열 생성

NumPy는 수치 계산을 위한 대표 라이브러리이다.

    import numpy as np

    x = np.array([1.0, 2.0, 3.0])
    print(x)
    type(x)

결과:

    [1. 2. 3.]
    numpy.ndarray

---

### 3.11.2 NumPy 배열 연산

NumPy 배열은 원소별 연산이 가능하다.

    y = x / 3
    print(y)

결과:

    [0.33333333 0.66666667 1.        ]

배열끼리 연산:

    x = np.array([1.0, 2.0, 3.0])
    y = np.array([2.0, 4.0, 6.0])

    x + y
    x - y
    x * y
    x / y

결과:

    array([3., 6., 9.])
    array([-1., -2., -3.])
    array([ 2.,  8., 18.])
    array([0.5, 0.5, 0.5])

---

## 3.12 NumPy N차원 배열

### 3.12.1 2차원 배열 생성

    import numpy as np

    A = np.array([[5, 7], [9, 11]])
    print(A)

결과:

    [[ 5  7]
     [ 9 11]]

---

### 3.12.2 배열 원소 접근

    A[0]

결과:

    array([5, 7])

    A[1]

결과:

    array([9, 11])

    A[0, 0]

결과:

    5

    A[1, 0]

결과:

    9

주의:

- 파이썬 배열의 인덱스는 0부터 시작한다.
- `A[0,0]`은 첫 번째 행, 첫 번째 열이다.
- `A[1,0]`은 두 번째 행, 첫 번째 열이다.

---

### 3.12.3 배열 덧셈과 곱셈

    B = np.array([[3, 0], [0, 6]])

    A + B

결과:

    array([[ 8,  7],
           [ 9, 17]])

    A * B

결과 예:

    array([[15,  0],
           [ 0, 66]])

해석:

- NumPy의 `A * B`는 행렬곱이 아니라 원소별 곱셈이다.

---

## 3.13 Broadcast

Broadcast는 형상이 다른 배열끼리 계산할 때 작은 배열을 자동으로 확장하여 계산하는 기능이다.

예:

    import numpy as np

    A = np.array([[1, 2], [3, 4]])
    B = np.array([10, 20])
    C = 10

    A * B

결과:

    array([[10, 40],
           [30, 80]])

    A * C

결과:

    array([[10, 20],
           [30, 40]])

해석:

- `B = [10, 20]`이 각 행에 맞게 확장되어 곱해진다.
- `C = 10`은 배열 전체에 적용된다.

---

## 3.14 원소 접근과 조건 선택

### 3.14.1 원소 접근

    X = np.array([[51, 55], [14, 19], [0, 4]])
    print(X)

결과:

    [[51 55]
     [14 19]
     [ 0  4]]

    X[0]

결과:

    array([51, 55])

    X[0][1]

결과:

    55

---

### 3.14.2 반복문으로 행 접근

    for row in X:
        print(row)

결과:

    [51 55]
    [14 19]
    [0 4]

---

### 3.14.3 flatten

`flatten()`은 다차원 배열을 1차원으로 펼친다.

    Y = X.flatten()
    print(Y)

결과:

    [51 55 14 19  0  4]

---

### 3.14.4 조건식

    Y > 15

결과:

    array([ True,  True, False,  True, False, False])

    Y[Y > 15]

결과:

    array([51, 55, 19])

해석:

- `Y > 15`는 각 원소가 15보다 큰지 검사한다.
- `Y[Y > 15]`는 조건을 만족하는 원소만 선택한다.

---

## 3.15 matplotlib

### 3.15.1 기본 그래프 그리기

matplotlib은 파이썬에서 그래프를 그릴 때 사용하는 대표 라이브러리이다.

    import matplotlib.pyplot as plt
    import numpy as np

    x = np.arange(0, 6, 0.1)
    y = np.sin(x)

    plt.plot(x, y)
    plt.show()

해석:

- `np.arange(0, 6, 0.1)`은 0부터 6 전까지 0.1 간격의 값을 만든다.
- `np.sin(x)`는 사인값을 계산한다.
- `plt.plot()`은 그래프를 그린다.
- `plt.show()`는 그래프를 표시한다.

---

### 3.15.2 sin과 cos 그래프

    import matplotlib.pyplot as plt
    import numpy as np

    x = np.arange(0, 6, 0.1)
    y1 = np.sin(x)
    y2 = np.cos(x)

    plt.plot(x, y1, label='sin')
    plt.plot(x, y2, linestyle='--', label='cos')
    plt.xlabel('x-axis')
    plt.ylabel('y-axis')
    plt.title('sin & cos')
    plt.legend()
    plt.show()

해석:

- `label`은 범례 이름을 지정한다.
- `linestyle='--'`는 점선으로 표시한다.
- `xlabel()`은 x축 이름을 지정한다.
- `ylabel()`은 y축 이름을 지정한다.
- `title()`은 그래프 제목을 지정한다.
- `legend()`는 범례를 표시한다.

---

## 정리하기

1. 파이썬은 Windows, Unix, MacOS 등 다양한 운영체제에서 사용할 수 있는 플랫폼 독립적인 언어이다.

2. 파이썬은 설치와 사용이 비교적 쉽고, 문법이 간단하여 배우기 쉽다.

3. 파이썬은 라이브러리 패키지를 통해 쉽게 확장할 수 있다.

4. 파이썬의 개발자는 Guido van Rossum이다.

5. 자료분석을 위해 Anaconda를 설치하면 Python, Jupyter Notebook, Spyder 등 여러 도구를 함께 사용할 수 있다.

6. `pip`는 Python 패키지를 설치하고 관리하는 프로그램이다.

7. Jupyter Notebook에서는 Markdown 셀과 Code 셀을 구분하여 사용할 수 있다.

8. Google Colab은 웹에서 파이썬을 실행할 수 있는 온라인 환경이다.

9. 파이썬에서 거듭제곱은 `**`, 몫은 `//`, 나머지는 `%`를 사용한다.

10. 파이썬의 주요 자료형에는 int, float, str, bool이 있다.

11. 리스트는 여러 값을 순서대로 저장하는 자료형이며, 인덱스는 0부터 시작한다.

12. 딕셔너리는 key와 value를 한 쌍으로 저장한다.

13. bool 자료형은 True와 False 값을 가지며, `not`, `and`, `or` 연산을 사용할 수 있다.

14. `if` 문은 조건에 따라 실행 여부를 결정하고, 파이썬은 들여쓰기로 코드 블록을 구분한다.

15. `for` 문은 리스트나 range 같은 반복 가능한 객체를 순서대로 처리한다.

16. `range(10)`은 0부터 9까지의 값을 생성한다.

17. 함수는 `def`로 정의한다.

18. 클래스는 객체를 만들기 위한 틀이며, `__init__`은 객체 생성 시 실행되는 초기화 메서드이다.

19. NumPy 배열은 `np.array()`로 만들며, 원소별 연산을 쉽게 수행할 수 있다.

20. NumPy 배열의 인덱스도 0부터 시작한다.

21. Broadcast는 형상이 다른 배열끼리 계산할 때 작은 배열을 자동 확장하여 계산하는 기능이다.

22. `flatten()`은 다차원 배열을 1차원 배열로 변환한다.

23. 조건식을 이용하면 조건을 만족하는 배열 원소만 선택할 수 있다.

24. matplotlib은 파이썬에서 그래프를 그릴 때 사용하는 대표 라이브러리이다.

---

## 핵심 요약

### 1. 파이썬 설치와 실행

| 개념               | 핵심                         |
|------------------|----------------------------|
| Anaconda         | 파이썬과 자료분석 패키지 배포판          |
| Path 설정          | 명령 프롬프트에서 파이썬 명령 사용 가능하게 함 |
| pip              | 패키지 설치와 관리                 |
| Spyder           | 파이썬 개발 환경                  |
| Jupyter Notebook | 웹 기반 파이썬 실행 환경             |
| Google Colab     | 온라인 파이썬 실행 환경              |

---

### 2. 파이썬 기초 문법

| 항목   | 핵심                    |
|------|-----------------------|
| 산술연산 | +, -, *, /, **, //, % |
| 자료형  | int, float, str, bool |
| 변수   | 값을 저장하는 이름            |
| 리스트  | 순서가 있는 자료형            |
| 딕셔너리 | key-value 쌍           |
| if   | 조건문                   |
| for  | 반복문                   |
| 함수   | def로 정의               |
| 클래스  | 객체를 만들기 위한 틀          |

---

### 3. 리스트 핵심

| 표현     | 결과 또는 의미    |
|--------|-------------|
| a[0]   | 첫 번째 원소     |
| a[4]   | 다섯 번째 원소    |
| a[0:2] | 0번째부터 1번째까지 |
| a[1:]  | 1번째부터 끝까지   |
| a[:3]  | 처음부터 2번째까지  |
| a[:-1] | 마지막 원소 제외   |
| a[:-2] | 마지막 두 원소 제외 |

---

### 4. NumPy 핵심

| 기능     | 코드                         |
|--------|----------------------------|
| 가져오기   | import numpy as np         |
| 배열 생성  | np.array([1.0, 2.0, 3.0])  |
| 수열 생성  | np.arange(0, 6, 0.1)       |
| 2차원 배열 | np.array([[5,7], [9,11]])  |
| 1차원 변환 | X.flatten()                |
| 조건 선택  | Y[Y > 15]                  |
| 배열 연산  | x + y, x - y, x * y, x / y |

---

### 5. matplotlib 핵심

| 기능      | 코드                              |
|---------|---------------------------------|
| 가져오기    | import matplotlib.pyplot as plt |
| 그래프 그리기 | plt.plot(x, y)                  |
| 그래프 표시  | plt.show()                      |
| x축 이름   | plt.xlabel('x-axis')            |
| y축 이름   | plt.ylabel('y-axis')            |
| 제목      | plt.title('sin & cos')          |
| 범례      | plt.legend()                    |
| 점선      | linestyle='--'                  |

---

## 연습문제 정리

### Q1. Python 패키지를 설치하고 관리하는 프로그램은?

문제 예:

    C:\anaconda3> _____ install tensorflow

정답:

    pip

해설:
`pip`는 Python 패키지를 설치하고 관리하는 프로그램이다.

    pip install tensorflow

---

### Q2. 다음과 같이 함수가 정의되어 있을 때, `hello2("Jeong")`의 결과는?

문제:

    def hello2(object):
        print("Hello " + object + " !")

    hello2("Jeong")

정답:

    Hello Jeong !

해설:
`object`에 `"Jeong"`이 전달되어 문자열이 연결된다.

---

### Q3. 다음 파이썬 프로그램에서 `a[4]`의 값은?

문제:

    a = [1, 2, 3, 4, 5]
    a[4]

정답:

    5

해설:
파이썬의 리스트 인덱스는 0부터 시작한다.

| 인덱스  | 값 |
|------|---|
| a[0] | 1 |
| a[1] | 2 |
| a[2] | 3 |
| a[3] | 4 |
| a[4] | 5 |

---

### Q4. 파이썬에서 딕셔너리로 선언한 것 중 적합한 것은?

정답:

    me = {'height': 180, 'weight': 70}

해설:
딕셔너리는 key와 value를 콜론으로 연결하고, 전체를 중괄호로 묶는다.

    {'key': value}

---

### Q5. 파이썬을 설치하기 위한 아나콘다 사이트는?

정답:

    www.anaconda.com

해설:
아나콘다는 파이썬과 자료분석 관련 패키지를 함께 제공하는 배포판이며, 공식 사이트에서 다운로드할 수 있다.

---

## 시험 직전 체크포인트

### 반드시 암기하기

- Python 개발자 = Guido van Rossum
- Anaconda 설치 사이트 = www.anaconda.com
- pip = Python 패키지 설치 및 관리 프로그램
- Jupyter Notebook = 웹 기반 실행 환경
- Google Colab = 온라인 파이썬 실행 환경
- 거듭제곱 = `**`
- 몫 = `//`
- 나머지 = `%`
- 자료형 확인 = `type()`
- 리스트 길이 = `len()`
- 리스트 인덱스는 0부터 시작
- 딕셔너리 = key와 value를 한 쌍으로 저장
- bool 값 = True, False
- 조건문 = if
- 반복문 = for
- range(10) = 0부터 9까지
- 함수 정의 = def
- 클래스 초기화 메서드 = `__init__`
- NumPy 가져오기 = `import numpy as np`
- NumPy 배열 = `np.array()`
- matplotlib 가져오기 = `import matplotlib.pyplot as plt`
- 그래프 그리기 = `plt.plot()`
- 그래프 출력 = `plt.show()`

---

### 객관식에서 자주 나올 표현

| 문제 표현            | 정답 후보                          |
|------------------|--------------------------------|
| Python 패키지 설치·관리 | pip                            |
| 파이썬 설치 배포판       | Anaconda                       |
| 아나콘다 사이트         | www.anaconda.com               |
| 웹 기반 파이썬 실행      | Jupyter Notebook, Google Colab |
| 3 ** 2           | 9                              |
| 17 // 4          | 4                              |
| 17 % 4           | 1                              |
| type(10)         | int                            |
| type(2.710)      | float                          |
| type("hello")    | str                            |
| True 또는 False    | bool                           |
| a[4]             | 다섯 번째 원소                       |
| key-value 저장     | dictionary                     |
| 조건 판단            | if                             |
| 반복 처리            | for                            |
| 0부터 9까지          | range(10)                      |
| 함수 정의            | def                            |
| 객체 생성 틀          | class                          |
| 배열 계산 라이브러리      | NumPy                          |
| 그래프 작성 라이브러리     | matplotlib                     |

---

### 헷갈리는 개념 구분

| 개념               | 구분 포인트           |
|------------------|------------------|
| 리스트              | 순서가 있고 인덱스로 접근   |
| 딕셔너리             | key로 value 접근    |
| 튜플               | 이 강의에서는 중심 내용 아님 |
| bool             | True, False      |
| if               | 조건문              |
| for              | 반복문              |
| def              | 함수 정의            |
| class            | 객체를 만들기 위한 틀     |
| NumPy 배열         | 수치 계산에 적합        |
| pandas DataFrame | 표 형태 데이터 처리      |
| matplotlib       | 그래프 작성           |
| range(10)        | 0부터 9까지          |
| `*`              | 곱셈               |
| `**`             | 거듭제곱             |
| `//`             | 몫                |
| `%`              | 나머지              |

---