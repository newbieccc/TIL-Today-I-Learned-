# 정보처리기사 2024

## # 2-5. 소프트웨어 개발 - 인터페이스 구현

### # 1. 인터페이스 설계 확인 2-122page

---

### # 2. 인터페이스 기능 구현 2-127page

### 6. 인터페이스 간의 통신을 위한 데이터 포맷

- 인터페이스 간의 통신을 위해서 이용되는 데이터 포멧은..
  - JSON
  - XML
  - YAML
- AJTML(x)

```markdown
- JSON
  - 비동기 브라우저/서버 통신(AJAX)을 위해 "속성-값 쌍", "키-값 쌍"으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷
- XML
  - W3C에서 개발된, 다른 특수한 목적을 갖는 마크업 언어를 만드는 데 사용하도록 권장하는 다목적 마크업 언어
- YAML
  - 데이터를 사람이 쉽게 읽을 수 있는 형태로 표현하기 위해 사용하는 데이터 직렬화 양식
```

### 8. 단위 테스트 도구의 종류

- 단위 테스트 도구로 사용할 수 있는 종류
  - CppUnit(C++)
  - JUnit(java)
  - HttpUnit(Web)
- 인터페이스 구현 검증 도구의 종류 중 xUnit은 소프트웨어의 함수나 클래스 같은 서로 다른 구성 원소(단위)를 테스트할 수 있게 해주는 도구이다.
