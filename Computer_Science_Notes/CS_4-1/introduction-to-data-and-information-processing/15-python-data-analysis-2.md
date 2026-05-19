# 데이터정보처리입문

## 15. 파이썬을 활용한 자료분석 (2)

### 강의 목차

1. 자료 읽기
2. 기술통계량 및 빈도표
3. 그래프 그리기

---

## 1. 자료 읽기

### 1.1 실습 자료

이번 강의에서는 다음 자료 파일을 사용한다.

| 파일          | 설명        |
|-------------|-----------|
| nex8-1.csv  | CSV 형식 자료 |
| nex8-1.xlsx | 엑셀 형식 자료  |

자료는 다음 변수들로 구성된다.

| 변수     | 의미   |
|--------|------|
| id     | 번호   |
| sex    | 성별   |
| age    | 나이   |
| edu    | 교육정도 |
| salary | 월수입  |

예시 자료:

| id | sex | age | edu    | salary |
|---:|-----|----:|--------|-------:|
|  1 | m   |  21 | high   |    150 |
|  2 | f   |  22 | middle |    100 |
|  3 | m   |  33 | high   |    200 |
|  4 | f   |  33 | univ   |    220 |
|  5 | m   |  28 | high   |    170 |

---

### 1.2 CSV 파일 읽기

CSV 파일은 pandas의 `read_csv()` 함수를 이용하여 읽는다.

    import pandas as pd

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8.head()

실행 결과 예:

    id sex age edu salary
    0  1   m  21 high   150
    1  2   f  22 middle 100
    2  3   m  33 high   200
    3  4   f  33 univ   220
    4  5   m  28 high   170

해석:

- `pd.read_csv()`는 CSV 파일을 읽는다.
- `header=0`은 첫 번째 행을 변수명으로 사용한다는 의미이다.
- `head()`는 데이터의 앞부분을 보여준다.

---

### 1.3 데이터 앞부분과 뒷부분 확인

앞의 3개 행만 확인할 때는 `head(3)`을 사용한다.

    nex8.head(3)

실행 결과:

    id sex age edu salary
    0  1   m  21 high   150
    1  2   f  22 middle 100
    2  3   m  33 high   200

뒤의 3개 행을 확인할 때는 `tail(3)`을 사용한다.

    nex8.tail(3)

실행 결과:

    id sex age edu salary
    7  8   m  32 univ   220
    8  9   f  44 middle 370
    9 10   m  55 univ   410

---

### 1.4 데이터프레임 확인

자료의 형태와 크기를 확인할 수 있다.

    type(nex8)

실행 결과:

    pandas.core.frame.DataFrame

    nex8.shape

실행 결과:

    (10, 5)

해석:

- `type(nex8)`은 nex8 객체가 pandas DataFrame임을 보여준다.
- `shape`는 행과 열의 개수를 보여준다.
- `(10, 5)`는 10행 5열이라는 뜻이다.

---

### 1.5 엑셀 파일 읽기

엑셀 파일은 pandas의 `read_excel()` 함수를 이용하여 읽는다.

    import pandas as pd

    nex8_2 = pd.read_excel("c:/data/dataintro/nex8-1.xlsx", header=0)
    nex8_2.head(3)

실행 결과:

    id sex age edu salary
    0  1   m  21 high   150
    1  2   f  22 middle 100
    2  3   m  33 high   200

시험에서는 CSV는 `pd.read_csv()`, 엑셀은 `pd.read_excel()`로 구분해서 기억한다.

---

## 2. 변수 선택

### 2.1 하나의 변수 선택

하나의 변수를 선택하는 방법은 두 가지가 있다.

    nex8["age"]

또는

    nex8.age

둘 다 `age` 변수만 선택한다.

---

### 2.2 여러 변수 선택

여러 변수를 선택할 때는 변수 이름 목록을 만든 뒤 사용한다.

    cols = ['sex', 'age', 'edu', 'salary']
    nex8[cols]

해석:

- `cols`에 선택할 변수 이름을 리스트로 저장한다.
- `nex8[cols]`는 해당 변수들만 가져온다.

---

### 2.3 iloc를 이용한 변수 선택

`iloc`는 행과 열의 위치 번호를 이용하여 데이터를 선택한다.

    nex8.iloc[:, 1:]

해석:

- `:`는 모든 행을 의미한다.
- `1:`은 두 번째 열부터 끝까지를 의미한다.
- 즉, 첫 번째 변수인 `id`를 제거하고 나머지 변수를 선택한다.

예:

    nex8 = nex8.iloc[:, 1:]
    nex8.head(2)

실행 결과:

    sex age edu salary
    0  m  21 high   150
    1  f  22 middle 100

시험에서는 `nex8.iloc[:, 1:]`이 첫 번째 열을 제외하고 나머지 열을 선택한다는 점을 기억한다.

---

## 3. 기술통계량 구하기

### 3.1 자료 읽고 id 제거하기

    import pandas as pd

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8 = nex8.iloc[:, 1:]
    nex8.head(2)

실행 결과:

    sex age edu salary
    0  m  21 high   150
    1  f  22 middle 100

---

### 3.2 평균, 표준편차, 중앙값, 분위수

월수입 `salary` 변수의 기술통계량을 구한다.

    nex8["salary"].mean()

실행 결과:

    243.0

    nex8["salary"].std()

실행 결과:

    98.21178929006209

    nex8.salary.median()

실행 결과:

    220.0

    nex8.salary.quantile(0.75)

실행 결과:

    297.5

---

### 3.3 주요 함수 정리

| 함수             | 기능          |
|----------------|-------------|
| mean()         | 평균          |
| std()          | 표준편차        |
| median()       | 중앙값         |
| quantile(0.75) | 제3사분위수      |
| describe()     | 주요 기술통계량 요약 |

---

### 3.4 describe 함수

`describe()`는 수치형 변수의 기술통계량을 한 번에 보여준다.

    nex8.describe()

실행 결과 예:

    age       salary
    count  10.000000  10.000000
    mean   34.800000 243.000000
    std    10.347302  98.211789
    min    21.000000 100.000000
    25%    29.000000 177.500000
    50%    33.000000 220.000000
    75%    40.500000 297.500000
    max    55.000000 410.000000

| 항목    | 의미     |
|-------|--------|
| count | 자료 개수  |
| mean  | 평균     |
| std   | 표준편차   |
| min   | 최소값    |
| 25%   | 제1사분위수 |
| 50%   | 중앙값    |
| 75%   | 제3사분위수 |
| max   | 최대값    |

---

## 4. 범주형 변수로 바꾸기

### 4.1 범주형 변수 변환의 필요성

성별이나 교육정도처럼 숫자로 입력되어 있지만 실제 의미는 범주인 변수들이 있다.

예:

| 변수  | 실제 의미 |
|-----|-------|
| sex | 성별    |
| edu | 교육정도  |

이런 변수는 수치형으로 분석하면 평균이나 표준편차가 계산되어 의미가 이상해질 수 있다.

---

### 4.2 category로 변환

    ex8 = pd.read_csv("c:/data/dataintro/ex8-1.csv", header=0)

    ex8["sex"] = ex8["sex"].astype("category")
    ex8["edu"] = ex8["edu"].astype("category")

    ex8.describe()

해석:

- `astype("category")`는 변수를 범주형으로 변환한다.
- 범주형으로 변환하면 `describe()`에서 수치형 변수 중심으로 요약된다.
- 성별과 교육정도는 숫자가 아니라 범주로 해석해야 한다.

---

## 5. 그룹별 기술통계량 구하기

### 5.1 groupby 함수

그룹별 통계량은 `groupby()`를 이용한다.

성별에 따라 월수입 `salary`의 기술통계량을 구한다.

    import pandas as pd

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8 = nex8.iloc[:, 1:]

    group_stat_by_sex = nex8.groupby("sex")["salary"].describe()
    group_stat_by_sex

실행 결과:

    count       mean         std    min    25%    50%    75%    max
    sex
    f     4.0 245.000000 114.455231 100.0 190.0 255.0 310.0 370.0
    m     6.0 241.666667  97.450842 150.0 177.5 210.0 280.0 410.0

---

### 5.2 그룹별 평균과 표준편차 선택

성별 월수입 평균만 선택한다.

    group_stat_by_sex["mean"]

실행 결과:

    sex
    f    245.000000
    m    241.666667

성별 월수입 표준편차만 선택한다.

    group_stat_by_sex["std"]

실행 결과:

    sex
    f    114.455231
    m     97.450842

---

### 5.3 loc를 이용한 특정 그룹 선택

남성 자료만 선택한다.

    group_stat_by_sex.loc["m"]

여성 자료만 선택한다.

    group_stat_by_sex.loc["f"]

여성 자료 실행 결과 예:

    count      4.000000
    mean     245.000000
    std      114.455231
    min      100.000000
    25%      190.000000
    50%      255.000000
    75%      310.000000
    max      370.000000
    Name: f, dtype: float64

---

## 6. 빈도표 및 분할표 구하기

## 6.1 빈도표

빈도표는 `pd.crosstab()`을 이용해 만들 수 있다.

성별 빈도표:

    import pandas as pd

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)

    sex_freq = pd.crosstab(index=nex8["sex"], columns="count")
    sex_freq

실행 결과:

    col_0 count
    sex
    f        4
    m        6

교육정도 빈도표:

    edu_freq = pd.crosstab(index=nex8["edu"], columns="count")
    edu_freq

실행 결과:

    col_0  count
    edu
    high      4
    middle    2
    univ      4

---

### 6.2 분할표

두 범주형 변수의 교차 빈도는 `pd.crosstab()`에 행과 열을 모두 지정하여 구한다.

    sex_edu_table = pd.crosstab(index=nex8["sex"], columns=nex8["edu"])
    sex_edu_table

실행 결과:

    edu high middle univ
    sex
    f      1      2    1
    m      3      0    3

---

### 6.3 카이제곱 독립성 검정

분할표에 대해 카이제곱 독립성 검정을 할 수 있다.

    from scipy.stats import chi2_contingency

    chi2_contingency(sex_edu_table)

실행 결과:

    (3.7499999999999996,
     0.1533549668449285,
     2,
     array([[1.6, 0.8, 1.6],
            [2.4, 1.2, 2.4]]))

해석:

| 결과 위치  | 의미       |
|--------|----------|
| 첫 번째 값 | 카이제곱 통계량 |
| 두 번째 값 | p-value  |
| 세 번째 값 | 자유도      |
| 네 번째 값 | 기대도수 배열  |

---

## 7. 그래프 그리기

## 7.1 막대그림

성별 빈도표와 교육정도 빈도표를 이용하여 막대그림을 그린다.

    import pandas as pd
    import matplotlib.pyplot as plt

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8 = nex8.iloc[:, 1:]

    sex_freq = pd.crosstab(index=nex8["sex"], columns="count")
    edu_freq = pd.crosstab(index=nex8["edu"], columns="count")

    plt.bar(sex_freq.index, sex_freq["count"])
    plt.bar(edu_freq.index, edu_freq["count"])

해석:

- `plt.bar()`는 막대그림을 그린다.
- `sex_freq.index`는 성별 범주이다.
- `sex_freq["count"]`는 성별 도수이다.

---

## 7.2 원그림

교육정도 빈도표로 원그림을 그린다.

    plt.pie(edu_freq["count"], labels=edu_freq.index)

해석:

- `plt.pie()`는 원그림을 그린다.
- `labels=edu_freq.index`는 각 조각의 이름을 지정한다.

---

## 7.3 겹친막대그림

성별과 교육정도의 분할표를 이용하여 겹친막대그림을 그린다.

    sex_edu_table = pd.crosstab(index=nex8["sex"], columns=nex8["edu"])
    sex_edu_table.plot.bar(stacked=True)

해석:

- `plot.bar(stacked=True)`는 누적 막대그래프를 그린다.
- 성별에 따른 교육정도 구성을 비교할 수 있다.

---

## 8. 히스토그램, 줄기-잎 그림, 상자그림

## 8.1 히스토그램

월수입 `salary` 변수의 히스토그램을 그린다.

    import pandas as pd
    import matplotlib.pyplot as plt

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8 = nex8.iloc[:, 1:]

    plt.hist(nex8["salary"], bins=4)

실행 결과 정보:

    array([3., 3., 2., 2.])
    array([100., 177.5, 255., 332.5, 410.])

해석:

- `bins=4`는 계급을 4개로 나눈다는 뜻이다.
- 첫 번째 배열은 각 계급의 도수이다.
- 두 번째 배열은 계급 경계값이다.

---

## 8.2 줄기-잎 그림

줄기-잎 그림을 그리려면 `stemgraphic` 패키지를 사용할 수 있다.

DOS 창에서 먼저 설치한다.

    pip install stemgraphic

파이썬에서 실행한다.

    import stemgraphic

    stemgraphic.stem_graphic(nex8.salary, scale=100)

해석:

- `stemgraphic`은 줄기-잎 그림을 그리는 패키지이다.
- `scale=100`은 줄기 단위 조정에 사용된다.

---

## 8.3 상자그림

상자그림은 seaborn의 `boxplot()`을 이용할 수 있다.

    import seaborn as sns

    sns.boxplot(x="sex", y="salary", data=nex8)

해석:

- 성별에 따른 월수입 분포를 상자그림으로 비교한다.
- 중앙값, 사분위수, 산포를 확인할 수 있다.

---

## 9. 산점도 그리기

### 9.1 기본 산점도

나이와 월수입의 관계를 산점도로 그린다.

    import pandas as pd
    import matplotlib.pyplot as plt

    nex8 = pd.read_csv("c:/data/dataintro/nex8-1.csv", header=0)
    nex8 = nex8.iloc[:, 1:]

    plt.scatter(nex8.age, nex8.salary)

해석:

- `plt.scatter()`는 산점도를 그린다.
- x축은 나이, y축은 월수입이다.

---

### 9.2 성별에 따라 색상 구분

`np.where()`를 이용하여 성별에 따라 색을 다르게 지정할 수 있다.

    import numpy as np

    colors = np.where(nex8["sex"] == 'm', 'r', 'b')
    colors

실행 결과:

    array(['r', 'b', 'r', 'b', 'r', 'r', 'b', 'r', 'b', 'r'], dtype='<U1')

산점도:

    plt.scatter(nex8.age, nex8.salary, c=colors)

해석:

- 성별이 남성 `m`이면 빨간색 `r`
- 여성 `f`이면 파란색 `b`
- `c=colors`는 점 색상을 지정한다.

---

### 9.3 범례가 있는 산점도

남성과 여성 자료를 분리하여 점 모양과 색상을 다르게 지정한다.

    import matplotlib.pyplot as plt
    import numpy as np

    colors = np.where(nex8["sex"] == 'm', 'r', 'b')

    plt.scatter(nex8.age, nex8.salary, c=colors)

    mage = nex8.age[nex8.sex == 'm']
    fage = nex8.age[nex8.sex == 'f']
    msalary = nex8.salary[nex8.sex == 'm']
    fsalary = nex8.salary[nex8.sex == 'f']

    plt.scatter(mage, msalary, marker="x", color="r", label='Male')
    plt.scatter(fage, fsalary, marker="o", color="b", label='Female')

    plt.legend()
    plt.show()

해석:

- 남성은 빨간색 x 모양으로 표시한다.
- 여성은 파란색 o 모양으로 표시한다.
- `label`은 범례 이름이다.
- `plt.legend()`는 범례를 표시한다.
- `plt.show()`는 그래프를 화면에 출력한다.

---

## 정리하기

1. pandas의 `read_csv()`는 CSV 파일을 읽을 때 사용한다.

2. pandas의 `read_excel()`은 엑셀 파일을 읽을 때 사용한다.

3. `head()`는 데이터 앞부분, `tail()`은 데이터 뒷부분을 확인할 때 사용한다.

4. `type()`을 이용하여 데이터 객체의 형식을 확인할 수 있다.

5. `shape`는 데이터의 행과 열의 개수를 확인할 때 사용한다.

6. 하나의 변수는 `nex8["age"]` 또는 `nex8.age`로 선택할 수 있다.

7. 여러 변수는 변수 이름 리스트를 만든 뒤 `nex8[cols]`로 선택할 수 있다.

8. `iloc[:, 1:]`는 첫 번째 열을 제외하고 나머지 열을 선택한다.

9. `mean()`은 평균, `std()`는 표준편차, `median()`은 중앙값, `quantile()`은 분위수를 구한다.

10. `describe()`는 기술통계량을 한 번에 요약한다.

11. `astype("category")`는 변수를 범주형으로 변환할 때 사용한다.

12. `groupby()`는 그룹별 통계량을 구할 때 사용한다.

13. `pd.crosstab()`은 빈도표와 분할표를 만들 때 사용한다.

14. `chi2_contingency()`는 분할표에 대한 카이제곱 독립성 검정을 수행한다.

15. `plt.bar()`는 막대그림을 그릴 때 사용한다.

16. `plt.pie()`는 원그림을 그릴 때 사용한다.

17. `plot.bar(stacked=True)`는 겹친막대그림을 그릴 때 사용한다.

18. `plt.hist()`는 히스토그램을 그릴 때 사용한다.

19. `stemgraphic.stem_graphic()`은 줄기-잎 그림을 그릴 때 사용한다.

20. `sns.boxplot()`은 상자그림을 그릴 때 사용한다.

21. `plt.scatter()`는 산점도를 그릴 때 사용한다.

22. `np.where()`는 조건에 따라 값을 선택할 때 사용한다.

23. `plt.legend()`는 범례를 추가할 때 사용한다.

24. `plt.show()`는 그래프를 화면에 출력할 때 사용한다.

---

## 핵심 요약

### 1. 자료 읽기

| 작업        | 명령                             |
|-----------|--------------------------------|
| CSV 파일 읽기 | pd.read_csv("파일명", header=0)   |
| 엑셀 파일 읽기  | pd.read_excel("파일명", header=0) |
| 앞부분 확인    | head()                         |
| 뒷부분 확인    | tail()                         |
| 자료형 확인    | type()                         |
| 행·열 개수 확인 | shape                          |

---

### 2. 변수 선택

| 작업        | 명령               |
|-----------|------------------|
| 하나의 변수 선택 | nex8["age"]      |
| 하나의 변수 선택 | nex8.age         |
| 여러 변수 선택  | nex8[cols]       |
| 첫 번째 열 제거 | nex8.iloc[:, 1:] |

---

### 3. 기술통계량

| 작업      | 명령                 |
|---------|--------------------|
| 평균      | mean()             |
| 표준편차    | std()              |
| 중앙값     | median()           |
| 분위수     | quantile()         |
| 요약통계량   | describe()         |
| 범주형 변환  | astype("category") |
| 그룹별 통계량 | groupby()          |

---

### 4. 빈도표와 분할표

| 작업      | 명령                                     |
|---------|----------------------------------------|
| 빈도표     | pd.crosstab(index=변수, columns="count") |
| 분할표     | pd.crosstab(index=행변수, columns=열변수)    |
| 카이제곱 검정 | chi2_contingency(분할표)                  |

---

### 5. 그래프 함수

| 그래프     | 명령                         |
|---------|----------------------------|
| 막대그림    | plt.bar()                  |
| 원그림     | plt.pie()                  |
| 겹친막대그림  | plot.bar(stacked=True)     |
| 히스토그램   | plt.hist()                 |
| 줄기-잎 그림 | stemgraphic.stem_graphic() |
| 상자그림    | sns.boxplot()              |
| 산점도     | plt.scatter()              |
| 범례      | plt.legend()               |

---

## 연습문제 정리

### Q1. 다음 출력 결과와 같이 데이터 객체 `nex8`의 각 변수의 기술통계량을 구하고자 한다. 빈칸에 들어갈 명령은?

문제 상황:

    nex8.head(3)
    nex8.describe()

정답:

    nex8.describe()

해설:
`describe()`는 데이터프레임의 수치형 변수에 대해 count, mean, std, min, 25%, 50%, 75%, max 등을 한 번에 출력한다.

---

### Q2. `nex8.head()` 결과가 다음과 같을 때, 변수 `id`를 제거하고 나머지 변수를 가져오기 위한 명령은?

정답:

    nex8.iloc[:, 1:]

해설:
`iloc[:, 1:]`은 모든 행을 선택하고, 열은 두 번째 열부터 끝까지 선택한다. 따라서 첫 번째 열인 `id`를 제외할 수 있다.

---

### Q3. 다음과 같은 막대그래프를 그리고자 한다. 알맞은 명령은?

정답:

    plt.bar

해설:
matplotlib에서 막대그래프는 `plt.bar()` 함수를 이용하여 그린다.

---

### Q4. 파이썬에서 엑셀 파일을 읽기 위한 명령은?

문제 예:

    import pandas as pd
    nex8 = (   )("c:/data/dataintro/nex8-1.xlsx", header=0)

정답:

    pd.read_excel

해설:
엑셀 파일은 pandas의 `pd.read_excel()` 함수를 사용하여 읽는다.

---

### Q5. 파이썬에서 CSV 텍스트 파일을 읽기 위한 명령은?

문제 예:

    import pandas as pd
    nex8 = (   )("c:/data/dataintro/nex8-1.csv", header=0)

정답:

    pd.read_csv

해설:
CSV 파일은 pandas의 `pd.read_csv()` 함수를 사용하여 읽는다.

---

## 시험 직전 체크포인트

### 반드시 암기하기

- CSV 파일 읽기 = `pd.read_csv()`
- 엑셀 파일 읽기 = `pd.read_excel()`
- 데이터 앞부분 확인 = `head()`
- 데이터 뒷부분 확인 = `tail()`
- 데이터 형태 확인 = `type()`
- 행과 열 개수 확인 = `shape`
- 첫 번째 열 제거 = `iloc[:, 1:]`
- 평균 = `mean()`
- 표준편차 = `std()`
- 중앙값 = `median()`
- 분위수 = `quantile()`
- 요약통계량 = `describe()`
- 범주형 변환 = `astype("category")`
- 그룹별 통계량 = `groupby()`
- 빈도표·분할표 = `pd.crosstab()`
- 카이제곱 독립성 검정 = `chi2_contingency()`
- 막대그림 = `plt.bar()`
- 원그림 = `plt.pie()`
- 겹친막대그림 = `plot.bar(stacked=True)`
- 히스토그램 = `plt.hist()`
- 줄기-잎 그림 = `stemgraphic.stem_graphic()`
- 상자그림 = `sns.boxplot()`
- 산점도 = `plt.scatter()`
- 조건별 색상 지정 = `np.where()`
- 범례 추가 = `plt.legend()`

---

### 객관식에서 자주 나올 표현

| 문제 표현           | 정답 후보                               |
|-----------------|-------------------------------------|
| CSV 읽기          | pd.read_csv                         |
| 엑셀 읽기           | pd.read_excel                       |
| 앞 5개 자료 확인      | head()                              |
| 뒤 5개 자료 확인      | tail()                              |
| DataFrame 크기 확인 | shape                               |
| 첫 번째 열 제외       | iloc[:, 1:]                         |
| 기술통계량 전체 요약     | describe()                          |
| 성별 월수입 평균       | groupby("sex")["salary"].describe() |
| 빈도표 작성          | pd.crosstab                         |
| 분할표 작성          | pd.crosstab                         |
| 독립성 검정          | chi2_contingency                    |
| 막대그래프           | plt.bar                             |
| 원그래프            | plt.pie                             |
| 히스토그램           | plt.hist                            |
| 상자그림            | sns.boxplot                         |
| 산점도             | plt.scatter                         |
| 조건에 따라 색 지정     | np.where                            |
| 범례 표시           | plt.legend                          |

---

### 헷갈리는 개념 구분

| 개념         | 구분 포인트        |
|------------|---------------|
| read_csv   | CSV 파일 읽기     |
| read_excel | 엑셀 파일 읽기      |
| head       | 앞부분 확인        |
| tail       | 뒷부분 확인        |
| iloc       | 위치 번호로 행·열 선택 |
| loc        | 이름으로 행·열 선택   |
| describe   | 기술통계량 요약      |
| groupby    | 그룹별 계산        |
| crosstab   | 빈도표와 분할표      |
| bar        | 막대그래프         |
| pie        | 원그래프          |
| hist       | 연속형 자료 분포     |
| boxplot    | 중앙값과 사분위수 비교  |
| scatter    | 두 변수 관계 확인    |
| np.where   | 조건에 따라 값 선택   |

---