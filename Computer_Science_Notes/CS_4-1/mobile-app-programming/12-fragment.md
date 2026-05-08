# 모바일앱프로그래밍

## 12. 프래그먼트

- 컴퓨터과학과 정광식 교수님

---

## 1. 학습 목차

1. 프래그먼트 1
2. 프래그먼트 2
3. 프래그먼트 통신

---

## 2. 프래그먼트

### 2-1. 액티비티의 한계

- 액티비티는 기본적으로 다음 2개의 파일로 구성됨
    - `MainActivity.java`
        - 동적 실행 파일
    - `activity_main.xml`
        - 레이아웃 파일
- 하나의 화면에 하나의 액티비티만 노출시킬 수 있으므로
  다양한 기능과 다양한 화면 출력에는 한계가 있음
- 이러한 액티비티의 한계를 보완하기 위해
  **서브 액티비티**의 개념인 **프래그먼트**가 정의됨

### 2-2. 프래그먼트를 포함하는 안드로이드 프로젝트 구조

- 액티비티의 여러 프래그먼트를 관리하기 위해서는
  **프래그먼트 매니저**가 필요함
- 액티비티가 두 개의 프래그먼트를 가질 때
  액티비티의 전체적인 구조 안에서 프래그먼트들이 관리됨

### 2-3. 프래그먼트의 개념

- 프래그먼트는 하나의 액티비티를 분할하여
  개별적인 목적에 맞는 특정 기능을 수행함
- 스마트폰 화면의 일부 부분을 차지할 수 있음
- 하나의 액티비티를 출력하는 스마트폰 화면에서
  여러 프래그먼트들을 노출시킬 수 있음
- 이를 통해 사용자는 더욱 풍족한 사용자 인터페이스를 접할 수 있음

### 2-4. 프래그먼트의 특징

- 하나의 액티비티가 여러 개의 프래그먼트로 구성될 수 있음
- 프래그먼트는 스마트폰 화면에서 전체 또는 부분적으로 노출될 수 있음
- 하나의 프래그먼트는 다른 액티비티에서 재사용 가능함
- 프래그먼트는 자체적인 생애주기를 가짐
- 입력 이벤트 수신 및 액티비티 수행 중 추가·삭제가 가능함
- 프래그먼트의 생애주기는 결합된 액티비티의 생애주기에 종속됨
- 프래그먼트를 소유한 액티비티가 소멸되면 프래그먼트도 소멸됨

### 핵심 정리

- 프래그먼트는 하나의 액티비티를 여러 부분으로 나누어
  각 부분이 독립적인 기능과 UI를 담당하게 하는 구조임
- 액티비티보다 재사용성과 화면 구성 유연성이 높음
- 단, 프래그먼트는 항상 액티비티 안에서 관리됨

---

## 3. 프래그먼트 관리와 데이터 통신

### 3-1. 프래그먼트 매니저

- 프래그먼트 매니저는 액티비티와 프래그먼트 사이의
  통신 중계자 역할을 수행함
- 프래그먼트 트랜잭션을 통해
  프래그먼트의 추가·변경·삭제 기능을 제공함
- 프래그먼트도 액티비티와 마찬가지로
  레이아웃 파일과 Java 파일로 구성됨

### 3-2. 프래그먼트 매니저 코드 흐름

    manager = getSupportFragmentManager();
    ft = manager.beginTransaction();

### 코드 해석

- `getSupportFragmentManager()`
    - 프래그먼트를 관리하는 매니저 객체를 가져옴
- `beginTransaction()`
    - 프래그먼트에 대한 변경 작업을 시작함
- 프래그먼트 작업이 끝나면 `commit()`을 호출하여 변경 내용을 적용함

### 3-3. 프래그먼트 레이아웃과 Java 파일

- 프래그먼트 레이아웃은 프래그먼트의 사용자 인터페이스를 표현함
- 프래그먼트의 Java 파일은 `Fragment` 클래스를 상속하여 생성됨
- 프래그먼트는 `setContentView()` 메소드가 없음
- 따라서 `inflate()` 메소드를 통해
  View를 인플레이션하여 액티비티의 레이아웃에 출력함

### 3-4. 기본 Fragment 클래스 예시

    public class MainFragment extends Fragment {
        @Override
        public View onCreateView(LayoutInflater inflater,
                                 ViewGroup container,
                                 Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_main, container, false);
        }
    }

### 코드 해석

- `Fragment` 클래스를 상속하여 프래그먼트 클래스를 생성함
- `onCreateView()` 메소드는 프래그먼트의 화면을 생성할 때 호출됨
- `inflater.inflate(...)`
    - XML 레이아웃 파일을 View 객체로 변환함
- `R.layout.fragment_main`
    - 프래그먼트에 연결할 레이아웃 파일
- `container`
    - 프래그먼트가 담길 부모 `ViewGroup`
- `false`
    - 생성한 View를 즉시 부모에 붙이지 않도록 설정함

### 핵심 정리

- 프래그먼트는 Java 파일과 XML 레이아웃 파일로 구성됨
- 프래그먼트 화면 출력은 `setContentView()`가 아니라 `inflate()`를 사용함
- 프래그먼트의 추가·교체·삭제는 `FragmentManager`와 `FragmentTransaction`을 통해 처리함

---

## 4. 액티비티와 프래그먼트 비교

### 4-1. 개요

- 액티비티는 응용 프로그램의 단일 화면을 구성할 때 주로 사용되는 사용자 인터페이스 구성 요소임
- 하나 이상의 프래그먼트를 가질 수 있음
- 프래그먼트는 화면의 독립된 한 부분을 표현함
- 프래그먼트는 모듈화된 액티비티 설계를 가능하게 하는 액티비티의 한 부분임
- 프래그먼트는 고유한 레이아웃과 생명주기를 가지며,
  항상 액티비티에 의해 관리됨

### 4-2. 액티비티와 프래그먼트의 차이

| 구분       | 액티비티                                  | 프래그먼트                         |
|----------|---------------------------------------|-------------------------------|
| 역할       | 사용자와 상호작용할 수 있는 UI를 제공하는 응용 프로그램 구성요소 | 액티비티의 일부이며 액티비티에 부분적 UI를 제공   |
| 종속성      | 프래그먼트에 종속적이지 않고 독립적으로 수행 가능           | 액티비티에 종속적이며 독립적으로 관리될 수 있음    |
| 관리 방식    | 인텐트를 통해 관리됨                           | 프래그먼트 매니저를 통해 액티비티 안에서 관리됨    |
| 화면 구성    | 프래그먼트를 사용하지 않고는 멀티스크린 UI 구현이 제한적      | 여러 프래그먼트를 사용하여 다중 화면 UI 구성 가능 |
| 매니페스트 등록 | `AndroidManifest.xml`에 등록해야 함         | 매니페스트에 등록하지 않음                |
| 백 스택     | 시스템의 액티비티 백 스택에 의해 관리됨                | 프래그먼트 백 스택 관리는 개발자의 개입이 필요함   |
| 재사용성     | 재사용이 제한적                              | 재사용 가능                        |
| 교체       | 화면 전환 비용이 상대적으로 큼                     | 액티비티 내부에서 교체 가능               |

### 핵심 정리

- 액티비티는 앱의 큰 화면 단위임
- 프래그먼트는 액티비티 내부에서 재사용 가능한 작은 화면 단위임
- 프래그먼트는 액티비티의 일부이지만,
  고유한 레이아웃과 생명주기를 가짐

---

## 5. 프래그먼트의 생명주기

### 5-1. 프래그먼트 단계

- 프래그먼트는 전체적으로 세 가지 단계로 나눌 수 있음

1. 프래그먼트 초기 단계
    - 액티비티에 프래그먼트가 선언되고 초기화가 수행됨
2. 프래그먼트 실행 단계
    - 정의된 동작을 수행함
3. 프래그먼트 종료 단계
    - 프래그먼트의 동작을 완료하고 종료됨

### 5-2. 대표 생명주기 흐름

- 프래그먼트 추가
    - `onAttach()`
    - `onCreate()`
    - `onCreateView()`
    - `onActivityCreated()`
    - `onStart()`
    - `onResume()`
- 프래그먼트가 백 스택에 추가된 경우
    - `onPause()`
    - `onStop()`
    - `onDestroyView()`
- 사용자가 뒤로 돌아오는 경우
    - `onCreateView()`
    - `onActivityCreated()`
    - `onStart()`
    - `onResume()`
- 프래그먼트 종료
    - `onPause()`
    - `onStop()`
    - `onDestroyView()`
    - `onDestroy()`
    - `onDetach()`

### 5-3. 주요 생명주기 메소드

| 메소드                   | 설명                                |
|-----------------------|-----------------------------------|
| `onAttach()`          | 프래그먼트가 액티비티에 처음 연결될 때 호출됨         |
| `onCreate()`          | 프래그먼트를 생성할 때 호출되며 속성값을 초기화함       |
| `onCreateView()`      | 프래그먼트 자신의 View를 화면에 출력함           |
| `onActivityCreated()` | 부모 액티비티의 `onCreate()`가 종료된 후 실행됨  |
| `onStart()`           | 액티비티가 시작된 상태에 들어가면 호출됨            |
| `onResume()`          | 일시 정지 후 다시 재개되거나 활성 상태로 전환될 때 호출됨 |
| `onPause()`           | 화면이 중지되거나 사용자가 프래그먼트를 떠날 때 호출됨    |
| `onStop()`            | 다른 액티비티가 화면을 가려 화면에 보이지 않을 때 호출됨  |
| `onDestroyView()`     | 프래그먼트와 관련된 View가 제거됨              |
| `onDestroy()`         | 액티비티 또는 프래그먼트가 소멸될 때 호출됨          |
| `onDetach()`          | 프래그먼트가 액티비티로부터 해제될 때 호출됨          |

### 5-4. `onPause()`의 중요성

- `onPause()`는 사용자가 프래그먼트와 상호작용하지 않게 되는 경우 호출되는 첫 번째 메소드임
- 수행 중인 프래그먼트를 정지시킴
- 사용자가 해당 프래그먼트로 다시 돌아온다는 보장이 없으므로,
  이 시점에 보존해야 하는 데이터를 저장해야 함

### 핵심 정리

- 프래그먼트는 액티비티와 비슷한 생명주기를 가지지만,
  액티비티 내부에서 동작하므로 액티비티 생명주기에 종속됨
- `onAttach()`는 액티비티에 연결될 때 호출됨
- `onCreateView()`는 프래그먼트 UI를 생성하는 핵심 메소드임
- `onDetach()`는 액티비티로부터 분리될 때 호출됨

---

## 6. 프래그먼트 예제 1: 프래그먼트 교체

### 6-1. 예제 개요

- 두 개의 버튼을 통해 서로 다른 프래그먼트를 화면에 출력하는 예제임
- `FragmentFirst.java`와 `FragmentSecond.java`에 대한 레이아웃을 정의함
- 각 프래그먼트의 레이아웃을 호출하여
  사용자 인터페이스가 `MainActivity.java`의 `FrameLayout`을 통해 출력됨

### 6-2. `activity_main.xml` 구조

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <Button
            android:id="@+id/button1"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:onClick="showFragment"
            android:text="프래그먼트1" />

        <Button
            android:id="@+id/button2"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:onClick="showFragment"
            android:text="프래그먼트2" />

        <FrameLayout
            android:id="@+id/fragment_container"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="10"
            android:orientation="vertical" />

    </LinearLayout>

### 코드 해석

- `button1`
    - 프래그먼트1을 출력하기 위한 버튼
- `button2`
    - 프래그먼트2를 출력하기 위한 버튼
- `android:onClick="showFragment"`
    - 버튼 클릭 시 `showFragment()` 메소드를 호출함
- `FrameLayout`
    - 프래그먼트가 출력될 영역
- `fragment_container`
    - 프래그먼트를 교체하여 출력할 컨테이너 ID

### 6-3. `FragmentFirst.java`

    public class FragmentFirst extends Fragment {
        public View onCreateView(LayoutInflater inflater,
                                 ViewGroup container,
                                 Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_first, container, false);
        }
    }

### 6-4. `FragmentSecond.java`

    public class FragmentSecond extends Fragment {
        public View onCreateView(LayoutInflater inflater,
                                 ViewGroup container,
                                 Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_second, container, false);
        }
    }

### 코드 해석

- 두 프래그먼트 모두 `Fragment` 클래스를 상속함
- `onCreateView()`를 재정의하여 각자의 레이아웃을 화면에 출력함
- `inflate()`는 XML 레이아웃을 View 객체로 변환하는 역할을 함

### 6-5. `MainActivity.java`

    public class MainActivity extends AppCompatActivity {
        FragmentManager manager;
        FragmentTransaction ft;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            manager = getSupportFragmentManager();
            ft = manager.beginTransaction();
        }

        public void showFragment(View view) {
            ft = manager.beginTransaction();

            if (view == findViewById(R.id.button1)) {
                FragmentFirst fr1 = new FragmentFirst();
                ft.replace(R.id.fragment_container, fr1);
                ft.commit();
            } else {
                FragmentSecond fr2 = new FragmentSecond();
                ft.replace(R.id.fragment_container, fr2);
                ft.commit();
            }
        }
    }

### 코드 해석

- `FragmentManager manager`
    - 프래그먼트를 관리하기 위한 객체
- `FragmentTransaction ft`
    - 프래그먼트 변경 작업을 수행하기 위한 객체
- `getSupportFragmentManager()`
    - 프래그먼트 매니저 객체 생성
- `beginTransaction()`
    - 프래그먼트 트랜잭션 시작
- `replace(R.id.fragment_container, fr1)`
    - `fragment_container` 영역에 `FragmentFirst`를 출력함
- `replace(R.id.fragment_container, fr2)`
    - `fragment_container` 영역에 `FragmentSecond`를 출력함
- `commit()`
    - 변경 내용을 실제 화면에 적용함

### 핵심 정리

- 한 화면에 출력되는 프래그먼트 교체는 `FragmentTransaction`의 `replace()` 메소드를 통해 이루어짐
- `replace()`의 첫 번째 인자는 프래그먼트가 배치될 최상위 `ViewGroup`의 리소스 ID임
- 두 번째 인자는 교체하고자 하는 프래그먼트 객체임
- 화면에 반영하려면 반드시 `commit()`을 호출해야 함

---

## 7. 프래그먼트 통신 방법

### 7-1. 프래그먼트 간 통신의 기본 원칙

- 프래그먼트들은 서로 직접적으로 데이터 통신을 수행할 수 없음
- 반드시 액티비티를 통해 다른 프래그먼트와 통신을 수행해야 함

### 7-2. 안드로이드에서 프래그먼트 간 통신 방법

1. 인터페이스 기반 프래그먼트 통신
2. 프래그먼트 전용 요청 API 통신
3. 프래그먼트 간의 뷰 모델 통신

### 핵심 정리

- 프래그먼트끼리 직접 데이터를 주고받기보다,
  액티비티를 중간 통로로 삼거나 공식 통신 방식을 사용함
- 강의 예제에서는 인터페이스 기반 통신을 중심으로 다룸

---

## 8. 인터페이스 기반 프래그먼트 통신 예제

### 8-1. 예제 흐름

- `BottomFragment`에서 사용자가 메시지를 입력함
- 버튼을 클릭하면 `BottomFragment`의 인터페이스 메소드가 호출됨
- `MainActivity`가 해당 인터페이스를 구현하여 입력값을 전달받음
- `MainActivity`가 `TopFragment`의 `setText()` 메소드를 호출함
- `TopFragment`의 `TextView`에 입력한 메시지가 출력됨

### 흐름 정리

    BottomFragment
        → listener.BottomSender(input)
        → MainActivity의 BottomSender(input)
        → TopFragment의 setText(input)
        → TextView에 출력

### 8-2. `fragment_top.xml`

- 위쪽 프래그먼트 화면을 구성함
- `TextView`를 통해 전달받은 메시지를 출력함

  <TextView
  android:id="@+id/textView"
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:text="메시지 대기중" />

### 8-3. `fragment_bottom.xml`

- 아래쪽 프래그먼트 화면을 구성함
- `EditText`에 메시지를 입력하고,
  `Button`을 클릭하여 메시지를 전송함

  <EditText
  android:id="@+id/edit_text"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:layout_gravity="center"
  android:text="메시지를 작성하세요!" />

  <Button
  android:id="@+id/btn_send"
  android:layout_width="wrap_content"
  android:layout_height="wrap_content"
  android:text="메시지 보내기" />

### 8-4. `activity_main.xml`

- 위쪽에는 `TopFragment`가 출력될 영역을 지정함
- 아래쪽에는 `BottomFragment`가 출력될 영역을 지정함

  <FrameLayout
  android:id="@+id/TopFrame"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:layout_weight="0.5" />

  <FrameLayout
  android:id="@+id/BottomFrame"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
  android:layout_weight="0.5" />

### 코드 해석

- `TopFrame`
    - `TopFragment`가 배치될 영역
- `BottomFrame`
    - `BottomFragment`가 배치될 영역
- 두 개의 `FrameLayout`을 선언하여
  상단과 하단 프래그먼트를 각각 출력함

### 8-5. `TopFragment.java`

    public class TopFragment extends Fragment {
        @Override
        public View onCreateView(LayoutInflater inflater,
                                 ViewGroup container,
                                 Bundle savedInstanceState) {
            return inflater.inflate(R.layout.fragment_top, container, false);
        }

        public void setText(CharSequence text) {
            TextView tv = (TextView) getView().findViewById(R.id.textView);
            tv.setText(text);
        }
    }

### 코드 해석

- `onCreateView()`
    - `fragment_top.xml` 레이아웃을 화면에 출력함
- `setText(CharSequence text)`
    - 전달받은 문자열을 `TextView`에 출력함
- `getView().findViewById(R.id.textView)`
    - 프래그먼트 내부의 `TextView`를 찾음

### 8-6. `BottomFragment.java`

    public class BottomFragment extends Fragment {
        private BottomListener listener;
        private EditText editText;
        private Button sendButton;

        public interface BottomListener {
            void BottomSender(CharSequence input);
        }

        public View onCreateView(LayoutInflater inflater,
                                 ViewGroup container,
                                 Bundle savedInstanceState) {
            View v = inflater.inflate(R.layout.fragment_bottom, container, false);

            editText = v.findViewById(R.id.edit_text);
            sendButton = v.findViewById(R.id.btn_send);

            sendButton.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    CharSequence input = editText.getText();
                    listener.BottomSender(input);
                }
            });

            return v;
        }

        @Override
        public void onAttach(Context context) {
            super.onAttach(context);

            if (context instanceof BottomListener) {
                listener = (BottomListener) context;
            } else {
                throw new RuntimeException(context.toString()
                        + " must implement FragmentListener");
            }
        }

        @Override
        public void onDetach() {
            super.onDetach();
            listener = null;
        }
    }

### 코드 해석

- `BottomListener`
    - `BottomFragment`에서 `MainActivity`로 데이터를 전달하기 위한 인터페이스
- `BottomSender(CharSequence input)`
    - 입력한 문자열을 전달하는 메소드
- `editText.getText()`
    - 사용자가 입력한 문자열을 가져옴
- `listener.BottomSender(input)`
    - 액티비티에 입력값 전달
- `onAttach(Context context)`
    - 프래그먼트가 액티비티에 연결될 때 호출됨
    - 액티비티가 `BottomListener`를 구현했는지 확인함
- `onDetach()`
    - 프래그먼트가 액티비티에서 분리될 때 호출됨
    - `listener`를 `null`로 초기화함

### 8-7. `MainActivity.java`

    public class MainActivity extends AppCompatActivity
            implements BottomFragment.BottomListener {

        TopFragment top;
        BottomFragment bottom;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            top = new TopFragment();
            bottom = new BottomFragment();

            getSupportFragmentManager().beginTransaction()
                    .replace(R.id.TopFrame, top)
                    .replace(R.id.BottomFrame, bottom)
                    .commit();
        }

        @Override
        public void BottomSender(CharSequence input) {
            top.setText(input);
        }
    }

### 코드 해석

- `implements BottomFragment.BottomListener`
    - `MainActivity`가 `BottomFragment`의 인터페이스를 구현함
- `top = new TopFragment()`
    - 위쪽 프래그먼트 객체 생성
- `bottom = new BottomFragment()`
    - 아래쪽 프래그먼트 객체 생성
- `replace(R.id.TopFrame, top)`
    - 상단 영역에 `TopFragment` 출력
- `replace(R.id.BottomFrame, bottom)`
    - 하단 영역에 `BottomFragment` 출력
- `BottomSender(CharSequence input)`
    - `BottomFragment`에서 전달받은 메시지를 받음
- `top.setText(input)`
    - 전달받은 메시지를 `TopFragment`에 출력함

### 핵심 정리

- 프래그먼트 간 직접 통신은 하지 않음
- `BottomFragment` → `MainActivity` → `TopFragment` 순서로 데이터를 전달함
- 인터페이스는 프래그먼트가 액티비티에 데이터를 전달하는 통로 역할을 함

---

## 9. 정리하기

### 9-1. 프래그먼트

- 하나의 액티비티를 분할하여
  개별적인 목적에 맞는 특정 기능을 수행함
- 스마트폰 화면의 일부 부분을 차지함

### 9-2. 프래그먼트 레이아웃

- 프래그먼트의 사용자 인터페이스를 표현함

### 9-3. 프래그먼트의 생명주기

- 프래그먼트 초기 단계
- 프래그먼트 실행 단계
- 프래그먼트 종료 단계

### 9-4. 프래그먼트 매니저

- 액티비티의 여러 프래그먼트를 관리함

---

## 10. 핵심 요약

### 10-1. 프래그먼트를 쓰는 이유

- 하나의 액티비티 안에서 여러 UI 영역을 구성할 수 있음
- 화면 일부를 재사용 가능한 단위로 분리할 수 있음
- 태블릿, 스마트폰 등 다양한 화면 크기에 유연하게 대응할 수 있음
- 액티비티의 한계를 보완할 수 있음

### 10-2. 꼭 기억할 객체

| 객체                    | 역할                               |
|-----------------------|----------------------------------|
| `Fragment`            | 액티비티 안에서 독립적인 UI와 기능을 담당하는 화면 조각 |
| `FragmentManager`     | 여러 프래그먼트를 관리하는 객체                |
| `FragmentTransaction` | 프래그먼트 추가·교체·삭제 작업을 수행하는 객체       |
| `LayoutInflater`      | XML 레이아웃을 View 객체로 변환하는 객체       |
| `FrameLayout`         | 프래그먼트가 배치될 컨테이너 역할               |
| `onCreateView()`      | 프래그먼트의 UI를 생성하는 핵심 메소드           |

### 10-3. 프래그먼트 교체 흐름

1. `FragmentManager` 객체 생성
2. `beginTransaction()`으로 트랜잭션 시작
3. `replace()`로 컨테이너에 프래그먼트 배치 또는 교체
4. `commit()`으로 화면에 반영

### 10-4. 프래그먼트 통신 흐름

1. `BottomFragment`에서 입력값 생성
2. 인터페이스 메소드 호출
3. `MainActivity`가 값을 전달받음
4. `MainActivity`가 `TopFragment`의 메소드 호출
5. `TopFragment`가 화면에 값 출력

---

## 11. 연습문제 정리

### Q1. 프래그먼트 매니저에 대한 설명으로 틀린 것은?

1. 액티비티와 프래그먼트 사이의 통신 중계자 역할을 수행한다.
2. 프래그먼트 트랜잭션을 통해 프래그먼트의 추가·변경·삭제에 대한 기능을 제공한다.
3. 액티비티를 통해 모듈화된 프래그먼트의 설계가 가능하게 하고, 액티비티는 프래그먼트의 일부이다.
4. 프래그먼트도 액티비티와 마찬가지로 레이아웃 파일과 Java 파일로 구성된다.

- 정답: **3**

#### 해설

- 프래그먼트는 액티비티의 일부로 포함되는 구조임
- 따라서 “액티비티는 프래그먼트의 일부이다”라는 설명은 반대로 되어 있어 틀림

---

### Q2. 프래그먼트가 액티비티에서 선언될 때 호출되는 메소드는 무엇인가?

1. `void onAttach()`
2. `onCreate()`
3. `onCreateView()`
4. `onDetach()`

- 정답: **1**

#### 해설

- `onAttach()`는 프래그먼트가 액티비티에 처음 연결될 때 호출되는 메소드임
- 프래그먼트가 액티비티에 선언되어 사용되기 시작하는 가장 초기 단계에 해당함

---

### Q3. 프래그먼트의 통신에 포함되지 않는 것은?

1. 인터페이스 기반 프래그먼트 통신
2. 프래그먼트 전용 요청 API 통신
3. 프래그먼트 간의 뷰 모델 통신
4. 프래그먼트 간의 콜백 메소드 통신

- 정답: **4**

#### 해설

- 강의에서 제시한 프래그먼트 간 통신 방법은 다음 3가지임
    - 인터페이스 기반 프래그먼트 통신
    - 프래그먼트 전용 요청 API 통신
    - 프래그먼트 간의 뷰 모델 통신
- `프래그먼트 간의 콜백 메소드 통신`은 공식 분류에 포함되지 않음

---

## 12. 시험 직전 체크포인트

- 프래그먼트는 액티비티의 일부이다.
- 프래그먼트는 화면의 일부를 차지하며 특정 기능을 수행한다.
- 프래그먼트는 액티비티 안에서 재사용 가능한 UI 단위이다.
- 프래그먼트는 고유한 레이아웃과 생명주기를 가진다.
- 프래그먼트는 액티비티의 생명주기에 종속된다.
- 프래그먼트의 UI 생성은 `onCreateView()`에서 수행한다.
- 프래그먼트 레이아웃은 `inflate()`를 통해 View 객체로 변환한다.
- 프래그먼트 관리는 `FragmentManager`가 담당한다.
- 프래그먼트 변경 작업은 `FragmentTransaction`으로 수행한다.
- 프래그먼트 교체는 `replace()`로 처리한다.
- 변경 사항을 화면에 적용하려면 `commit()`을 호출해야 한다.
- 프래그먼트끼리는 직접 통신하지 않고 액티비티를 통해 통신한다.
- 인터페이스 기반 통신은 `Fragment → Activity → Fragment` 흐름으로 이해하면 된다.