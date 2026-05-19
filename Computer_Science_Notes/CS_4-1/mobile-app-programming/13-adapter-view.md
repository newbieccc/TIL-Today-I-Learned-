# 모바일 앱 프로그래밍

## 13. 어댑터 뷰

### 강의 목차

1. AdapterView
2. ListView
3. Spinner

---

## 1. AdapterView

### 1.1 AdapterView의 개요

AdapterView는 자료구조 또는 데이터베이스에 저장된 데이터를 활용하여 위젯을 구성하는 View이다.

XML 형태의 레이아웃 파일을 참조하여 위젯의 데이터 구조와 표현 방법을 결정한다.

| 개념          | 설명                                          |
|-------------|---------------------------------------------|
| AdapterView | 여러 항목을 가진 자식 View를 표현하고 사용자 상호작용을 처리하는 View |
| 데이터 원본      | ArrayList, 배열, 데이터베이스 등                     |
| 화면 표현       | XML 레이아웃을 기반으로 구성                           |
| 대표 위젯       | ListView, Spinner                           |

---

### 1.2 AdapterView 동작 과정

AdapterView는 직접 데이터를 가지고 화면을 구성하는 것이 아니라, Adapter를 통해 데이터를 공급받는다.

동작 흐름은 다음과 같다.

1. ArrayList 또는 데이터베이스에서 데이터 준비
2. Adapter가 데이터를 수집
3. Adapter가 데이터에 맞는 View 구성요소 생성
4. AdapterView가 Adapter에서 받은 View를 화면에 출력
5. 사용자의 터치, 선택, 스크롤 등 상호작용 처리

흐름 요약:

    데이터 원본
    → Adapter
    → View 구성요소 생성
    → AdapterView(ListView, Spinner)
    → 화면 출력 및 사용자 상호작용 처리

---

## 2. Adapter

### 2.1 Adapter의 역할

Adapter는 화면에 표시되는 AdapterView를 위해 데이터를 관리하는 역할을 한다.

| 구분      | 설명                                 |
|---------|------------------------------------|
| Adapter | 화면에 표시될 데이터를 관리                    |
| 역할      | 데이터 원본과 UI 사이를 연결                  |
| 대상      | ListView, Spinner 등                |
| 특징      | 전달받은 데이터 유형에 따라 여러 하위 Adapter로 세분화 |

---

### 2.2 Adapter 하위 계층

Adapter는 전달받는 데이터와 사용 목적에 따라 여러 종류로 나뉜다.

| 계층              | 예                          |
|-----------------|----------------------------|
| Adapter         | 최상위 Adapter                |
| ListAdapter     | ListView 계열에 사용            |
| SpinnerAdapter  | Spinner 계열에 사용             |
| BaseAdapter     | Adapter 구현의 기반 클래스         |
| ArrayAdapter<T> | 배열, ArrayList 등 배열형 자료에 사용 |
| CursorAdapter   | 데이터베이스 Cursor 자료에 사용       |
| SimpleAdapter   | Map 형태 자료를 간단히 연결할 때 사용    |

---

### 2.3 ArrayAdapter 초기화

JAVA 코드에서 배열 자료구조를 표현하는 ArrayList를 이용할 때는 ArrayAdapter를 사용할 수 있다.

ArrayAdapter의 기본 생성 형식은 다음과 같다.

    ArrayAdapter(Context context, int textViewResourceId, List<T> objects)

또는

    ArrayAdapter(Context context, int textViewResourceId, T[] objects)

매개변수 의미:

| 매개변수               | 설명                                            |
|--------------------|-----------------------------------------------|
| context            | AdapterView를 출력할 Activity의 Context, 보통 `this` |
| textViewResourceId | 아이템을 표현하는 레이아웃 리소스 ID                         |
| objects            | Adapter에 입력으로 전달되는 데이터 객체                     |

예:

    Adapter = new ArrayAdapter<String>(
        this,
        android.R.layout.simple_list_item_checked,
        arGeneral
    );

---

## 3. ListView

### 3.1 ListView의 개요

ListView는 여러 개의 항목을 수직으로 표시하는 위젯이다.

주소록, 회원 명단처럼 다수의 항목을 출력해야 할 때 사용된다.

| 특징    | 설명                        |
|-------|---------------------------|
| 표시 방향 | 수직 방향                     |
| 스크롤   | 수직 스크롤 지원                 |
| 항목 수  | 표시 항목 개수에 제한 없음           |
| 활용    | 주소록, 설정 목록, 회원 명단, 메뉴 목록  |
| 장점    | 작은 화면에서 많은 자료를 스크롤로 표시 가능 |

---

### 3.2 ListView의 item

item은 ListView에서 하나의 행을 구성하는 항목이다.

ListView의 item은 레이아웃을 통해 다양한 형태로 구성될 수 있다.

| item 구성     | 설명             |
|-------------|----------------|
| 문자열만 표시     | 간단한 목록         |
| 이미지 표시      | 아이콘 목록         |
| 문자열 + 이미지   | 복합 목록          |
| 직접 정의한 레이아웃 | 복잡한 행 UI 구성 가능 |

---

## 4. ListView 예제

### 4.1 activity_main.xml

ListView를 사용하기 위해 화면 XML에 ListView를 배치한다.

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ListView
            android:id="@+id/list"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

    </LinearLayout>

핵심:

- 최상위 LinearLayout 안에 ListView 1개가 구성된다.
- ListView의 내용은 JAVA 코드에서 Adapter를 통해 채워진다.

---

### 4.2 MainActivity.java: ArrayList 데이터 사용

ListView에 표시할 문자열 데이터를 ArrayList에 저장한 뒤 Adapter와 연결한다.

    public class MainActivity extends Activity {

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            ArrayList<String> arGeneral = new ArrayList<String>();

            arGeneral.add("APPLE");
            arGeneral.add("BANANA");
            arGeneral.add("ORANGE");
            arGeneral.add("MANGO");

            ArrayAdapter<String> Adapter;

            Adapter = new ArrayAdapter<String>(
                this,
                android.R.layout.simple_list_item_checked,
                arGeneral
            );

            ListView list = (ListView) findViewById(R.id.list);

            list.setAdapter(Adapter);
        }
    }

---

### 4.3 코드 해석

| 코드                            | 의미                             |
|-------------------------------|--------------------------------|
| `ArrayList<String> arGeneral` | ListView에 표시할 데이터를 보관하는 객체 생성  |
| `arGeneral.add()`             | 문자열 항목 추가                      |
| `ArrayAdapter<String>`        | 문자열 데이터를 ListView에 연결할 Adapter |
| `simple_list_item_checked`    | 오른쪽에 체크 표시가 나타나는 기본 레이아웃       |
| `findViewById(R.id.list)`     | XML의 ListView 객체 참조            |
| `list.setAdapter(Adapter)`    | ListView와 Adapter 연결           |

---

### 4.4 ListView의 기본 레이아웃

안드로이드 시스템은 ListView에서 사용할 수 있는 기본 레이아웃을 제공한다.

| 리소스 ID                             | 설명                          |
|------------------------------------|-----------------------------|
| `simple_list_item_1`               | 하나의 TextView로 구성된 레이아웃      |
| `simple_list_item_2`               | 두 개의 TextView로 구성된 레이아웃     |
| `simple_list_item_checked`         | 오른쪽에 체크 표시가 나타남             |
| `simple_list_item_single_choice`   | 오른쪽에 라디오 버튼이 나타남            |
| `simple_list_item_multiple_choice` | 오른쪽에 여러 개 선택 가능한 체크 버튼이 나타남 |

시험에서는 `simple_list_item_checked`, `simple_list_item_single_choice`, `simple_list_item_multiple_choice`의 차이를 구분해야 한다.

---

## 5. setAdapter 메소드

### 5.1 setAdapter의 역할

Adapter 객체가 준비되면 ListView의 `setAdapter()` 메소드를 호출하여 데이터와 ViewGroup을 연결해야 한다.

    list.setAdapter(Adapter);

---

### 5.2 setAdapter 동작

| 구성요소     | 역할                            |
|----------|-------------------------------|
| Adapter  | 데이터 원본을 기반으로 출력할 View 구성요소 생성 |
| ListView | Adapter가 제공한 View를 사용자에게 표시   |
| 사용자 입력   | 터치 입력, 항목 선택, 스크롤 기능 처리       |

핵심 흐름:

    Adapter 생성
    → ListView 찾기
    → setAdapter 호출
    → 데이터가 화면에 출력됨

---

## 6. 리소스에서 데이터 참조

### 6.1 배열 리소스 정의

안드로이드 앱 화면에 출력할 문자열 배열은 일종의 리소스이다.

고정적인 문자열이라면 Java 코드의 컬렉션이나 배열에 직접 넣는 것보다 XML 코드에 정의해 두고 사용하는 것이 바람직하다.

배열 리소스는 `values` 폴더의 `arrays.xml` 파일에 작성한다.

---

### 6.2 arrays.xml 예제

문자열 배열은 `string-array` 엘리먼트를 사용하여 작성한다.

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string-array name="mobile">
            <item>Application</item>
            <item>Activity</item>
            <item>Intent</item>
            <item>Layout</item>
            <item>Linear</item>
            <item>Relative</item>
            <item>Absolute</item>
            <item>Life Cycle</item>
            <item>Inflation</item>
            <item>View</item>
            <item>Permission</item>
            <item>Widget</item>
            <item>Preference</item>
            <item>Broadcast</item>
            <item>Fragment</item>
            <item>Drawable</item>
        </string-array>
    </resources>

---

### 6.3 배열 리소스 작성 핵심

| 구성               | 의미                        |
|------------------|---------------------------|
| `string-array`   | 문자열 배열 리소스를 선언하는 엘리먼트     |
| `name="mobile"`  | 배열 리소스 이름                 |
| `item`           | 배열의 각 요소값                 |
| `R.array.mobile` | Java 코드에서 배열 리소스를 참조하는 ID |

---

### 6.4 배열 리소스 활용 예제

`ArrayAdapter.createFromResource()`를 사용하면 XML에 정의된 배열 리소스를 Adapter에 연결할 수 있다.

    public class MainActivity extends Activity {

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            ArrayAdapter<CharSequence> Adapter;

            Adapter = ArrayAdapter.createFromResource(
                this,
                R.array.mobile,
                android.R.layout.simple_list_item_1
            );

            ListView list = (ListView) findViewById(R.id.list);

            list.setAdapter(Adapter);
        }
    }

---

### 6.5 createFromResource 코드 해석

| 코드                           | 의미                        |
|------------------------------|---------------------------|
| `ArrayAdapter<CharSequence>` | 문자열 배열을 원본으로 가지는 Adapter  |
| `createFromResource()`       | 리소스 배열에서 Adapter 생성       |
| `this`                       | Activity Context          |
| `R.array.mobile`             | arrays.xml에 정의된 문자열 배열    |
| `simple_list_item_1`         | 하나의 TextView로 구성된 기본 레이아웃 |
| `setAdapter()`               | Adapter와 ListView 연결      |

---

## 7. ListView 속성

## 7.1 choiceMode 속성

`choiceMode`는 ListView 내부의 View를 선택하는 형식을 정의한다.

기본값은 항목 클릭만 가능하고 선택은 할 수 없는 상태이다.

`choiceMode`를 설정하면 하나 이상의 항목을 선택할 수 있다.

Java 코드에서 변경할 때는 `setChoiceMode()` 메소드를 사용한다.

---

### 7.2 choiceMode 속성값

| 속성값              | Java 인수                | 설명            |
|------------------|------------------------|---------------|
| `none`           | `CHOICE_MODE_NONE`     | 항목을 선택할 수 없음  |
| `singleChoice`   | `CHOICE_MODE_SINGLE`   | 하나의 항목만 선택 가능 |
| `multipleChoice` | `CHOICE_MODE_MULTIPLE` | 복수 개 항목 선택 가능 |

예:

    list.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE);

---

## 7.3 divider 속성

`divider`는 ListView 항목 사이의 구분선을 지정하는 속성이다.

| 속성                   | 설명                        |
|----------------------|---------------------------|
| `divider`            | 항목 사이 구분선 지정              |
| `dividerHeight`      | 구분선 두께 지정                 |
| `setDivider()`       | Java 코드에서 구분선 Drawable 지정 |
| `setDividerHeight()` | Java 코드에서 구분선 높이 지정       |

색상을 지정하거나 임의의 Drawable 객체를 지정할 수 있다.

---

### 7.4 divider 속성 활용 예제

여러 개 항목을 선택할 수 있도록 하고, 구분선을 파란색 5픽셀 두께로 표시한다.

    public class MainActivity extends Activity {

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            ArrayAdapter<CharSequence> Adapter;

            Adapter = ArrayAdapter.createFromResource(
                this,
                R.array.mobile,
                android.R.layout.simple_list_multiple_choice
            );

            ListView list = (ListView) findViewById(R.id.list);

            list.setAdapter(Adapter);

            list.setChoiceMode(ListView.CHOICE_MODE_MULTIPLE);

            list.setDivider(new ColorDrawable(Color.BLUE));
            list.setDividerHeight(5);
        }
    }

코드 해석:

| 코드                                          | 의미                      |
|---------------------------------------------|-------------------------|
| `simple_list_multiple_choice`               | 여러 항목 선택 가능한 체크 버튼 레이아웃 |
| `CHOICE_MODE_MULTIPLE`                      | 복수 선택 가능                |
| `setDivider(new ColorDrawable(Color.BLUE))` | 구분선을 파란색으로 지정           |
| `setDividerHeight(5)`                       | 구분선 두께를 5픽셀로 지정         |

---

## 8. Spinner

## 8.1 Spinner의 개요

Spinner는 여러 항목 중 하나를 선택할 때 사용하는 AdapterView이다.

ListView와 달리 항상 펼쳐져 있지 않고, 클릭할 때만 팝업 형식으로 펼쳐진다.

| 구분     | ListView         | Spinner           |
|--------|------------------|-------------------|
| 표시 방식  | 항상 펼쳐져 있음        | 클릭할 때만 팝업으로 펼쳐짐   |
| 선택 방식  | 항목을 바로 볼 수 있음    | 목록을 보려면 팝업을 열어야 함 |
| 선택 횟수  | 비교적 바로 선택 가능     | 최종 선택까지 최소 두 번 클릭 |
| 공간 사용  | 화면 공간을 많이 사용     | 화면 공간을 적게 사용      |
| 적합한 상황 | 많은 항목을 펼쳐서 보여줄 때 | 좁은 화면에서 하나를 선택할 때 |

---

### 8.2 Spinner의 특징

- Adapter로부터 데이터를 공급받는다.
- Adapter 생성 방법은 ListView와 동일하다.
- 여러 항목 중 하나를 선택할 때 사용한다.
- 화면 공간이 제한된 스마트폰과 태블릿에 적합하다.
- 선택 사항에 대한 Prompt 메시지를 팝업 상단에 표시할 수 있다.

---

### 8.3 Spinner 기본 레이아웃

Spinner에서 항목을 표시하기 위해 기본 레이아웃이 제공된다.

| 리소스 ID                         | 설명                  |
|--------------------------------|---------------------|
| `simple_spinner_item`          | 문자열만 나타남            |
| `simple_spinner_dropdown_item` | 문자열과 라디오 버튼이 함께 나타남 |

ListView와 마찬가지로 Adapter의 세 번째 인수로 레이아웃을 지정한다.

---

## 9. setDropDownViewResource 메소드

### 9.1 setDropDownViewResource의 의미

`setDropDownViewResource()` 메소드는 Spinner 자체에 적용할 레이아웃과 별도로, 클릭했을 때 나타나는 팝업의 레이아웃을 지정하는 메소드이다.

형식:

    public void setDropDownViewResource(int resource)

---

### 9.2 지정 가능한 레이아웃

| 레이아웃                           | 설명                 |
|--------------------------------|--------------------|
| `simple_spinner_item`          | 단순한 형태의 메뉴 모양      |
| `simple_spinner_dropdown_item` | 음영이 적용된 드롭다운 메뉴 모양 |

예:

    adspin.setDropDownViewResource(
        android.R.layout.simple_spinner_dropdown_item
    );

---

## 10. Prompt 메시지

### 10.1 Prompt 메시지의 개요

Spinner에서는 선택 사항에 대한 Prompt 메시지를 팝업 상단에 표시할 수 있다.

이는 ListView와 다른 점이다.

| 설정 방법   | 설명                     |
|---------|------------------------|
| Java 코드 | 문자열 ID 또는 문자열 직접 지정 가능 |
| XML 문서  | `prompt` 속성으로 지정 가능    |
| XML 제한  | XML에서는 리소스만 지정 가능      |

---

### 10.2 Prompt 설정 메소드

    void setPromptId(int promptId)

    void setPrompt(CharSequence prompt)

예:

    spin.setPrompt("prompt");

XML 예:

    android:prompt="@string/prompt"

---

## 11. OnItemSelectedListener 인터페이스

### 11.1 OnItemSelectedListener의 의미

Spinner의 팝업 레이아웃에서 item 선택을 변경하면 `AdapterView.OnItemSelectedListener` 인터페이스의 메소드가 호출된다.

주요 메소드는 다음과 같다.

    void onItemSelected(AdapterView<?> parent, View view, int position, long id)

    void onNothingSelected(AdapterView<?> parent)

---

### 11.2 메소드 역할

| 메소드                   | 호출 시점             |
|-----------------------|-------------------|
| `onItemSelected()`    | 항목이 선택되면 호출       |
| `onNothingSelected()` | 모든 항목이 선택 해제되면 호출 |

`OnItemSelectedListener` 인터페이스를 구현하려면 두 메소드를 모두 구현해야 한다.

항목 선택과 해제에 대해 특별한 동작이 필요하지 않으면 메소드 내부를 비워 두면 된다.

---

## 12. Spinner 프로젝트

### 12.1 activity_main.xml

Spinner를 활용한 화면은 TextView와 Spinner로 구성할 수 있다.

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:id="@+id/mytext"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="원하는 색상을 선택하세요." />

        <Spinner
            android:id="@+id/myspinner"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:spinnerMode="dialog" />

    </LinearLayout>

---

### 12.2 spinnerMode 속성

`spinnerMode`는 Spinner의 유형을 나타내는 속성이다.

| 속성값        | 설명               |
|------------|------------------|
| `dialog`   | 대화상자 형태의 Spinner |
| `dropdown` | 드롭다운 형태의 Spinner |

강의 예제에서는 `android:spinnerMode="dialog"`를 사용하여 대화상자 형태의 Spinner를 만들었다.

---

### 12.3 colors 배열 리소스

색상 이름을 문자열 배열로 정의한다.

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string-array name="colors">
            <item>검정색</item>
            <item>갈색</item>
            <item>짙은 회색</item>
            <item>회색</item>
            <item>짙은 회색</item>
            <item>빨간색</item>
            <item>연두색</item>
            <item>파란색</item>
            <item>노란색</item>
            <item>하늘색</item>
            <item>분홍색</item>
            <item>초록색</item>
            <item>남색</item>
        </string-array>
    </resources>

---

### 12.4 MainActivity.java

Spinner에서 선택한 색상을 Toast로 출력하는 예제이다.

    public class MainActivity extends Activity {

        ArrayAdapter<CharSequence> adspin;

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            Spinner spin = (Spinner) findViewById(R.id.myspinner);

            spin.setPrompt("prompt");

            adspin = ArrayAdapter.createFromResource(
                this,
                R.array.colors,
                android.R.layout.simple_spinner_item
            );

            adspin.setDropDownViewResource(
                android.R.layout.simple_spinner_dropdown_item
            );

            spin.setAdapter(adspin);

            spin.setOnItemSelectedListener(
                new AdapterView.OnItemSelectedListener() {

                    public void onItemSelected(
                        AdapterView<?> parent,
                        View view,
                        int position,
                        long id
                    ) {
                        Toast.makeText(
                            MainActivity.this,
                            adspin.getItem(position),
                            Toast.LENGTH_SHORT
                        ).show();
                    }

                    public void onNothingSelected(AdapterView<?> parent) {
                    }
                }
            );
        }
    }

---

### 12.5 Spinner 코드 해석

| 코드                                  | 의미                    |
|-------------------------------------|-----------------------|
| `Spinner spin`                      | XML의 Spinner 객체 참조    |
| `spin.setPrompt("prompt")`          | 팝업 상단 Prompt 메시지 설정   |
| `ArrayAdapter.createFromResource()` | 배열 리소스로 Adapter 생성    |
| `R.array.colors`                    | colors 배열 리소스 참조      |
| `simple_spinner_item`               | Spinner 자체에 표시되는 레이아웃 |
| `setDropDownViewResource()`         | 팝업 목록의 레이아웃 지정        |
| `simple_spinner_dropdown_item`      | 팝업에서 문자열과 라디오 버튼 표시   |
| `spin.setAdapter(adspin)`           | Spinner와 Adapter 연결   |
| `setOnItemSelectedListener()`       | 항목 선택 이벤트 처리          |
| `Toast.makeText()`                  | 선택한 항목을 짧은 메시지로 출력    |
| `adspin.getItem(position)`          | 선택한 위치의 항목값 가져오기      |

---

## 정리하기

1. AdapterView는 항목에 해당하는 여러 개의 자식 View를 가질 수 있으며, 사용자와의 상호작용도 처리할 수 있다.

2. Adapter는 화면에 표시될 데이터를 관리하고, 데이터 원본과 AdapterView 사이를 연결한다.

3. ArrayList는 크기가 고정되지 않은 배열이다.

4. ListView는 여러 항목을 수직으로 펼쳐서 보여주는 위젯이다.

5. ListView는 수직 스크롤을 지원하므로 많은 항목을 작은 화면에 표시할 수 있다.

6. ListView의 item은 하나의 행을 구성하는 항목이며, 문자열이나 이미지, 또는 문자열과 이미지를 함께 표시할 수 있다.

7. ListView와 Adapter를 연결할 때는 `setAdapter()` 메소드를 사용한다.

8. 고정적인 문자열 목록은 Java 코드보다 `arrays.xml`에 `string-array`로 정의하는 것이 바람직하다.

9. 배열 리소스는 `R.array.배열이름` 형식으로 참조한다.

10. `choiceMode`는 ListView 항목 선택 방식을 정의한다.

11. `choiceMode`의 주요 값은 `none`, `singleChoice`, `multipleChoice`이다.

12. `divider`는 ListView 항목 사이의 구분선을 지정하는 속성이다.

13. Spinner는 클릭할 때만 팝업으로 펼쳐지고, 여러 항목 중 하나를 선택할 때 사용된다.

14. Spinner는 화면이 좁은 모바일 환경에서 적합하다.

15. Spinner의 기본 레이아웃에는 `simple_spinner_item`과 `simple_spinner_dropdown_item`이 있다.

16. `setDropDownViewResource()`는 Spinner 팝업 목록의 레이아웃을 지정한다.

17. Spinner는 Prompt 메시지를 팝업 상단에 표시할 수 있다.

18. Spinner의 선택 이벤트는 `AdapterView.OnItemSelectedListener`로 처리한다.

19. `onItemSelected()`는 항목이 선택되면 호출된다.

20. `onNothingSelected()`는 모든 항목이 선택 해제되면 호출된다.

---

## 핵심 요약

### 1. AdapterView 핵심 구조

| 구성          | 역할                        |
|-------------|---------------------------|
| 데이터 원본      | ArrayList, 배열 리소스, 데이터베이스 |
| Adapter     | 데이터를 View 형태로 변환          |
| AdapterView | 변환된 View를 화면에 표시          |
| 대표 위젯       | ListView, Spinner         |

---

### 2. Adapter 핵심

| 개념                 | 핵심                     |
|--------------------|------------------------|
| Adapter            | 데이터와 UI를 연결            |
| ArrayAdapter       | 배열 또는 ArrayList 자료를 연결 |
| CursorAdapter      | 데이터베이스 Cursor 연결       |
| SimpleAdapter      | 단순 자료 구조를 View에 연결     |
| createFromResource | XML 배열 리소스로 Adapter 생성 |

---

### 3. ListView 핵심

| 개념            | 설명                   |
|---------------|----------------------|
| ListView      | 항목을 수직으로 나열          |
| item          | ListView의 한 행        |
| setAdapter    | ListView와 Adapter 연결 |
| choiceMode    | 선택 방식 지정             |
| divider       | 항목 사이 구분선            |
| dividerHeight | 구분선 두께               |

---

### 4. ListView 기본 레이아웃

| 리소스 ID                             | 핵심                |
|------------------------------------|-------------------|
| `simple_list_item_1`               | TextView 1개       |
| `simple_list_item_2`               | TextView 2개       |
| `simple_list_item_checked`         | 오른쪽 체크 표시         |
| `simple_list_item_single_choice`   | 오른쪽 라디오 버튼        |
| `simple_list_item_multiple_choice` | 여러 개 선택 가능한 체크 버튼 |

---

### 5. choiceMode

| 속성값              | Java 인수                | 의미      |
|------------------|------------------------|---------|
| `none`           | `CHOICE_MODE_NONE`     | 선택 불가   |
| `singleChoice`   | `CHOICE_MODE_SINGLE`   | 하나만 선택  |
| `multipleChoice` | `CHOICE_MODE_MULTIPLE` | 여러 개 선택 |

---

### 6. Spinner 핵심

| 개념                             | 설명                  |
|--------------------------------|---------------------|
| Spinner                        | 여러 항목 중 하나 선택       |
| 표시 방식                          | 클릭할 때 팝업으로 펼쳐짐      |
| 장점                             | 좁은 화면에서 공간 절약       |
| `simple_spinner_item`          | 선택된 문자열만 표시         |
| `simple_spinner_dropdown_item` | 팝업에서 문자열과 라디오 버튼 표시 |
| `setPrompt()`                  | 팝업 상단 메시지 지정        |
| `setDropDownViewResource()`    | 팝업 목록 레이아웃 지정       |
| `OnItemSelectedListener`       | 선택 이벤트 처리           |

---

## 연습문제 정리

### Q1. ListView에 대한 설명으로 옳지 않은 것은?

1. 수직 스크롤을 지원한다.
2. 주소록과 설정창 등이 활용 예이다.
3. 복수 개의 항목들을 수직으로 표시한다.
4. 모바일 장비의 화면이 넓지 않으므로 항목 개수에 제한이 있다.

정답: 4

해설:
ListView는 수직 스크롤을 통해 많은 데이터를 표시할 수 있으므로 표시되는 항목 개수에는 제한이 없다.

---

### Q2. Spinner에 대한 설명으로 옳은 것은?

1. 목록을 보려면 팝업을 열어야 한다.
2. 어댑터로부터 데이터를 공급받는다.
3. 여러 가지 선택 사항 중 복수 개를 선택받을 때만 사용된다.
4. 선택 사항에 대한 프롬프트 메시지를 팝업 상단에 표시할 수 없다.

정답: 1

해설:
Spinner는 기본적으로 선택된 항목만 보이고, 전체 목록을 보려면 클릭하여 드롭다운 또는 팝업을 열어야 한다. 복수 선택용이 아니라 여러 항목 중 하나를 선택할 때 주로 사용된다.

---

### Q3. AdapterView의 구현에서 표시할 데이터를 품고 있는 객체는 무엇인가?

1. Spinner
2. Adapter
3. Container
4. Carrier

정답: 2

해설:
Adapter는 ListView나 Spinner 등에 표시할 데이터를 보관하고, 이를 View로 연결해 주는 핵심 객체이다.

---

### Q4. ListView에서 오른쪽에 라디오 버튼이 나타나는 기본 레이아웃은?

1. simple_list_item_1
2. simple_list_item_checked
3. simple_list_item_single_choice
4. simple_spinner_item

정답: 3

해설:
`simple_list_item_single_choice`는 오른쪽에 라디오 버튼이 나타나는 ListView 기본 레이아웃이다.

---

### Q5. ListView에서 복수 개 항목 선택이 가능하도록 설정할 때 사용하는 choiceMode 인수는?

1. CHOICE_MODE_NONE
2. CHOICE_MODE_SINGLE
3. CHOICE_MODE_MULTIPLE
4. CHOICE_MODE_SPINNER

정답: 3

해설:
복수 개 항목 선택은 `CHOICE_MODE_MULTIPLE`로 설정한다.

---

### Q6. 고정적인 문자열 배열을 XML 리소스로 정의할 때 사용하는 엘리먼트는?

1. string-array
2. text-array
3. list-view
4. spinner-array

정답: 1

해설:
문자열 배열은 `arrays.xml`에서 `string-array` 엘리먼트로 정의한다.

---

### Q7. Spinner에서 클릭했을 때 나타나는 팝업 목록의 레이아웃을 지정하는 메소드는?

1. setAdapter()
2. setChoiceMode()
3. setDropDownViewResource()
4. setDividerHeight()

정답: 3

해설:
`setDropDownViewResource()`는 Spinner의 팝업 목록 레이아웃을 지정한다.

---

### Q8. Spinner에서 항목이 선택될 때 호출되는 메소드는?

1. onClick()
2. onItemSelected()
3. onNothingSelected()
4. setPrompt()

정답: 2

해설:
Spinner의 항목이 선택되면 `AdapterView.OnItemSelectedListener`의 `onItemSelected()`가 호출된다.

---

## 시험 직전 체크포인트

### 반드시 암기하기

- AdapterView = 데이터 기반으로 위젯을 구성하는 View
- 대표 AdapterView = ListView, Spinner
- Adapter = 데이터와 화면 View를 연결
- ArrayAdapter = ArrayList나 배열 자료를 AdapterView에 연결
- ArrayAdapter 생성 인수 = context, layout resource id, objects
- ListView = 여러 항목을 수직으로 표시
- ListView = 수직 스크롤 지원, 항목 개수 제한 없음
- ListView item = 하나의 행
- ListView와 Adapter 연결 = `setAdapter()`
- 고정 문자열 배열 = `arrays.xml`의 `string-array`
- 배열 리소스 참조 = `R.array.mobile`
- 리소스 기반 Adapter 생성 = `ArrayAdapter.createFromResource()`
- `simple_list_item_1` = TextView 1개
- `simple_list_item_checked` = 체크 표시
- `simple_list_item_single_choice` = 라디오 버튼
- `simple_list_item_multiple_choice` = 복수 선택 체크 버튼
- `choiceMode` = 선택 방식 정의
- `divider` = 항목 사이 구분선
- Spinner = 클릭할 때만 팝업으로 펼쳐짐
- Spinner = 여러 항목 중 하나를 선택
- `simple_spinner_item` = 문자열만 표시
- `simple_spinner_dropdown_item` = 문자열 + 라디오 버튼
- Spinner 팝업 레이아웃 = `setDropDownViewResource()`
- Spinner prompt = 팝업 상단 메시지
- Spinner 선택 이벤트 = `OnItemSelectedListener`

---

### 객관식에서 자주 나올 표현

| 문제 표현               | 정답 후보                            |
|---------------------|----------------------------------|
| 데이터와 View를 연결       | Adapter                          |
| 항목에 해당하는 여러 자식 View | AdapterView                      |
| 항목들을 수직으로 펼쳐서 보여줌   | ListView                         |
| 클릭할 때만 팝업으로 펼쳐짐     | Spinner                          |
| 크기가 고정되지 않은 배열      | ArrayList                        |
| 데이터와 ViewGroup 연결   | setAdapter                       |
| 문자열 배열 리소스          | string-array                     |
| 배열 리소스 위치           | values/arrays.xml                |
| 배열 리소스 참조           | R.array.mobile                   |
| 하나의 TextView        | simple_list_item_1               |
| 오른쪽 체크 표시           | simple_list_item_checked         |
| 오른쪽 라디오 버튼          | simple_list_item_single_choice   |
| 여러 개 선택 가능 체크 버튼    | simple_list_item_multiple_choice |
| 복수 선택               | CHOICE_MODE_MULTIPLE             |
| 항목 사이 구분선           | divider                          |
| 구분선 두께              | dividerHeight                    |
| Spinner 팝업 레이아웃     | setDropDownViewResource          |
| Spinner prompt 메시지  | setPrompt, android:prompt        |
| 선택 시 호출             | onItemSelected                   |
| 선택 해제 시 호출          | onNothingSelected                |

---

### 헷갈리는 개념 구분

| 개념                               | 구분 포인트                     |
|----------------------------------|----------------------------|
| AdapterView                      | 데이터를 화면에 표시하는 View 계열      |
| Adapter                          | 데이터 원본을 View로 바꿔 주는 중간 연결자 |
| ListView                         | 목록을 항상 펼쳐서 수직 표시           |
| Spinner                          | 클릭해야 목록이 팝업으로 펼쳐짐          |
| ArrayList                        | Java 코드에서 직접 데이터 저장        |
| string-array                     | XML 리소스에 고정 문자열 저장         |
| simple_list_item_checked         | 체크 표시만 있는 ListView 항목      |
| simple_list_item_multiple_choice | 여러 개 선택 가능한 체크 버튼          |
| simple_spinner_item              | Spinner 자체 표시용             |
| simple_spinner_dropdown_item     | Spinner 팝업 목록 표시용          |
| setAdapter                       | AdapterView와 Adapter 연결    |
| setChoiceMode                    | ListView 선택 방식 지정          |
| setDivider                       | ListView 구분선 지정            |
| setPrompt                        | Spinner 팝업 상단 문구 지정        |
| onItemSelected                   | 선택된 항목 처리                  |

---