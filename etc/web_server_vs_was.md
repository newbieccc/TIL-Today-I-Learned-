# Web Server와 WAS

## Web Server

### # Web Server란?

- 웹 서버란 클라이언트(사용자)가 웹 브라우저에서 어떤 페이지 요청을 하면 웹 서버에서 그 요청을 받아 `정적 컨텐츠를 제공하는 서버`이다.
</br>(정적 컨텐츠 = 단순 HTML 문서, CSS, javascript, 이미지, 파일 등 즉시 응답가능한 컨텐츠)

- 웹 서버가 동적 컨텐츠를 요청 받으면 WAS에게 해당 요청을 넘겨주고, WAS에서 처리한 결과를 클라이언트(사용자)에게 전달해주는 역할도 한다.

- 대표적인 웹 서버 : Apache

![webServer.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FpxLJe%2FbtqBTL7f4OE%2FO54n7FkOZUKAItvIPUpwGK%2Fimg.png)

- 웹 서버 사용자 요청 처리 과정

---

## WAS

### # WAS란?

- WAS는 웹 서버와 웹 컨테이너가 합쳐진 형태로서, 웹 서버 단독으로는 처리할 수 없는 `데이터베이스의 조회나 다양한 로직 처리가 필요한 동적 컨텐츠를 제공`한다.
</br>(웹 컨테이너 : 웹 서버가 보낸 JSP, PHP 등의 파일을 수행한 결과를 다시 웹 서버로 보내주는 역할을 함)

- 이 덕분에 사용자의 다양한 요구에 맞춰 웹 서비스를 제공할 수 있다. WAS는 JSP, Servlet 구동환경을 제공해주기 때문에 웹 컨테이너 혹은 서블릿 컨테이너라고도 불린다.

- 대표적인 WAS 종류 : Tomcat

![was.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FpAqij%2FbtqBS7bDSam%2FGJDanZaV3kMKPqfXtlEqL0%2Fimg.png)

- WAS 사용자 요청 처리 과정

---

### # Web Service Architecture

- 웹 어플리케이션은 요청 처리 방식에 따라 다양한 구조를 가질 수 있다.

![Web Service Architecture.jpg](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FcjdthZ%2FbtqBUUpmzjp%2FFqUA0NUhwetKmpjurXQwf1%2Fimg.png)

‼ [ 클라이언트(사용자)  →  Web Server  →  WAS  →  DB ] 구조의 동작 과정 ‼

1. Web Server는 웹 브라우저 클라이언트(사용자)로부터 HTTP 요청을 받는다.
2. Web Server는 클라이언트의 요청(Request)을 WAS에 보낸다.
3. WAS는 관련된 Servlet을 메모리에 올린다.
4. WAS는 web.xml을 참조하여 해당 Servlet에 대한 Thread를 생성한다. (Thread Pool 이용)
5. HttpServletRequest와 HttpServletResponse 객체를 생성하여 Servlet에 전달한다.
5-1. Thread는 Servlet의 service() 메서드를 호출한다.
5-2. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출한다.
6. protected doGet(HttpServletRequest request, HttpServletResponse response)
7. doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지를 Response 객체에 담아 WAS에 전달한다.
8. WAS는 Response 객체를 HttpResponse 형태로 바꾸어 Web Server에 전달한다.
9. 생성된 Thread를 종료하고, HttpServletRequest와 HttpServletResponse 객체를 제거한다.

---

### # WAS는 이러해야한다

- WAS는 DB 조회 및 다양한 로직을 처리하는 데 집중해야 한다.
- 따라서 단순한 정적 컨텐츠는 웹 서버에게 맡기며 기능을 분리시켜 서버 부하를 방지한다.
- 만약 WAS가 정적 컨텐츠 요청까지 처리하면, 부하가 커지고 동적 컨텐츠 처리가 지연되면서 수행 속도가 느려지고 이로 인해 페이지 노출 시간이 늘어나는 문제가 발생하여 효율성이 크게 떨어진다.

---

### # Web Server와 WAS를 구분하는 이유

- Web Server가 필요한 이유?
  - 클라이언트(웹 브라우저)에 이미지 파일(정적 컨텐츠)을 보내는 과정을 생각해보자.
    - 이미지 파일과 같은 정적인 파일들은 웹 문서(HTML 문서)가 클라이언트로 보내질 때 함께 가는 것이 아니다.
    - 클라이언트는 HTML 문서를 먼저 받고 그에 맞게 필요한 이미지 파일들을 다시 서버로 요청하면 그때서야 이미지 파일을 받아온다.
    - Web Server를 통해 정적인 파일들을 Application Server까지 가지 않고 앞단에서 빠르게 보내줄 수 있다.
  - 따라서 Web Server에서는 `정적 컨텐츠만 처리하도록 기능을 분배`하여 `서버의 부담을 줄일 수 있다.`

- WAS가 필요한 이유?
  - 웹 페이지는 정적 컨텐츠와 동적 컨텐츠가 모두 존재한다.
    - 사용자의 요청에 맞게 적절한 동적 컨텐츠를 만들어서 제공해야 한다.
    - 이때, Web Server만을 이용한다면 사용자가 원하는 요청에 대한 결과값을 모두 미리 만들어 놓고 서비스를 해야 한다.
    - 하지만 이렇게 수행하기에는 자원이 절대적으로 부족하다.
  - 따라서 WAS를 통해 `요청에 맞는 데이터를 DB에서 가져와서 비즈니스 로직에 맞게` 그때 그때 결과를 만들어서 제공함으로써 `자원을 효율적으로 사용할 수 있다.`

### 참고자료

- [[Web] Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
- [[Web] 웹 서버와 WAS의 차이를 쉽게 알아보자](https://codechasseur.tistory.com/25)
