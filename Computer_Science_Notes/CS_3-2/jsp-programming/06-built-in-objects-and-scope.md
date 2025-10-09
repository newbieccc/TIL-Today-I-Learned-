# # JSP프로그래밍

## 06. 내장 객체와 Scope

- 컴퓨터과학과 김희천 교수님

### (1) 내장 객체

- 내장 객체
    - 웹 컨테이너가 자동 제공하여 선언 없이 사용할 수 있는 객체
        - request, response, session, application, out, pageContext, config, page, exception (총 9개)
    - 스크립트 요소에서 바로 사용 가능
- 사용자 정의 객체
    - 스크립트 요소에서 선언된 일반 자바 객체
        - 선언문 <%! ... %>의 객체는 서블릿의 멤버 변수가 됨
        - 스크립트릿 <% ... %>의 객체는 메서드의 지역 변수가 됨
    - 자바빈 객체: 별도의 자바빈 클래스를 정의하고, jsp: useBean 태그로 생성하며, scope 속성에서 객체의 생존 범위가 지정됨
        - <jsp: useBean id="member" class="mypkg.Member" scope="session">
- JSP 내장 객체 요약

| 내장 객체         | 클래스                   | 기능                                                              |
|---------------|-----------------------|-----------------------------------------------------------------|
| `request`     | `HttpServletRequest`  | 클라이언트의 요청 정보 관리 *(request 영역)*                                  |
| `response`    | `HttpServletResponse` | 웹 서버의 응답 정보 관리                                                  |
| `pageContext` | `PageContext`         | JSP 페이지에 대한 정보 관리 *(page 영역)*                                   |
| `session`     | `HttpSession`         | HTTP 세션 정보 관리 *(session 영역)*                                    |
| `application` | `ServletContext`      | 웹 애플리케이션에 대한 정보 관리 *(application 영역)*                           |
| `out`         | `JspWriter`           | 브라우저에게 보낼 콘텐츠를 출력할 때 사용되는 출력 스트림                                |
| `config`      | `ServletConfig`       | JSP 페이지에 대한 설정 정보 관리                                            |
| `page`        | `Object(HttpJspBase)` | JSP 서블릿 클래스의 인스턴스( `this` 와 같음)                                 |
| `exception`   | `Throwable`           | 에러 페이지(`isErrorPage="true"`) 안에서만 사용 가능. 오류 메시지 출력 등의 예외 처리에 사용 |

- PageContext 내장 객체
    - JSP의 실행 컨텍스트를 대표하는 객체
        - JSP 실행 환경의 허브 역할
        - javax.servlet.jsp.PageContext의 인스턴스
    - page 영역의 저장소
        - page 영역의 자바빈 객체 또는 속성 객체 등을 저장
        - page 영역 외의 다른 영역에도 속성을 저장하거나 조회할 수 있음
            - 예: pageContext.setAttribute("msg", "hello", PageContext.REQUEST_SCOPE);
        - 다른 내장 객체에 대한 통합적 접근을 제공
            - getRequest(), getResponse(), getSession() 등
        - 에러 처리, 포워딩, 인클루드 등 JSP 실행 관리 기능 제공
            - 예: pageContext.forward("next.jsp");
- application 내장 객체
    - 웹 애플리케이션에서 공유되는 정보 관리
        - web.xml의 <context-param> 조회
        - 웹 컨테이너의 정보 조회: getServerInfo()
        - 서버측 로그 기록: log()
    - application 영역의 저장소
        - 애플리케이션 전역에서 공유되는 데이터 저장/조회
            - setAttribute()와 getAttribute()로 저장하고 조회
        - 동일한 웹 애플리케이션 내 모든 JSP/서블릿이 하나의 application 객체(ServletContext 인스턴스)를 공유
- application 내장 객체 web.xml
    - web.xml
        - 웹 애플리케이션 실행 관련 전역 설정 저장
        - 웹 애플리케이션 배포 후, 위치는 [톰캣설치폴더]/webapps/[웹 애플리케이션]/WEB-INF/web.xml
        - <context-param>태그를 이용해 웹 애플리케이션 내 모든 JSP/서블릿에서 공유할 수 있는 설정 값 지정 가능

```xml

<context-param>
    <description>파라미터 설명(생략 가능)</description>
    <param-name>파라미터 이름</param-name>
    <param-value>파라미터 값</param-value>
</context-param>
```

- web.xml의 전역 설정 <context-param> 정보 조회 메서드

| 메서드                             | 리턴 타입                 | 기능                                   |
|---------------------------------|-----------------------|--------------------------------------|
| `getInitParameter(String name)` | `String`              | 지정한 초기화 파라미터의 값을 반환(존재하지 않으면 `null`) |
| `getInitParameterNames()`       | `Enumeration<String>` | 모든 초기화 파라미터의 이름을 리턴                  |

- 웹 컨테이너 정보 조회 메서드

| 메서드                 | 리턴 타입    | 기능                        |
|---------------------|----------|---------------------------|
| `getServerInfo()`   | `String` | 웹 컨테이너의 이름과 버전 정보를 리턴     |
| `getMajorVersion()` | `int`    | 지원하는 서블릿 API 규약의 주 버전을 리턴 |
| `getMinorVersion()` | `int`    | 지원하는 서블릿 API 규약의 부 버전을 리턴 |

- out 내장 객체
    - JSP에서 클라이언트로 보낼 컨텐츠를 작성하기 위한 출력 스트림
    - 버퍼 제어 메서드를 제공
        - clearBuffer(), flush(), getRemaining() 등
        - 실제 버퍼는 response 객체에 존재
    - out 객체는 JspWriter 타입
        - JSP에서 서블릿 변환 시, 정적 텍스트와 HTML 태그는 서비스 메서드에서 out.write("..."); 코드로 변환 됨
        - 표현식 <%= ... %>은 out.print(수식); 코드로 변환됨
- out 내장 객체의 출력 메서드
    - JSP Writer의 주요 메서드
        - print(값): 다양한 타입을 문자열로 변환하여 출력
        - println(값): 출력 후 줄 바꿈 추가
        - println(): 줄 바꿈만 출력
        - newline(): 줄 바꿈 문자 출력
        - write(문자열 or 문자배열): 지정한 문자열이나 문자 배열을 그대로 출력
- out 내장 객체와 버퍼
    - out 객체의 버퍼 제어 메서드
        - JSP의 out 객체(JspWriter)는 버퍼를 사용하고 제어할 수 있는 인터페이스를 제공

| 메서드               | 리턴 타입     | 기능                                              |
|-------------------|-----------|-------------------------------------------------|
| `getBufferSize()` | `int`     | 버퍼의 전체 크기를 리턴                                   |
| `getRemaining()`  | `int`     | 현재 남아 있는 버퍼의 공간 크기를 리턴                          |
| `clear()`         | `void`    | 버퍼의 내용을 비움. 버퍼가 이미 플러시된 적이 있으면 `IOException` 발생 |
| `clearBuffer()`   | `void`    | 버퍼의 내용을 비움. **플러시 여부와 상관없이** 예외를 발생시키지 않음       |
| `flush()`         | `void`    | 버퍼의 내용을 클라이언트로 전송하고 버퍼를 비움                      |
| `isAutoFlush()`   | `boolean` | `page` 지시어의 `autoFlush` 속성 값을 리턴                |

### (2) 내장 객체와 영역

- JSP 객체의 영역(scope)
    - 객체가 유효하게 사용될 수 있는 범위
        - 같은 영역 내 JSP 페이지 간에는 데이터를 공유하여 협력 가능
        - pageContext, request, session, application 내장 객체가 존재
    - 영역의 네가지 종류
        - page
            - 현재 JSP 페이지 내부에서만 유효
            - 메서드의 지역변수와 유사
        - request
            - 하나의 요청 처리 과정 동안 유효
            - 다른 JSP/서블릿으로 forward/include 시 공유 가능
        - session
            - 같은 클라이언트와의 세션이 유지되는 동안 유효
            - 브라우저 단위
        - application
            - 웹 애플리케이션 전체에서 유효
            - 모든 사용자, 모든 JSP/서블릿이 공유
- 영역의 비교

| 구분          | 범위                           | 소멸 시점                                   | 저장 위치            | 활용                                                                                    |
|-------------|------------------------------|-----------------------------------------|------------------|---------------------------------------------------------------------------------------|
| page        | 현재 JSP 페이지 내부                | 클라이언트에게 응답을 보내거나, 다른 페이지로 포워딩/인클루드되면 소멸 | `pageContext` 객체 | JSP 내 **지역 변수**처럼 사용                                                                  |
| request     | 하나의 클라이언트 요청을 처리하는 동안        | 요청에 대한 응답이 완료되면 소멸                      | `request` 객체     | 같은 요청을 처리하는 JSP/서블릿들 사이에서 **공유 가능**. `\<jsp:forward>` 또는 `\<jsp:include>` 사용 시 데이터 전달 |
| session     | 같은 클라이언트(브라우저)와의 여러 요청 동안 유지 | 브라우저 종료 또는 로그아웃 또는 세션 타임아웃 시 소멸         | `session` 객체     | 로그인 정보, 장바구니 정보 등 **개별 사용자별 데이터** 저장                                                  |
| application | 1개 웹 애플리케이션 전체(모든 사용자 공유)    | 서버(웹 컨테이너) 종료 또는 재시작 시 소멸               | `application` 객체 | 방문자 카운트, 공용 데이터/환경 설정 값 등 **전역 데이터** 저장 (모든 사용자와 모든 JSP/서블릿이 공유)                      |

### (3) 속성을 이용한 데이터 공유

- JSP 페이지 간 데이터 공유
    - 데이터 공유 방법
        - 영역 개념을 통해 여러 JSP 페이지 사이에서 데이터 공유 가능
        - 영역을 표현하는 내장 객체(pageContext, request, session, application)가 데이터 저장소 역할을 함
            - 공유되는 데이터를 속성이라 함
            - 영역 객체가 속성(attribute)을 관리
            - 속성은 <이름, 값> 쌍으로 저장됨
            - 이름은 String, 값은 Object 유형
        - 같은 영역에 속하는 JSP/서블릿은 setAttribute()로 속성을 저장하고, getAttribute()로 읽어 사용할 수 있음
- 속성 관리 메서드
    - 모든 영역에서 공통으로 제공하는 메서드

| 메서드                                       | 리턴 타입                 | 기능                                                    |
|-------------------------------------------|-----------------------|-------------------------------------------------------|
| `setAttribute(String name, Object value)` | `void`                | 이름이 `name`인 속성에 `value`를 저장. 이미 같은 이름이 있으면 덮어씀        |
| `getAttribute(String name)`               | `Object`              | 이름이 `name`인 속성의 값을 리턴. 없으면 `null`. 실제 사용 시 **형변환** 필요 |
| `removeAttribute(String name)`            | `void`                | 이름이 `name`인 속성을 삭제                                    |
| `getAttributeNames()`                     | `Enumeration<String>` | 현재 영역에 저장된 **모든 속성 이름 목록**을 리턴                        |

- 속성에 기본형 값 저장과 읽기
    - 속성에 기본형 값 저장하기
        - setAttribute(String, Object)에서 Object 유형의 값만 저장
        - 기본형 값은 자동 래퍼 클래스 객체로 변환 가능(오토 박싱)
        - 예: request.setAttribute("age", 25);
    - 속성에 저장된 기본형 값 읽기
        - getAttribute()는 항상 Object 유형을 반환
            - 원래의 래퍼 클래스로 명시적 형변환이 필요
        - 형 변호나 후, 래퍼 클래스 객체가 기본형 변수에 대입될 때는 자동 기본형으로 변환됨(언박싱)
        - 예: int age = (Integer) request.getAttribute("age");
