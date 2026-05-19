# 데이터정보처리입문

## 13. R을 활용한 자료분석 (2)

### 강의 목차

1. Function 문
2. 정규분포
3. 이산형 그래프 그리기
4. 연속형 그래프 그리기
5. R 알기

---

## 1. Function 문

### 1.1 Function 문의 필요성

R에서 자주 사용하는 계산이나 반복적으로 쓰이는 작업은 `function` 문으로 작성하는 것이 좋다.

함수를 만들어 두면 같은 계산을 여러 번 반복할 때 편리하다.

| 구분       | 설명                 |
|----------|--------------------|
| function | 사용자가 직접 만드는 함수     |
| 인수       | 함수에 전달하는 입력값       |
| 반환값      | 함수 실행 결과           |
| return   | 결과를 명시적으로 반환할 때 사용 |

---

### 1.2 제곱값을 반환하는 함수

어떤 값 x를 입력받아 x의 제곱을 반환하는 함수이다.

    sq_value <- function(x) {
        x * x
    }

    sq_value(4)

실행 결과:

    [1] 16

해석:

- `x`에 4가 들어감
- `4 * 4`가 계산됨
- 결과는 16

---

### 1.3 거듭제곱값을 반환하는 함수

x와 n을 입력받아 x의 n제곱을 반환하는 함수이다.

    fpower <- function(x, n) {
        x^n
    }

    fpower(3, 2)

실행 결과:

    [1] 9

    fpower(4, 1/2)

실행 결과:

    [1] 2

해석:

- `fpower(3, 2)`는 3^2 = 9
- `fpower(4, 1/2)`는 4^(1/2) = 2

---

### 1.4 여러 개의 power 값을 동시에 반환하는 함수

여러 개의 거듭제곱 결과를 동시에 반환할 때는 `list()`를 사용할 수 있다.

파일명 예:

    powerfun.r

함수 내용:

    power_value <- function(x, n1, n2, n3=5) {
        n1_val = x^n1
        n2_val = x^n2
        n3_val = x^n3
        value = list(v1=n1_val, v2=n2_val, v3=n3_val)
        return(value)
    }

함수 불러오기:

    source("c:/rpgm/powerfun.r")

실행 예:

    power_value(2, 1/2, 2, 3)

실행 결과:

    $v1
    [1] 1.414214

    $v2
    [1] 4

    $v3
    [1] 8

---

### 1.5 기본값이 있는 인수

함수에서 `n3=5`처럼 기본값을 지정할 수 있다.

    power_value <- function(x, n1, n2, n3=5)

이 경우 `n3` 값을 따로 입력하지 않으면 자동으로 5가 사용된다.

실행 예:

    power_value(2, 1/2, 2)

실행 결과:

    $v1
    [1] 1.414214

    $v2
    [1] 4

    $v3
    [1] 32

해석:

- v1 = 2^(1/2) = 1.414214
- v2 = 2^2 = 4
- v3 = 2^5 = 32
- n3를 입력하지 않았으므로 기본값 5가 사용됨

---

## 2. 정규분포

### 2.1 정규분포

정규분포(normal distribution)는 통계에서 가장 중요한 연속형 확률분포 중 하나이다.

R에서는 정규분포와 관련하여 다음 함수를 사용할 수 있다.

| 함수      | 기능              |
|---------|-----------------|
| dnorm() | 정규분포의 밀도값 계산    |
| pnorm() | 정규분포의 누적확률 계산   |
| rnorm() | 정규분포를 따르는 난수 생성 |

---

### 2.2 정규분포 그래프 그리기

표준정규분포의 그래프를 그리는 명령은 다음과 같다.

    plot(function(x) dnorm(x), -3, 3, main="정규분포")

해석:

- `dnorm(x)`는 정규분포의 밀도값을 계산한다.
- `-3, 3`은 x축 범위이다.
- `main="정규분포"`는 그래프 제목이다.

---

### 2.3 누적확률 구하기

`pnorm(x)`는 표준정규분포에서 `Pr(X <= x)` 값을 구한다.

    pnorm(0)

실행 결과:

    [1] 0.5

    pnorm(1)

실행 결과:

    [1] 0.8413447

    pnorm(2)

실행 결과:

    [1] 0.9772499

    pnorm(3)

실행 결과:

    [1] 0.9986501

시험에서는 `pnorm(x)`가 정규분포의 누적확률을 구하는 함수라는 점을 기억한다.

---

### 2.4 정규분포 난수 생성

정규분포를 따르는 난수는 `rnorm()` 함수로 생성한다.

#### 평균 0, 표준편차 1인 정규분포 난수 20개

    rnorm(20)

#### 평균 -5, 표준편차 2.5인 정규분포 난수 100개

    rnorm(100, -5, 2.5)

---

### 2.5 생성한 난수의 평균, 표준편차, 히스토그램

    ran_norm = rnorm(100)
    mean(ran_norm)
    sd(ran_norm)
    hist(ran_norm)

실행 결과 예:

    [1] 0.02829867
    [1] 1.053695

해석:

- `rnorm(100)`은 표준정규분포를 따르는 난수 100개 생성
- `mean()`은 평균 계산
- `sd()`는 표준편차 계산
- `hist()`는 히스토그램 작성

---

## 3. 이산형 그래프 그리기

## 3.1 예제 1: 세 그룹의 기부 자료

세 그룹 C1, C2, C3이 다섯 자선단체 T1~T5에 기부하는 가상자료를 사용한다.

자료 예:

| 구분 |   C1 |   C2 |   C3 |
|----|-----:|-----:|-----:|
| T1 |  5.4 |  3.1 |  3.5 |
| T2 |  5.7 |  8.6 | 25.0 |
| T3 | 20.4 | 26.0 | 22.0 |
| T4 | 36.3 | 34.1 | 28.0 |
| T5 | 14.4 | 11.4 |  4.5 |

---

### 3.2 데이터 읽기

    percData <- read.table("c:/data/dataintro/perc.txt", header=T)
    percData <- as.matrix(percData)

    var_name <- colnames(percData)
    case_name <- rownames(percData)

해석:

- `read.table()`은 텍스트 자료를 읽는다.
- `header=T`는 첫 행을 변수명으로 사용한다는 뜻이다.
- `as.matrix()`는 자료를 행렬로 변환한다.
- `colnames()`는 열 이름을 가져온다.
- `rownames()`는 행 이름을 가져온다.

---

### 3.3 막대그림 그리기

    barplot(percData, names=var_name)
    legend(locator(1), case_name)
    title("Barplot")

해석:

- `barplot()`은 막대그림을 그린다.
- `names=var_name`은 막대 이름을 C1, C2, C3으로 표시한다.
- `legend(locator(1), case_name)`은 사용자가 클릭한 위치에 범례를 표시한다.
- `title()`은 그래프 제목을 넣는다.

---

### 3.4 원그림 그리기

C1 자료에 대한 원그림을 그리는 예이다.

    pie(percData[,1], labels=case_name)
    title("Pie Chart of Company 1")

해석:

- `percData[,1]`은 첫 번째 열, 즉 C1 자료를 의미한다.
- `labels=case_name`은 T1~T5 이름을 표시한다.
- `pie()`는 원그림을 그린다.

---

## 4. 예제 2: 설문조사 자료 그래프

### 4.1 설문자료의 변수

40명을 대상으로 다음 6개 문항을 조사한 자료이다.

| 변수       | 내용                         |
|----------|----------------------------|
| sex      | 성별, 1: 남자, 2: 여자           |
| marriage | 결혼 여부, 1: 미혼, 2: 기혼, 3: 이혼 |
| age      | 나이                         |
| job      | 직업                         |
| edu      | 학력                         |
| salary   | 가족의 월수입                    |

---

### 4.2 교육정도 막대그림

자료 읽기:

    ex8_2 = read.csv("c:/data/dataintro/ex8-2.csv")
    colnames(ex8_2)

실행 결과:

    [1] "sex" "marriage" "age" "job" "edu" "salary"

교육정도 빈도표 작성:

    edu_tb = table(ex8_2$edu)
    edu_tb

실행 결과:

    edu
     1  2  3  4  5
     1  1  3 19 16

행 이름 지정:

    rownames(edu_tb) = c("무학", "초졸", "중졸", "고졸", "대졸")
    edu_tb

실행 결과:

    무학 초졸 중졸 고졸 대졸
      1   1   3  19  16

막대그림:

    barplot(edu_tb)

---

### 4.3 성별 구분 막대그림

성별과 교육정도의 분할표를 만든다.

    EduSex = list(ex8_2$sex, ex8_2$edu)
    EduSex_tb = table(EduSex)
    EduSex_tb

실행 결과:

             1  2  3  4  5
    1        1  1  1 13 11
    2        0  0  2  6  5

행과 열 이름 지정:

    colnames(EduSex_tb) = c("무학", "초졸", "중졸", "고졸", "대졸")
    rownames(EduSex_tb) = c("남성", "여성")
    EduSex_tb

실행 결과:

          무학 초졸 중졸 고졸 대졸
    남성   1   1   1  13  11
    여성   0   0   2   6   5

막대그림:

    barplot(EduSex_tb)

---

### 4.4 성별 구분 원그림

화면을 1행 2열로 나누고 남성과 여성의 교육정도 원그림을 각각 그린다.

    par(mfrow=c(1,2))

    pie(EduSex_tb[1,])
    title("Education of Male")

    pie(EduSex_tb[2,])
    title("Education of Female")

해석:

- `par(mfrow=c(1,2))`는 그래프 창을 1행 2열로 나눈다.
- `EduSex_tb[1,]`은 남성 자료이다.
- `EduSex_tb[2,]`은 여성 자료이다.

---

## 5. 연속형 그래프 그리기

## 5.1 상자그림

세 회사 C1, C2, C3 자료의 상자그림을 그린다.

    boxplot(percData[,1], percData[,2], percData[,3], names=var_name)
    title("Box Plot")

해석:

- `boxplot()`은 상자그림을 그린다.
- 여러 변수의 분포를 비교할 때 유용하다.
- 중앙값, 사분위수, 산포, 특이값을 한눈에 볼 수 있다.

---

## 5.2 줄기-잎 그림 및 히스토그램

자유도가 5인 t-분포를 따르는 난수 50개를 만든 뒤 히스토그램과 줄기-잎 그림을 그린다.

    my_sample <- rt(50, 5)
    hist(my_sample)
    stem(my_sample)

해석:

- `rt(50, 5)`는 자유도 5인 t-분포를 따르는 난수 50개를 생성한다.
- `hist()`는 히스토그램을 그린다.
- `stem()`은 줄기-잎 그림을 그린다.

---

## 5.3 시계열 그림

R 시스템에 내장된 `co2` 데이터를 이용하여 시계열 그림을 그린다.

    co2
    plot(co2)
    lines(smooth(co2), col="BLUE")

해석:

- `co2`는 R에 내장된 시계열 자료이다.
- `plot(co2)`는 시계열 그래프를 그린다.
- `lines(smooth(co2), col="BLUE")`는 부드럽게 처리한 추세선을 파란색 선으로 추가한다.

---

## 5.4 함수 그래프 그리기

수학 함수 그래프를 그리는 예이다.

    x = seq(-30, 30, 0.1)
    y = 2*(x-3)^3 + (x-2)^2 + 4*x - 3
    plot(x, y, type="l")
    abline(h=0, v=0, lty=2)

해석:

- `seq(-30, 30, 0.1)`은 -30부터 30까지 0.1 간격의 수열을 만든다.
- `plot(x, y, type="l")`은 선 그래프를 그린다.
- `abline(h=0, v=0, lty=2)`는 x축과 y축 위치에 점선 기준선을 추가한다.
- `h=0`은 수평선, `v=0`은 수직선이다.
- `lty=2`는 점선 스타일이다.

---

## 5.5 히스토그램 그리기

예제 2 자료에서 변수 `age`의 히스토그램을 그린다.

    ageHist = hist(ex8_2$age, col="BLUE")
    names(ageHist)

실행 결과:

    [1] "breaks" "counts" "density" "mids" "xname" "equidist"

계급 경계값:

    ageHist$breaks

실행 결과:

    [1] 20 25 30 35 40 45 50 55 60

계급별 도수:

    ageHist$counts

실행 결과:

    [1] 11 6 9 1 4 4 2 3

계급 중앙값:

    ageHist$mids

실행 결과:

    [1] 22.5 27.5 32.5 37.5 42.5 47.5 52.5 57.5

해석:

- `hist()`의 결과는 단순 그래프가 아니라 여러 정보를 가진 객체이다.
- `breaks`는 계급 경계값이다.
- `counts`는 각 계급의 도수이다.
- `mids`는 각 계급의 중앙값이다.

---

## 5.6 그룹별 줄기-잎 그림

남녀별로 나이 변수의 줄기-잎 그림을 그린다.

남성:

    stem(ex8_2$age[ex8_2$sex==1])

여성:

    stem(ex8_2$age[ex8_2$sex==2])

해석:

- `ex8_2$sex==1`은 남성 자료만 선택한다.
- `ex8_2$sex==2`는 여성 자료만 선택한다.
- 대괄호 `[]` 안에 조건을 넣어 특정 조건의 자료만 추출한다.

---

### 5.7 back-to-back 줄기-잎 그림

두 집단을 마주 보는 형태로 비교하려면 `aplpack` 패키지를 사용할 수 있다.

    library(aplpack)

    m_age = ex8_2$age[ex8_2$sex==1]
    f_age = ex8_2$age[ex8_2$sex==2]

    stem.leaf.backback(m_age, f_age)

해석:

- `library(aplpack)`은 aplpack 패키지를 불러온다.
- `stem.leaf.backback()`은 두 집단의 줄기-잎 그림을 양쪽으로 비교한다.

---

## 5.8 그룹별 상자그림

남녀별 나이의 상자그림을 그린다.

    boxplot(age ~ sex, data=ex8_2)

해석:

- `age ~ sex`는 sex별 age 분포를 비교한다는 뜻이다.
- `data=ex8_2`는 사용할 자료를 지정한다.
- 그룹별 상자그림은 집단 간 중앙값과 산포를 비교할 때 유용하다.

---

## 5.9 그룹 구분 산점도

남녀별로 구분한 나이와 월수입 산점도를 그린다.

문자 M, F로 구분하는 방식:

    plot(ex8_2$age, ex8_2$salary, type="n")

    points(ex8_2$age[ex8_2$sex==1],
           ex8_2$salary[ex8_2$sex==1],
           pch="M", col=4)

    points(ex8_2$age[ex8_2$sex==2],
           ex8_2$salary[ex8_2$sex==2],
           pch="F", col=2)

    legend("bottomright",
           legend=c("Male", "Female"),
           pch=c("M", "F"),
           col=c("BLUE", "RED"))

점 모양으로 구분하는 방식:

    plot(ex8_2$age, ex8_2$salary, type="n")

    points(ex8_2$age[ex8_2$sex==1],
           ex8_2$salary[ex8_2$sex==1],
           pch=19, col=4)

    points(ex8_2$age[ex8_2$sex==2],
           ex8_2$salary[ex8_2$sex==2],
           pch=17, col=2)

    legend("bottomright",
           legend=c("Male", "Female"),
           pch=c(19, 17),
           col=c(4, 2))

해석:

- `type="n"`은 좌표축만 만들고 점은 찍지 않는다.
- `points()`는 기존 그래프에 점을 추가한다.
- `pch`는 점의 모양이다.
- `col`은 색상이다.
- `legend()`는 범례를 추가한다.

---

## 6. R 알기

### 6.1 R과 S 언어

R은 S 언어의 영향을 받아 만들어졌다.

S language는 Bell Laboratories에서 개발되었다.

주요 기여자는 다음과 같다.

| 구분            | 인물                                         |
|---------------|--------------------------------------------|
| S language 개발 | John Chambers, Richard Becker, Allan Wilks |
| R 최초 개발자      | Robert Gentleman, Ross Ihaka               |
| R 개발 기관       | University of Auckland 통계학과                |

R이라는 이름은 Robert Gentleman과 Ross Ihaka의 이름에서 나온 “R & R”과 관련된다.

---

### 6.2 R 매뉴얼

R에서는 기본 매뉴얼을 제공한다.

대표적인 매뉴얼은 다음과 같다.

| 매뉴얼                   | 설명        |
|-----------------------|-----------|
| An Introduction to R  | R 입문 문서   |
| R Data Import/Export  | 자료 입력과 출력 |
| R Language Definition | R 언어 정의   |
| Writing R Extensions  | R 확장 작성   |

---

### 6.3 R Commander

R Commander는 메뉴 기반으로 R을 사용할 수 있게 해 주는 도구이다.

    library(Rcmdr)

해석:

- `Rcmdr` 패키지를 불러온다.
- 명령어를 직접 입력하는 대신 메뉴를 통해 분석을 수행할 수 있다.

---

### 6.4 R Studio

R Studio는 사용자가 친숙하게 R을 사용할 수 있도록 개발된 통합환경 시스템이다.

| 구분       | 설명                        |
|----------|---------------------------|
| R Studio | R을 쉽게 사용할 수 있도록 만든 통합개발환경 |
| 기능       | 콘솔, 스크립트, 그래프, 파일, 패키지 관리 |
| 다운로드     | www.rstudio.com           |

R Studio를 사용하면 R 콘솔, 변수, 그래프, 파일 등을 한 화면에서 관리할 수 있다.

---

## 정리하기

1. R에서 자주 쓰는 계산은 `function` 문으로 작성하는 것이 좋다.

2. `function(x) { x*x }`처럼 함수를 정의하면 반복 계산을 편리하게 수행할 수 있다.

3. 함수의 인수에는 기본값을 지정할 수 있으며, 예를 들어 `n3=5`처럼 작성할 수 있다.

4. 여러 결과를 반환할 때는 `list()`를 사용할 수 있다.

5. 외부 R 파일에 저장한 함수는 `source()`로 불러올 수 있다.

6. 정규분포 그래프는 `plot(function(x) dnorm(x), -3, 3)`으로 그릴 수 있다.

7. `pnorm()`은 정규분포의 누적확률을 구하는 함수이다.

8. `rnorm()`은 정규분포를 따르는 난수를 생성하는 함수이다.

9. `barplot()`은 막대그림, `pie()`는 원그림을 그릴 때 사용한다.

10. `table()`은 빈도표와 분할표를 만들 때 사용한다.

11. `par(mfrow=c(1,2))`는 그래프 화면을 1행 2열로 나눌 때 사용한다.

12. `boxplot()`은 상자그림을 그리는 함수이다.

13. `rt()`는 t-분포를 따르는 난수를 생성한다.

14. `hist()`는 히스토그램, `stem()`은 줄기-잎 그림을 그린다.

15. `plot()`은 기본 그래프, 시계열 그래프, 산점도 등을 그릴 때 사용한다.

16. `lines()`는 기존 그래프에 선을 추가할 때 사용한다.

17. `abline()`은 그래프에 수평선 또는 수직선을 추가할 때 사용한다.

18. 히스토그램 결과 객체에는 `breaks`, `counts`, `density`, `mids` 등이 포함된다.

19. `stem.leaf.backback()`은 두 집단의 줄기-잎 그림을 마주 보게 그릴 때 사용한다.

20. `boxplot(age ~ sex, data=ex8_2)`는 성별에 따른 나이의 상자그림을 그린다.

21. `points()`는 기존 그래프에 점을 추가하고, `legend()`는 범례를 추가한다.

22. R은 S 언어의 영향을 받아 만들어졌으며, Robert Gentleman과 Ross Ihaka가 처음 개발하였다.

23. R Commander는 메뉴 기반 R 사용 도구이고, R Studio는 R을 쉽게 사용할 수 있도록 개발된 통합환경 시스템이다.

---

## 핵심 요약

### 1. 함수 관련 명령

| 명령         | 기능           |
|------------|--------------|
| function() | 사용자 정의 함수 생성 |
| return()   | 결과 반환        |
| list()     | 여러 결과를 묶어 반환 |
| source()   | 외부 R 파일 불러오기 |

---

### 2. 정규분포 관련 함수

| 함수      | 기능         |
|---------|------------|
| dnorm() | 정규분포 밀도값   |
| pnorm() | 정규분포 누적확률  |
| rnorm() | 정규분포 난수 생성 |
| mean()  | 평균         |
| sd()    | 표준편차       |
| hist()  | 히스토그램      |

---

### 3. 이산형 그래프 함수

| 함수                | 기능        |
|-------------------|-----------|
| table()           | 빈도표, 분할표  |
| barplot()         | 막대그림      |
| pie()             | 원그림       |
| legend()          | 범례 추가     |
| title()           | 제목 추가     |
| par(mfrow=c(r,c)) | 그래프 화면 분할 |

---

### 4. 연속형 그래프 함수

| 함수        | 기능                  |
|-----------|---------------------|
| boxplot() | 상자그림                |
| hist()    | 히스토그램               |
| stem()    | 줄기-잎 그림             |
| plot()    | 기본 그래프, 산점도, 시계열 그림 |
| lines()   | 기존 그래프에 선 추가        |
| abline()  | 기준선 추가              |
| points()  | 점 추가                |
| legend()  | 범례 추가               |

---

### 5. 그래프별 핵심

| 그래프     | 함수               | 활용             |
|---------|------------------|----------------|
| 막대그림    | barplot()        | 이산형 자료, 범주별 비교 |
| 원그림     | pie()            | 범주별 비율         |
| 상자그림    | boxplot()        | 중앙값, 사분위수, 산포  |
| 히스토그램   | hist()           | 연속형 자료 분포      |
| 줄기-잎 그림 | stem()           | 자료값과 분포 형태 확인  |
| 시계열 그림  | plot()           | 시간 흐름 자료       |
| 산점도     | plot(), points() | 두 연속형 변수 관계    |

---

### 6. R 관련 인물과 도구

| 항목          | 내용                                         |
|-------------|--------------------------------------------|
| S language  | John Chambers, Richard Becker, Allan Wilks |
| R 최초 개발     | Robert Gentleman, Ross Ihaka               |
| R 개발 기관     | University of Auckland                     |
| R Commander | library(Rcmdr)                             |
| R Studio    | R 통합환경 시스템                                 |

---

## 연습문제 정리

### Q1. 다음 R 명령의 수행 결과는?

명령:

    sq_value <- function(x) {
        x * x
    }

    sq_value(2)

선택지:

1. 1.414
2. 2
3. 4
4. 8

정답: 3

해설:

`sq_value(2)`는 2의 제곱을 계산한다.

    2 * 2 = 4

따라서 결과는 4이다.

---

### Q2. 다음 R 명령의 수행 결과는?

명령:

    power_value <- function(x, n1, n2, n3=5) {
        n1_val = x^n1
        n2_val = x^n2
        n3_val = x^n3
        value = list(v1=n1_val, v2=n2_val, v3=n3_val)
        return(value)
    }

    a1 = power_value(2, 1/2, 2)
    a1$v1

선택지:

1. 1.414
2. 8
3. 16
4. 32

정답: 1

해설:

`a1$v1`은 `2^(1/2)` 값을 의미한다.

    2^(1/2) = 1.414...

따라서 결과는 약 1.414이다.

---

### Q3. 다음 R 명령의 수행 결과는?

명령:

    power_value <- function(x, n1, n2, n3=5) {
        n1_val = x^n1
        n2_val = x^n2
        n3_val = x^n3
        value = list(v1=n1_val, v2=n2_val, v3=n3_val)
        return(value)
    }

    a1 = power_value(2, 1/2, 2)
    a1$v3

선택지:

1. 1.414
2. 8
3. 16
4. 32

정답: 4

해설:

함수에서 `n3=5`라는 기본값이 지정되어 있다.  
따라서 `a1$v3`은 `2^5`이다.

    2^5 = 32

---

### Q4. 상자그림을 그리는 명령은?

1. stem(ex.data)
2. boxplot(ex.data)
3. box(data)
4. box.plot(ex.data)

정답: 2

해설:

상자그림은 `boxplot()` 함수로 그린다.

    boxplot(ex.data)

---

## 시험 직전 체크포인트

### 반드시 암기하기

- 함수 정의 = `function()`
- 외부 함수 파일 불러오기 = `source()`
- 여러 결과 반환 = `list()`
- 기본 인수값 = `n3=5`
- 정규분포 밀도 = `dnorm()`
- 정규분포 누적확률 = `pnorm()`
- 정규분포 난수 = `rnorm()`
- t-분포 난수 = `rt()`
- 막대그림 = `barplot()`
- 원그림 = `pie()`
- 상자그림 = `boxplot()`
- 히스토그램 = `hist()`
- 줄기-잎 그림 = `stem()`
- 시계열 그림 = `plot(co2)`
- 함수 그래프 = `plot(x, y, type="l")`
- 기준선 추가 = `abline(h=0, v=0, lty=2)`
- 기존 그래프에 점 추가 = `points()`
- 범례 추가 = `legend()`
- 그래프 화면 분할 = `par(mfrow=c(1,2))`
- 그룹별 상자그림 = `boxplot(age ~ sex, data=ex8_2)`
- R 최초 개발자 = Robert Gentleman, Ross Ihaka
- R Studio = R 통합환경 시스템

---

### 객관식에서 자주 나올 표현

| 문제 표현                 | 정답 후보                   |
|-----------------------|-------------------------|
| 자주 쓰는 계산을 함수로 작성      | function                |
| 외부 R 파일 실행            | source                  |
| 여러 결과를 v1, v2, v3로 반환 | list                    |
| 정규분포 누적확률             | pnorm                   |
| 정규분포 난수               | rnorm                   |
| 자유도 5인 t-분포 난수        | rt(50,5)                |
| 이산형 범주 비교             | barplot                 |
| 비율 그래프                | pie                     |
| 연속형 자료 분포             | hist                    |
| 줄기-잎 그림               | stem                    |
| 상자그림                  | boxplot                 |
| 그래프 제목                | title                   |
| 범례                    | legend                  |
| 클릭 위치에 범례             | legend(locator(1), ...) |
| 화면을 1행 2열로 분할         | par(mfrow=c(1,2))       |
| 기존 그래프에 선 추가          | lines                   |
| 기준선 추가                | abline                  |
| 점 추가                  | points                  |
| R Commander 실행        | library(Rcmdr)          |

---

### 헷갈리는 개념 구분

| 개념          | 구분 포인트            |
|-------------|-------------------|
| dnorm       | 밀도값               |
| pnorm       | 누적확률              |
| rnorm       | 정규분포 난수           |
| rt          | t-분포 난수           |
| barplot     | 범주형 자료 막대         |
| pie         | 범주별 비율            |
| hist        | 연속형 자료 계급별 분포     |
| stem        | 실제 자료값과 분포 확인     |
| boxplot     | 중앙값, 사분위수, 이상치 확인 |
| plot        | 기본 그래프, 산점도, 시계열  |
| lines       | 선 추가              |
| points      | 점 추가              |
| abline      | 기준선 추가            |
| table       | 빈도표, 분할표          |
| list        | 여러 객체를 묶음         |
| source      | 외부 R 스크립트 실행      |
| R Commander | 메뉴 기반 R 도구        |
| R Studio    | R 통합개발환경          |

---