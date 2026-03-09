# 모바일앱프로그래밍

## 04. 사용자 인터페이스를 위한 위젯

- 컴퓨터과학과 정광식 교수님

---

# 1. Button

## 1) Button 개요

### Button

- 스마트폰 환경에서 사용자는 마우스나 키보드 없이 터치 동작으로만 앱에 명령을 전달해야 할 상황이 자주 발생함
- 사용자로부터 선택 이벤트를 수집할 수 있는 인터페이스를 제공하는 위젯임(⇒ focusable 속성)
- 사각형 모양이며 사용자는 사각형 영역 내부를 터치하는 동작을 통해 선택 명령을 내릴 수 있음(⇒ MainActivity.java와 연결됨)
- 그림이나 문자를 배경으로 표시 가능
    - TextView 위젯으로부터 상속

## 2) text 속성

### 개요

- Button 내부에 출력되는 문자열을 결정하는 속성임
- 해당 Button이 어떤 목적을 가지고 있는지 표현하는 역할을 수행함
- Button은 TextView의 속성과 메소드를 상속받아 구현되었기 때문에 3장에서 다루었던 문자열 관련 속성들도 사용할 수 있음

## 3) textAllCaps 속성

### 개요

- Button 내부에 출력되는 문자열을 모두 대문자로 출력할지 여부를 결정하는 속성임
- (프로그램 4.1)에서 Button의 text 속성을 통해 알파벳으로 구성된 문자열을 출력하면 대문자로 변환되는 것을 확인할 수 있음
    - textAllCaps 속성의 기본값이 true로 지정되어 있음
- 이를 변경하려면 (프로그램 4.2)와 같이 textAllCaps 속성을 추가하고 false 값을 지정해야 함
    - false는 소문자 출력

## 4) onClick 속성

### 개요

- 사용자가 버튼을 터치하면 클릭 이벤트가 발생하고, 개발자는 이벤트가 발생할 때 앱이 어떤 동작을 수행할지 지정하여 서비스의 흐름을 제어하는 JAVA 코드(MainActivity.java)를 작성해야 함
- onClick 속성은 버튼의 클릭 이벤트가 발생할 때 수행되는 동작을 연결하기 위한 속성임
- 액티비티 내부에서 정의된 함수명을 onClick 속성값으로 명시함

### Button 위젯의 onClick 속성 예제 설명

- (프로그램 4.3)은 2개의 Button과 1개의 TextView를 포함하는 LinearLayout을 가진 레이아웃 파일임
- 2개의 Button에는 onClick 속성이 적용되어 있으며, onButtonClick이라는 동일한 속성값(호출될 함수)을 가짐
- 속성값으로 명시된 onButtonClick 함수는 MainActivity.java의 MainActivity 클래스 내부에 정의되어 버튼이 클릭되면 호출됨

### Button 위젯의 onClick 속성 예제 - java 파일 설명

- (프로그램 4.4)의 onButtonClick 함수는 View 객체를 인수로 받으며, View 객체는 클릭 이벤트를 발생시킨 위젯임
- getId 메소드를 통해 위젯의 id를 참조하여 어떤 버튼을 클릭하는지 여부를 확인하고 switch-case 문을 이용하여 각 버튼에 대한 이벤트 처리로 분기함
- button1 아이디를 가진 버튼을 선택할 때에는 TextView 내용이 "hello"라는 문자열로 변경됨
- button2 아이디를 가진 버튼을 선택할 때에는 "world"라는 문자열로 변경됨

  public class MainActivity extends AppCompatActivity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
        }

        public void onButtonClick(View view) {
            TextView text1 = (TextView) findViewById(R.id.text1);

            switch(view.getId()) {
                case R.id.button1:
                    text1.setText("hello");
                    break;

                case R.id.button2:
                    text1.setText("world");
                    break;
            }
        }
  }

---

# 2. EditText

## 1) EditText 개요

### EditText

- EditText는 사용자로부터 문자열을 입력받을 수 있는 인터페이스를 제공하는 위젯임
- TextView의 서브 클래스로 TextView의 모든 속성을 사용할 수 있음
- EditText를 통해 입력한 문자열을 편집하고 활용하기 위해 다양한 메소드가 제공됨

## 2) text 속성

### 개요

- TextView의 가장 중요한 속성으로 출력할 문자열을 지정함
- EditText가 처음 화면에 출력될 때 빈칸에 기본적으로 들어갈 문자열을 지정함
- 가장 단순하게 text="XXX"와 같은 형태로 문자열을 지정할 수 있음
- 안드로이드 앱에서 사용하는 다양한 메시지들은 문자열을 직접 지정하는 것보다 strings.xml에 id와 함께 문자열을 정의하고 필요 시점에 참조하여 사용함
- 이러한 방식은 다국어 버전 개발에도 유용하게 사용될 수 있음

          <EditText
            android:id="@+id/edit"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Input Please" />
        
          <Button
            android:id="@+id/button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="button"
            android:onClick="onButtonClick" />

## 3) getText 메소드

### 개요

- 사용자가 EditText 위젯에 입력한 문자열을 JAVA 코드(MainActivity.java)에서 활용하기 위해 참조하는 메소드임
- getText 메소드는 Editable 이라는 객체가 반환되는데, 이를 toString 메소드를 통해 문자열로 변환하여 사용하는 것이 일반적임

### EditText 위젯의 getText 속성 예제 설명

- Button 위젯에서 onClick 속성을 통해 클릭할 때 onButtonClick 함수가 호출되도록 하였음
- 이때 호출되는 onButtonClick 함수는 MainActivity.java의 MainActivity 클래스 내부에 정의됨

### EditText 위젯의 getText 속성 예제 - MainActivity.java 설명

- onButtonClick 함수 내부에 있는 findViewById 함수를 통해서 EditText를 참조하고 있음
- getText 함수와 toString 함수를 통해 입력된 문자열을 String 자료형 str 객체에 저장함
- 최종적으로 해당 문자열을 Toast로 출력함

            public void onButtonClick(View view) {
                EditText edit = (EditText) findViewById(R.id.edit);
                String str = edit.getText().toString();
                Toast.makeText(MainActivity.this, str, Toast.LENGTH_SHORT).show();
            }

---

# 3. CheckBox

## 1) CheckBox 예제

    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <CheckBox
            android:id="@+id/checkbox1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="apple" />

        <CheckBox
            android:id="@+id/checkbox2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="banana" />

        <CheckBox
            android:id="@+id/checkbox3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="orange" />

    </LinearLayout>

## 2) CheckBox 위젯 예제 설명

- (프로그램 4.8)에서는 LinearLayout 내부에 3개의 체크박스를 정의함
- id 속성의 속성값을 각각 checkbox1, checkbox2, checkbox3로 지정하여 구분함
- CheckBox는 isChecked 메소드를 통해 체크 여부를 확인할 수 있음
- isChecked 메소드는 해당 CheckBox가 사용자에 의해 체크된 경우 true를 반환하고, 체크되지 않은 경우 false를 반환함
- findViewById 메소드를 통해 XML 레이아웃을 통해 생성된 CheckBox 객체를 참조함
- isChecked 메소드를 통해 사용자가 선택한 문자열 정보를 확인함

---

# 4. RadioButton

## 1) RadioButton 개요

### 개요

- 라디오 버튼(radio button)은 사용자가 문자열 리스트에서 하나의 구성요소를 선택하기 위한 인터페이스임
- 설문이나 회원가입을 할 때, 다수의 정보중에서 하나의 정보를 선택하여 입력하기 위하여 사용됨
- RadioButton은 안드로이드 환경에서 라디오 버튼 인터페이스를 제공하는 위젯임

## 2) RadioButton 예제

    <RadioButton
        android:id="@+id/radio1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Apple" />

    <RadioButton
        android:id="@+id/radio2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Banana" />

    <RadioButton
        android:id="@+id/radio3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Orange" />

## 3) RadioButton 위젯 예제 설명

- (프로그램 4.9)에서 선택 문자열 리스트 하나를 구성하는 RadioButton들은 text 속성을 통해 출력할 문자열을 명시함
- RadioGroup 태그로 감싸서 선택 범위를 지정함
- RadioButton은 isChecked 함수를 통해 체크 여부를 확인할 수 있음
- findViewById 함수를 통해 XML 레이아웃을 통해 RadioButton 객체를 참조함
- isChecked 메소드를 통해 사용자가 선택한 문자열 정보를 확인함

---

# 5. Switch / 이벤트

## 정리하기

1. Button
    - 사용자로부터 선택 이벤트를 수집할 수 있는 인터페이스를 제공하는 위젯
    - 속성: text, textAllCaps, onClick

2. EditText
    - 사용자로부터 문자열을 입력받을 수 있는 인터페이스를 제공하는 위젯
    - 속성: text, getText

3. CheckBox
    - 사용자가 문자열 리스트에서 다수의 구성요소를 선택하기 위한 인터페이스를 제공하는 위젯

4. RadioButton
    - 사용자가 문자열 리스트에서 하나의 구성요소를 선택하기 위한 인터페이스를 제공하는 위젯

5. Switch
    - 사용자의 선택에 따라 On, Off를 전환하는 토글 형태의 인터페이스를 제공하는 위젯

6. 이벤트
    - 프로그램이 반응하도록 사용자가 생성시키는 동작 또는 사건의 발생
