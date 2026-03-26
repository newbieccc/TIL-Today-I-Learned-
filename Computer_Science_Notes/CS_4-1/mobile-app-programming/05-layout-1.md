# 모바일앱프로그래밍

## 05. 레이아웃 1

- 컴퓨터과학과 정광식 교수님

---

# (1) ViewGroup 속성

## 1. ViewGroup 개요

### ViewGroup

- 다양한 View에 대한 그룹 관리를 수행하고, 이들이 스마트폰 화면에 어떻게 보여지는지(배치되는지) 결정함
- 계층적 관리 구조를 제공하여 화면 관리의 효율성을 높여줌
- 그룹에 해당되는 위젯과 View를 모아서 관리할 수 있는 쟁반 역할
- 각 View마다 ViewGroup 내부에서 표현되는 구체적인 형태를 지정할 수 있음

## 2. layout_width와 layout_height 속성

### 개요

- View가 레이아웃에 배치될 때 크기를 결정하는 기준이 됨
- 가로 크기를 결정하는 기준인 `layout_width`와 세로 크기를 결정하는 기준인 `layout_height`가 있음
- 각각 독립적으로 동작함

### layout_width와 layout_height 속성

| 속성값            | 설명                                 |
|----------------|------------------------------------|
| `match_parent` | View가 위치한 레이아웃의 크기에 맞춰 최대한의 크기로 출력 |
| `wrap_content` | View가 출력하는 내용물의 크기에 맞춰 최소한의 크기로 출력 |
| 직접 값(literal)  | 입력한 값에 따라 크기가 결정되어 출력              |

### layout_width와 layout_height 값에 따른 TextView의 배치

| layout_width   | layout_height  | 배치 형태                                      |
|----------------|----------------|--------------------------------------------|
| `match_parent` | `wrap_content` | 가로는 부모 레이아웃에 맞게 최대한 넓어지고, 세로는 내용물 크기만큼만 출력 |
| `match_parent` | `match_parent` | 가로와 세로 모두 부모 레이아웃에 맞게 최대한 넓게 출력            |
| `wrap_content` | `wrap_content` | 가로와 세로 모두 내용물 크기만큼만 출력                     |
| `wrap_content` | `match_parent` | 가로는 내용물 크기만큼, 세로는 부모 레이아웃에 맞게 최대한 높게 출력    |

### layout_width와 layout_height 속성 예제

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="New Button"
            android:id="@+id/button1"
            android:padding="20pt" />

        <Button
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="New Button"
            android:id="@+id/button2"
            android:padding="20pt" />
    </LinearLayout>

### layout_width와 layout_height 속성 예제 설명

- **〈프로그램 5.1〉의 실행 결과에서**
    - 첫 번째 버튼의 가로 너비는 부모 레이아웃의 크기값으로 결정되었음
    - 첫 번째 버튼의 세로는 버튼 내부 문자열과 기본 여백의 크기를 합한 크기값으로 결정되었음
    - 두 번째 버튼은 가로/세로 모두 부모 레이아웃의 크기값으로 결정됨

## 3. layout_margin 속성

### 개요

- View와 형제 View 사이의 간격을 지정하는 속성임
- View가 레이아웃에 독립적으로 있을 경우 부모 View 사이의 간격으로 설정됨
- 근처에 형제 View가 있으면 형제 View와의 간격이 됨

### 추가 설명

- 제2장에서 설명한 `padding` 속성과 마찬가지로 `layout_margin` 속성 자체는 4면의 여백을 동일하게 지정함
- 각 변에 개별적인 여백을 지정하고 싶으면 `layout_marginLeft`, `layout_marginRight`, `layout_marginTop`, `layout_marginBottom` 속성을 각각 대입할
  수 있음

## 4. padding과 layout_margin 비교

### 개요

- `padding`과 `layout_margin`은 둘 다 View에 적용되는 여백을 지정하는 속성이며, 목적은 유사하지만 적용되는 위치는 다름
- `layout_margin`은 View와 부모, 또는 형제 View 사이에 적용됨
- `padding`은 View와 내용물(그림, 문자 등) 사이에 적용됨

- **View의 입장에서 볼 때**
    - `layout_margin` 속성은 바깥 여백
    - `padding` 속성은 안쪽 여백

### 추가 설명

- `padding`은 View의 내부에 적용되므로 크기에 포함되지만, `layout_margin`은 그렇지 않다는 점에서 다름
- `padding`은 View 자체 속성이지만 `layout_margin`은 레이아웃 속성임

### padding과 layout_margin 예제 1 설명

- 〈프로그램 5.2〉의 전체 레이아웃은 수직 `LinearLayout`이고, 이 안에 두 개의 `TextView`와 하나의 `LinearLayout`을 중첩하여 배치해 놓았으며, 안쪽 `LinearLayout`에는
  `Button`이 배치되어 있음
- `LinearLayout`도 하나의 View이므로 중첩할 수 있음
- 아래와 위의 `TextView`는 여백을 쉽게 관찰하기 위해 삽입된 것임
- `Button`은 `LinearLayout`의 입장에서 볼 때 내용물에 해당함
- 이때 안쪽 `LinearLayout`을 명확히 확인하려면 각각 배경색을 지정해야 함

### padding과 layout_margin 예제 2 설명

- 안쪽 `LinearLayout`에 `layout_margin`을 20픽셀(pixel) 정도, `padding`을 15dp(density independent pixel)로 지정하는 것이 적당함
- `layout_margin` 속성에 값을 대입하면 네 방향으로 모두 같은 `layout_margin`이 적용됨
- 원하는 방향에 대해서만 `layout_margin`을 지정할 수도 있음

---

# (2) LinearLayout 1

## 1. LinearLayout 개요

### LinearLayout

- LinearLayout은 내부 구성요소를 선형적으로 배치하는 ViewGroup임
- LinearLayout은 상대적으로 정의하는 방식이 단순하고, 구성요소들이 배치되는 결과를 유추하기 쉬움

## 2. orientation 속성

### 개요

- `LinearLayout` 내부에 포함된 View들을 배치하는 방향을 지정하는 속성임
- `LinearLayout`의 선형적 배치 방법으로는 수직 배치와 수평 배치의 두 가지 방향이 있음
- `"vertical"`은 View들을 XML 코드에 정의한 순서로 위에서 아래로 수직 방향으로 배열함
- `"horizontal"`은 왼쪽에서 오른쪽으로 수평 방향으로 배열함
- `orientation` 속성을 별도로 지정하지 않을 경우 기본값으로 `"horizontal"`이 적용되어 수평 방향으로 View를 배치함

### orientation 속성 예제 1

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="horizontal">

        <EditText
            android:id="@+id/edit"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Input Please" />

        <Button
            android:id="@+id/btn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

    </LinearLayout>

### orientation 속성 예제 설명

- 〈프로그램 5.4〉와 〈프로그램 5.5〉의 각각의 소스 코드 6번 줄은 아래와 같음

  android:orientation="horizontal"

  android:orientation="vertical"

- `android:orientation` 속성에 `horizontal`과 `vertical`을 지정하면, 소스 코드 7번 줄과 12번 줄에 선언된 `EditText`와 `Button`이 수평 또는 수직으로 배치된
  것을 확인할 수 있음
- `orientation` 속성을 설정하면 앞서 설명한 것과 같이 XML 코드에 정의된 순서대로 자식 View가 배치됨

## 3. baselineAligned 속성

### 개요

- 수평으로 서로 높이가 다른 다수의 `TextView`를 배치했을 때, `TextView` 아래쪽을 기준으로 텍스트 뷰들을 정렬해 주는 속성임
- 단, `baselineAligned` 속성에서 `TextView`를 정렬할 때 View들이 수평으로 있어야 속성값이 적용되고, 수직 레이아웃에서는 의미가 없는 속성임
- `android:baselineAligned` 속성값의 기본값은 `true`이며 자동적으로 `TextView` 정렬이 적용됨

---

# (3) LinearLayout 2

## 1. gravity 속성

### 개요

- View의 안쪽에 배치되는 `TextView`, `ImageView`와 같은 내용물의 정렬 방식을 결정하는 속성임
- 수평/수직 방향에 대해 정렬 방식을 지정할 수 있으며 `|` 연산자로 두 속성을 묶어서 지정할 수 있음

### 추가 설명

- 각 정렬 방식은 비트 필드(bit field)로 정의되어 있으며, `center` 속성값과 `fill` 속성값은 수평/수직 정렬 상태 플래그(flag)의 조합으로 정의됨
- `gravity` 속성의 기본값은 좌측 상단에 배치되는 것이므로, 뷰가 좌측 상단에 적용됨

### gravity 속성 예제 1 설명

- 〈프로그램 5.7〉은 소스 코드 12번 줄과 같이 `gravity` 속성을 `center`로 설정한 소스 코드임
- 실행 결과와 같이 화면의 중앙에 `TextView`가 출력된 것을 볼 수 있음
- `gravity` 속성의 `center`는 `center_horizontal | center_vertical`과 같으며, 실제로도 그렇게 정의되어 있음을 알 수 있음

## 2. layout_weight 속성

### 개요

- 상위 레이아웃의 영역에서 내부 레이아웃이나 위젯의 영역 할당 비율을 지정하는 속성임
- `layout_weight` 값이 0이면 원래 크기만큼 영역을 차지하고, 1 이상이면 상위 레이아웃에 포함된 레이아웃이나 위젯들이 `layout_weight` 값의 크기에 비례하여 상위 레이아웃의 영역을 차지하게
  됨

### layout_weight 속성 예제 설명

- `layout_weight`를 지정하지 않거나 0일 경우 해당 자식 View는 지정된 높이만큼만 차지하고 영역 분할에는 참여하지 않음
- 중요도가 0인 자식 View는 분할에서 제외되며, 나머지 View들끼리 중요도가 0인 자식 View가 차지하고 있는 영역을 제외한 남은 영역을 중요도에 따라 할당받음

---

## 정리하기

1. **LinearLayout**

- 자식 View를 일렬로 배치하는 레이아웃

2. **layout_width와 layout_height 속성**

- View가 레이아웃에 배치될 때 크기를 결정하는 기준을 정하는 속성

3. **layout_margin 속성**

- View와 형제 View 사이의 간격을 지정하는 속성

4. **orientation 속성**

- LinearLayout 내부에 포함된 View들을 배치하는 방향을 지정하는 속성

5. **baselineAligned 속성**

- 수평으로 서로 높이가 다른 다수의 TextView를 배치했을 때 TextView 아래쪽을 기준으로 텍스트 뷰들을 정렬해 주는 속성

6. **gravity 속성**

- View의 안쪽에 배치되는 TextView, ImageView와 같은 내용물의 정렬 방식을 결정하는 속성

7. **layout_weight 속성**

- 상위 레이아웃의 영역에서 내부 레이아웃이나 위젯의 영역 할당 비율을 지정하는 속성

---

## 확인문제

### 1. LinearLayout 내부에 포함된 View들을 배치하는 방향을 지정하는 속성은 무엇인가?

**정답: ① orientation 속성**

- `orientation` 속성은 LinearLayout 안의 자식 View들을 어느 방향으로 나열할지 결정함
- 속성값으로 `horizontal`(가로 배치), `vertical`(세로 배치)이 있음

- **안드로이드 예시 문법**
  android:orientation="vertical"

- **오답 정리**
    - `layout_margin`
        - 뷰의 바깥 여백(외부 간격)을 설정하는 속성
        - 배치 방향을 결정하지는 않음
        - 예:
          android:layout_margin="16dp"

    - `gravity`
        - 내용물 또는 자식 뷰가 어느 쪽으로 정렬될지 결정하는 속성
        - 나열 방향과는 다름
        - 예:
          android:gravity="center"

    - `layout_weight`
        - 남는 공간을 비율로 분배하는 속성
        - 배치 방향 자체를 정하지는 않음
        - 예:
          android:layout_weight="1"

### 2. 상위 레이아웃의 영역에서 내부 레이아웃이나 위젯의 영역 할당 비율을 지정하는 속성은 무엇인가?

**정답: ④ layout_weight 속성**

- `layout_weight`는 상위 레이아웃(주로 `LinearLayout`)의 남는 공간을 자식 뷰들에게 가중치(비율)로 나눠주는 속성임
- 예를 들어 weight 값이 `1:2:1`이면 남는 공간을 그 비율로 배분함

- **안드로이드 예시 문법**
  android:layout_weight="1"

- **오답 정리**
    - `orientation`
        - 자식 뷰들을 가로 또는 세로 중 어떤 방향으로 배치할지 결정하는 속성
        - 예:
          android:orientation="horizontal"

    - `layout_margin`
        - 뷰의 바깥 여백을 설정하는 속성
        - 예:
          android:layout_marginTop="12dp"

    - `gravity`
        - 뷰 내부의 콘텐츠 또는 자식들의 정렬 위치를 정하는 속성
        - 예:
          android:gravity="right"
