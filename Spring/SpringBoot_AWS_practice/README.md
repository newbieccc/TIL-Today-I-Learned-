# Spring Study

### 인텔리제이 장점

- 강력한 추천 기능(Smart Completion)
- 훨씬 더 다양한 리팩토링과 디버깅 기능
- 이클립스의 깃(Git)에 비해 훨씬 높은 자유도
- 프로젝트 시작할 때 인덱싱을 하여 파일을 비롯한 자원들에 대한 빠른 검색 속도
- HTML과 CSS, JS, XML에 대한 강력한 기능 지원
- 자바, 스프링 부트 버전업에 맞춘 빠른 업데이트
  
### 인텔리제이 커뮤니티 (무료) 사용해도 되는 점

- 자바 개발에 대한 모든 기능 지원
- Maven, Gradle과 같은 빌드 도구 기능 지원
- 깃 & 깃허브와 같은 VCS(버전 관리 시스템) 기능 지원
- 스프링 부트의 경우 톰캣과 별도의 외장 서버 업이 실행 가능
- HTML과 CSS, 자바스크립트에 대한 지원은 부족 <u>(VS Code를 사용할 것)</u>

### build.gradle 설정하기

```spring
//스프링 이니셜라이저(http://start.spring.io/)는 스프링 부트와 그레이들을 충분히 이해하고 사용하기
//처음에는 하나씩 코드를 작성하면서 어떤 역할을 하는지 이해하면서 공부하기

//buildscript는 이 프로젝트의 플러그인 의존성 관리를 위한 설정이다.
buildscript {
    //ext는 build.gradle에서 사용하는 전역변수를 설정하겠다는 의미다.
    //springBootVersion 전역변수를 생성하고 그 값을 '2.1.9.RERELEASE'로 하겠다는 의미한다.
    ext {
        springBootVersion = '2.1.9.RELEASE'
    }
    //repositories는 각종 의존성 (라이브러리)들을 어떤 원격 저장소에서 받을 지를 정한다.
    repositories {
        //기본적으로 mavenCentral을 많이 사용하지만,
        //최근에는 라이브러리 업로드 난이도 때문에 jcenter도 많이 사용한다.
        /* mavenCentral은 이전부터 많이 사용하는 저장소지만, 본인이 만든 라이브러리를 업로드하기 위해서는
        * 정말 많은 과정과 설정이 필요하다. 그러다 보니 개발자들이 직접 만든 라이브러리를 업로드하는 것이 힘들어 점점
        * 공유가 안되는 상황이 발생했다.*/
        /* jcenter는 이런 문제점을 개선하여 라이브러리 업로드를 간단하게 하였다. 또한, 여기서 한 걸음 더 나아가 jcenter에
        * 라이브러리를 업로드하면 mavenCentral에도 업로드될 수 있도록 자동화를 할 수 있다.
        * 그러다 보니 개발자들의 라이브러리가 점점 jcenter로 이동하고 있다.*/
        mavenCentral()
        jcenter()
    }
    //spring-boot-gradle-plugin라는 스프링 부트 그레이들 플러그인의 2.1.9.RELEASE를 의존성으로 받겠다는 의미한다.
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

//위에 선언한 플러그인 의존성들을 적용할 것인지를 결정하는 코드이다.
//io.spring.dependency-management 플러그인은 스프링 부트의 의존성을 관리해 주는 플러그인이라 꼭 추가해야 한다.
//자바와 스프링 부트를 사용하기 위해서는 필수 플러그인들이니 항상 추가하여야 한다.
apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

group 'com.newbieccc.test'
version '1.0-SNAPSHOT'
sourceCompatibility = '17'

repositories {
    mavenCentral()
}

//dependencies는 프로젝트 개발에 필요한 의존성들을 선언하는 곳이다.
//특정 버전을 명시하면 안 된다.
//그래야 'org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}'의 버전을 따라가게 된다.
//이렇게 관리할 경우 각 라이브러리들의 버전 관리가 한 곳에 집중 되고
//버전 충돌 문제도 해결되어 편하게 개발을 진행할 수 있다.
dependencies {
    //책은 compile로 작성 되었다.
    //Gradle 7버전을 유기 위해 implementation으로 변경한다.
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

<hr>

- Setting : ctrl + alt + s
- Action : ctrl + shift + a
- terminal 설정

<hr>

### 참고사항
- 책은 시기가 좀 지난 부분이라 아래 해당 내역으로 수정하여 진행한다.
- 책 : compile ('org.springframework.boot:spring-boot-starter-web')
- 수정 : implementation 'org.springframework.boot:spring-boot-starter-web'