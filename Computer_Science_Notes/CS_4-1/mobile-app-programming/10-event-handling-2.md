# 모바일앱프로그래밍

## 10. 이벤트 처리 2

- 컴퓨터과학과 정광식 교수님

---

# 1. 터치 입력

## 1-1. 개요

- 사용자가 레이아웃(화면)을 터치하면서 발생하는 **사용자 이벤트**를 처리하는 방법
- 사용자 이벤트는 **사용자와의 직접적인 상호작용**과 **JAVA 프로그램의 동적인 기능 수행**을 통해 처리됨
- 안드로이드 앱에서는 사용자 이벤트에 대하여 사전에 사용자가 정의한 함수를 호출하고 실행할 수 있음
- 사용자 이벤트가 발생한 지점의 좌표 정보는 `MotionEvent` 객체에 포함되어 수집·활용할 수 있음

## 1-2. 참고

- 이벤트는
    - 사용자가 앱과 상호작용(터치, 키 입력 등)하거나
    - 시스템/앱 내부에서 어떤 일(화면 회전, 알림 수신 등)이 발생했을 때
    - 앱에 알려주는 신호(발생 사실)임

## 1-3. 이벤트 처리 방식

- 이벤트 처리 방식에는 다음 2가지가 있음
    - **콜백 메소드를 정의하는 방식**
    - **이벤트 리스너의 핸들러로 처리하는 방식**
- 터치 이벤트와 관련된 대표적인 함수는 다음 2가지임

  Boolean onTouchEvent(MotionEvent event)
  Boolean onTouch(View v, MotionEvent event)

### 정리

- `onTouchEvent(MotionEvent event)`
    - `View`의 콜백 메소드 방식에서 사용됨
- `onTouch(View v, MotionEvent event)`
    - 이벤트 리스너 방식에서 사용됨

## 1-4. 콜백 메소드

- **콜백 메소드**는 하나의 이벤트에 대한 정보만 가지는 데 비해
  **이벤트 리스너**는 여러 대상에 등록될 수 있음
- 여러 대상에 등록될 경우에는
  사용자 이벤트가 발생한 `View`의 ID를 전달받아
  사용자 이벤트의 발생 위치를 구분할 수 있음 (`R.java`)
- `MotionEvent` 객체의 `getAction()` 메소드는
  사용자의 행동(화면 터치 등)에 대한 정보를 알려주는 기능임
- 사용자가 터치한 부분의 좌표를 수집하는 기능을 구현할 때
  `MotionEvent` 객체를 활용할 수 있음

## 1-5. 프로그램 10.1 터치 기반의 그림판 예제 (`MainActivity.java`)

### 개요

- 터치 입력을 활용해 그림을 그리는 예제임
- `MainActivity` 내부에서 사용자 정의 `View`와 좌표 데이터를 관리하는 구조임
- 터치 좌표를 저장하기 위한 `Vertex` 클래스와 `ArrayList<Vertex>`가 사용됨

### 코드 1: 좌표 저장 구조

    public class MainActivity extends Activity {
        private MyView vw;

        public class Vertex {
            Vertex(float ax, float ay, boolean ad) {
                x = ax;
                y = ay;
                Draw = ad;
            }

            float x;
            float y;
            boolean Draw;
        }

        ArrayList<Vertex> arVertex;

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            vw = new MyView(this);
            setContentView(vw);
            arVertex = new ArrayList<Vertex>();
        }
    }

### 코드 해석

- `MyView`
    - 그림을 그리기 위한 사용자 정의 View
- `Vertex`
    - 터치 좌표와 그리기 여부를 저장하는 내부 클래스
- `x`, `y`
    - 터치한 위치의 좌표값
- `Draw`
    - 해당 좌표를 실제 그리기용으로 사용할지 여부를 저장하는 값
- `ArrayList<Vertex> arVertex`
    - 여러 터치 좌표를 순서대로 저장하는 리스트

### 코드 2: `MyView`와 `Paint` 초기화

    protected class MyView extends View {
        Paint Pnt;

        public MyView(Context context) {
            super(context);
            Pnt = new Paint();
            Pnt.setColor(Color.BLUE);
            Pnt.setStrokeWidth(3);
            Pnt.setAntiAlias(true);
        }
    }

### 코드 3: `onDraw()` 메소드

    public void onDraw(Canvas canvas) {
        int i;
        canvas.drawColor(Color.LTGRAY);

        for (i = 0; i < arVertex.size(); i++) {
            if (arVertex.get(i).Draw) {
                canvas.drawLine(arVertex.get(i-1).x, arVertex.get(i-1).y,
                                arVertex.get(i).x, arVertex.get(i).y, Pnt);
            }
        }
    }

### 코드 해석

- `Paint Pnt`
    - 선의 색상, 두께, 안티앨리어싱 등의 그리기 속성을 담당하는 객체
- `Pnt.setColor(Color.BLUE)`
    - 선 색상을 파란색으로 설정
- `Pnt.setStrokeWidth(3)`
    - 선 두께를 3으로 설정
- `Pnt.setAntiAlias(true)`
    - 선을 부드럽게 출력하도록 설정
- `canvas.drawColor(Color.LTGRAY)`
    - 배경색을 연한 회색으로 칠함
- `canvas.drawLine(...)`
    - 이전 좌표와 현재 좌표를 선으로 연결함

### 코드 4: `onTouchEvent(MotionEvent event)`

    public boolean onTouchEvent(MotionEvent event) {
        if (event.getAction() == MotionEvent.ACTION_DOWN) {
            arVertex.add(new Vertex(event.getX(), event.getY(), false));
            return true;
        }

        if (event.getAction() == MotionEvent.ACTION_MOVE) {
            arVertex.add(new Vertex(event.getX(), event.getY(), true));
            invalidate();
            return true;
        }

        return false;
    }

### 코드 해석

- `onTouchEvent(MotionEvent event)`
    - 터치 이벤트가 발생했을 때 호출되는 콜백 메소드
- `event.getAction()`
    - 현재 터치 동작의 종류를 확인함
- `MotionEvent.ACTION_DOWN`
    - 화면을 처음 눌렀을 때의 이벤트
- `MotionEvent.ACTION_MOVE`
    - 화면을 누른 상태에서 손가락을 움직일 때의 이벤트
- `invalidate()`
    - View를 다시 그리도록 요청함
    - 이 호출로 `onDraw()`가 다시 실행되어 선이 화면에 반영됨

### `Draw` 변수의 의미

- `Draw = true`
    - 이전 좌표와 **계속 연결해서 그림**
- `Draw = false`
    - 터치가 화면에서 떨어졌다가 다시 터치 후 이동이 시작되는 것을 의미함

### 핵심 정리

- `ACTION_DOWN`
    - 터치 시작 좌표 저장
- `ACTION_MOVE`
    - 이동 좌표 저장 + 화면 다시 그리기
- 즉, 손가락이 움직인 경로를 `arVertex`에 계속 저장하고
  `onDraw()`에서 점들을 선으로 연결해 그림판처럼 동작하게 만드는 구조임

---

# 2. 키보드 입력

## 2-1. `onKeyDown` 콜백 메소드

- 키보드 이벤트는 `onKeyDown` 콜백 메소드를 통해 처리함

  boolean onKeyDown(int keyCode, KeyEvent event)

- 사용자가 키보드를 누르면 포커스를 가진 `View`의 `onKeyDown()` 메소드가 호출됨
- `View` 클래스의 자식 클래스들은 `onKeyDown()` 메소드를 재정의하여 키 입력을 처리함

### 핵심 정리

- `onKeyDown()`
    - 키를 **누르는 순간** 호출되는 콜백 메소드
- 키보드 입력 처리는 포커스를 가진 `View`가 담당함

## 2-2. `KeyEvent` 객체

### 개요

- 키보드, 물리 버튼 등의 입력 이벤트 정보를 담고 있는 객체
- `KeyEvent` 객체의 `getKeyCode()` 메소드는 눌린 키코드(`keyCode` 인수)를 전달함
- 조합키의 상태나 이벤트 발생 시간 등을 조사하는 메소드도 제공됨

### 핵심 정리

- `KeyEvent`
    - 키 입력 관련 정보를 담는 객체
- `getKeyCode()`
    - 어떤 키가 눌렸는지 확인하는 메소드

## 2-3. 이동키 관련 `keyCode`

- 실제 `keyCode`는 정수로 예약되어 있으나,
  프로그래머의 사용 편의성을 위해 상수에 대응되어 있음

| 동작                    | 설명             |
|-----------------------|----------------|
| `KEYCODE_DPAD_LEFT`   | 왼쪽 이동          |
| `KEYCODE_DPAD_RIGHT`  | 오른쪽 이동         |
| `KEYCODE_DPAD_UP`     | 위쪽 이동          |
| `KEYCODE_DPAD_DOWN`   | 아래쪽 이동         |
| `KEYCODE_DPAD_CENTER` | 이동키 중앙의 Button |

## 2-4. 문자 관련 `keyCode`

| 동작                    | 설명          |
|-----------------------|-------------|
| `KEYCODE_A ~ Z`       | 알파벳 `A ~ Z` |
| `KEYCODE_0 ~ 9`       | 숫자 `0 ~ 9`  |
| `KEYCODE_CALL`        | 통화          |
| `KEYCODE_ENDCALL`     | 통화 종료       |
| `KEYCODE_HOME`        | 홈           |
| `KEYCODE_BACK`        | 뒤로          |
| `KEYCODE_VOLUME_UP`   | 볼륨 증가 버튼    |
| `KEYCODE_VOLUME_DOWN` | 볼륨 감소 버튼    |

### 핵심 정리

- 문자, 숫자, 기능 버튼도 모두 `keyCode` 상수로 구분됨
- 방향키뿐 아니라 홈, 뒤로가기, 통화, 볼륨 버튼도 `keyCode`로 처리 가능함

## 2-5. `getAction()` 메소드

- 키보드 터치 동작 `keyCode`는 키보드에 어떤 동작을 했는지를 나타내는 값임
- 세 가지 상수이며, `getAction()` 메소드의 반환값으로 사용됨

| 동작                | 설명                |
|-------------------|-------------------|
| `ACTION_DOWN`     | 키를 누른 상태          |
| `ACTION_UP`       | 키를 누른 후 뗀 상태      |
| `ACTION_MULTIPLE` | 동일한 키를 여러 번 누른 상태 |

### 핵심 정리

- `getAction()`
    - 키 입력이 어떤 형태로 발생했는지 확인하는 메소드

## 2-6. 키보드 입력 처리 예제 (`MainActivity.java`)

### 포커스 설정

- 키보드 입력을 처리하기 위해서는 `View`가 **포커스를 받을 수 있도록 설정**해야 함

  public class MainActivity extends Activity {
  private MyView vw;

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            vw = new MyView(this);
            vw.setFocusable(true);
            vw.setFocusableInTouchMode(true);
            setContentView(vw);
        }
  }

### 코드 해석

- `vw.setFocusable(true);`
    - 해당 View가 포커스를 받을 수 있도록 설정
- `vw.setFocusableInTouchMode(true);`
    - 터치 모드에서도 포커스를 받을 수 있도록 설정

### XML의 `focusable` 속성

    android:focusable="true"
    android:focusable="false"

## 2-7. 도형 이동 예제

### `MyView` 클래스

    protected class MyView extends View {
        float mX, mY, mR, mL;
        int mColor;

        public MyView(Context context) {
            super(context);
            mX = 500;
            mY = 500;
            mR = 600;
            mL = 600;
            mColor = Color.RED;
        }
    }

### `onDraw(Canvas canvas)`

    public void onDraw(Canvas canvas) {
        canvas.drawColor(Color.WHITE);
        Paint Pnt = new Paint();
        Pnt.setColor(mColor);
        Pnt.setAntiAlias(true);
        canvas.drawRect(mX, mY, mR, mL, Pnt);
    }

### `onKeyDown()` 메소드

    public boolean onKeyDown(int keyCode, KeyEvent event) {
        super.onKeyDown(keyCode, event);

        if (event.getAction() == KeyEvent.ACTION_DOWN) {
            switch (keyCode) {
                case KeyEvent.KEYCODE_DPAD_LEFT:
                    mX -= 5;
                    mR -= 5;
                    invalidate();
                    return true;

                case KeyEvent.KEYCODE_DPAD_RIGHT:
                    mX += 5;
                    mR += 5;
                    invalidate();
                    return true;

                case KeyEvent.KEYCODE_DPAD_UP:
                    mY -= 5;
                    mL -= 5;
                    invalidate();
                    return true;
            }
        }

        return false;
    }

### 코드 해석

- 방향키 입력에 따라 좌표값(`mX`, `mY`, `mR`, `mL`)을 변경함
- `invalidate()` 메소드는 화면을 갱신할 때 사용되며 `onDraw()` 메소드를 호출함
- 오른쪽, 위쪽, 아래쪽도 비슷한 방식으로 처리함

### 핵심 정리

- 키 입력 → 좌표값 변경 → `invalidate()` 호출 → `onDraw()` 재실행
- 즉, 키보드 입력에 따라 사각형 위치가 다시 그려지는 구조임

---

# 3. 위젯 이벤트

## 3-1. 개요

- 위젯도 `View`를 상속받기 때문에 다른 종류의 `View`들과 비교하여 이벤트를 처리하는 방법은 동일함
- 다수의 위젯에서 발생하는 이벤트를 한 번에 처리할 수 있도록 하는 것이 효율적임

## 3-2. Button 이벤트

### 개요

- `Button`은 위젯이며, 클래스를 바로 사용하는 것이 일반적인 방식이므로 추가적인 상속을 받지 않고 이벤트를 처리할 수 있어야 함
- `View.OnClickListener` 인터페이스를 구현하고, `onClick(View v)` 메소드 안에서 클릭 이벤트에 대한 처리 코드를 작성함
- 버튼으로 답을 하면 답을 텍스트로 출력하여 보여 주는 예제가 자주 사용됨

### 예제 1: `good` 버튼

    public class MainActivity extends AppCompatActivity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            Button btnGood = (Button) findViewById(R.id.good);
            btnGood.setOnClickListener(new Button.OnClickListener() {
                public void onClick(View v) {
                    TextView textPoll = (TextView) findViewById(R.id.question);
                    textPoll.setText("Good!!^^");
                }
            });
        }
    }

### 예제 2: `bad` 버튼

    Button btnBad = (Button) findViewById(R.id.bad);

    btnBad.setOnClickListener(new Button.OnClickListener() {
        public void onClick(View v) {
            TextView textPoll = (TextView) findViewById(R.id.question);
            textPoll.setText("Bad~ㅠㅠ");
        }
    });

### 코드 해석

- `findViewById()`
    - 버튼과 `TextView` 객체를 가져옴
- `setOnClickListener()`
    - 클릭 이벤트 리스너를 등록함
- `textPoll.setText(...)`
    - 버튼 클릭 시 텍스트 내용을 변경함

### 핵심 정리

- 버튼은 `findViewById()`로 객체를 참조함
- 클릭 이벤트는 `setOnClickListener()`로 연결함
- 클릭 시 `TextView`의 내용을 바꾸는 방식으로 결과를 화면에 표시할 수 있음

## 3-3. 리스너의 통합

### 예제

    public class MainActivity extends AppCompatActivity implements View.OnClickListener {

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            Button btnGood = (Button) findViewById(R.id.good);
            btnGood.setOnClickListener(this);

            Button btnBad = (Button) findViewById(R.id.bad);
            btnBad.setOnClickListener(this);
        }
    }

### 코드 해석

- `implements View.OnClickListener`
    - 액티비티가 클릭 이벤트 리스너를 직접 구현함
- `setOnClickListener(this)`
    - 현재 액티비티를 리스너로 등록함

### 핵심 정리

- 버튼마다 각각 리스너 객체를 새로 만들지 않고
  **하나의 리스너로 여러 버튼 이벤트를 처리**할 수 있음

---

# 4. 타이머 이벤트

## 4-1. 개요

- 안드로이드 플랫폼에서는 **특정 시간을 간격으로 함수를 주기적으로 실행하기 위한 타이머 이벤트**를 제공함
- 다른 이벤트와 달리 타이머 이벤트는 **프로그램이 이벤트를 실행**하며, **매개변수로 지정한 값에 따라 이벤트 발생 간격과 횟수**가 결정됨
- 예제에서는 **1초에 한 번씩 정수값을 증가시켜 `TextView`로 출력**함

### 핵심 정리

- 타이머 이벤트는 **일정 시간 간격마다 자동 실행되는 이벤트**임
- 사용자 입력이 아니라 **프로그램이 직접 발생시키는 이벤트**임

## 4-2. 프로그램 10.6 타이머 이벤트 처리 예제 (`MainActivity.java`)

    public class MainActivity extends AppCompatActivity {
        int value = 0;
        TextView mText;

        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.app_10_6);
            mText = (TextView) findViewById(R.id.text);
            mHandler.sendEmptyMessage(0);
        }

        Handler mHandler = new Handler() {
            public void handleMessage(Message msg) {
                value++;
                mText.setText("Timer Value = " + value);
                mHandler.sendEmptyMessageDelayed(0, 1000);
            }
        };
    }

### 코드 해석

- `mHandler.sendEmptyMessage(0);`
    - 핸들러에 첫 메시지를 보내 타이머 동작을 시작함
- `handleMessage(Message msg)`
    - 메시지를 받았을 때 실행되는 메소드
- `value++;`
    - 타이머 값을 1 증가시킴
- `mText.setText("Timer Value = " + value);`
    - 증가한 값을 `TextView`에 출력함
- `mHandler.sendEmptyMessageDelayed(0, 1000);`
    - 1초 후 다시 메시지를 보내 같은 작업을 반복함

### 핵심 흐름

1. `onCreate()`에서 화면과 `TextView`를 준비함
2. `sendEmptyMessage(0)`으로 첫 메시지를 보냄
3. `handleMessage()`가 실행됨
4. 값 증가 후 화면 갱신
5. `sendEmptyMessageDelayed(0, 1000)`으로 1초 뒤 다시 실행
6. 이 과정을 반복함

## 4-3. 프로그램 10.7 설명

- 핸들러는 스스로 자신에게 다시 메시지를 보내며,
  `sendEmptyMessageDelayed` 메소드로 **1초간의 지연 시간**을 둠
- `onCreate()` 메소드는 **시작만** 하며,
  이후에는 핸들러가 스스로를 **재호출**함으로써 계속 메시지를 받게 됨

### 핵심 정리

- 초기 시작은 `onCreate()`에서 하고,
- 반복 실행은 핸들러가 스스로 담당하는 구조임

---

# 5. 방향 이벤트

## 5-1. 안드로이드 플랫폼 센서 사용

- 안드로이드 플랫폼은 가속도, 회전, 조도 센서 등 다양한 종류의 센서를 다루기 위한 API를 제공함
- 이러한 센서 API를 이용하여 앱에 다양한 기능을 적용할 수 있음

## 5-2. 센서 사용을 위한 클래스 및 인터페이스

### (1) `SensorManager` 클래스

- 센서에 접근하게 해 줄 수 있는 메소드들을 제공함

### (2) `Sensor` 클래스

- `SensorManager` 클래스의 메소드를 활용해 접근하고자 하는 센서의 객체를 선언함

### (3) `SensorEventListener` 인터페이스

- 센서값이 변경되면 `SensorManager`를 통해 이벤트 형태로 변경된 센서값을 전달받을 수 있게 함

### (4) `SensorEvent` 클래스

- 센서에 대한 정보를 담고 있음
- 객체를 통해 센서값들을 획득할 수 있으며, 이를 통해 센서값에 접근할 수 있음

## 5-3. 안드로이드 센서 이용 과정

1. 센서 매니저 생성
2. 센서 객체 생성
3. 센서 리스너 등록
4. 센서값 획득

### 핵심 정리

- 센서 사용은 보통
  **매니저 준비 → 센서 객체 준비 → 리스너 등록 → 값 획득**
  순서로 이해하면 됨

## 5-4. 프로그램 10.8 방향 이벤트를 통한 화면 전환 예제 (`AndroidManifest.xml`)

    <activity
        android:name=".MainActivity"
        android:screenOrientation="portrait">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

### 코드 해석

- `android:screenOrientation="portrait"`
    - 화면 방향을 **세로(portrait)** 로 고정함
- `MAIN`
    - 앱의 메인 진입점
- `LAUNCHER`
    - 런처(앱 아이콘)에서 실행 가능한 액티비티

## 5-5. 프로그램 10.10 방향 이벤트를 통한 화면 전환 예제 (`MainActivity.java`)

### 코드 1: 리스너 준비

    public class MainActivity extends AppCompatActivity {
        OrientationEventListener mOrientationListener;
        TextView mDir;
        TextView mArrow;

        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            mDir = (TextView) findViewById(R.id.orientation);
            mArrow = (TextView) findViewById(R.id.arrow);

            mOrientationListener = new OrientationEventListener(this,
                    SensorManager.SENSOR_DELAY_NORMAL) {
            };
        }
    }

### 코드 2: 방향 변화 처리

    @Override
    public void onOrientationChanged(int orientation) {
        mDir.setText("회전 각: " + String.valueOf(orientation));

        if (orientation >= 315 || orientation < 45) {
            mArrow.setRotation(0);
        } else if (orientation >= 45 && orientation < 135) {
            mArrow.setRotation(270);
        } else if (orientation >= 135 && orientation < 225) {
            mArrow.setRotation(180);
        } else if (orientation >= 225 && orientation < 315) {
            mArrow.setRotation(90);
        }
    }

    mOrientationListener.enable();

### 코드 해석

- `OrientationEventListener`
    - 방향 변화를 감지하는 리스너 객체
- `mDir`
    - 현재 회전 각도를 출력하는 `TextView`
- `mArrow`
    - 방향 화살표를 표시하는 `TextView`
- `onOrientationChanged(int orientation)`
    - 기기의 방향 값이 바뀔 때 호출되는 메소드
- `mArrow.setRotation(...)`
    - 화살표를 회전시켜 방향을 시각적으로 표시함
- `mOrientationListener.enable();`
    - 방향 이벤트 리스너를 활성화함

### 각도 구간별 회전값

- `315 이상 또는 45 미만` → `0`
- `45 이상 135 미만` → `270`
- `135 이상 225 미만` → `180`
- `225 이상 315 미만` → `90`

### 설명 정리

- `onOrientationChanged()` 메소드는 **방향이 전환될 때** 호출됨
- `SensorManager`를 통해 방향 센서에 접근하여 스마트폰의 회전 상태를 나타내는 값을 전달받음
- 전달받은 값에 따라 두 `TextView`의 문자열 또는 회전 상태를 변경함
- `enable()` 메소드는 `OrientationEventListener`를 활성화하여 센서값을 모니터링함
- 이 예제는 `SensorEvent`가 아니라 `int`형 방향값을 직접 받아 처리하는 구조임

---

## 정리하기

1. **핸들러**
    - 다른 객체들이 보낸 메시지를 받고 이를 처리하는 객체임

2. **익명 클래스**
    - 일회용 객체를 한 번만 만들고 끝낼 때 사용함
    - 이벤트를 처리할 때 자주 사용함

3. **화면 터치 이벤트**
    - `boolean onTouchEvent(MotionEvent event)`
    - `boolean onTouch(View v, MotionEvent event)`
    - 콜백 메소드나 리스너의 핸들러를 이용하여 처리함

4. **키보드 입력 이벤트**
    - `boolean onKeyDown(int keyCode, KeyEvent event)`의 콜백 메소드가 처리함

5. **센서 사용을 위한 클래스 및 인터페이스**
    - `SensorManager`
        - 센서 접근 관련 메소드 제공
    - `Sensor`
        - 접근하려는 센서 객체 선언
    - `SensorEventListener`
        - 센서값 변경 이벤트를 전달받기 위한 인터페이스
    - `SensorEvent`
        - 센서 정보를 담고 센서값에 접근할 수 있게 해 주는 객체

---

## 연습문제

### Q1. `getAction` 메소드에 해당하지 않는 것은?

1. `ACTION_UP` : 키를 뗐다.
2. `ACTION_DOWN` : 키를 눌렀다.
3. `ACTION_CANCEL` : 키 입력을 취소한다.
4. `ACTION_MULTIPLE` : 같은 키를 여러 번 눌렀다.

- 정답: **3**
- 이유:
    - `ACTION_CANCEL`은 `KeyEvent.getAction()`의 값이 아님

### Q2. 다음 중 화면 터치 이벤트 처리를 위한 리스너의 핸들러 메소드는?

1. `onTouchEvent`
2. `onTouch`
3. `get_ACTION`
4. `get_MotionEvent`

- 정답: **2**
- 이유:
    - 터치 이벤트 리스너는 `View.OnTouchListener`
    - 그 안의 핸들러 메소드는 `onTouch()`임

### Q3. 다음 중 `KeyCode`에 대한 설명으로 옳은 것은?

1. `KEYCODE_DPAD_LEFT` : 왼쪽 이동키
2. `KEYCODE_DPAD_RIGHT` : 아래쪽 이동키
3. `KEYCODE_DPAD_UP` : 오른쪽 이동키
4. `KEYCODE_DPAD_DOWN` : 위쪽 이동키

- 정답: **1**
- 이유:
    - `KEYCODE_DPAD_LEFT`는 왼쪽 방향키를 의미함
