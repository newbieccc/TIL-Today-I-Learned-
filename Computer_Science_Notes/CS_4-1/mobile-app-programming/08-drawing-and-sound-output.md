# 모바일앱프로그래밍

## 08. 도형 및 소리 출력

- 컴퓨터과학과 정광식 교수님

---

# 1. 도형 출력 1

## CustomView

### 개요

- `Canvas`는 액티비티가 실행되는 화면에서 도형을 그리기 위한 도화지 역할을 함
- `Canvas`는 `View` 클래스 내부에 정의되어 있기 때문에 `View` 또는 `View`의 파생 클래스를 상속받고, `onMeasure()`, `onDraw()` 메소드를 재정의하여 도형을 그릴 수 있음
- 이러한 방식을 `CustomView를 정의하여 사용한다`고 표현함

## CustomView를 구현한 예제 (`MainActivity.java`)

### 예제 코드

    public class MainActivity extends Activity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);

            TestView tv = new TestView(this);
            setContentView(tv);
        }
    }

### 예제 설명

- `onCreate()`에서 `TestView` 객체를 생성함
- `setContentView(tv)`를 호출하여 XML 레이아웃 대신 직접 만든 `CustomView`를 화면에 출력함
- 즉, 사용자 정의 View를 액티비티의 메인 화면으로 설정한 예제임

## CustomView 동작 설명

- (프로그램 8.1)에서 `MainActivity`의 `onCreate()`에서는 하나의 `TestView` 객체를 생성하고, 이 `TestView`를 `setContentView()`의 인수로 전달하여
  `MainActivity`의 화면을 채우는 실행 순서를 가짐
- 기존에는 `setContentView()`의 인수를 `R.layout.activity_main`으로 지정하였음
- 화면에 그리기를 수행할 때 `onDraw()`(콜백 메소드)를 호출하며, 그리기에 필요한 `Canvas` 클래스의 객체인 `canvas`가 인수로 전달됨

## onDraw 예제 설명

- `canvas`의 `drawColor()` 메소드를 통해 View의 전체 색을 밝은 파랑(`CYAN`)색으로 설정하고, `drawRect()` 메소드를 통해 직사각형을 그림
- `Paint` 클래스의 객체인 `Pnt`는 `canvas`에 그리는 도형의 특징을 정의하기 위해 사용됨

### 화면에 보이는 코드

    public void onDraw(Canvas canvas) {
        canvas.drawColor(Color.CYAN);

        Paint Pnt = new Paint();
        Pnt.setColor(Color.RED);

        canvas.drawRect(120, 100, 320, 500, Pnt);
    }

## Canvas 객체

### 개요

- `Canvas` 객체는 `Canvas` 기능을 구현하기 위한 객체로 화면 위에 다양한 그림을 그리는 메소드를 지원함
- `Canvas` 객체는 시스템이 초기화하며 `View`의 `onDraw()` 함수에 인수로 전달됨

### 주요 메소드

- `void drawPoint(float x, float y, Paint paint)`
- `void drawLine(float startX, float startY, float stopX, float stopY, Paint paint)`
- `void drawCircle(float cx, float cy, float radius, Paint paint)`
- `void drawRect(float left, float top, float right, float bottom, Paint paint)`
- `void drawText(String text, float x, float y, Paint paint)`

### 설명

- 각각의 메소드들은 영어 이름으로부터 기능을 짐작할 수 있음
- 예를 들어 `drawRect()` 메소드는 직사각형(rectangle)을 그리는 기능을 제공함

## Canvas 객체 예제

### Canvas 객체를 활용하는 예제 (`CanvasView.java`)

    public void onDraw(Canvas canvas) {
        canvas.drawColor(Color.LTGRAY);

        Paint Pnt = new Paint();
        Pnt.setStrokeWidth(30f);

        // 빨간색 사각형
        Pnt.setColor(Color.RED);
        canvas.drawRect(10, 10, 200, 400, Pnt);

        // 파란색 반투명 원
        Pnt.setColor(0x800000ff);
        canvas.drawCircle(350, 550, 250, Pnt);
    }

### 예제 설명

- `canvas.drawColor(Color.LTGRAY)`로 배경색을 연한 회색으로 설정함
- `Paint` 객체 `Pnt`를 생성하고 `setStrokeWidth(30f)`로 선 두께를 설정함
- 빨간색으로 사각형을 그림
- 반투명 파란색으로 원을 그림
- 현재 스크린샷에 보이는 부분만 기준으로 정리함

## Canvas 객체 예제 설명

- (프로그램 8.2)를 보면 생성된 `Pnt` 객체의 `Color` 속성을 빨간색으로 정의하고, 좌표 `(10, 10, 200, 400)`에 직사각형을 그림(`canvas.drawRect`)
- 좌표 `(350, 550, 250)`에 원을 그림(`canvas.drawCircle`)
- `Pnt` 객체를 검은색으로 변경하고(`Pnt.setColor(Color.BLACK)`), 좌표 `(30, 30)`에 검은색 점을 그림(`canvas.drawPoint`)

---

# 2. 도형 출력 2

## Paint 객체

### 개요

- `Paint` 객체는 그리기에 대한 속성 정보를 가지는 객체이며 `Canvas` 객체의 도형 그리기 메소드에 인수로 전달됨
- 화면에 그려지는 도형의 색상, 선의 굵기에 대한 속성값을 `Paint` 객체를 이용하여 지정함
- `new` 연산자로 `Paint` 객체를 생성하면 디폴트 속성을 가지고 생성되며, 속성을 지정하는 메소드를 이용하여 각각의 속성을 원하는 속성값으로 지정할 수 있음

## setAntiAlias 메소드

- 색상의 차이가 뚜렷한 경계 부분에 중간색을 삽입하거나 도형이나 글꼴이 주변 배경과 잘 어울리도록 하는 기법으로, Boolean 유형의 속성값을 가짐

## setColor 메소드

- 도형의 색을 지정하는 메소드임
- 속성값으로 16진수 색상 코드 또는 색상명으로 구성된 상수를 지정할 수 있음

### setColor 메소드의 속성 예

- `Pnt.setColor(Color.RED);`
    - 빨간색으로 그려진다.
- `Pnt.setColor(Color.GREEN);`
    - 초록색으로 그려진다.
- `Pnt.setColor(Color.YELLOW);`
    - 노란색으로 그려진다.

## getColor 메소드

- 현재 설정된 색상을 조회할 때 사용함
- 16진수로 설정된 색상값을 반환하므로 비트 연산을 통해 각 요소를 분리할 수 있음
- 색상에 대해 별다른 지정을 하지 않으면 디폴트 색상인 검은색으로 그려짐

## setStrokeCap 메소드

- 선 끝 모양을 지정하는 데 사용됨

### setStrokeCap 메소드의 속성

| 속성값      | 설명                           |
|----------|------------------------------|
| `BUTT`   | 지정된 좌표에서 선이 끝난다.             |
| `ROUND`  | 둥근 모양으로 끝이 장식된다.             |
| `SQUARE` | 사각형 모양이며 지정한 좌표보다 조금 더 그어진다. |

## setStrokeWidth 메소드

- 도형의 테두리 선이나 직선의 굵기를 지정하는 데 사용됨
- 속성값으로 `float` 형태의 실수값을 가짐

## setStyle 메소드

- 사각형이나 원처럼 내부가 채워진 도형을 그릴 때 외곽선의 모양을 결정함

### setStyle 메소드의 속성

| 속성값               | 설명                    |
|-------------------|-----------------------|
| `FILL`            | 채우기만 하며 외곽선은 그리지 않는다. |
| `FILL_AND_STROKE` | 채우기도 하고 외곽선도 그린다.     |
| `STROKE`          | 채우지는 않고 외곽선만 그린다.     |

## setStrokeJoin 메소드

- 도형을 구성하는 두 선이 만나는 모서리를 표현하는 방식을 결정함

### setStrokeJoin 메소드의 속성

| 속성값                | 설명                                |
|--------------------|-----------------------------------|
| `Paint.Join.MITER` | 두 선이 만나는 곳의 외부 모서리가 날카로운 각도를 가진다. |
| `Paint.Join.BEVEL` | 두 선이 만나는 곳의 외부 모서리가 굽는 각도를 가진다.   |
| `Paint.Join.ROUND` | 두 선이 만나는 곳의 외부 모서리가 둥근 형태로 표현된다.  |

## Paint 활용 예제

### Paint 객체를 활용하는 예제 (`MainActivity.java`) 설명

- 캡 모양이 다른 2개의 빨간 선과 모서리 모양이 다른 3개의 사각형을 출력하는 예제임
- 스타일이 다른 5개의 원을 출력해 봄으로써 스타일 속성에 따른 차이를 확인할 수 있음

---

# 3. 메시지 알림

## Toast 객체

### 개요

- `Toast` 객체는 화면에 일시적으로 나타나는 작은 팝업(pop-up)으로 사용자에게 간단한 피드백 메시지를 제공함
- `Toast`는 안드로이드 플랫폼 내부에서 발생한 이벤트를 사용자에게 알려 줄 때 유용하게 사용됨
- `Toast` 객체가 출력되어도 기존의 실행 중인 액티비티의 작업은 그대로 실행됨
- 하지만 사용자에게 일방적으로 정보를 알려 주기 때문에 사용자의 상호작용에 대해 반응하지 않고 포커스도 갖지 않음

## Toast 표시 문자열 정의

- `Toast` 객체는 `makeText()` 메소드를 통해 내부에 표시되는 문자열을 정의하며, 컨텍스트, 표시할 문자열, 메시지 표시 시간(`LENGTH_SHORT`, `LENGTH_LONG`) 등의 인수를 가짐

### makeText 예제

    makeText(MainActivity.this, "Short Time Message", Toast.LENGTH_SHORT)

- `makeText(콘텍스트, 리소스 ID, 출력 시간)`
- `makeText(콘텍스트, 텍스트, 출력 시간)`

## Toast 프로젝트 예제 (`MainActivity.java`)

### 화면에 보이는 코드

    public class MainActivity extends Activity {
        Toast mToast = null;
        int count;
        String str;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            findViewById(R.id.shortmsg).setOnClickListener(mClickListener);
            findViewById(R.id.longmsg).setOnClickListener(mClickListener);
        }
    }

### 예제 설명

- `Toast` 객체 `mToast`를 선언하고 `count`, `str` 변수를 함께 정의함
- `onCreate()`에서 `activity_main` 레이아웃을 화면에 설정함
- `shortmsg`, `longmsg` 버튼에 각각 `mClickListener`를 연결하여 버튼 클릭 시 Toast 메시지가 출력되도록 구성한 예제임
- 스크린샷에 보이는 부분만 기준으로 정리함

---

# 4. 소리 알림

## 소리 알림 개요

### SoundPool 객체

- 버튼 클릭음, 알림음, 게임 효과음 등과 같은 짧은 소리를 발생함

### AudioManager 객체

- 시스템 오디오를 제어하거나 관리하는 관리자로서 오디오 상태, 볼륨, 포커스를 관리함

## SoundPool 객체

- 안드로이드에서 지원하는 소리 파일(`wav`, `mp3`, `ogg` 등)의 소리 알림을 위해 사용되는 객체
- 재생하고자 하는 소리 파일은 프로젝트의 `res/raw` 폴더에 저장하고 JAVA 코드에서 참조하여 사용함
- `raw` 폴더는 프로젝트를 생성할 때 자동으로 생성되지 않으므로 `raw` 폴더를 먼저 만든 후 소리 파일을 복사해 놓아야 함
- `raw` 폴더에 소리 파일을 저장하면 AAPT가 자동으로 `R.java` 파일에 소리 파일명으로 ID를 등록함

### SoundPool 객체 상세 정보

#### SoundPool 객체 생성자

    SoundPool(1, AudioManager.STREAM_MUSIC, 0);

- `SoundPool(스트림 개수, 스트림 타입, 음질, 0(Default));`

#### load 메소드

    mPool.load(this, R.raw.bgm, 1);

- `load(Context, 파일 리소스 ID, 우선순위(priority))`

#### play 메소드

    mPool.play(mDing, 1, 1, 0, 0, 1);

- `play(사운드 ID, 왼쪽 볼륨, 오른쪽 볼륨, 우선순위, 반복횟수, 재생속도);`

## AudioManager 객체

- 출력 장비와 오디오를 관리하는 객체
- 별도의 효과음(사운드) 파일을 준비하지 않고도 시스템에서 제공하는 오디오 파일을 사용할 수 있는 장점이 있음

### 객체 생성자

- 객체 생성자는 안드로이드 프레임워크에서 제공되는 시스템 레벨의 서비스 핸들을 생성함

#### AudioManager 객체 생성자

    (AudioManager)getSystemService(AUDIO_SERVICE);

### playSoundEffect 메소드

    mAm.playSoundEffect(AudioManager.FX_KEYPRESS_STANDARD);

- `playSoundEffect(효과음 종류(정수형))`

## 소리 알림 예제 (`activity_main.xml`)

### 화면에 보이는 코드

    <LinearLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:id="@+id/beep1"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="SoundPool" />

        <Button
            android:id="@+id/beep2"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="AudioManager" />

    </LinearLayout>

### 예제 설명

- `LinearLayout`을 루트 레이아웃으로 사용
- `orientation`은 `vertical`로 설정
- 첫 번째 버튼 `beep1`은 `SoundPool` 실행용
- 두 번째 버튼 `beep2`는 `AudioManager` 실행용
- 현재 스크린샷에 보이는 부분만 기준으로 정리함

## 소리 알림 예제 (`MainActivity.java`) 준비 코드

### 화면에 보이는 코드

    public class MainActivity extends Activity {
        SoundPool mPool;
        int mDing;
        AudioManager mAm;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            mPool = new SoundPool(1, AudioManager.STREAM_MUSIC, 0);
            mDing = mPool.load(this, R.raw.bgm, 1);

            mAm = (AudioManager)getSystemService(AUDIO_SERVICE);

            findViewById(R.id.beep1).setOnClickListener(mClickListener);
            findViewById(R.id.beep2).setOnClickListener(mClickListener);
        }
    }

### 예제 설명

- `SoundPool` 객체 `mPool`을 생성함
- `load()` 메소드로 `R.raw.bgm` 사운드 파일을 로드하고 `mDing`에 저장함
- `AudioManager` 객체 `mAm`을 `getSystemService(AUDIO_SERVICE)`로 얻음
- `beep1`, `beep2` 버튼에 클릭 리스너를 연결하여 소리 알림이 실행되도록 구성함
- 현재 스크린샷에 보이는 부분만 기준으로 정리함

## 소리 알림 예제 (`MainActivity.java`) 클릭 이벤트 처리

### 화면에 보이는 코드

    Button.OnClickListener mClickListener = new Button.OnClickListener() {
        public void onClick(View v) {
            MediaPlayer player;

            switch(v.getId()) {
                case R.id.beep1:
                    mPool.play(mDing, 1, 1, 0, 0, 1);
                    break;

                case R.id.beep2:
                    mAm.playSoundEffect(AudioManager.FX_KEYPRESS_STANDARD);
                    break;
            }
        }
    };

### 예제 설명

- 버튼 클릭 이벤트를 처리하기 위해 `mClickListener`를 정의함
- `switch(v.getId())`로 클릭된 버튼의 ID를 구분함

#### `R.id.beep1`인 경우

- `mPool.play(mDing, 1, 1, 0, 0, 1)`을 호출하여 `SoundPool`로 사운드를 재생함

#### `R.id.beep2`인 경우

- `mAm.playSoundEffect(AudioManager.FX_KEYPRESS_STANDARD)`를 호출하여 시스템 효과음을 재생함

## 소리 알림 예제 (`MainActivity.java`) 설명

- (프로그램 8.7)은 두 개의 소리를 각기 다른 두 가지 방법으로 출력하는 예제임
- 첫 번째 방법(`SoundPool`)은 `SoundPool` 객체의 `load()` 메소드를 이용하여 미리 준비된 음원 파일을 재생함
- 두 번째 방법(`AudioManager`)은 `AudioManager` 객체의 `playSoundEffect()` 메소드를 사용하여 시스템에서 제공하는 소리를 재생함

---

#### 정리하기

1. Canvas
    - 뷰의 그리기 표면이며 이 위에 그림을 그림

2. Antialiasing
    - 이미지의 외곽선이 곡선으로 된 경우, 계단식 모서리가 나타나는데, 이것을 부드럽게 만들어 곡선으로 보이게 하는 렌더링 기술

3. AudioManager 객체
    - 출력 장비와 오디오를 관리하는 역할을 하며, 별도의 효과음 파일을 준비하지 않고도 시스템에서 제공하는 오디오 파일을 사용할 수 있다는 장점이 있음

---

# 연습문제

## Q1. Canvas에 대한 설명으로 옳지 않은 것은?

### 정답

- 3

### 이유

- `기본적으로 도형을 그리는 메소드로 선과 점은 제외된다.`는 틀린 설명임
- `Canvas`는 선과 점도 그릴 수 있음
    - `drawLine()` : 선 그리기
    - `drawPoint()` : 점 그리기

### 보기 정리

- `뷰의 그리기 표면이며 이 위에 그림을 그린다.`
    - 맞는 설명
- `시스템이 초기화되어 뷰의 onDraw 인수로 전달한다.`
    - 맞는 설명
- `기본적으로 도형을 그리는 메소드로 선과 점은 제외된다.`
    - 틀린 설명
- `별도로 생성할 필요없이 전달받은 인수를 사용하기만 하면 된다.`
    - 맞는 설명

## Q2. AntiAlias에 대한 설명으로 옳은 것은?

### 정답

2. 도형이나 글꼴이 주변 배경과 부드럽게 어울리도록 하는 기법

### 이유

- `AntiAlias`는 도형, 텍스트, 선, 곡선 등의 경계를 부드럽게 만들어 배경과 자연스럽게 연결하는 기법임

### 오답 정리

1. `도형의 색상을 반전시켜 주는 기법`
    - AntiAlias와 무관함

2. `도형이나 글꼴이 주변 배경과 부드럽게 어울리도록 하는 기법`
    - 맞는 설명

3. `뚜렷한 경계 부근에 어두운색을 삽입하여 경계가 안보이도록 하는 기법`
    - AntiAlias와 무관함

4. `글꼴에는 해당이 되지 않으나 도형일 경우에는 계단현상을 해결해주는 기법`
    - 틀린 설명
    - AntiAlias는 글꼴에도 적용됨
