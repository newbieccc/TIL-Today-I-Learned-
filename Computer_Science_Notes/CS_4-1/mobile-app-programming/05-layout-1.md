# 모바일앱프로그래밍

## 05. 레이아웃 1

- 컴퓨터과학과 정광식 교수님

---

# (1). ViewGroup 속성

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

## 2. layout_width와 layout_height 속성

### layout_width와 layout_height 속성

| 속성값            | 설명                                 |
|----------------|------------------------------------|
| `match_parent` | View가 위치한 레이아웃의 크기에 맞춰 최대한의 크기로 출력 |
| `wrap_content` | View가 출력하는 내용물의 크기에 맞춰 최소한의 크기로 출력 |
| 직접 값(literal)  | 입력한 값에 따라 크기가 결정되어 출력              |

## 2. layout_width와 layout_height 속성

### layout_width와 layout_height 값에 따른 TextView의 배치

| layout_width   | layout_height  | 배치 형태                                      |
|----------------|----------------|--------------------------------------------|
| `match_parent` | `wrap_content` | 가로는 부모 레이아웃에 맞게 최대한 넓어지고, 세로는 내용물 크기만큼만 출력 |
| `match_parent` | `match_parent` | 가로와 세로 모두 부모 레이아웃에 맞게 최대한 넓게 출력            |
| `wrap_content` | `wrap_content` | 가로와 세로 모두 내용물 크기만큼만 출력                     |
| `wrap_content` | `match_parent` | 가로는 내용물 크기만큼, 세로는 부모 레이아웃에 맞게 최대한 높게 출력    |

## 2. layout_width와 layout_height 속성

### layout_width와 layout_height 속성 예제

```xml
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
            android:padding="20pt"/>

    <Button
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="New Button"
            android:id="@+id/button2"
            android:padding="20pt"/>
</LinearLayout>
```

## 2. layout_width와 layout_height 속성

### layout_width와 layout_height 속성 예제 설명

- **〈프로그램 5.1〉의 실행 결과에서**
    - 첫 번째 버튼의 가로 너비는 부모 레이아웃의 크기값으로 결정되었음
    - 첫 번째 버튼의 세로는 버튼 내부 문자열과 기본 여백의 크기를 합한 크기값으로 결정되었음
    - 두 번째 버튼은 가로/세로 모두 부모 레이아웃의 크기값으로 결정됨

## 2. layout_width와 layout_height 속성

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

## 3. layout_margin 속성

### 개요

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

# (2). LinearLayout 1

# (3). LinearLayout 2

