# # JSP프로그래밍

## 07. 모듈화된 JSP 페이지 만들기

- 컴퓨터과학과 김희천 교수님

### (1) `<jsp:include>` 액션 태그

- JSP 페이지의 모듈화
    - 모듈화
        - 공통 UI(상단 메뉴, 좌측 메뉴, 푸터 등)을 반복 작성하면 유지보수에 문제가 생김
        - 공통 부분을 별도 JSP 페이지로 분리하고, 필요 할 때 include 해서 재사용
        - 포함 방식
            - 정적 include
            - 동작 include
- `<jsp:include>` 액션 태그
    - 동적 인클루드(include)
        - 현재 페이지에 대한 요청이 처리되는 도중(run-time)에 다른 JSP 페이지를 실행하고 그 실행 결과를 가져와 현재 페이지의 실행 결과에 삽입
            - 매 요청마다 결과가 바뀌는 경우(사용자 정보, 현재 시간, 게시판 화면 등), 파라미터 추가 전달이 필요할 때, 조건에 따라 page를 선택할 때 사용
            - 두 페이지는 같은 request 영역을 공유
                - 당연히 session과 application 영역도 공유
        - 예:`<jsp:include page="/templates/user.jsp" flush="true"/>`
            - page 속성은 포함할 JSP 페이지의 경로
            - flush 속성으 ㄴ현재 출력 버퍼를 플러시(전송)할지 여부

### (2) `<jsp:param>` 액션 태그

- `<jsp:param>` 태그
    - `<jsp:include>` 또는 `<jsp:forward>` 액션을 사용하여 다른 JSP 페이지에 요청을 전달할 때, 파라미터를 전달하기 위함
        - name 속성과 value 속성을 통해 데이터를 키-값 쌍으로 전달
        - `<jsp:include>`나 `<jsp:forward>`의 서브 엘리먼트로만 사용 가능
    - 원래 요청에 포함된 파라미터에 추가로 덧붙여짐
        - 전달된 파라미터는 포함된(또는 포워딩된) JSP 페이지에서 request.getParameter("p1") 형태로 접근 가능

```jsp
<jsp:include page='page.jsp' flush="true">
    <jsp:param name="p1" value="v1"/>
    <jsp:param name="p2" value="v2"/>
</jsp:include>
```

- 파라미터 우선 순위
    - `<jsp:include>`나 `<jsp:forward>`를 사용할 때 요청이 그대로 전달됨
    - 원래 요청에 포함되었던 파라미터보다 `<jsp:forward>` 태그에서 정의 된 파라미터가 기존 파라미터보다 우선 적용됨

### (3) include 지시어

- 정적 인클루드(include)
    - JSP 페이지에서 다른 JSP/HTML 파일의 소스를 그대로 포함(붙여넣기)할 때 사용하는 지시어
        - JSP 페이지가 서블릿으로 변환되기 전에 이루어짐(번역 시점)
        - 원래 소스와 포함된 소스가 합쳐져 하나의 서블릿으로 변환/컴파일 됨
        - 여러 페이지에서 동일하게 반복되는 부분을 포함함 때 사용
        - 실행 시점에 값이 달라지지 않는 공통 소스 코드가 조각을 포함
            - <Header>, <footer> 같은 공통 레이아웃, CSS, 자바스크립트, 회사 로고 이미지, 정적 HTML 태그, 공통 스크립트 요소 등
        - 예: <%@include file="파일경로" %>

### (4) `<jsp:forward>` 액션 태그
