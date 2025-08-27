# # JSP프로그래밍

## 02. 개발환경 설정하기

- 컴퓨터과학과 김희천 교수님

### (1) JSP 개발 환경

- JSP 개발 환경
    - Java SE Development Kit
        - 오라클 - JDK
        - 오픈 - JDK
    - Tomcat 9 또는 Tomcat 11
    - Eclipse IDE for Enterprise Java Developers
- 이클립스
    - Eclipse IDE
        - 다양한 프로그래밍 언어로 개발하도록 지원하는 오픈소스 개발도구
        - 무료 오픈 소스 소프트웨어로 플러그-인을 추가하여 기능을 확장할 수 있음
        - 오픈 소스 커뮤니티 eclipse.org의 프로젝트 결과물
- 톰캣
    - 아파치 톰캣(Apache Tomcat)
        - 아파치 소프트웨어 재단에서 개발된 오픈소스 웹 컨테이너
            - Java 웹 기술인 서블릿과 JSP 규약을 구현
            - 웹 서버 역할도 수행

### 웹 프로젝트의 배포

- 배포(deployment)
    - 개발이 끝난 웹 프로젝트를 서비스 제공을 위해 톰캣에 올리는 것
        - 외부에서 서비스에 접속 가능하도록 등록하는 과정
        - 웹 프로젝트는 HTML 페이지
- WAR 파일
    - 웹 아카이브(Web Application)
        - 배포를 위해 웹 프로젝트를 압축한 파일
