# Java 기초

- 출처
  - [자바를 공부하기 전에 알아두면 좋을 것들!! #1 (JDK, JRE, JVM 알아보기) - 공부하는 개발자](https://www.youtube.com/watch?v=f0cAmTYo4tQ&t=351s)
  - [JDK 라인엔지니어링 blog](https://engineering.linecorp.com/ko/blog/line-open-jdk/)

## LTS

- Long Time Support = 오래 써도 되는 버전 (오래 지원하겠다는!)

## JVM

- 자바 가상 머신의 약자.
- Java Virtual Machine.
- OS 별로 존재한다.
- 바이너리 코드를 읽고 검증하고 실행한다.

>1. "Hello World"를 출력한다고 가정하자
>2. Java에서는 `컴파일러`를 통해 01010100011....이란 결과물로 컴파일한다.
>3. C언어와는 다르게 운영체제(Windows, MAC, Linux)에서 `모두 동일한 결과물`은 나타낸다.
>4. `각각의 운영체제 JVM`으로 올라간다. (ex. Windows JVM / MAC JVM / Linux JVM)
>5. JVM이 운영체제에게 한 번 더 번역해준다.

### JVM 특징

- 그런 점에서 Java뿐만 아니라 `그루비` / `스칼라` / `코틀린`에서도 많이 사용된다.
- JVM = 똑같은 JAVA 바이트 코드를 OS마다 다르게 해석해준다!
- 포함하는 큰 순서
  - JDK > JRE > JVM
  - JDK를 설치하면 JRE, JVM도 함께 설치된다.
  - 이것은 즉, `JAVA의 버전 = JDK의 버전`이 된다.

---

## JDK

- JDK에는 `버전`이 있다.
  - 각 버전별로 새로운 기능이 추가되거나 기존 기능이 사라진다.
- JDK에는 `종류`가 있다.
  - 기능 자체는 모두 동일하나 성능과 비용에 약간의 차이가 있을 수 있다.

### Oracle JDK

- 오라클에서 만든 JDK
- 개인 = `무료` / 기업용 = `유료`

### Open JDK

- Oracle JDK와 비슷한 성능
- 언제든 `무료`

---

### 비고

- JDK 5가 되면서 Generic이 추가되고...
- JDK 8이 되면서 Lambda가 들어왔다는...
