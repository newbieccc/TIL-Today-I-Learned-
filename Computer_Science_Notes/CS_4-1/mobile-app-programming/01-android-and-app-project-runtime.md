# 모바일앱프로그래밍

## 01. 안드로이드 프로젝트와 앱의 동작 원리

- 컴퓨터과학과 정광식 교수님

---

## (1) 안드로이드 프로젝트

### 안드로이드 프로젝트의 개념

- **안드로이드 프로젝트(Android Project)**
    - 하나의 앱을 개발하기 위해 통합 개발 환경(IDE) 내에 구성하는 작업 공간(Work Space)
- **개발에 필요한 기본 파일과 폴더**
    - 안드로이드 프로젝트를 생성하면 지정된 경로에 다양한 기본 폴더/파일이 Android Studio에 의해 자동 생성됨

### 안드로이드 프로젝트를 구성하는 주요 파일 및 폴더

| 파일 및 폴더명                       | 설명                                                                  |
|--------------------------------|---------------------------------------------------------------------|
| `java/MainActivity.java`       | 스마트폰 화면을 구성하는 **액티비티(Activity)** 를 정의하는 파일. (예제에서 보통 앱 시작점 역할)      |
| `R.java` (`R 클래스` / `R.jar`)   | 앱이 참조하는 **자원(문자열, 이미지, 소리, 레이아웃 등)** 들의 **리소스 ID가 정의되는 자동 생성 클래스**  |
| `res/drawable/`                | 화면에 표시되는 **이미지 파일(png, jpg, gif)** 이 저장되는 폴더                        |
| `res/layout/activity_main.xml` | `MainActivity.java`에 대한 **레이아웃(UI 구조)을 정의하는 XML 파일**                |
| `res/values/strings.xml`       | 앱이 동작하면서 참조하는 **문자열들이 정의된 파일**                                      |
| `AndroidManifest.xml`          | 앱에 대한 **전반적인 정보를 담고 있는 파일**로, 앱의 **구성요소**나 **권한(permission)** 등을 정의 |

> 참고: “앱 실행 시 처음 실행되는 화면”은 보통 **Manifest에 런처(Launcher)로 등록된 Activity**입니다. 예제에서는 `MainActivity`가 런처인 경우가 많아요.

---

## (2) 안드로이드 프로젝트 구조

### 주요 파일들의 참조 관계(핵심)

- 안드로이드 프로젝트를 구성하는 주요 파일들은 **서로 유기적으로 연결**되어 있음
- `MainActivity.java` 안에서 정의되는 Activity는 (일반적으로) **앱의 시작 화면** 역할을 함
- 일반적인 프로그래밍 언어의 **main 함수와 유사한 시작점**으로 이해해도 됨

### 파일별 역할 요약

- `strings.xml`
    - **ID 값에 해당하는 문자열 값**을 저장하는 파일
- `activity_main.xml`
    - **화면 레이아웃(UI 구조/배치)** 를 정의하는 파일
    - 텍스트/이미지 등을 `@string/...`, `@drawable/...` 형태로 **리소스 ID로 참조**
- `R.java`
    - 앱 실행 시 필요한 **리소스 ID(속성값) 정보**가 저장되는 자동 생성 파일
    - `res/` 아래 리소스들이 빌드되면서 자동으로 생성/갱신됨
- `MainActivity.java`
    - XML 파일을 사용하여 실제 화면을 구성하거나 작업을 수행하는 파일
    - 보통 `activity_main.xml`을 불러와 화면을 띄우고, 이벤트/로직을 처리함
- `AndroidManifest.xml`
    - 앱 구성요소 선언, 권한, 최소 API 등 앱의 “설정/명세”를 정의함
    - 런처 Activity 지정도 여기서 함

### 한 번에 보는 연결 흐름(예시)

1. `AndroidManifest.xml`에서 런처 Activity 지정
2. `MainActivity.java`가 `setContentView(R.layout.activity_main)`로 레이아웃 연결
3. `activity_main.xml`이 `@string/app_name` 같은 문자열 리소스를 참조
4. `strings.xml`에 실제 문자열 값이 들어있고,
5. `R.java`가 위 리소스들을 코드에서 쓸 수 있게 ID로 연결해줌

---

## Activity 개념

### Activity란?

- **Activity**는 안드로이드 앱에서 **하나의 화면**을 표현하기 위한 구성요소
- Activity에는 다양한 기능을 수행하기 위한 코드가 작성되며, 크게 **실행 부분**과 **데이터(UI) 부분**으로 구분해 이해할 수 있음

### 실행 부분 vs 데이터 부분

- Activity 안의 **Java 소스 코드** = **실행 부분**
- `strings.xml`, `activity_main.xml` 같은 **XML 리소스** = **데이터(UI) 부분**
- **실행 부분과 데이터 부분의 연결은 `R.java`가 담당**
    - `R.java`는 XML로 정의된 데이터들을 실행 부분에서 활용할 수 있도록 **변수 형태의 ID 값**을 제공

---

## 3) MainActivity.java

### MainActivity.java 개념

- 안드로이드 앱의 화면을 구성하거나 사용자와 상호작용하는 Activity 클래스를 상속받아 **새로운 액티비티(화면)** 를 생성
- 사용자가 발생시키는 이벤트에 반응하여
    - 새로운 액티비티(화면)를 생성하거나
    - 사용자의 요구사항을 만족시키는 **동적 작업**을 수행

### 예시 코드(설명용)

    public class MainActivity extends AppCompatActivity {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
        }
    }

- `onCreate()`에서 `setContentView(R.layout.activity_main);`로 **화면 레이아웃(activity_main.xml)** 을 연결함

---

## (3) 안드로이드 프로젝트의 구성 1

### activity_main.xml

- 하나의 안드로이드 앱은 **실행 부분(Java)** 과 **데이터 부분(XML)** 이 분리되어 있음
- 데이터 부분 중 하나인 **화면 구조(레이아웃)** 는 일반적으로 Java 코드에 직접 기술하지 않고 **XML에서 기술**함

### activity_main.xml에서 하는 일

- `RelativeLayout` 같은 레이아웃 안에 `TextView` 등의 View를 배치
- `TextView`의 `android:text` 속성에 `@string/app_name` 같은 값을 지정 가능
    - 문자열 “값”을 직접 쓰는 게 아니라 **문자열 리소스 ID를 참조**하는 방식

### 예시(핵심만)

    <RelativeLayout>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/app_name" />
    </RelativeLayout>

---

## strings.xml

- 문자열(String)은 관리 편의성을 위해 **XML 파일에 따로 정의**
- 문자열이 정의되는 XML 파일은 기본적으로 `strings.xml`

### 예시

    <resources>
        <string name="app_name">helloworld</string>
        <string name="hello_world">Hello world!</string>
        <string name="action_settings">Settings</string>
    </resources>

### 연결 관계 정리

- `activity_main.xml`에서 `@string/app_name`을 사용  
  → `strings.xml`의 `name="app_name"` 문자열 리소스를 참조
- 문자열 리소스의 **ID 정보**는 `R.java`에, **실제 문자열 값**은 `strings.xml`에 저장됨

---

## (4) 안드로이드 프로젝트의 구성 2

## R.java (R.jar / R.class)

### R.java란?

- 안드로이드 앱에서 사용하는 리소스를 코드에서 참조할 수 있도록  
  **리소스 ID가 정의된 클래스 `R`** 을 포함하는 파일/클래스(자동 생성)

### 왜 필요한가?

- Java 코드나 XML에서 참조하는 리소스의 ID는 `R.java`에 정의됨
    - 예: `R.layout.activity_main`
    - 예: `R.string.app_name`
    - 예: `R.drawable.icon`

### 어떻게 만들어지나?

- `R` 클래스(내부 ID 값 포함)는  
  **AAPT(Android Asset Packaging Tool)** 에 의해 **자동 생성**
    - 개발자가 직접 작성/수정하는 파일이 아니라 빌드 과정에서 생성되는 산출물

---

## AndroidManifest.xml

### 개요

- 앱의 **구성 정보(설정/메타데이터)** 를 담고 있는 파일
- 파일명은 프로젝트와 무관하게 **AndroidManifest.xml로 고정**
- 앱을 구성하는 전반적인 기능에 대한 **명세**를 포함

### 대표적인 역할

- 앱 컴포넌트(구성요소) 선언
- 앱 실행을 위한 권한(permission) 정의
- 최소 API 레벨(minSdk 등) 정의
- 하드웨어/소프트웨어 기능(feature) 정의
- API 라이브러리(library) 정의

### 주요 안드로이드 앱 컴포넌트

- **Activity**: 하나의 스마트폰 화면을 관리
- **Service**: 화면과 별도로 백그라운드에서 독립적으로 동작
- **Broadcast Receiver**: 플랫폼/시스템 이벤트를 수신하고 처리
- **Content Provider**: 데이터를 체계적으로 관리하고 앱이 활용할 수 있도록 인터페이스 제공

---

## XML 코드

- 안드로이드에서는 앱의 레이아웃을 위해 주로 Java 코드보다는 **XML 코드**를 이용
- XML은 **eXtensible Markup Language**의 약자, HTML과 같은 마크업 언어

---

## XML 레이아웃의 장점

- 앱의 실행 코드는 Java로, UI 컴포넌트(이미지/버튼 등)는 XML로 작성 → **개발 난이도 감소**
- 레이아웃 코드가 직관적이고 수정/관리가 쉬움
- 상황/조건에 따라 레이아웃 변경, 텍스트 변경이 쉬움
- 다양한 스마트폰 크기/특성에 따라 유지보수가 용이함
- 언어 변경이나 전체적인 화면 변경이 필요할 때 편리함
- UI 수정과 Java 로직 수정이 독립적/병렬적으로 진행될 수 있음

---

## (5) 안드로이드 앱의 동작 원리

## 1. 앱의 실행 과정

### 실행하기 위한 과정

- 안드로이드 앱은 **JAVA 언어**를 이용하여 작성됨
- 개발자가 작성한 JAVA 코드는 **JAVA 컴파일러**에 의해 **JAVA 바이트 코드(.class)** 로 컴파일됨
- 일반 Java 환경에서는 Java VM에서 실행하지만,  
  안드로이드는 **ART/Dalvik** 런타임에서 바이트코드를 실행함
- Android SDK가 제공하는 DEX 변환기를 이용하여  
  `.class`를 Dalvik 실행 포맷인 `.dex` 파일로 변환함
- 변환된 `.dex` + 리소스 파일들은 설치 가능한 `.apk` 파일로 만들어짐

### 프로젝트 실행 과정(흐름)

- 배포/설치를 위한 `.apk` 생성은 AAPT를 이용하며, 이 과정을 **패키징(packaging)** 이라고 함
- 패키징이 끝난 `.apk`를 설치하면 런타임에서 실행 가능

### 한 줄 흐름도(요약)

- `.java` → `.class` → `.dex` → (AAPT 패키징) → `.apk` → 설치 → ART/Dalvik 런타임 실행

---

## 2. 앱의 배포 과정

### 배포 과정(개요)

- 안드로이드 앱은 `.apk` 확장자로 패키징되어 배포됨
- 코드 컴파일이 수행되면 `.class` 생성 → `.dex` 생성(Dalvik/ART에 적합한 포맷)

### 패키징에 포함되는 산출물

- 컴파일된 리소스(XML)는 `resources.arsc` 파일로 생성됨
- 앱 설정 환경을 정의하는 `AndroidManifest.xml`이 포함됨
- 최종적으로 다음 항목들이 함께 패키징되어 `.apk`가 생성됨
    - 컴파일되지 않은 리소스(이미지, 아이콘 등)
    - `.dex` 파일
    - `resources.arsc`
    - `AndroidManifest.xml`

### 서명(Signing) 및 업로드

- 서명 Key로 `.apk`에 서명하여 위·변조를 방지함
- 서명 Key 구분
    - Debug Key: 디버그 빌드용
    - Release Key: 배포 빌드용
- 서명 키는 앱 업데이트 과정에서 개발자 식별에도 사용됨
- 최종적으로 Google Play 같은 마켓에 업로드함

### 한 줄 흐름 정리

- `.java` → `.class` → `.dex` → (리소스 + `resources.arsc` + Manifest 포함) → `.apk` → 서명 → 스토어 업로드

---

## 정리하기(용어)

1. **XML**
    - 문서를 사람이/기계가 모두 읽을 수 있는 형식으로 부호화하는 규칙(마크업) 정의
2. **레이아웃(Layout)**
    - 안드로이드 화면 출력 및 화면 배치(양식/설계)
3. **런타임(Runtime)**
    - 프로그램이 실행되고 있는 동안의 동작
4. **Dalvik**
    - JIT 기반의 안드로이드(과거) 가상 머신 런타임
    - 현재는 주로 ART 사용(개념 이해용으로 함께 언급됨)
5. **ART(Android RunTime)**
    - 앱을 설치하기 전에 컴파일을 끝내고 앱을 실행하는 안드로이드 스마트폰의 가상머신