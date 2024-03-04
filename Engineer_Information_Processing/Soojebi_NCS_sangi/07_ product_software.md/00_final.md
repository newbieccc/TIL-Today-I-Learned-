# 제품 소프트웨어 패키징 - 단원종합문제

## 제품 소프트웨어 패키징하기 / 제품 소프트웨어 매뉴얼 작성 및 버전 등록 / 애플리케이션 배포 환경 구성 / 애플리케이션 소스 검증 및 배포 - 단원종합문제

### 01. 용어

- 정해진 시간을 기준으로 그 이후에 변경된 파일만을 백업하는 방식을 무엇이라고 하는지 쓰시오.
  - `증분 백업(Incremental Backup)`

---

### 02. 컴파일러 언어의 빌드 과정

- 전처리기 -> 파서 -> 번역 -> 어셈블러 -> ( `링커(Linker)` ) -> 로더

>- 어셈블러가 목적 파일(Object File)을 생성하면 링커가 오브젝트 파일을 합쳐서 하나의 실행 파일을 만든다

### 03. 괄호 안의 용어

- ( `바이트 코드 언어` )은/는 컴파일 결과물이 실행파일이 아닌 class 파일로 생성되는 언어로 Java, C# 등이 있다.

>- 바이트 코드 언어는 컴파일의 결과물이 실행 파일이 아닌 바이트 코드 파일로 생성되는 언어이다.
>- Java 바이트 코드 언어는 class 파일을 가상 실행환경인 JRE(Java Runtime Environment)에서 빌드 된다.

---

### 04. 괄호 안의 용어

- ( `인터프리터 언어` )은/는 소스 코드를 한 줄씩 번역하여 실행하는 언어로 Javascript, Python, Ruby 등이 있다.

---

### 05. 괄호 안의 용어

- ( `회귀 테스트(Regression Test)` )은/는 오류를 제거하거나 수정한 시스템에서 오류 제거와 수정 때문에 새로이 유입된 오류가 없는지 확인하는 일종의 반복 테스트 기법이다.

---

### 06. 괄호 안의 용어

- ( `WAS(Web Application Server)` )은/는 애플리케이션 배포 동작 환경 중 사용자의 요청을 받아 동적인 처리를 수행한다.

>- 애플리케이션 배포 동작 환경 중 사용자의 요청을 받아 동적인 처리를 수행하는 것은 WAS이다.
>- WAS 구성 및 운용을 위한 국제 표준 규격을 정하고 있으며, 제품마다 배포 방식과 설정이 일부 다르다.

---

### 07. 애플리케이션 배포단위

- ( `jar(Java Archive)` )은/는 자바 프로그램에서 참조하는 라이브러리, 리소스, 프로퍼티(Property), 구현된 비즈니스 서비스를 배포할 때 패키징하여 배포한다
- ( `war(Web Archive)` )은/는 웹 컨테이너에 배포되는 배포단위로 Servlet, ( `jar(Java Archive)` ) 파일과 WEB-INF 폴더에 있는 web, xml 파일로 구성된다.

>- 자바 프로그램은 jar 형태와 war 형태로 배포할 수 있다.

---

### 08. 괄호 안의 용어

- ( `형상 통제` )은/는 항상 항목의 변경사항에 대하여 형상통제위원회가 승인/기각/보류를 결정하고, 승인된 변경 사항의 이행을 체계적으로 통제하는 활동이다.
- ( `형상 감사` )은/는 형상 관리 계획대로 형상 관리가 진행되고 있는지, 형상 항목의 변경이 요구사항에 맞도록 제대로 이뤄졌는지 등을 살펴보는 활동이다.

- 형상관리 절차

|||
|:--:|--|
|형상 식별|형상 관리 계획을 근거로 형상 관리의 대상이 무엇인지 식별하는 활동|
|형상 통제|형상 항목의 변경 사항에 대하여 형상통제위원회가 승인/기각/보류를 결정하고, 승인된 변경사항의 이행을 체계정으로 통제하는 활동|
|형상 감사|형상 관리 계획대로 형상 관리가 진행되고 있는지, 형상 항목의 변경이 요구사항에 맞도록 제대로 이뤄졌는지 등을 살펴보는 활동|
|형상 기록|소프트웨어 형상 및 변경 관리에 대한 각종 수행 결과를 기록하는 활동|
|||

---

### 09. 괄호 안의 용어

- ( `코드 인스펙션(Code Inspection)` )은/는 사전에 정의된 코드 작성 규칙(Rule) 기반으로 소스 코드를 점검하여 작성 규칙에 위반되는 소스 코드를 추출하는 정적 분석 기법이다.

---

### 10. 해당 설명의 용어는?

|||
|:--:|--|
|CVS|가장 오래된 형상 관리 도구 중의 하나로서 중앙 집중형 서버 저장소를 두고 클라이언트가 접속해서 버전 관리를 실행하는 형상 관리 도구|
|`SVN`|중앙 집중형 클라이언트-서버 방식으로 CVS의 단점을 보완해 가장 널리 사용되고 있는 형상 관리 도구|
|Git|분산 저장소 방식으로 로컬 저장소와 원격 저장소로 분리되어 분산 저장하는 방식의 형상 관리 도구|
|||