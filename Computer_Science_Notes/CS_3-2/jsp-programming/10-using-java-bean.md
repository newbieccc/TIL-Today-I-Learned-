# # JSP프로그래밍

## 09. 자바 빈 사용하기

- 컴퓨터과학과 김희천 교수님

### (1) 자바빈 개요

- 자바빈 개념
    - 자바빈 정의
        - JSP요소들과 맞물려 사용 가능한 사용자 정의 자바 클래스
        - 자바빈 설계 규약(자바빈 API 스펙)에 따라 작성해야 함
    - 자바빈 사용 이유
        - 프레젠테이션과 비즈니스 로직 분리
            - JSP는 화면 출력, 데이터와 로직은 자바빈, 흐름제어는 서블릿에 캡슐화
        - 재사용성과 테스트 용이성
            - 여러 JSP에서 같은 빈의 공유 가능. 다양한 액션 태그 제공
        - 안정적 데이터 전달 객체(DTO)로 활용
            - 폼 입력값 또는 데이터 조회 결과를 빈의 프로퍼티로 보관하고, JSP에서 사용
- 자바빈 클래스 설계 규약
    - 생성자가 필요하면 파라미터가 없는 기본 생성자를 만들어야 함
    - 기본적으로 읽기와 쓰기가 가능한 속성을 가짐
        - 속성은 관례상 private 필드로 선언
        - private String name;
    - public getter 메서드와 public setter 메서드를 가짐
        - 경우에 따라 getter만 있으면 read-only로 간주
    - 메서드 명명 규칙
        - getter 메서드는 파라미터가 없으며 속성의 타입과 일치하는 리턴 타입을 가짐
        - public String getName();
            - 속성의 유형이 boolean인 경우 isXxx() 가능
        - setter 메서드는 속성의 타입과 일치하는 1개 파라미터를 가지며 리턴 타입은 void
        - public void setName(String xxx);
    - 필요에 따라 equals(), hashCode(), toString() 메서드를 재정의

```java
package com.member;

public class Member {
    private String name;
    private int age;

    public Person() {
        //기본값 설정
    }

    public String getName() {   //name 속성의 getter 메서드
        return name;
    }

    public void setName(String name) {  //name 속성의 setter 메서드
        this.name = name;
    }

    public int getAge() {   //age 속성의 getter 메서드
        return age;
    }

    public void setAge(int age) {   //age 속성의 setter 메서드
        this.age = age;
    }
}
```

- Eclipse로 자바빈 클래스 정의하기
    - Project Explorer 뷰에서 프로젝트 이름을 오른쪽 마우스 버튼으로 클릭 후 팝업 메뉴에서 New-Class를 선택
    - 패키지와 클래스 이름을 입력하고 Finish
    - 자바빈 클래스를 작성
        - 멤버 변수를 정의
        - 멤버 변수를 선택하고 오른쪽 마우스 버튼으로 클릭한 후 팝업 메뉴에서 Sources-Generate Getters and Setters... 선택
    - Eclipse에서 자바 소스(.java)와 클래스 파일(.class)의 위치
        - 웹프로젝트폴더\src\main\java\패키지\자바소스
        - 웹프로젝트폴더\build\classes\패키지\클래스파일
- 자바빈 클래스의 전형적 사용
- 서블릿 - 영역 객체의 속성으로 자바빈 객체를 저장

```java
void main() {
    Member member = new Member();
    member.setName("John");
    member.setAge(25);
    request.setAttribute("bean", member);
}
```

- JSP - 자바빈 객체 생성(해당 영역에 없는 경우)과 속성의 설정

```jsp
<jsp:useBean id="bean" class="com.member.Member" scope="request"/>
<jsp:setProperty name="bean" property="name" value="John"/>
<jsp:setProperty name="bean" property="age" value="25"/>
```

- 표현 언어(EL) - 자바빈 객체의 속성 읽기

```jsp
${bean.name},
${bean.age}
```

### (2) 자바빈과 액션 태그

- 자바빈 관련 액션 태그
    - `<jsp:useBean>`
        - 지정 영역에서 자바빈 객체를 찾아 선언, 찾지 못하면 자바빈 객체를 생성함
        - `<jsp:useBean id="자바빈이름" class="패키지이름.클래스이름" scope="범위"/>`
    - `<jsp:setProperty>`
        - 자바빈 객체의 속성을 설정함
        - `<jsp:setProperty name="자바빈이름" property="속성이름" value="속성값"/>`
        - `<jsp:setProperty name="자바빈이름" property="*"/>`
    - `<jsp:getProperty>`
        - 자바빈 객체의 속성을 읽음
        - `<jsp:getProperty name="자바빈이름" property="속성이름"/>`
- `<jsp:useBean>` 액션 태그
    - JSP 페이지에서 자바빈을 사용할 것이라는 선언
    - (본문이 없는 경우)
        - `<jsp:useBean id="자바빈이름" class="패키지이름.클래스이름" scope="영역"/>`
            - scope가 생략되면 page 영역이며, self-closing 태그로 끝남
            - scope에 지정된 영역에 같은 이름(id)의 자바빈 객체가 존재하면 사용하겠다는 선언
            - 만약 존재하지 않으면 자바빈 객체를 생성
            - id는 자바빈 객체의 이름, class는 자바빈 객체의 클래스 이름, scope는 영역
    - (본문을 포함하는 경우)
        - `<jsp:useBean id="자바빈이름" class="패키지이름.클래스이름" scope="범위">`
            - `<jsp:setProperty ... />`
        - `</jsp:useBean>`
            - 객체를 생성하는 경우만 본문의 `<jsp:setProperty>` 초기화 코드가 실행됨
            - 만약 독립적으로 `<jsp:setProperty>`를 사용하면 항상 실행됨

| scope 속성의 값 | 사용 범위                                   |
|-------------|-----------------------------------------|
| page        | 현재 JSP 페이지(기본값)                         |
| request     | 같은 요청이 처리되는 forward 또는 include 되는 페이지까지 |
| session     | 같은 session 객체가 유지될 때까지                  |
| Application | 웹 컨테이너가 재시작 또는 종료될 때까지                  |

- `<jsp:setProperty>` 액션 태그
    - 자바빈 객체의 속성 값을 변경
    - `<jsp:setProperty name="자바빈이름" property="속성이름" value="속성값"/>`
        - setter 메서드와 대응됨
        - property="age"에서, setAge(...)를 수행하는 셈
        - name은 자바빈 객체의 이름이어야 함
        - value는 표현식이나 EL도 가능
            - value="10", value="<%=calc() %>", value="${param.age}"
        - `<jsp:setProperty>`가 `<jsp:useBean>`의 내부에서 사용될 때는 자바빈 객체가 생성되는 경우에만 실행됨
    - `<jsp:setProperty>` 액션 태그에서 value 속성이 없는 경우
        - 폼을 통해 전송된 요청 파라미터 값을 이용해 자바빈의 속성 값을 지정
            - `<jsp:setProperty name="자바빈이름" property="속성이름" param="파라미터이름"/>`
                - 해당 파라미터의 갑승로 속성 값을 설정
        - param 속성을 생략한 경우
            - `<jsp:setProperty name="자바빈이름" property="속성이름" />`
                - param 속성이 없으면, 동일한 이름의 요청 파라미터를 적용
        - 자바빈의 모든 속성과 요청 파라미터의 이름을 비교해서 같은 것이 있으면 모두 적용하는 경우
            - `<jsp:setProperty name="자바빈이름" property="*"/>`
                - property가 "*"인 경우에 한꺼번에 적용됨
- 액션 태그와 스크립트릿 비교
    - 액션 태그로 작성
        - `<jsp:useBean id="meminfo" class="com.example.MemberInfo" scope="request"/>`
        - `<jsp:setProperty name="meminfo" property="age" value="10" />`
    - 스크립트릿으로 작성
        - `<jsp:useBean id="meminfo" class="com.example.MemberInfo" scope="request" />`
        - `<% meminfo.setAge(10); %>`
- `<jsp:getProperty>` 액션 태그
    - 자바빈 객체의 속성 값을 읽음
    - `<jsp:getProperty name="자바빈이름" property="속성이름"/>`
        - getter 메서드와 대응됨

### (3) 자바빈 예제

- 예제 설명
    - HTML폼을 통해 입력 받은 데이터를 자바빈 객체에 저장
    - 자바빈 객체의 공유를 통해 다른 페잊비에서 출력
- 예제 파일
    - BoardData.java: 게시글 저장을 위한 자바빈 클래스
        - title, writer, text, pass 속성을 가짐
    - write_form.jsp: 게시물 작성을 위한 입력 폼 -> write.jsp로 전송
    - write.jsp: 데이터를 받아 자바빈 객체를 생성하고, view.jsp로 포워딩
    - view.jsp: 자바빈 객체의 속성을 화면에 출력
