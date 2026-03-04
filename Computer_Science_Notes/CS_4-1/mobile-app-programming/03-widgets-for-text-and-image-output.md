# 모바일앱프로그래밍

## 03. 문자 및 이미지 출력을 위한 위젯

- 컴퓨터과학과 정광식 교수님

---

# (1) TextView

## 1) text 속성

### 개요

- `text` 속성은 **출력할 문자열을 지정**함
- 기본값이 빈 문자열이므로 화면에 문자열 표시를 위해 **필수 속성**
- 단순 지정: `text="xxx"`
- 권장 방식: `strings.xml`에 문자열을 id(name)로 정의하고 필요 시점에 참조
    - 다국어 버전 개발에도 유용

### (예) `strings.xml` 문자열 정의

    <resources>
        <string name="hello_world">Hello world!</string>
    </resources>

### 프로그램 3.2 `strings.xml` 문자열 참조 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world" />
    </LinearLayout>

---

## 2) textColor 속성

### 개요

- `textColor`는 **문자열 색상 지정**
- 색상 코드 형식: `#rrggbb` 또는 `#aarrggbb`
    - `r`=빨강, `g`=초록, `b`=파랑(각 색의 강도)
    - `a`=알파값(투명도)

### 프로그램 3.3 문자열에 색상을 적용 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world"
            android:textColor="#ff405aff" />
    </LinearLayout>

---

## 3) textSize 속성

### 개요

- `textSize`는 **문자열 폰트 크기 지정**
- 숫자 뒤에 단위 필요: `sp`, `dp`, `px`, `in`, `mm`
- 텍스트 크기는 보통 **가변적인 `sp` 사용이 합리적**
    - (강의 예제는 `dp`로 작성되어 있음)

### 프로그램 3.5 글자 크기 변경 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world"
            android:textSize="50dp" />
    </LinearLayout>

---

## 4) textStyle 속성

### 개요

- `textStyle`은 **폰트 스타일 지정**
- `normal`, `bold`, `italic` 중 선택
- `|`로 여러 값 동시 지정 가능(공백 없이): `bold|italic`

### 프로그램 3.8 bold + italic 적용 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world"
            android:textSize="35dp"
            android:textStyle="bold|italic" />
    </LinearLayout>

---

## 5) typeface 속성

### 개요

- `typeface`는 **글꼴 모양 지정**
- 안드로이드는 기본 내장 폰트 개수에 제약이 있어 선택지가 제한됨
- `normal`, `sans`, `serif`, `monospace` 중 **하나만 지정**

### 프로그램 3.9 `serif` 적용 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world"
            android:textSize="35dp"
            android:typeface="serif" />
    </LinearLayout>

---

## 6) singleLine 속성

### 개요

- 문자열이 위젯 폭보다 길 때 **한 줄로 출력**하도록 하는 속성
- 폭을 넘는 부분은 `...`로 생략되어 출력
- 기본값은 `false`
    - `false`면 다음 줄로 이어서 출력

### 프로그램 3.11 singleLine 적용 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/hello_world"
            android:textSize="35dp"
            android:singleLine="true"
            android:width="100dp" />
    </LinearLayout>

---

## 7) TextView 프로젝트

### 개요

- TextView 프로젝트 소스 코드를 통해 화면에 문자열을 출력하는 흐름을 확인
- `MainActivity.java`는 기본 생성 파일을 활용

### 프로그램 3.12 문자열 리소스 예제 (`strings.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string name="app_name">helloworld</string>
        <string name="action_settings">Settings</string>
        <string name="hello_world">Hello world!</string>
        <string name="welcome">Welcome to KOREA!!!</string>
        <string name="android">Start! Android Programming!</string>
    </resources>

### 문자열 코드 수정 요약

- 기본 `"Hello world!"` 외에 아래 2개 문자열을 추가로 생성
    - `welcome` → `"Welcome to KOREA!!!"`
    - `android` → `"Start! Android Programming!"`

---

# (2) ImageView

## 1) ImageView 개요

- 화면에 그림을 보여 주는 위젯(아이콘/비트맵 출력 가능)
- 다양한 속성으로 같은 이미지에 여러 효과를 적용 가능

---

## 2) src 속성

### 개요

- `src`는 **출력할 이미지를 지정**
- 값을 지정하지 않으면 아무것도 보이지 않으므로 ImageView 사용 시 **필수**
- `#rrggbb` 형태 색상 코드 또는 외부 이미지 지정 가능

### src로 이미지 출력 방식

- 보통 `res` 폴더에 이미지를 넣고 `@drawable/ID` 형식으로 참조
- 예제에서는 `@mipmap/ic_launcher` 사용
    - `drawable`: 이미지 관리 폴더
    - `mipmap`: `ic_launcher` 아이콘 저장 폴더

### 프로그램 3.14 src 적용 예제 (`activity_main.xml`)

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <ImageView
            android:id="@+id/imageView1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@mipmap/ic_launcher"
            android:visibility="visible" />
    </LinearLayout>

---

## 3) 이미지 포맷

- 공식 지원 포맷: `jpg`, `png`, `gif` 등
- `png`는 알파 채널(투명도) 지원 → 실용성 높음
- 다양한 해상도 기기 대응을 위해 OS가 적절한 리소스를 자동 선택해 출력

---

## 4) maxWidth, maxHeight / minWidth, minHeight

### 개요

- `maxWidth`, `maxHeight`: 화면에 표현되는 이미지 가로/세로 **최대값**
- `minWidth`, `minHeight`: 화면에 표현되는 이미지 가로/세로 **최소값**

### 프로그램 3.15 maxWidth/maxHeight 예제 (`activity_main.xml`)

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:src="@drawable/banana"
            android:maxWidth="100pt"
            android:maxHeight="100pt"
            android:adjustViewBounds="true" />

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:src="@drawable/banana"
            android:maxWidth="50pt"
            android:maxHeight="50pt"
            android:adjustViewBounds="true" />
    </LinearLayout>

---

## 5) adjustViewBounds 속성

### 개요

- 이미지의 **종횡비(비율)**를 맞추기 위해 ImageView 크기 제한을 지정
- 값: `true` / `false`
    - `true`: 활성화
    - `false`: 비활성화

### 프로그램 3.16 설명 요약

- `false`: 이미지가 가로·세로 모두 화면 전체를 채우게 됨
- `true`: 원본 종횡비 유지 + `maxWidth`, `maxHeight`에 맞춰 크기가 적응적으로 결정됨

---

## 6) cropToPadding 속성

### 개요

- ImageView 크기가 `maxWidth/maxHeight`로 결정된 상태에서,
    - 레이아웃 `padding`에 따라 이미지 일부가 잘리는지 여부를 지정
- 값: `true` / `false`

### 속성값 의미

- `true`: padding이 ImageView 영역까지 포함되면 겹치는 부분을 잘라 **일부만 표시**
- `false`: padding이 ImageView 영역에는 무력화되어 **원본이 보임**

---

## 7) scaleType 속성

### 개요

- 원본 이미지는 해상도/비율 때문에 원하는 형태로 항상 배치되지 않음
- ImageView는 크기 조정 기준을 지정하는 `scaleType` 제공
- 예: `matrix`, `fitXY`, `center`, `centerCrop` 등

---

## 8) ImageView 프로젝트

### 이미지 리소스 ID

- 이미지를 `res` 폴더에 추가하면 AAPT가 파일을 찾아 **`R.java(R.class)`에 ID 자동 등록**
- 리소스 ID는 **파일 이름 기반**이라 임의 변경 불가
- 파일명 규칙: 알파벳 소문자, `_`만 허용(공백/특수문자 불가)
- 파일명으로 ID가 생성되므로 **같은 이름의 이미지 파일은 넣을 수 없음**
- 위 주의점을 제외하면 다른 리소스와 동일하게 사용

### 실행 결과 요약

- 1번째 ImageView: `layout_height` < `maxHeight` → 세로 100dp 출력
- 2번째 ImageView: `maxWidth/maxHeight`가 더 작음 → 가로/세로 50dp 출력
- 3번째 ImageView: 종횡비 유지 + 부모 레이아웃 크기 채움 형태로 출력

---

# 정리하기

1. **TextView**: 화면에 텍스트를 출력하는 위젯
2. **TextView의 다양한 속성**: `text`, `textColor`, `textSize`, `textStyle`, `typeface`, `singleLine`
3. **ImageView**: 화면에 아이콘이나 비트맵을 출력하는 위젯
4. **ImageView의 다양한 속성**: `src`, `maxWidth`, `maxHeight`, `minWidth`, `minHeight`, `adjustViewBounds`, `cropToPadding`,
   `scaleType`
5. **위젯**: 운영체제 위 응용 프로그램의 결과를 화면에 표시하는 작은 GUI 도구