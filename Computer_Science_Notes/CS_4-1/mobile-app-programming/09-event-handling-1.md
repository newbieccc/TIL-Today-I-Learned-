# 모바일앱프로그래밍

## 09. 이벤트 처리

- 컴퓨터과학과 정광식 교수님

---

## 1. 이벤트 핸들러

### 1-1. 이벤트(Event)

- 이벤트는 사용자가 앱과 상호작용하거나, 시스템/앱 내부에서 어떤 일이 발생했을 때 앱에 전달되는 신호임
- 예:
    - 화면 터치
    - 키 입력
    - 화면 회전
    - 알림 수신

### 1-2. 이벤트 핸들러(Event Handler)

- 이벤트 핸들러는 사용자의 반응이나 시스템 구성요소에서 발생한 이벤트를 처리하는 주체임
- 특정 이벤트가 발생하면 이를 탐지하고, 그에 맞는 기능을 실행함

### 1-3. 안드로이드의 대표적인 이벤트 처리 방법 4가지

1. `View`를 통한 콜백 메소드의 구현
2. 클래스를 통한 이벤트 리스너 인터페이스의 구현
3. 액티비티를 통한 이벤트 리스너 인터페이스의 구현
4. `View`를 통한 이벤트 리스너 인터페이스의 구현

---

## 2. View를 통한 콜백 메소드의 구현

### 2-1. 콜백 메소드

- 콜백 메소드는 특정 이벤트가 발생했을 때 안드로이드 프레임워크에 의해 자동으로 호출되는 메소드임
- 개발자가 해당 메소드를 재정의해 두면, 이벤트 발생 시 자동 실행됨

### 2-2. 특징

- 사용자와 상호작용하는 주체인 `View`에서 구현됨
- 터치, 키 입력, 포커스 변화 등의 이벤트에 대응 가능함
- 이벤트 정보는 메소드의 인수로 전달됨

### 2-3. 주요 콜백 메소드

| 콜백 메소드                                                                             | 설명               |
|------------------------------------------------------------------------------------|------------------|
| `boolean onTouchEvent(MotionEvent event)`                                          | 화면 터치 시 호출       |
| `boolean onKeyDown(int keyCode, KeyEvent event)`                                   | 키를 눌렀을 때 호출      |
| `boolean onKeyUp(int keyCode, KeyEvent event)`                                     | 키를 뗐을 때 호출       |
| `boolean onTrackballEvent(MotionEvent event)`                                      | 트랙볼 사용 시 호출      |
| `void onFocusChanged(boolean hasFocus, int direction, Rect previouslyFocusedRect)` | 포커스를 얻거나 잃을 때 호출 |

> `onKeyDown()` / `onKeyUp()` 설명은 헷갈리기 쉬우므로 구분해서 기억하기

### 2-4. 예제

    public class MainActivity extends Activity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            View vw = new MyView(this);
            setContentView(vw);
        }
    }

    class MyView extends View {
        public MyView(Context context) {
            super(context);
        }

        public boolean onTouchEvent(MotionEvent event) {
            super.onTouchEvent(event);

            if (event.getAction() == MotionEvent.ACTION_DOWN) {
                Toast.makeText(MainActivity.this, "Touch Event Received", Toast.LENGTH_SHORT).show();
                return true;
            }
            return false;
        }
    }

### 2-5. 예제 해석

- `MyView`는 `View`를 상속한 사용자 정의 View임
- `onCreate()`에서 `MyView` 객체를 생성해 화면에 설정함
- `onTouchEvent(MotionEvent event)`를 재정의해 터치 이벤트를 처리함
- `MotionEvent.ACTION_DOWN`은 화면을 누른 순간의 이벤트임
- `return true`
    - 이벤트를 처리했음을 의미함
- `return false`
    - 이벤트를 처리하지 않았음을 의미함

### 2-6. 핵심 정리

- 콜백 메소드는 프레임워크가 자동 호출함
- 이벤트 발생 시 실행할 동작을 미리 정의해 두는 방식임
- `MotionEvent` 객체에는 터치 종류와 좌표 정보가 들어 있음

---

## 3. 클래스를 통한 이벤트 리스너 인터페이스의 구현

### 3-1. 이벤트 리스너(Event Listener)

- 특정 이벤트를 처리하는 인터페이스임
- 이벤트가 발생할 때까지 대기하다가, 해당 이벤트에 맞는 콜백 메소드를 수행함
- 보통 `View` 내부 인터페이스 형태로 제공됨

### 3-2. 특징

- `View`의 콜백 메소드보다 더 범용적으로 사용 가능함
- `View`를 상속받지 않아도 됨
- 별도의 클래스를 만들어 리스너 인터페이스를 구현함

### 3-3. 대표적인 이벤트 리스너

| 이벤트 리스너                      | 콜백 메소드                                               | 설명                |
|------------------------------|------------------------------------------------------|-------------------|
| `View.OnTouchListener`       | `boolean onTouch(View v, MotionEvent event)`         | 화면 터치 시 호출        |
| `View.OnKeyListener`         | `boolean onKey(View v, int keyCode, KeyEvent event)` | 키를 누르거나 뗄 때 호출    |
| `View.OnClickListener`       | `void onClick(View v)`                               | View 클릭 시 호출      |
| `View.OnLongClickListener`   | `boolean onLongClick(View v)`                        | View를 길게 클릭할 때 호출 |
| `View.OnFocusChangeListener` | `void onFocusChange(View v, boolean hasFocus)`       | 포커스 변경 시 호출       |
| `View.OnDragListener`        | `boolean onDrag(View v, DragEvent event)`            | 드래그 시 호출          |

### 3-4. 예제

    public class MainActivity extends Activity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            View vw = new View(this);
            vw.setOnTouchListener(TouchListener);
            setContentView(vw);
        }
    }

    class TouchListenerClass implements View.OnTouchListener {
        public boolean onTouch(View v, MotionEvent event) {
            if (event.getAction() == MotionEvent.ACTION_DOWN) {
                Toast.makeText(MainActivity.this, "Touch Event Received",
                        Toast.LENGTH_SHORT).show();
                return true;
            }
            return false;
        }
    }

    TouchListenerClass TouchListener = new TouchListenerClass();

### 3-5. 예제 해석

- `TouchListenerClass`가 `View.OnTouchListener`를 구현함
- `onTouch()` 메소드를 재정의해 터치 이벤트를 처리함
- `setOnTouchListener()`로 `View`에 이벤트 리스너를 등록함
- 장점:
    - 다양한 이벤트를 범용적으로 처리 가능
- 단점:
    - View가 많아지면 클래스 수가 늘어나 코드가 복잡해질 수 있음

### 3-6. 핵심 정리

- 이벤트 리스너 인터페이스는 틀만 제공함
- 실제 이벤트 처리를 위해서는 별도의 구현 클래스와 객체가 필요함

---

## 4. 액티비티를 통한 이벤트 리스너 인터페이스의 구현

### 4-1. 개요

- 별도의 리스너 클래스를 만들지 않고, 액티비티가 직접 인터페이스를 구현하는 방식임
- 안드로이드 프로젝트에는 최소 1개의 액티비티가 존재하므로 활용하기 쉬움
- 자바에서는 클래스는 하나만 상속할 수 있지만, 인터페이스는 여러 개 구현할 수 있음

### 4-2. 특징

- 별도의 리스너 클래스가 필요 없어 코드가 간결함
- 리스너 객체를 따로 생성하지 않아도 됨
- 단, View가 액티비티에 종속적이어서 재사용성은 떨어질 수 있음

### 4-3. 예제

    public class MainActivity extends Activity implements View.OnTouchListener {

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            View vw = new View(this);
            vw.setOnTouchListener(this);
            setContentView(vw);
        }

        public boolean onTouch(View v, MotionEvent event) {
            if (event.getAction() == MotionEvent.ACTION_DOWN) {
                Toast.makeText(this, "Touch Event Received", Toast.LENGTH_SHORT).show();
                return true;
            }
            return false;
        }
    }

### 4-4. 핵심 정리

- 액티비티 선언부에서 `implements View.OnTouchListener` 작성
- 클래스 내부에서 `onTouch()`를 구현
- `setOnTouchListener(this)`로 현재 액티비티를 리스너로 등록함
- 코드가 단순하지만, 액티비티 의존성이 커짐

---

## 5. View를 통한 이벤트 리스너 인터페이스의 구현

### 5-1. 개요

- `View` 클래스를 선언하는 부분에서 필요한 이벤트 리스너 인터페이스를 구현하는 방식임
- 액티비티가 아닌 `View` 쪽에서 이벤트 리스너를 구현함

### 5-2. 특징

- 액티비티에 직접 종속되지 않음
- 클래스 재사용 면에서 유리함
- `View`를 통한 콜백 메소드 구현과 비슷해 보이지만, 사용 메소드가 다름

### 5-3. 구분

- 콜백 메소드 방식: `onTouchEvent()`
- 이벤트 리스너 방식: `onTouch()`

### 5-4. 핵심 정리

- 터치 이벤트가 발생하면 `View`에 등록된 이벤트 리스너를 찾아 `onTouch()`를 호출함
- 재사용성 측면에서는 액티비티 구현 방식보다 유리함

---

## 6. 이벤트 핸들러 우선순위

### 6-1. 개요

- 하나의 `View`에 여러 이벤트 처리 방식이 중복 구현되면, 사전에 정해진 우선순위에 따라 호출 순서가 결정됨

### 6-2. 일반적인 우선순위

1. `View`의 이벤트 리스너
2. `View`의 콜백 메소드
3. 액티비티의 콜백 메소드

### 6-3. 핵심 원리

- 내부에 더 가까운 쪽(안쪽 범위일수록) 우선순위가 높음
- 각 이벤트 핸들러의 반환값에 따라 다음 단계 호출 여부가 결정됨

### 6-4. 반환값 의미

- `return true`
    - 현재 단계에서 이벤트를 처리 완료함
    - 다음 우선순위의 핸들러는 호출되지 않음
- `return false`
    - 현재 단계에서 이벤트를 처리하지 못함
    - 다음 우선순위의 핸들러가 호출됨

### 6-5. 예제 상황 정리

- 이벤트 리스너의 `onTouch()`에서 `true`를 반환하면 처리 종료
- 이벤트 리스너가 `false`를 반환하면 `View`의 `onTouchEvent()`가 호출될 수 있음
- `View`도 `false`를 반환하면 액티비티의 `onTouchEvent()`까지 전달될 수 있음
- `return true`를 모두 제거하면 여러 `Toast`가 순서대로 출력될 수 있음

### 6-6. 안드로이드의 이벤트 종류

| 이벤트 속성       | 설명                     |
|--------------|------------------------|
| 터치 이벤트       | 스마트폰 화면을 손가락으로 터치할 때   |
| 키 이벤트        | 키패드/하드웨어 버튼을 누를 때      |
| 제스처 이벤트      | 터치 중 일정 패턴으로 움직일 때     |
| 포커스 이벤트      | View 객체가 포커스를 받거나 잃을 때 |
| 화면 방향 감지 이벤트 | 화면 방향(가로/세로)이 바뀔 때     |

---

## 7. 안드로이드 프레임워크의 구조

### 7-1. 개요

- 안드로이드 프레임워크는 다양한 기기와 폼 팩터에서 사용될 수 있도록 만들어진 리눅스 기반 오픈 소스 소프트웨어 스택임

### 7-2. 주요 계층

1. 시스템 앱
2. JAVA API 프레임워크
3. 네이티브 C/C++ 라이브러리
4. 안드로이드 런타임
5. Hardware Abstraction Layer(HAL)
6. Linux 커널

---

## 8. 시스템 앱

### 개요

- 사용자를 위한 기본 앱 또는 개발자가 접근 가능한 기본 구성 앱을 의미함

### 예시

- 캘린더
- 전화번호부
- 구글 맵
- 웹 브라우저
- 이메일
- SMS 프로그램

### 핵심 정리

- 기본 시스템 앱 위에 개발자가 만든 앱이 추가되며 앱 생태계를 구성함

---

## 9. JAVA API 프레임워크

### 개요

- 앱 개발에 필요한 클래스와 메소드를 JAVA API 형태로 제공하는 계층임
- 안드로이드의 핵심 시스템 구성요소와 서비스를 재사용할 수 있게 해 줌
- 개발의 단순성과 재사용성을 높여 줌

### 주요 구성 예시

- Content Providers
- View System
- Managers
    - Activity Manager
    - Location Manager
    - Package Manager
    - Resource Manager
    - Notification Manager
    - Telephony Manager
    - Window Manager

### 주요 구성 요소 설명

- **View System**
    - 목록, 그리드, 텍스트 상자, 버튼, 웹 브라우저 등을 포함한 UI 구성에 사용됨
- **Resource Manager**
    - 문자열, 그래픽, 레이아웃 파일 등 코드 외 리소스에 접근하게 해 줌
- **Notification Manager**
    - 상태 표시줄에 사용자 정의 알림을 표시할 수 있게 해 줌

### 한 줄 정리

- JAVA API 프레임워크는 안드로이드 앱 개발에 필요한 기능을 API 형태로 제공하는 핵심 계층이다.

---

## 10. 네이티브 C/C++ 라이브러리

### 개요

- 안드로이드의 많은 핵심 구성요소와 서비스는 C/C++ 기반으로 작성되어 있음
- JAVA 프레임워크 API를 통해 앱에서 네이티브 라이브러리 기능을 사용할 수 있음

### 예시

- BIONIC
- WebKit
- AudioManager
- 미디어 라이브러리
- SurfaceManager
- SGL
- 3D 라이브러리
- SQLite
- FreeType
- LibWebCore
- Media Framework

### 한 줄 정리

- 네이티브 C/C++ 라이브러리는 안드로이드의 핵심 기능을 저수준에서 지원하는 기반 계층이다.

---

## 11. 안드로이드 런타임

### 개요

- 앱 프로세스를 관리하고 앱 실행 환경을 제공하는 계층임
- 초기에는 달빅(Dalvik) 가상머신을 사용했음
- 달빅은 배터리 소모, CPU/메모리 점유율 문제 등이 있었음
- 안드로이드 5.0부터는 ART(Android Runtime)를 사용함

### 구성 요소

- Android Runtime (ART)
- Core Libraries

### 한 줄 정리

- 안드로이드 런타임은 앱이 실행될 수 있도록 환경을 제공하는 계층이다.

---

## 12. HAL(Hardware Abstraction Layer)

### 개요

- JAVA API 프레임워크에 기기 하드웨어 기능을 노출하는 표준 인터페이스를 제공함
- 카메라, 블루투스 등 하드웨어별 인터페이스를 구현함

### 예시

- Audio
- Bluetooth
- Camera
- Sensors

### 한 줄 정리

- HAL은 안드로이드 프레임워크와 실제 하드웨어 사이를 연결하는 표준 인터페이스 계층이다.

---

## 13. Linux 커널

### 개요

- 안드로이드 프레임워크 최하단에 위치함
- 시스템 자원 관리 역할을 수행함
- 모놀리식 커널 형태를 가짐

### 주요 기능

- 메모리 관리
- 프로세스 관리
- 네트워크 관리
- 드라이버 관리

### 그림 속 예시 구성

- Audio
- Binder (IPC)
- Display
- keypad
- Bluetooth
- Camera
- Shared Memory
- USB
- WiFi
- Power Management

### 한 줄 정리

- Linux 커널은 안드로이드 시스템의 최하단에서 하드웨어와 자원을 직접 관리하는 핵심 계층이다.

---

## 14. 핵심 용어 정리

### 1) 콜백(Callback)

- 특정 이벤트가 발생했을 때 시스템에 의해 자동으로 호출되는 메소드

### 2) 리스너(Listener)

- 특정 이벤트를 처리하는 인터페이스

### 3) 이벤트(Event)

- 앱에서 발생하는 하나의 행위 또는 변화
- 예:
    - 클릭
    - 터치
    - 값 변경

### 4) 핸들러(Handler)

- 전달된 메시지나 이벤트를 받아 처리하는 주체

---

## 15. 연습문제

### Q1. 안드로이드에서 이벤트를 처리하는 방법으로 옳지 않은 것은?

1. 콜백 메소드의 재정의
2. 리스너 인터페이스의 구현
3. 매니페스트를 통한 재정의
4. 액티비티를 통한 리스너의 구현

- 정답: **3**
- 이유:
    - 매니페스트 파일은 액티비티 등록, 권한 선언 등 앱 구성 정보를 적는 곳임
    - 버튼 클릭, 터치 등의 이벤트 처리는 보통 코드에서 수행함

### Q2. 리스너에 대한 설명으로 옳은 것은?

1. 콜백 발생 여부를 기다리고 있는 객체이다.
2. 리스너는 특정 이벤트를 처리하는 인터페이스이다.
3. 대응되는 이벤트를 받는 여러 개의 메소드가 선언되어 있다.
4. 모두 View 클래스의 상속을 받은 추상 메소드로 선언되어 있다.

- 정답: **2**
- 이유:
    - 리스너는 특정 이벤트를 처리하는 인터페이스임
    - 항상 여러 개의 메소드를 가지는 것은 아님
    - View 상속 구조로만 제한되지 않음

### Q3. 액티비티의 리스너 구현에 대한 설명으로 옳은 것은?

1. MainActivity 클래스를 상속받는다.
2. 본체에서 인터페이스를 상속받는다.
3. 선언문에서 핸들러 메소드를 구현하기만 하면 된다.
4. 인터페이스는 개수에 상관없이 얼마든지 구현할 수 있다.

- 정답: **4**
- 이유:
    - 자바에서는 클래스는 하나만 상속 가능하지만 인터페이스는 여러 개 구현 가능함
