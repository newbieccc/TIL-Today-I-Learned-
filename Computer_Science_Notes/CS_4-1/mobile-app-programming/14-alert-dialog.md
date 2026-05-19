# 모바일 앱 프로그래밍

## 14. 대화상자

### 강의 목차

1. AlertDialog
2. DatePickerDialog
3. TimePickerDialog

---

## 1. AlertDialog

### 1.1 AlertDialog의 개요

AlertDialog는 안드로이드 플랫폼에서 사용자에게 특정 메시지를 출력하고, 사용자의 의사를 전달받을 수 있는 Dialog UI 컴포넌트이다.

| 구분          | 설명                           |
|-------------|------------------------------|
| AlertDialog | 메시지 출력과 사용자 선택을 받을 수 있는 대화상자 |
| Toast       | 일정 시간 메시지만 출력하고 자동으로 사라짐     |
| 차이점         | AlertDialog는 사용자와 상호작용 가능    |
| 추가 기능       | 타이틀 바, 아이콘, 버튼 출력 가능         |

Toast는 단순히 메시지를 출력하는 기능에 가깝지만, AlertDialog는 사용자의 선택 결과를 받을 수 있다는 점에서 차이가 있다.

---

### 1.2 AlertDialog 생성 방식

AlertDialog 생성자는 `protected`로 숨겨져 있으므로 직접 생성할 수 없다.

따라서 `AlertDialog.Builder`를 통해 생성해야 한다.

생성 흐름은 다음과 같다.

    Activity(Context)
    → AlertDialog.Builder 생성
    → Builder 메소드로 속성 설정
    → AlertDialog 객체 생성
    → show()로 화면 출력

---

### 1.3 Builder 생성자

AlertDialog 객체 생성을 쉽게 하기 위해 별도의 Builder 클래스가 제공된다.

    AlertDialog.Builder(Context context)

`context`에는 AlertDialog를 생성하는 부모 Activity의 Context 객체를 전달한다.

Activity는 Context를 상속하므로 보통 `this`를 전달한다.

    AlertDialog.Builder bld = new AlertDialog.Builder(this);

---

### 1.4 Builder의 주요 설정 메소드

Builder 객체를 생성한 뒤, 다음 메소드로 AlertDialog의 속성을 설정한다.

| 메소드                                | 기능                  |
|------------------------------------|---------------------|
| `setMessage(CharSequence message)` | 대화상자 메시지 지정         |
| `setTitle(CharSequence title)`     | 타이틀 바 문자열 지정        |
| `setIcon(int iconId)`              | 아이콘 지정              |
| `show()`                           | AlertDialog를 화면에 출력 |
| `create()`                         | AlertDialog 객체만 생성  |

---

### 1.5 show()와 create()의 차이

| 메소드        | 설명                              |
|------------|---------------------------------|
| `create()` | AlertDialog를 생성만 하고 화면에 출력하지 않음 |
| `show()`   | AlertDialog를 화면에 출력함            |

`create()`로 생성한 AlertDialog는 메모리에만 존재하고 화면에는 나타나지 않는다.

따라서 화면에 보이게 하려면 `show()`를 호출해야 한다.

---

## 2. AlertDialog 예제

### 2.1 activity_main.xml

AlertDialog 예제 화면에는 안내 문자열과 버튼이 배치된다.

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TextView
            android:id="@+id/text"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Click Dialog Button" />

        <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="mOnClick"
            android:text="DIALOG CALL" />

    </LinearLayout>

핵심:

- TextView는 안내 문자열을 표시한다.
- Button은 AlertDialog 호출을 위한 버튼이다.
- `android:onClick="mOnClick"`은 버튼 클릭 시 실행될 Java 메소드를 지정한다.

---

### 2.2 MainActivity.java

버튼을 클릭하면 AlertDialog가 나타나도록 작성한다.

    public class MainActivity extends Activity {

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
        }

        public void mOnClick(View v) {
            AlertDialog.Builder bld = new AlertDialog.Builder(this);

            bld.setTitle("MESSAGE");
            bld.setMessage("AlertDialog Test is success !!");
            bld.setIcon(R.mipmap.ic_launcher);

            bld.show();
        }
    }

---

### 2.3 코드 해석

| 코드                              | 의미             |
|---------------------------------|----------------|
| `new AlertDialog.Builder(this)` | Builder 객체 생성  |
| `setTitle("MESSAGE")`           | 타이틀 지정         |
| `setMessage()`                  | 메시지 지정         |
| `setIcon()`                     | 아이콘 지정         |
| `show()`                        | AlertDialog 출력 |

AlertDialog는 화면에 출력되기 전에 속성 설정이 완료되어야 한다.

---

### 2.4 Toast와 AlertDialog 비교

| 구분        | Toast          | AlertDialog    |
|-----------|----------------|----------------|
| 메시지 출력    | 가능             | 가능             |
| 자동 사라짐    | 일정 시간 후 자동 사라짐 | 사용자가 닫을 때까지 유지 |
| 사용자 선택 처리 | 어려움            | 가능             |
| 타이틀 바     | 없음             | 가능             |
| 아이콘       | 없음             | 가능             |
| 긴 메시지     | 제한적            | 스크롤 가능         |

AlertDialog는 사용자가 닫을 때까지 사라지지 않으므로 장시간 메시지를 출력할 수 있다.

메시지가 길면 스크롤바가 나타나고, AlertDialog 안에서 스크롤하여 내용을 읽을 수 있다.

---

## 3. Builder 호출 및 반환

### 3.1 Builder 메소드 체이닝

Builder의 생성자와 설정 메소드들은 모두 Builder 자체를 반환한다.

따라서 Builder 객체 이름을 따로 만들지 않고 메소드를 연쇄적으로 호출할 수 있다.

    new AlertDialog.Builder(this)
        .setTitle("MESSAGE")
        .setMessage("AlertDialog Test is success!!")
        .setIcon(R.drawable.ic_launcher)
        .setPositiveButton("CLOSE", new DialogInterface.OnClickListener() {
            public void onClick(DialogInterface dialog, int which) {
            }
        })
        .show();

---

### 3.2 메소드 체이닝 핵심

| 특징         | 설명                                         |
|------------|--------------------------------------------|
| Builder 반환 | 설정 메소드가 Builder 객체를 반환                     |
| 연쇄 호출      | `.setTitle().setMessage().setIcon()` 형태 가능 |
| 최종 출력      | 마지막에 `show()` 호출                           |
| 장점         | 코드가 간결해짐                                   |

`new` 연산자는 Builder를 생성하고, AlertDialog는 최종적으로 호출되는 `show()` 메소드에 의해 화면에 출력된다.

---

## 4. AlertDialog 버튼

### 4.1 AlertDialog와 Activity의 관계

AlertDialog가 열리면 AlertDialog가 닫힐 때까지 뒤쪽 Activity는 실행 금지 상태가 된다.

사용자가 메시지를 읽고 AlertDialog를 닫은 후에 뒤쪽 Activity가 다시 동작할 수 있다.

---

### 4.2 AlertDialog 버튼 배치

AlertDialog에는 최대 세 개의 버튼을 배치할 수 있다.

| 버튼 종류 | 메소드                   |
|-------|-----------------------|
| 긍정 버튼 | `setPositiveButton()` |
| 중립 버튼 | `setNeutralButton()`  |
| 부정 버튼 | `setNegativeButton()` |

버튼은 긍정, 중립, 부정이라는 이름을 가지고 있지만, 실제 의미는 코드 구현에 따라 달라진다.

즉, `setPositiveButton()`으로 만든 버튼이 반드시 긍정적인 작업을 수행해야 하는 것은 아니다.

---

### 4.3 버튼 메소드 형식

    setPositiveButton(CharSequence text, DialogInterface.OnClickListener listener)

    setNeutralButton(CharSequence text, DialogInterface.OnClickListener listener)

    setNegativeButton(CharSequence text, DialogInterface.OnClickListener listener)

| 인수         | 설명                 |
|------------|--------------------|
| `text`     | 버튼에 표시할 문자열        |
| `listener` | 버튼 클릭 시 실행될 클릭 리스너 |

버튼 텍스트는 문자열 상수로 직접 지정할 수도 있고, 리소스 문자열 ID로 지정할 수도 있다.

---

### 4.4 AlertDialog 버튼 예제

    public class MainActivity extends Activity {

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
        }

        public void mOnClick(View v) {
            new AlertDialog.Builder(this)
                .setTitle("MESSAGE")
                .setMessage("AlertDialog Test is success!!")
                .setIcon(R.drawable.ic_launcher)
                .setPositiveButton("CLOSE", new DialogInterface.OnClickListener() {
                    public void onClick(DialogInterface dialog, int which) {
                    }
                })
                .show();
        }
    }

---

### 4.5 버튼 예제 해석

| 코드                                     | 의미                |
|----------------------------------------|-------------------|
| `setPositiveButton("CLOSE", listener)` | CLOSE 버튼 배치       |
| `onClick()` 내부가 비어 있음                  | 버튼 클릭 시 특별한 동작 없음 |
| 버튼 클릭                                  | AlertDialog가 닫힘   |
| 실행 제어                                  | 뒤쪽 Activity로 돌아감  |

클릭 리스너의 `onClick()` 메소드에 아무 코드가 없어도 버튼을 누르면 AlertDialog가 닫힌다.

---

## 5. DatePickerDialog

### 5.1 DatePickerDialog의 개요

DatePickerDialog는 사용자가 손쉽게 날짜 정보를 입력할 수 있는 인터페이스를 제공하는 Dialog UI 컴포넌트이다.

| 구분               | 설명                      |
|------------------|-------------------------|
| DatePickerDialog | 날짜 선택 대화상자              |
| 입력 정보            | 연, 월, 일                 |
| 이벤트              | OK 버튼 클릭 시 날짜 선택 이벤트 실행 |

---

### 5.2 DatePickerDialog 생성자

    public DatePickerDialog(
        Context context,
        DatePickerDialog.OnDateSetListener listener,
        int year,
        int monthOfYear,
        int dayOfMonth
    )

매개변수 의미:

| 매개변수          | 설명                     |
|---------------|------------------------|
| `context`     | Activity의 Context      |
| `listener`    | OK 버튼 클릭 시 실행될 이벤트 리스너 |
| `year`        | 기본값으로 설정될 연도           |
| `monthOfYear` | 기본값으로 설정될 월            |
| `dayOfMonth`  | 기본값으로 설정될 일            |

---

## 6. DatePickerDialog 예제

### 6.1 activity_main.xml

DatePickerDialog 예제 화면에는 Button과 TextView가 있다.

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="mOnClick"
            android:text="날짜 설정" />

        <TextView
            android:id="@+id/text1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />

    </LinearLayout>

구성:

| View     | 역할                   |
|----------|----------------------|
| Button   | DatePickerDialog 활성화 |
| TextView | 선택한 날짜 정보 출력         |

---

### 6.2 MainActivity.java

    public class MainActivity extends AppCompatActivity {

        Button btnSelectDate;
        DatePickerDialog datePickerDialog;
        TextView display;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            btnSelectDate = (Button) findViewById(R.id.button1);
            display = (TextView) findViewById(R.id.text1);
        }

        public void mOnClick(View v) {
            if (v == btnSelectDate) {
                final Calendar c = Calendar.getInstance();

                int mYear = c.get(Calendar.YEAR);
                int mMonth = c.get(Calendar.MONTH);
                int mDay = c.get(Calendar.DAY_OF_MONTH);

                datePickerDialog = new DatePickerDialog(
                    this,
                    new DatePickerDialog.OnDateSetListener() {
                        @Override
                        public void onDateSet(
                            DatePicker view,
                            int year,
                            int monthOfYear,
                            int dayOfMonth
                        ) {
                            display.setText(
                                dayOfMonth + "/" + (monthOfYear + 1) + "/" + year
                            );
                        }
                    },
                    mYear,
                    mMonth,
                    mDay
                );

                datePickerDialog.show();
            }
        }
    }

---

### 6.3 DatePickerDialog 코드 해석

| 코드                       | 의미                              |
|--------------------------|---------------------------------|
| `Calendar.getInstance()` | 현재 날짜와 시간 정보를 가진 Calendar 객체 생성 |
| `Calendar.YEAR`          | 현재 연도                           |
| `Calendar.MONTH`         | 현재 월                            |
| `Calendar.DAY_OF_MONTH`  | 현재 일                            |
| `new DatePickerDialog()` | 날짜 선택 대화상자 생성                   |
| `OnDateSetListener`      | 날짜 선택 후 OK 버튼 클릭 시 실행           |
| `onDateSet()`            | 선택된 날짜 정보를 처리                   |
| `display.setText()`      | TextView에 날짜 출력                 |
| `show()`                 | DatePickerDialog 출력             |

주의:

    monthOfYear는 0부터 시작하므로 출력할 때는 monthOfYear + 1을 사용한다.

---

## 7. TimePickerDialog와 TimePicker

### 7.1 TimePickerDialog의 개요

TimePickerDialog는 사용자가 손쉽게 시간 정보를 입력할 수 있는 인터페이스를 제공하는 Dialog UI 컴포넌트이다.

알람, 타이머처럼 시간을 다루는 기본 앱에서 많이 활용된다.

| 구분               | 설명                |
|------------------|-------------------|
| TimePickerDialog | 시간 선택 대화상자        |
| 입력 정보            | 시, 분              |
| 지원 모드            | 24시간 모드, AM/PM 모드 |

---

### 7.2 TimePicker의 화면 유형

XML 코드에서 TimePicker를 정의하고 Java 코드에서 ID로 참조하여 사용할 수 있다.

TimePicker의 레이아웃 유형은 `timePickerMode` 속성으로 지정한다.

| 속성값       | 설명           |
|-----------|--------------|
| `clock`   | 시계 모양의 대화상자  |
| `spinner` | 스피너 형태의 대화상자 |

---

## 8. TimePicker 예제

### 8.1 activity_main.xml

TimePicker 예제 화면은 TimePicker, Button, TextView로 구성된다.

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <TimePicker
            android:id="@+id/timePicker1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:timePickerMode="clock" />

        <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="선택" />

        <TextView
            android:id="@+id/text1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="time" />

    </LinearLayout>

구성:

| View       | 역할           |
|------------|--------------|
| TimePicker | 시간 정보 입력     |
| Button     | 입력 완료 이벤트 전달 |
| TextView   | 선택한 시간 정보 출력 |

---

### 8.2 MainActivity.java

    public class MainActivity extends AppCompatActivity {

        TimePicker timePicker1;
        TextView text1;
        Button button1;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                timePicker1 = findViewById(R.id.timePicker1);

                final Calendar c = Calendar.getInstance();

                int mHour = c.get(Calendar.HOUR_OF_DAY);
                int mMinute = c.get(Calendar.MINUTE);

                timePicker1.setHour(mHour);
                timePicker1.setMinute(mMinute);
            }

            button1 = findViewById(R.id.button1);

            button1.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                        text1 = findViewById(R.id.text1);

                        int mHour = timePicker1.getHour();
                        int mMinute = timePicker1.getMinute();

                        text1.setText("time : " + mHour + ":" + mMinute);
                    }
                }
            });
        }
    }

---

### 8.3 TimePicker 코드 해석

| 코드                             | 의미                      |
|--------------------------------|-------------------------|
| `timePicker1 = findViewById()` | XML의 TimePicker 참조      |
| `Calendar.getInstance()`       | 현재 시스템 시간 가져오기          |
| `Calendar.HOUR_OF_DAY`         | 24시간 기준 현재 시            |
| `Calendar.MINUTE`              | 현재 분                    |
| `setHour()`                    | TimePicker에 시 설정        |
| `setMinute()`                  | TimePicker에 분 설정        |
| `getHour()`                    | TimePicker에서 선택된 시 가져오기 |
| `getMinute()`                  | TimePicker에서 선택된 분 가져오기 |
| `text1.setText()`              | 선택된 시간 출력               |

---

### 8.4 TimePicker 예제 흐름

1. 앱 실행 시 현재 시스템 시간을 가져온다.
2. TimePicker에 현재 시와 분을 설정한다.
3. 사용자가 TimePicker로 시간을 변경한다.
4. 선택 버튼을 누른다.
5. TimePicker에서 시와 분을 읽는다.
6. TextView에 시간 정보를 출력한다.

---

## 정리하기

1. AlertDialog는 사용자에게 특정 메시지를 출력하고, 사용자의 의사를 전달받을 수 있는 Dialog UI 컴포넌트이다.

2. AlertDialog는 Toast와 달리 사용자의 선택 결과를 받을 수 있다.

3. AlertDialog는 타이틀 바와 아이콘을 출력할 수 있다.

4. AlertDialog는 생성자가 `protected`이므로 직접 생성하지 않고 Builder를 통해 생성한다.

5. AlertDialog 생성 흐름은 Context → Builder 설정 → AlertDialog 생성 → show 출력이다.

6. Builder의 주요 메소드에는 `setMessage()`, `setTitle()`, `setIcon()`, `show()`, `create()`가 있다.

7. `create()`는 AlertDialog를 생성만 하고 화면에 출력하지 않는다.

8. `show()`는 AlertDialog를 화면에 출력한다.

9. AlertDialog는 사용자가 닫을 때까지 사라지지 않으므로 긴 메시지를 출력할 수 있다.

10. AlertDialog에는 최대 세 개의 버튼을 배치할 수 있다.

11. AlertDialog 버튼은 Positive, Neutral, Negative로 구분되지만 실제 의미는 구현된 코드로 결정된다.

12. `setPositiveButton()`, `setNeutralButton()`, `setNegativeButton()`은 버튼에 표시할 텍스트와 클릭 리스너를 인수로 받는다.

13. DatePickerDialog는 사용자가 손쉽게 날짜 정보를 입력할 수 있는 Dialog UI 컴포넌트이다.

14. DatePickerDialog 생성자의 주요 인수는 Context, OnDateSetListener, year, monthOfYear, dayOfMonth이다.

15. DatePickerDialog에서 날짜를 선택하고 OK 버튼을 누르면 OnDateSetListener가 실행된다.

16. TimePickerDialog는 사용자가 손쉽게 시간 정보를 입력할 수 있는 Dialog UI 컴포넌트이다.

17. TimePicker는 `timePickerMode` 속성을 통해 clock 또는 spinner 형태로 표시할 수 있다.

18. TimePicker는 시와 분을 입력받으며, 24시간 모드와 AM/PM 모드를 모두 지원한다.

19. TimePicker 예제에서는 Calendar에서 현재 시스템 시간을 가져와 TimePicker에 반영한다.

20. 사용자가 선택한 시간은 `getHour()`, `getMinute()`로 가져와 TextView에 출력할 수 있다.

---

## 핵심 요약

### 1. Dialog 종류

| Dialog           | 핵심                |
|------------------|-------------------|
| AlertDialog      | 메시지 출력과 사용자 선택 처리 |
| DatePickerDialog | 날짜 정보 입력          |
| TimePickerDialog | 시간 정보 입력          |

---

### 2. AlertDialog 핵심

| 항목          | 설명             |
|-------------|----------------|
| 생성 방식       | Builder를 통해 생성 |
| 직접 생성 불가 이유 | 생성자가 protected |
| 메시지 설정      | `setMessage()` |
| 제목 설정       | `setTitle()`   |
| 아이콘 설정      | `setIcon()`    |
| 화면 출력       | `show()`       |
| 객체 생성만      | `create()`     |
| 버튼 최대 개수    | 3개             |

---

### 3. AlertDialog 버튼

| 버튼       | 메소드                   |
|----------|-----------------------|
| Positive | `setPositiveButton()` |
| Neutral  | `setNeutralButton()`  |
| Negative | `setNegativeButton()` |

버튼 이름은 구분을 위한 것이며, 실제 의미는 구현 코드에 따라 결정된다.

---

### 4. DatePickerDialog 핵심

| 항목     | 설명                                                        |
|--------|-----------------------------------------------------------|
| 목적     | 날짜 입력                                                     |
| 생성자 인수 | Context, OnDateSetListener, year, monthOfYear, dayOfMonth |
| 이벤트    | `onDateSet()`                                             |
| 출력     | TextView에 선택 날짜 표시                                        |
| 주의     | monthOfYear는 0부터 시작하므로 +1 필요                              |

---

### 5. TimePicker 핵심

| 항목     | 설명             |
|--------|----------------|
| 목적     | 시간 입력          |
| 입력 정보  | 시, 분           |
| 모드     | clock, spinner |
| 현재 시간  | Calendar에서 가져옴 |
| 시 설정   | `setHour()`    |
| 분 설정   | `setMinute()`  |
| 시 가져오기 | `getHour()`    |
| 분 가져오기 | `getMinute()`  |

---

## 연습문제 정리

### Q1. AlertDialog에 대한 설명으로 옳은 것은?

1. 문자열 메시지만 출력할 수 있다.
2. 사용자의 입력을 받아들일 수 없다.
3. Toast보다 좀 더 짧고 간단한 메시지를 전달할 때 이용된다.
4. 생성자가 protected로 숨겨져 있으므로 직접적으로 생성할 수 없다.

정답: 4

해설:
AlertDialog의 생성자는 `protected`이므로 `new AlertDialog()`로 직접 생성할 수 없다. 대신 `AlertDialog.Builder`를 사용하여 객체를 생성해야 한다.

---

### Q2. AlertDialog 버튼 표시 방법으로 옳지 않은 것은?

1. 버튼의 텍스트는 문자열 상수를 바로 지정할 수 없다.
2. 버튼의 실제 의미는 구현된 코드로 결정된다.
3. 버튼의 이름은 구분을 위한 것이다.
4. 클릭리스너가 비어 있더라도 버튼은 나타난다.

정답: 1

해설:
버튼의 텍스트는 `"확인"`, `"취소"`와 같은 문자열 상수로 직접 지정할 수 있다. 또한 리소스 문자열 ID를 지정할 수도 있다.

---

### Q3. AlertDialog를 화면에 출력하는 메소드는?

1. create()
2. show()
3. setTitle()
4. setMessage()

정답: 2

해설:
`show()`는 AlertDialog를 화면에 출력한다. `create()`는 객체를 생성만 하고 화면에는 출력하지 않는다.

---

### Q4. DatePickerDialog 생성자의 인수로 보기 어려운 것은?

1. Context
2. OnDateSetListener
3. year
4. hourOfDay

정답: 4

해설:
DatePickerDialog는 날짜를 선택하므로 year, monthOfYear, dayOfMonth를 인수로 받는다. hourOfDay는 시간과 관련된 값이다.

---

### Q5. DatePickerDialog에서 날짜 선택 후 OK 버튼을 클릭하면 실행되는 리스너는?

1. OnClickListener
2. OnDateSetListener
3. OnTimeSetListener
4. OnItemSelectedListener

정답: 2

해설:
DatePickerDialog에서 날짜 선택 후 OK 버튼을 누르면 `OnDateSetListener`가 실행된다.

---

### Q6. TimePicker의 레이아웃 유형을 지정하는 속성은?

1. timePickerMode
2. datePickerMode
3. dialogMode
4. alertMode

정답: 1

해설:
TimePicker의 레이아웃 유형은 `timePickerMode` 속성으로 지정한다.

---

### Q7. TimePicker의 `timePickerMode` 속성값으로 알맞은 것은?

1. list, grid
2. clock, spinner
3. date, time
4. positive, negative

정답: 2

해설:
TimePicker의 `timePickerMode` 속성값에는 시계 모양의 `clock`과 스피너 형태의 `spinner`가 있다.

---

## 시험 직전 체크포인트

### 반드시 암기하기

- AlertDialog = 메시지 출력 + 사용자 의사 전달받기
- Toast = 단순 메시지 출력 후 자동 사라짐
- AlertDialog는 사용자와 상호작용 가능
- AlertDialog는 타이틀 바와 아이콘 출력 가능
- AlertDialog 생성자는 protected
- AlertDialog는 Builder를 통해 생성
- `create()` = 생성만 하고 출력하지 않음
- `show()` = 화면에 출력
- Builder 설정 메소드 = `setTitle()`, `setMessage()`, `setIcon()`
- AlertDialog 버튼 최대 3개
- 버튼 종류 = Positive, Neutral, Negative
- 버튼 이름은 구분용, 실제 의미는 코드로 결정
- DatePickerDialog = 날짜 입력
- DatePickerDialog 리스너 = `OnDateSetListener`
- DatePickerDialog 인수 = Context, listener, year, monthOfYear, dayOfMonth
- monthOfYear는 0부터 시작하므로 출력 시 +1
- TimePickerDialog = 시간 입력
- TimePicker는 24시간 모드와 AM/PM 모드 지원
- TimePicker 모드 = `clock`, `spinner`
- TimePicker 현재 시간 설정 = `Calendar.getInstance()`
- TimePicker 값 읽기 = `getHour()`, `getMinute()`

---

### 객관식에서 자주 나올 표현

| 문제 표현                   | 정답 후보                  |
|-------------------------|------------------------|
| 메시지 출력과 사용자 선택          | AlertDialog            |
| 일정 시간 후 자동 사라짐          | Toast                  |
| AlertDialog 직접 생성 불가 이유 | protected 생성자          |
| AlertDialog 생성 도구       | AlertDialog.Builder    |
| AlertDialog 화면 출력       | show()                 |
| 객체 생성만 수행               | create()               |
| 타이틀 설정                  | setTitle()             |
| 메시지 설정                  | setMessage()           |
| 아이콘 설정                  | setIcon()              |
| 긍정 버튼                   | setPositiveButton()    |
| 중립 버튼                   | setNeutralButton()     |
| 부정 버튼                   | setNegativeButton()    |
| 날짜 선택 대화상자              | DatePickerDialog       |
| 날짜 선택 이벤트               | OnDateSetListener      |
| 시간 선택 대화상자              | TimePickerDialog       |
| TimePicker 모드 속성        | timePickerMode         |
| 시계 모양                   | clock                  |
| 스피너 형태                  | spinner                |
| 현재 시각 가져오기              | Calendar.getInstance() |
| 시간 가져오기                 | getHour(), getMinute() |

---

### 헷갈리는 개념 구분

| 개념                       | 구분 포인트                       |
|--------------------------|------------------------------|
| Toast                    | 메시지만 잠깐 출력                   |
| AlertDialog              | 메시지 출력 후 사용자 선택 가능           |
| create()                 | 생성만 함                        |
| show()                   | 화면에 보여 줌                     |
| setPositiveButton        | 이름은 Positive지만 실제 의미는 코드가 결정 |
| DatePickerDialog         | 연, 월, 일 선택                   |
| TimePickerDialog         | 시, 분 선택                      |
| OnDateSetListener        | 날짜 선택 완료 이벤트                 |
| OnClickListener          | 버튼 클릭 이벤트                    |
| timePickerMode="clock"   | 시계 모양                        |
| timePickerMode="spinner" | 스피너 모양                       |

---