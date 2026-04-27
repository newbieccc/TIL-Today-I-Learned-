# 모바일앱프로그래밍

## 11. Activity와 인텐트

- 컴퓨터과학과 정광식 교수님

---

# 0. 학습 목차

1. Activity 1
2. 인텐트 1
3. Activity 2
4. 인텐트 2

---

## 1. Activity

### 개요

- 현재까지는 각 예제마다 하나의 앱에 `Activity`를 만들었는데,
  각 예제의 화면 하나가 바로 `Activity`임
- 즉, `Activity`는 **사용자와 상호작용할 수 있는 일종의 통로**라고 생각할 수 있음

### 주요 안드로이드 앱 컴포넌트

| 컴포넌트                | 설명                                            |
|---------------------|-----------------------------------------------|
| `Activity`          | 하나의 스마트폰 화면을 관리하는 컴포넌트                        |
| `Service`           | 화면 없이 백그라운드에서 독립적으로 동작하는 컴포넌트                 |
| `BroadcastReceiver` | 안드로이드 플랫폼에서 발생하는 다양한 이벤트를 수신하고 처리하는 컴포넌트      |
| `ContentProvider`   | 데이터를 체계적으로 관리하고 앱이 활용할 수 있도록 인터페이스를 제공하는 컴포넌트 |

## 2. Activity의 특징

- `Activity`는 사용자의 인터페이스를 구성하지만,
  그 자체에는 **출력 기능이 없음**
- 따라서 직접적으로 보이지 않고 **통로 역할**만 함
- 안드로이드는 멀티태스킹을 지원하므로 여러 개의 앱을 동시에 실행할 수 있음

## 3. 앱의 구성

- 앱은 다음 4개의 주요 컴포넌트로 구성됨
    - `Activity`
    - `ContentProvider`
    - `BroadcastReceiver`
    - `Service`

### `Activity`

- 사용자가 앱과 상호작용을 수행하는 가장 기본적인 주요 컴포넌트

### `ContentProvider`

- 앱 계층과 데이터 계층 간의 매개체 역할을 수행함
- 앱은 `ContentProvider`를 통해 데이터를 얻어올 수 있음
- 예:
    - 오디오
    - 이미지
    - 주소록 접근 등

### `BroadcastReceiver`

- 안드로이드 플랫폼에서 특정 이벤트가 발생했을 때,
  앱에서 수신 및 처리를 수행하는 컴포넌트
- 예:
    - 배터리 부족
    - 문자 수신 등

### `Service`

- 사용자에게 노출되지 않으면서
  백그라운드에서 작업을 수행하는 컴포넌트
- 예:
    - 백그라운드 음악 재생 등

## 4. Activity의 제약적인 부분

- 데스크톱 환경과 달리 스마트폰은 자원이 넉넉하지 않으므로 여러 가지 제약이 발생함
- 많은 앱을 동시에 실행하기에는 메모리 크기로 인한 무리가 있음
- 화면이 좁기 때문에 여러 개의 앱을 중첩시켜 보여 줄 수 없으며,
  한 번에 하나의 앱만 보이는 구조임

## 5. Activity와 View

- `Activity` 자체는 사용자에게 보이는 수단이 아니라,
  안드로이드 앱을 관리하기 위한 단위임
- 사용자에게 실제로 보이는 것은 `View`임
- `Activity`는 반드시 내부에 `View`나 `ViewGroup`을 가져야 함
- `Activity`가 생성될 때마다 호출되는 `setContentView()` 메소드가
  `Activity` 안에 `View`를 화면에 출력하는 기능을 함

### 핵심 정리

- `Activity`
    - 화면을 관리하는 단위
- `View`
    - 사용자에게 실제로 보이는 UI 요소
- `setContentView()`
    - `Activity` 안에 화면으로 보여 줄 `View` 또는 레이아웃을 설정하는 메소드

## 6. 앱과 Activity

- 실제 앱이 수행될 때는 한 화면에서 복잡한 동작을 모두 수행할 수 없으므로,
  기능별로 나누어 앱의 작업을 실행할 수 있는 여러 개의 `Activity`가 필요함
- 여러 개의 `Activity` 간에 여러 가지 데이터를 공유하기 위한 통신이 필요할 수 있음

---

# 2. 생명주기

## 1. 생명주기 개요

- 여러 개의 앱을 동시에 실행할 수 있지만,
  사용자 눈에 보이고 직접 사용하는 앱은 일반적으로 하나임
- 사용자는 스마트폰에서 실행 중인 앱들을 활성화함으로써 교대로 실행할 수 있음
- `Activity`의 생명주기(lifecycle)는
  `Activity`가 다음 상태들을 순환하는 것을 의미함

  시작 → 실행 → 활성 → 비활성화 → 정지 → 종료

## 2. Activity 상태 변화

- 사용자의 선택이나 안드로이드 플랫폼의 자원 사정에 따라
  `Activity`의 상태는 끊임없이 바뀜
- 안드로이드 플랫폼은 태스크를 실행 중인 `Activity`들을
  스택(stack)으로 관리함

## 3. 실행 상태(active, running)

- 사용자에게 보이며 사용자가 직접 사용하는 상태
- 스택의 제일 위에 있으며 화면에서도 제일 위에 출력됨
- 입력 포커스를 가지고 사용자의 입력을 직접 처리함
- 사용자가 앱의 `Activity`를 보면서 상호작용 중인 상태

## 4. 일시정지 상태(pause)

- 화면에 다른 `Activity`가 있지만,
  화면 전체를 다 가리지 않았거나 반투명한 상태임
- 실행 상태와 비슷하지만 안드로이드 플랫폼에 의해 강제 종료될 수도 있음
- 예:
    - 카카오톡 채팅 중 알림, 메시지, 사진 접근 등으로 포커스를 잃은 상태

## 5. 정지 상태(stopped)

- 다른 `Activity`에 의해 완전히 가려진 상태이며,
  사용자에게 보이지 않는 상태임
- 모든 정보를 유지하고 있으므로 언제든지 다시 활성화될 수 있음
- 안드로이드 플랫폼은 메모리가 부족하면
  정지 상태의 `Activity`를 언제든지 강제 종료할 수 있음
- 예:
    - 카카오톡 대화창에서 URL 접속으로 인터넷 웹 브라우저 화면이 전면에 보이는 경우
    - 홈 버튼을 눌러 카카오톡을 나간 경우

### 핵심 정리

- `Activity`는 보이는 상태, 일부 보이는 상태, 완전히 가려진 상태에 따라 생명주기가 달라짐
- 안드로이드는 제한된 메모리 환경 때문에
  사용하지 않는 `Activity`를 강제로 종료할 수 있음
- `Activity` 상태는 스택 구조와 밀접하게 관련됨

---

## 1. 인텐트(Intent)

### 개요

- 인텐트(`Intent`)는 여러 개의 `Activity`로 구성된 앱에서
  `Activity`들 사이의 통신을 위해 필요한 **통신 장치** 또는 **메시지 전달 방법**을 의미함
- 인텐트는 `Activity`뿐만 아니라
  `BroadcastReceiver`, `Service`, `ContentProvider` 등 주요 컴포넌트들이
  수행해야 할 작업에 대한 정보를 가지며,
  작업 결과를 반환하기 위해서도 사용됨

### 예시

- 예 1:
    - 그림을 보여 주는 `Activity`를 호출해야 한다면,
      출력해야 할 그림이 무엇인지 함께 알려 주어야 함
    - 이런 상황에서 인텐트를 사용함
- 예 2:
    - 입력을 받는 `Activity`를 호출한 경우,
      사용자가 입력한 정보가 무엇인지 반환해야 함
    - 이런 상황에서도 인텐트가 사용됨

### 핵심 정리

- 인텐트는 함수의 인수나 반환값과 비슷한 역할을 함
- 다른 컴포넌트를 호출할 때 필요한 정보와 작업 요청을 담는 객체임

## 2. 인텐트 생성자

### 개요

- 인텐트 생성자는 현재 `Activity`에서 다른 `Activity`를 호출할 때 사용되는 인텐트의 생성자임
- 자주 사용되는 인텐트 생성자는 크게 두 가지가 있음

  Intent(Context packageContext, Class<?> cls)
    Intent(String action, Uri uri, Context packageContext, Class<?> cls)

### 내부 서브 Activity 호출용 생성자

    Intent(Context packageContext, Class<?> cls)

- 내부의 서브 `Activity`를 호출할 때 주로 사용됨
- `Activity` 클래스를 구현하는 `Context`와
  호출될 `Activity`의 클래스 정보(`Class`)가 인수로 전달됨
- `Context`는 호출자의 정보이며, 주로 `this`를 사용함
- 호출될 `Activity`의 클래스(`cls`)는 호출되는 `Activity`의 클래스 정보임
- 실행 중에 `Activity`를 생성하려면 호출할 클래스 정보가 필요함

## 3. 인텐트를 통한 Activity 호출: `startActivity()`

### 개요

- 인텐트 생성자를 통해 새로운 인텐트를 생성했으면,
  `Activity`를 호출하기 위해 `startActivity()` 메소드를 호출해야 함
- 인텐트는 단지 `Activity`를 실행하기 위한 정보만 가지고 있음
- 실제로 `Activity`를 실행시키는 것은 `startActivity()` 메소드가 담당함

### 기본 예시

    Intent intent = new Intent(MainActivity.this, SubActivity.class);
    startActivity(intent);

### 코드 해석

- `MainActivity.this`
    - 호출자, 즉 현재 `MainActivity` 자신을 의미함
- `SubActivity.class`
    - 호출할 대상 `Activity`의 클래스 정보
- `startActivity(intent)`
    - 생성된 인텐트를 이용해 `SubActivity`를 호출함

## 4. 명시적 인텐트

### 개요

- 명시적 인텐트는 호출할 대상 컴포넌트가 분명한 인텐트임
- 호출할 `Activity`의 이름을 분명히 알고 있기 때문에 사용할 수 있음

### 예시

    Intent searchIntent = new Intent(MainActivity.this, SearchService.class);
    searchIntent.setData(Uri.parse(mapUrl));
    startService(searchIntent);

### 핵심 정리

- 명시적 인텐트는 실행할 컴포넌트를 정확히 지정함
- 같은 앱 내부의 특정 `Activity`나 `Service`를 호출할 때 주로 사용됨

## 5. 암시적 인텐트

### 개요

- 명시적 인텐트와 달리 호출 대상이 분명히 정해지지 않은 인텐트를
  암시적 인텐트(implicit intent)라고 함
- 주로 다른 앱의 컴포넌트를 호출할 때 사용됨
- 다른 앱의 내부 코드를 보지 않는 이상 호출할 대상의 분명한 이름을 알 수 없기 때문임

### 동작 방식

- 안드로이드 플랫폼은 인텐트의 정보를 참조하여
  호출될 적절한 컴포넌트를 검색함
- 설치된 모든 앱의 컴포넌트를 조사하여
  최적의 호출 대상을 결정함
- 홈 화면 런처, 다이얼러 등의 호출은 모두 암시적 인텐트를 통해 이루어짐

### 암시적 인텐트 예시

- URL을 통해 구글 홈페이지를 띄우는 예제

  Intent intent =
  new Intent(Intent.ACTION_VIEW, Uri.parse("http://www.google.com/"));
  startActivity(intent);

### 핵심 정리

- 명시적 인텐트
    - 호출할 컴포넌트를 직접 지정함
- 암시적 인텐트
    - 수행할 작업과 데이터만 지정하고,
      실제 실행 대상은 안드로이드 플랫폼이 결정함

## 6. Activity 예제 1

### `activity_main.xml`

- `callactivity.xml(activity_main.xml)`을 작성하여 레이아웃을 정의함
- `MainActivity`에서 `SubActivity`를 호출하기 위해 버튼을 하나 생성함
- `MainActivity`라는 것을 표시하기 위한 문자열을 배치함
- 버튼의 `android:onClick="mOnClick"` 속성을 이용하여
  클릭 이벤트만 예외적으로 XML 파일에서 `onClick` 속성으로 정의할 수 있음

### XML 예시 구조

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Main Activity"
        android:textColor="#0000FF"
        android:textSize="25sp"
        android:typeface="serif" />

    <Button
        android:id="@+id/CALL"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="mOnClick"
        android:text="CALL" />

### `subactivity_main.xml`

- `Sub Activity` 화면을 구성하는 레이아웃임
- `TextView`에 `"Sub Activity"`라는 문자열을 표시함
- `Button`에 `android:onClick="mOnClick"` 속성을 지정함
- 버튼 텍스트는 `"CLOSE"`로 설정함

### XML 예시 구조

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Sub Activity"
        android:textColor="#FF5500"
        android:textSize="25sp"
        android:typeface="serif" />

    <Button
        android:id="@+id/CLOSE"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="mOnClick"
        android:text="CLOSE" />

---

## 1. 서브 액티비티 호출

### 개요

- 프로그램 11.4, 11.5는 호출될 `Activity`가 준비되어 있고,
  `SubActivity.java`, `subactivity_main.xml`이 포함됨
- `MainActivity`에서 `CALL` 버튼을 누를 때
  `SubActivity`를 호출하여 화면을 전환하는 예제임
- `CALL` 버튼의 클릭 이벤트 핸들러에
  `Activity` 호출문을 작성하여 구현함

## 2. Activity 예제 2 - `MainActivity.java`

### 코드

    public class MainActivity extends AppCompatActivity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.subactivity_main);
        }

        public void mOnClick(View v) {
            Intent intent = new Intent(this, SubActivity.class);
            startActivity(intent);
        }
    }

### 코드 해석

- `mOnClick()` 메소드를 통해 `Activity`를 호출할 때는
  `startActivity()` 메소드를 사용함
- 호출할 대상을 지정하는 `Intent` 객체는
  `startActivity()` 메소드의 인수로 전달됨
- 관련 코드가 구현되어 있어도,
  `SubActivity`가 아직 정상 동작하지 않을 수 있음

## 3. SubActivity가 동작하지 않는 이유

- 보안상의 이유로 앱에 포함된 모든 `Activity`는 반드시
  `AndroidManifest.xml`에 등록되어야 하기 때문임
- 앞의 예제에서는 `SubActivity`가 아직 `AndroidManifest.xml`에 등록되어 있지 않아,
  존재하지 않은 `Activity`를 호출하는 상황이 되어 예외가 발생함
- 따라서 `AndroidManifest.xml`에 `SubActivity`를 등록해야 함

## 4. Activity 예제 2 - `AndroidManifest.xml`

### 기본 구조

    <activity
        android:name=".MainActivity"
        android:label="@string/app_name">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

    <activity
        android:name=".SubActivity"
        android:label="SubActivity" />

### 코드 해석

- `MainActivity`
    - 앱 실행 시 처음 시작되는 메인 액티비티
- `intent-filter`
    - 앱의 시작점과 실행 조건을 지정함
- `MAIN`
    - 앱의 메인 진입점
- `LAUNCHER`
    - 런처 아이콘을 통해 실행 가능한 액티비티
- `SubActivity`
    - 새로 등록한 서브 액티비티
- `android:label`
    - 화면 상단 등에 표시되는 액티비티 제목

## 5. Activity 등록 시 주의점

- `AndroidManifest.xml`에 새로운 `Activity`를 등록할 때는
  `Activity`의 이름과 타이틀 바에 표시할 이름(`label`)을 반드시 지정해야 함
- `Activity`의 이름은 패키지명을 포함한 전체 경로로 지정함
- 만일 같은 패키지에 속해 있을 때는 앞에 `.`을 붙여서 표현할 수 있음

### 예시

    android:name=".SubActivity"
    android:label="SubActivity"

## 6. 인텐트 필터(intent-filter)

- 인텐트 필터(`intent-filter`)란
  `Activity` 내부에서 선언되며,
  `Activity`가 어떠한 종류의 인텐트를 받을 것인지 명시하는 역할을 수행함
- 앱에 `Intent`가 전달되었을 때,
  기술된 조건에 맞는 `Intent`만 통과시키는 필터링 역할을 함
- 인텐트 필터 및 권한을 포함하여
  전체 앱에 대한 여러 가지 정의를 `AndroidManifest.xml`을 통해 관리함

### 핵심 정리

- 새로운 `Activity`는 반드시 `AndroidManifest.xml`에 등록해야 함
- `intent-filter`는 어떤 인텐트를 받을 수 있는지 선언하는 조건임
- `MAIN`과 `LAUNCHER`는 앱의 시작 액티비티를 결정하는 대표적인 설정임

---

## 1. 인텐트의 정보

### 개요

- 사용할 인텐트를 명확히 하기 위해서는 여러 가지 속성 정보가 포함되어야 함
- 대표 속성:
    - `Action`
    - `Data`
    - `Type`
    - `Category`
    - `Component`
    - `Extras`
- 이 정보들은 생성자에게 전달되어 초기화할 수도 있고,
  일단 인텐트 객체를 생성한 후 메소드로 변경하거나 내용을 확인할 수도 있음

## 2. 인텐트 정보 명세 - Action

### 개요

- `Action`은 개발자가 실행하고자 하는 동작을 의미함
- 인텐트를 통한 **수행 작업을 지정하는 역할**을 하는 속성임
- 예를 들어, `BroadcastReceiver` 컴포넌트는 발생 사건에 대한 정보를 알려줌
- 안드로이드 플랫폼에 미리 정의해 놓은 인텐트 명세를 위한 수행 작업들을 사용할 수도 있고,
  사용자가 임의의 동작을 정의할 수도 있음

### 대표 Action 예시 1

| 액션            | 대상       | 설명                               |
|---------------|----------|----------------------------------|
| `ACTION_CALL` | Activity | 통화를 시작한다.                        |
| `ACTION_EDIT` | Activity | 데이터를 표시하고 편집한다.                  |
| `ACTION_MAIN` | Activity | 메인 Activity를 실행한다. 입력되는 데이터는 없다. |
| `ACTION_VIEW` | Activity | 무엇을 보여준다.                        |
| `ACTION_DIAL` | Activity | 전화를 건다.                          |

### 대표 Action 예시 2

| 액션                        | 대상                | 설명                |
|---------------------------|-------------------|-------------------|
| `ACTION_BATTERY_LOW`      | BroadcastReceiver | 배터리가 부족하다.        |
| `ACTION_HEADSET_PLUG`     | BroadcastReceiver | 헤드셋이 장착되거나 분리되었다. |
| `ACTION_SCREEN_ON`        | BroadcastReceiver | 화면이 켜졌다.          |
| `ACTION_TIMEZONE_CHANGED` | BroadcastReceiver | 타임존이 변경되었다.       |

### Action 관련 메소드

- `Action`의 종류는 다양하며, 정수 타입이 아니라 문자열 타입으로 정의되어 있음
- `Action`을 조사하거나 변경할 때는 다음 메소드를 사용함

  getAction()
  setAction()

## 3. 인텐트 정보 명세 - Data

### 개요

- `Data`는 `Action`에 필요한 상세 데이터를 제공하는 역할을 함
- 대부분의 `Action`은 수행 작업에 대한 정보가 필요하기 때문에
  `Action`과 `Data`는 주로 함께 사용됨

### 예시

- `ACTION_EDIT`
    - 편집을 하기 위한 파일을 지정해야 함
- `ACTION_CALL`
    - 통화하기 위한 대상을 지정해야 함

## 4. URI

- `Action`의 목적이 되는 대상은 광범위하기 때문에
  임의의 대상을 유일하게 가리킬 수 있는 `URI(Uniform Resource Identifier)` 타입이 사용됨
- URI는 웹 사이트 주소인 URL, 파일 경로 등을 유일하게 지정할 수 있는 범용적인 포맷임
- 데이터로 전달하기에 적합한 형태임
- `Data` 값에 접근하기 위해서는 다음 메소드를 사용함

  getData()
  setData()

## 5. Action과 Data의 관계

- `Action`과 `Data` 정보는
  “무엇에 대한 동작”인지를 지정할 수 있음
- 대개의 경우 이 두 정보만으로도 대상 컴포넌트를 찾을 수 있음
- 정확한 명세를 위해 추가적인 정보가 더 필요한 경우가 있음
- `Action`을 처리할 수 있는 컴포넌트가 여러 개이거나
  `Data`의 타입이 애매한 경우에는 다음 정보를 더 지정하면 명확한 처리 명세가 가능함
    - `Type`
    - `Category`
    - `Component`
    - `Extras`

## 6. 전화 걸기 Activity 예제

### 개요

- 예제 프로그램 11.6은 인텐트를 사용하여
  안드로이드 플랫폼의 `전화 걸기 Activity`를 호출하는 예제임
- 전화 걸기와 관련된 안드로이드 플랫폼 자신의 `Activity` 이름을 알 수 없으므로
  암시적 인텐트를 사용함

## 7. 수정된 `AndroidManifest.xml`

### 권한 설정

- 전화 걸기 기능을 사용하기 위해 권한을 추가함

    <uses-permission android:name="android.permission.CALL_PHONE" />

### 메인 Activity 등록 구조

    <activity
        android:name=".MainActivity"
        android:label="@string/app_name">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>

### 코드 해석

- `CALL_PHONE`
    - 전화 걸기 권한
- `MAIN`
    - 앱의 메인 진입점
- `LAUNCHER`
    - 앱 아이콘에서 실행할 수 있도록 지정

## 8. `activity_main.xml`

### 화면 구성

- 사용자로부터 전화번호를 입력받을 `EditText`와
  전화 걸기 이벤트를 발생시킬 `Button`을 정의함
- 전화번호는 숫자로 이루어지기 때문에
  `EditText`의 `inputType`을 `"phone"`으로 지정하여
  엉뚱한 입력을 사전에 차단함

### XML 예시 구조

    <EditText
        android:id="@+id/telText"
        android:layout_width="150dp"
        android:layout_height="wrap_content"
        android:inputType="phone" />

    <Button
        android:id="@+id/callBtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="mOnClick"
        android:text="CALL" />

## 9. `MainActivity.java`

### 전화 걸기 인텐트 코드

    public class MainActivity extends AppCompatActivity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            Button callBtn = (Button) findViewById(R.id.callBtn);
            callBtn.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    EditText telText = (EditText) findViewById(R.id.telText);
                    Intent intent = new Intent(Intent.ACTION_CALL);
                    intent.setData(Uri.parse("tel:" + telText.getText()));
                    startActivity(intent);
                }
            });
        }
    }

### 코드 해석

- `EditText telText`
    - 입력된 전화번호를 가져오기 위한 객체
- `new Intent(Intent.ACTION_CALL)`
    - 전화 걸기 동작을 수행하는 인텐트 생성
- `intent.setData(Uri.parse("tel:" + telText.getText()))`
    - 전화번호를 `tel:` 형식의 URI로 변환하여 인텐트에 설정
- `startActivity(intent)`
    - 전화 걸기 Activity 실행

### 핵심 정리

- 전화 걸기 예제는 암시적 인텐트를 사용함
- 호출 대상 Activity 이름을 직접 알지 못해도
  `Action`과 `Data`를 지정하면 안드로이드 플랫폼이 적절한 Activity를 찾아 실행함

---

# 핵심 요약

## 1. Activity

- `Activity`는 사용자와 상호작용할 수 있는 화면 관리 단위임
- 실제로 화면에 보이는 것은 `View`이며,
  `Activity`는 `setContentView()`를 통해 `View`를 화면에 배치함
- 앱은 여러 개의 `Activity`로 나눌 수 있고,
  각 `Activity` 간 통신을 위해 인텐트를 사용함

## 2. 앱의 주요 컴포넌트

| 컴포넌트                | 핵심 역할            |
|---------------------|------------------|
| `Activity`          | 화면 관리 및 사용자 상호작용 |
| `Service`           | 백그라운드 작업         |
| `BroadcastReceiver` | 시스템/앱 이벤트 수신     |
| `ContentProvider`   | 앱 간 데이터 제공       |

## 3. Activity 생명주기

- `Activity`는 실행 상태, 일시정지 상태, 정지 상태 등을 오가며 동작함
- 안드로이드는 제한된 자원 환경에서 `Activity`를 스택으로 관리함
- 메모리가 부족하면 정지 상태의 `Activity`가 강제 종료될 수 있음

## 4. 인텐트

- 인텐트는 컴포넌트 간 작업 요청과 데이터 전달을 위한 메시지 객체임
- `Activity`, `Service`, `BroadcastReceiver` 등 다양한 컴포넌트 간 통신에 사용됨
- 실제 실행은 `startActivity()` 또는 `startService()` 등이 담당함

## 5. 명시적 인텐트와 암시적 인텐트

| 구분      | 설명                            | 예                                     |
|---------|-------------------------------|---------------------------------------|
| 명시적 인텐트 | 호출 대상 컴포넌트를 직접 지정             | `new Intent(this, SubActivity.class)` |
| 암시적 인텐트 | 수행할 작업과 데이터만 지정하고 대상은 시스템이 결정 | `ACTION_VIEW`, `ACTION_CALL`          |

## 6. AndroidManifest.xml

- 앱에 포함된 `Activity`는 반드시 `AndroidManifest.xml`에 등록해야 함
- `intent-filter`는 해당 `Activity`가 어떤 인텐트를 받을 수 있는지 선언함
- `MAIN`과 `LAUNCHER`는 앱의 시작점을 지정하는 대표 설정임

## 7. 인텐트 정보

| 정보          | 의미             |
|-------------|----------------|
| `Action`    | 수행할 동작         |
| `Data`      | 동작에 필요한 대상 데이터 |
| `Type`      | 데이터 타입         |
| `Category`  | 인텐트의 분류        |
| `Component` | 실행할 컴포넌트       |
| `Extras`    | 추가 데이터         |

---

# 연습문제 정리

## Q1. 액티비티와 뷰에 대한 설명으로 옳은 것은?

1. 뷰는 자체 출력 기능이 없다.
2. 사용자 눈에 실제로 보이는 것은 액티비티이다.
3. 액티비티는 반드시 내부에 뷰나 뷰 그룹을 가져야 한다.
4. 액티비티 안에 뷰를 배치하는 명령어는 `setView` 메소드이다.

- 정답: **3**

### 해설

- ① 틀림
    - `View`는 `TextView`, `Button`처럼 화면에 직접 그려지는 UI 요소이므로 자체 출력 기능이 있음
- ② 틀림
    - 사용자가 실제로 보는 것은 `Activity` 자체가 아니라 `Activity` 안에 포함된 `View`임
- ③ 맞음
    - `Activity`가 화면을 구성하려면 `View` 또는 `ViewGroup`이 필요함
    - 보통 `setContentView()`를 통해 레이아웃을 설정함
- ④ 틀림
    - 올바른 메소드는 `setContentView()`임
    - `setView()`라는 메소드는 사용하지 않음

## Q2. 인텐트에 대한 설명으로 옳지 않은 것은?

1. 작업 결과를 돌려주기 위해서도 사용된다.
2. 뷰와 액티비티가 서로 메시지를 전달하기 위한 방법이다.
3. 인텐트에 호출할 대상 컴포넌트가 분명한 것을 명시적 인텐트라고 한다.
4. 서비스, CP, BR 등의 컴포넌트들이 수행해야 할 작업에 대한 정보를 가진다.

- 정답: **2**

### 해설

- ① 맞음
    - 인텐트는 `startActivityForResult()` 등에서 작업 결과를 반환하는 데도 사용됨
- ② 틀림
    - 인텐트는 `View`와 `Activity` 간 통신이 아니라,
      `Activity`, `Service`, `BroadcastReceiver` 같은 컴포넌트 간 통신에 사용됨
    - `View`와 `Activity`는 이벤트 리스너(`onClick` 등)를 통해 직접 상호작용함
- ③ 맞음
    - 실행할 컴포넌트를 정확히 지정하는 방식이 명시적 인텐트임
- ④ 맞음
    - 인텐트는 어떤 작업을 수행할지에 대한 정보(`action`, `data` 등)를 담고 있음

## Q3. 화면에 보이지 않은 연습문제

- 업로드된 연습문제 PDF의 3페이지는 썸네일상 일부 내용이 보이나,
  현재 화면에서 문제와 해설 전체가 명확히 확인되지 않음
- Q3는 추후 스크린샷을 다시 올리거나,
  해당 페이지를 더 선명하게 캡처하면 추가 정리 가능함

---

# 시험 직전 체크포인트

- `Activity`는 화면 자체가 아니라 화면을 관리하는 단위이다.
- 실제로 사용자에게 보이는 것은 `View`이다.
- `Activity`는 `setContentView()`로 레이아웃 또는 View를 화면에 배치한다.
- 앱의 주요 컴포넌트는 `Activity`, `Service`, `BroadcastReceiver`, `ContentProvider`이다.
- 인텐트는 컴포넌트 간 메시지 전달 객체이다.
- 명시적 인텐트는 호출 대상이 명확하다.
- 암시적 인텐트는 호출 대상이 명확하지 않고, 시스템이 적절한 컴포넌트를 찾는다.
- 새 `Activity`는 반드시 `AndroidManifest.xml`에 등록해야 한다.
- `intent-filter`는 어떤 인텐트를 받을 수 있는지 선언하는 필터 역할을 한다.
- `Action`은 수행할 동작, `Data`는 동작 대상 데이터를 의미한다.
- 전화 걸기 예제는 `ACTION_CALL`과 `tel:` URI를 사용한다.