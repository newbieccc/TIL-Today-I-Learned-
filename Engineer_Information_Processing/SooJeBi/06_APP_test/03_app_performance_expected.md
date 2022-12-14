# 애플리케이션 테스트 관리

## # 애플리케이션 성능 - 예상문제

### 01. 괄호안의 용어

- 애플리케이션 성능 측정 지표에 대한 설명
  - 처리량 : 애플리케이션이 주어진 시간에 처리할 수 있는 트랜잭션의 수로 웹 애플리케이션의 경우 시간당 페이지 수로 표현
  - ( `응답 시간` ) : 사용자 입력이 끝난 후, 애플리케이션의 응답 출력이 개시될 때까지의 시간으로 애플리케이션의 경우 메뉴 클릭 시 해당 메뉴가 나타나기까지 걸리는 시간
  - ( `경과 시간` ) : 애플리케이션에 사용자가 요구를 입력한 시점부터 트랜잭션을 처리 후 그 결과의 출력이 완료할 때까지 걸리는 시간
  - 자원 사용률 : 애플리케이션이 트랜잭션을 처리하는 동안 사용하는 CPU 사용량, 메모리 사용량, 네트워크 사용량

---

### 02. 괄호 안의 용어

- 애플리케이션의 성능 분석 도구는 ( `성능 테스트` ) 도구와 ( `시스템 모니터링` ) 도구로 분류 된다.
- ( `성능 테스트` ) 도구는 애플리케이션에 부하나 스트레스를 적용하여 애플리케이션의 성능 측정 지표를 점검하는 도구로 종류에는 JMeter, LoadUI, OpenSTA등이 있다.
- ( `시스템 모니터링` ) 도구는 애플리케이션이 실행되었을 때 시스템 자원 사용량을 확인하고, 분석이 가능한 도구로 종류에는 Scouter, Zabbix 등이 있다.

---

### 03. 괄호안의 용어

- 클린 코드 작성원칙
  - 가독성: 이해하기 쉬운 용어를 사용, 코드 작성 시 들여쓰기 기능을 사용
  - ( `단순성` ): 한 번에 한 가지 처리만 수행, 클래스/메서드/함수를 최소 단위로 분리
  - 의존성: 영향도를 최소화, 코드의 변경이 다른 부분에 영향이 없게 작성
  - 중복성: 중복된 코드를 제거, 공통된 코드를 사용
  - 추상화: 클래스/메서드/함수에 대해 동일한 수준의 추상화 구현, 상세 내용은 하위 클래스/메서드/함수에서 구현

- 소스코드 최적화 기법
  - 변수나 클래스, 메서드 명을 의도가 분명한 이름(사용용도, 작업명)으로 사용한다
  - 클래스는 행위의 주체로 명사나 명사구로 표현하고 함수 이름은 클래스가 행하는 행위로 동사 또는 동사구로 사용한다
  - 클래스는 하나의 역할, 책임만 수행할 수 있도록 ( `응집도` )를 높이고, 크기를 작게 작성한다
  - 클래스의 자료 구조, 메서드를 추상화할 수 있는 인터페이스 클래스를 이용하여 클래스 간의 ( `결합도` )를 최소화해야 한다

---

### 04. 괄호안의 용어

- 애플리케이션 성능 개선 방안에 대한 설명
  - 소스 코드 최적화 기법 적용: 인터페이스를 통해 ( `추상화` )된 자료구조를 구현하여 의존성을 최소화한다.
  - System.out.println() 사용 제외: 파일, 콘솔에 로그를 남기면 애플리케이션 대기 시간이 발생되므로 이에 대응하여 ( `log4j` )를 사용함으로써 성능을 개선한다

---

### 05. 약술

- 배드 코드 사례 중 외계인 코드(Ailen Code)는 무엇인가?
  - `아주 오래되거나 참고문서 또는 개발자가 없어 유지보수 작업이 아주 어려운 코드이다`

---

### 06. 약술

- 소스 코드 품질분석 도구 유형 중 정적 분석 도구의 개념에 대해서 약술하시오
  - `작성된 소스 코드를 실행시키지 않고, 코드 자체만으로 코딩 표준 준수 여부, 코딩 스타일 적정 여부, 잔존 결함 발견 여부를 확인하는 코드 분석 도구이다`

---

### 07. 서술

- 리팩토링(Refactoring)의 개념에 대해서 서술하시오
  - `유지보수 생산성 향상을 목적으로 기능을 변경하지 않고, 복잡한 소스 코드를 수정, 보완하여 가용성 및 가독성을 높이는 기법이다`
