# 모바일앱프로그래밍

## 07. 레이아웃 3

- 컴퓨터과학과 정광식 교수님

---

# 1. TableLayout

## TableLayout 개요

### TableLayout

- 표 형태로 자식 View를 배치하는 레이아웃임
- 표 형식이므로 행과 열의 구분이 필요함
- 여러 개의 `TableRow` 객체로 구성됨
- `TableRow` 객체 하나가 하나의 행에 해당됨
- `TableRow` 내부는 여러 개의 열로 구성되며, 하나의 열을 셀(cell)이라고 부름

### 구조적 특징

- 여러 개의 행이 쌓여서 하나의 표 형태를 이룸
- 하나의 행에는 여러 개의 열(셀)이 존재함
- 열(셀) 하나에는 하나의 자식 View가 포함됨
- `TableRow` 개수가 곧 행의 개수임
- 하나의 `TableRow` 안에 배치되는 자식 View의 개수가 열(셀)의 개수가 됨
- 따라서 `TableLayout`의 전체 크기는 `행 X 열`로 계산됨

## 자식 View 구성

### 개요

- 여러 개의 행이 하나의 `TableLayout`에 배치되려면 적응적으로 세로 크기가 조정되어야 함
- 이에 따라 `TableRow`의 높이는 `wrap_content`로 설정해야 함
- 하나의 칸에 배치되는 자식 View는 주어진 셀 안에 배치되므로 `layout_width` 속성은 `wrap_content`를 기본값으로 가짐
- 자식 View의 높이는 기본 속성값으로 `wrap_content`로 설정되지만, 필요한 경우 `match_parent`로 지정하여 하나의 셀로 행을 채울 수도 있음

## TableLayout 예제 1

### TableLayout 예제 1 (`activity_main.xml`)

- `TableLayout`을 루트 레이아웃으로 사용
- `android:layout_width`, `android:layout_height`는 `match_parent`로 설정
- 내부에 `TableRow`를 배치하여 행 단위로 자식 View를 구성

### 예제 코드

    <TableLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TableRow>
            <TextView
                android:text="SUN"
                android:textSize="50px"
                android:padding="5dip"
                android:textColor="#FF0000" />

            <TextView
                android:text="MON"
                android:textSize="50px"
                android:padding="5dip" />
        </TableRow>

### 예제 설명

- 화면에 보이는 부분 기준으로 정리함
- `TableLayout` 안에 `TableRow`가 들어가고, 그 안에 `TextView`들이 셀 단위로 배치됨
- 현재 스크린샷에서는 일부 코드만 보여서 보이는 부분만 작성함

## TableLayout 예제 1 설명

- (프로그램 7.1)은 `TableLayout` 안에 두 개의 `TableRow`를 배치하고, 각 `TableRow` 안에 세 개의 `TextView`를 배치하는 예제임
- 행과 열의 개수에는 특별한 제한이 없음

### 행과 열 늘리기

- 행의 개수를 늘리려면 아래쪽에 `TableRow`를 하나 더 정의
- 열의 개수를 늘리려면 `TableRow` 안의 `TextView`를 하나 더 정의

## shrinkColumns, stretchColumns 속성

### 개요

- 특정 열의 크기를 축소하거나 확장하는 속성임
- `shrinkColumns` 속성은 `축소 가능`을 의미하며, 부모 폭에 맞추기 위해 열의 폭을 강제로 축소함
- `stretchColumns` 속성은 `확장 가능`을 의미하며, 부모 View의 남는 여백을 채우기 위해 열의 폭을 임의로 확장할 수 있음
- 두 속성의 속성값으로는 열 번호를 입력하며, 열 번호는 가장 왼쪽의 첫 번째 열이 `0`이고 오른쪽으로 갈수록 1씩 증가함

## stretchColumns 예제

### stretchColumns 예제 (`activity_main.xml`)

- `TableLayout`에 `android:stretchColumns="1"` 속성을 지정한 예제임

### 예제 코드

    <TableLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:stretchColumns="1">
        ...
    </TableLayout>

### 예제 설명

- 열 번호 `1`인 열을 확장 가능하도록 설정
- 남는 여백이 있을 경우 해당 열이 확장되어 부모 View의 공간을 채움

## stretchColumns 예제 설명

- (프로그램 7.3)은 `TableLayout`의 자식 View 구성이 (프로그램 7.1)과 동일한 소스 코드에서 `TableLayout`의 `stretchColumns` 속성을 `"1"`로 지정함
- 실행 결과 열 번호 `1`번에 해당하는 두 번째 열의 너비가 부모 View의 공간을 채울 때까지 늘어난 형태로 출력됨

## shrinkColumns 예제 설명

- (프로그램 7.4)는 `TableLayout` 자식 View 구성이 (프로그램 7.1)과 동일한 소스 코드에서 모든 `TextView`의 `textSize` 속성을 `"100px"`로 변경하여 너비를 확장함
- `TableLayout`을 대상으로 5번 줄의 `shrinkColumns` 속성을 `"1,2"`로 지정함
- 실행 결과 `shrinkColumns` 속성으로 인하여 두 번째와 세 번째 열의 너비가 부모 View의 공간 안에 맞추어 축소됨

---

# 2. 레이아웃 중첩

## 레이아웃과 레이아웃 중첩

### 개요

- 레이아웃은 View들을 담는 하나의 컨테이너(쟁반)이며, View로부터 파생된 모든 `ViewGroup`과 `View`를 레이아웃 안에 포함할 수 있음
- 레이아웃 내에 자식 View로 포함하는 `ViewGroup`에 다른 View들을 중첩하여 배치할 수도 있음

## 레이아웃 중첩 예제

### 레이아웃 중첩을 적용한 예제 설명

- (프로그램 7.5)의 경우 전체 레이아웃은 `LinearLayout`이며 `orientation` 속성이 `vertical`로 선언되어 있으므로 자식 View들이 가장 넓은 레이아웃인 `LinearLayout`
  안에서 수직으로 배치됨
- 가장 밖에 위치한 `LinearLayout` 안에는 `TextView`, `TableLayout`, `LinearLayout`이 자식 View로 배치됨
- 즉, 하나의 위젯과 두 개의 레이아웃이 중첩되어 있음

### 레이아웃 중첩을 적용한 예제 결과 설명

- (프로그램 7.5)에서 `TableLayout`은 다시 `2행 3열`의 셀로 분할되고 각 셀에는 `TextView`가 들어 있음
- 수평 `LinearLayout` 안에는 세 개의 `TextView`가 배치되어 있음

---

# 3. 실행 중 속성 바꾸기

## 실행 중 속성 바꾸기

### 개요

- 안드로이드 앱 실행 중 특정 View의 속성값을 변경하는 방법
- 실시간으로 변경되는 속성은 동적인 화면 구성을 제공함
- 기본적으로 `set` 계열(`set + 속성이름`)의 함수를 이용함

## TextView 속성 변경 예제

### 개요

- `TextView`의 속성과 관련된 메소드는 `setText`, `setTextColor`, `setTextSize` 등이 있음
- `setText` 메소드는 인수로 문자열을 받기도 하고 리소스 ID를 받기도 하므로 문자열 정보를 가진 객체라면 어떤 것이든지 전달할 수 있음
- 버튼을 클릭할 때 `TextView`의 글자 크기가 변경되는 속성을 적용한 예제임

## 실행 중 TextView 속성 변경을 위한 화면 예제

### 실행 중 TextView 속성 변경을 위한 화면 예제 (`activity_main.xml`)

- `LinearLayout`을 루트 레이아웃으로 사용
- `orientation`은 `vertical`로 설정
- `TextView`의 `id`는 `@+id/textid`로 지정
- `textSize`는 `20dp`로 설정
- 아래에 버튼을 추가하여 실행 중 속성 변경이 가능하도록 구성한 예제임

### 예제 코드

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/textid"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="CodeLayout Example Test!!"
            android:textSize="20dp" />

        <Button
            android:id="@+id/buttonid"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="BUTTON" />

    </LinearLayout>

### 예제 설명

- 화면에 보이는 부분 기준으로 정리함
- 버튼을 클릭했을 때 `TextView`의 속성을 변경하는 예제 화면으로 보임
- 스크린샷에 보이는 코드 기준으로만 작성함

## 실행 중 TextView 속성 변경을 위한 화면 예제 설명

- (프로그램 7.6)은 수직 `LinearLayout` 안에 `TextView`, `ImageView`, `Button`을 배치하고, 이들에 대한 속성값(`textSize`)을 변경하고 있음
- 예제에서는 각 위젯의 `id`를 `textid`, `buttonid`로 이름을 정의함
- XML 문서에 지정한 ID는 `R.java` 파일에 자동으로 등록됨
- JAVA 코드에서 속성을 변경하는 메소드를 호출해 실행 직후 위젯들의 속성을 변경하게 됨

## 실행 중 TextView 속성 변경 예제 (`MainActivity.java`)

### 예제 코드

    public class MainActivity extends Activity {
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            setContentView(R.layout.activity_main);

            findViewById(R.id.buttonid).setOnClickListener(new View.OnClickListener() {
                public void onClick(View v) {
                    TextView txt = (TextView) findViewById(R.id.textid);
                    txt.setTextSize(40);
                }
            });
        }
    }

### 예제 설명

- 버튼 `buttonid`에 클릭 리스너를 연결
- 클릭 시 `textid`에 해당하는 `TextView`를 찾아 `setTextSize(40)`으로 글자 크기를 변경함
- 화면에 보이는 부분 기준으로 정리함

## 버튼을 클릭했을 때 글자 크기 변경 예제 결과 설명

- (프로그램 7.7)의 `MainActivity` 내부에서 `"buttonid"`라는 ID 속성값을 통해 `Button`을 찾고 `setOnClickListener` 메소드를 통해 이벤트 핸들러를 등록함
- 버튼을 클릭하면 핸들러 내부의 `onClick` 함수가 실행되고 `"textid"`라는 ID 속성값을 가진 `TextView`를 찾아 글자 크기를 크게 하는 작업을 수행함

## ImageView 속성 변경 예제

### 실행 중 ImageView 속성 변경을 위한 화면 예제 설명

- `setColorFilter` 메소드를 이용하여 버튼을 클릭할 때 `ImageView`의 이미지 색이 바뀌는 예제를 설명함
- (프로그램 7.8)의 수직 `LinearLayout` 안에 `ImageView`와 `Button`이 구성되어 있음

### 실행 중 ImageView 속성 변경을 위한 화면 예제 (`MainActivity.java`) 설명

- (프로그램 7.9)의 `MainActivity` 내부에서 `"buttonid"`라는 ID 속성값을 통해 `Button`을 찾고 `setOnClickListener` 메소드를 통해 이벤트 핸들러를 등록함
- 버튼을 클릭하면 핸들러 내부의 `onClick` 함수가 실행되고 `"imageid"`라는 ID 속성값을 가진 `ImageView`를 찾아 이미지 색을 변경하는 작업을 수행함

---

#### 정리하기

1. TableLayout
    - `TableRow`를 사용하여 행과 열로 자식 View를 정렬하는 레이아웃

2. TableRow
    - `TableLayout`의 행을 정의하는 객체

3. 컨테이너
    - 다른 View들을 포함하고 있거나 포함할 수 있는 View

4. 파생 클래스
    - 기본 클래스에서 메소드를 상속하지만 상속된 속성이나 메소드가 다르게 동작해야 하는 경우 재정의하는 클래스

---

#### 연습문제

### 문제 1. TableLayout에 대한 설명으로 옳은 것은?

### 정답

- 표 형식으로 자식 View를 배치하는 레이아웃이다.

### 이유

- `TableLayout`은 자식들을 행(Row)과 열(Column) 구조로 배치하는 레이아웃이다.
- 실제 구성은 `TableLayout` 안에 여러 개의 `TableRow`를 두고, 각 `TableRow` 안에 `View`들을 넣어 표처럼 보이게 만든다.

### 안드로이드 예시 문법

    <TableLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TableRow>
            <TextView android:text="A" />
            <TextView android:text="B" />
        </TableRow>

    </TableLayout>

### 오답 정리

- `셀 자체에 여러 개의 자식 View가 들어간다`
    - 일반 설명으로는 부정확함
    - 하나의 셀 위치에 여러 View를 넣고 싶다면 `LinearLayout` 같은 `ViewGroup`을 넣고, 그 안에 다시 여러 View를 배치해야 함

- `TableRow는 열(Column)이다`
    - 틀림
    - `TableRow`는 행(Row)임

- `TableRow 안에 배치되는 것은 행이다`
    - 틀림
    - `TableRow` 안에는 열에 해당하는 `View`들이 배치됨

---

### 문제 2. 레이아웃의 중첩에 대한 설명으로 옳은 것은?

### 정답

- 레이아웃은 View의 컨테이너이므로 View로부터 파생된 모든 `ViewGroup`과 위젯을 레이아웃 안에 중첩하여 배치할 수 있다.

### 이유

- 레이아웃은 보통 `ViewGroup`이며, 다른 View를 자식으로 포함할 수 있다.
- 따라서 다른 레이아웃(`ViewGroup`)도 넣을 수 있고, 버튼이나 텍스트뷰 같은 위젯도 함께 배치할 수 있다.
- 즉, 레이아웃끼리 중첩 배치하는 것이 가능하다.

### 안드로이드 예시 문법

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView android:text="제목" />

        <TableLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">
        </TableLayout>

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="horizontal">
        </LinearLayout>

    </LinearLayout>

### 오답 정리

- `레이아웃은 View 계열이므로 중첩이 불가능하다`
    - 틀림
    - 레이아웃은 보통 `ViewGroup`이므로 자식 View를 포함할 수 있음

- `orientation은 중첩 레이아웃에 적용되지 않는다`
    - 틀림
    - 부모 `LinearLayout`의 `orientation`은 부모의 자식 배치 방향에 영향을 주며, 중첩된 레이아웃 내부 배치는 그 레이아웃 자신의 속성에 따라 결정됨

- `setOrientation()`은 중첩 구조에서 의미가 없다`
    - 틀림
    - 중첩 구조에서도 정상적으로 자식 배치 방향을 결정함

