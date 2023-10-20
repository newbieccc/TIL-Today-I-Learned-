# Java

## 객체지향 언어

### 객체지향 언어란?

- 현실세상에서 우리가 관찰할 수 있는 모든 객체(ex, 자동차, 바퀴, 의자, 사람 등)는
- 자신만의 "속성"과 "기능"을 가지고 상호작용한다고 보고,
- 이러한 개념을 프로그램에 적용하여 여러가지 독립된 단위인 객체를 생성하고,
- 조작하여 객체끼리 상호작용할 수 있게 하는 프로그래밍 언어를 말한다.

### 객체, 클래스, 인스턴스

- 객체
  - 프로그램상에서 구현할 대상
- 클래스
  - 객체의 "속성"과 "기능"을 정의한 설계도와 같은 것
- 인스턴스
  - 클래스의 내용대로 메모리상에 구현된 실체

### 객체지향언어의 특징 (캡슐화, 상속, 다형성)

- 캡슐화 (Encapsulation)
  - 객체의 내부 구조 및 정보를 캡슐처럼 하나로 감싸 외부에서 볼수 없게 은닉하여 보호하는 것
  - 외부와의 상호작용을 위해 필요한 부분만 일부 공개

- 상속 (Inheritance)
  - 부모 클래스로부터 자식 클래스가 부모 클래스의 속성을 물려받는 것
  - 자식 클래스는 부모 클래스가 가지고 있는 속성에 자식 클래스만의 속성을 추가함으로써 기능을 확장시켜 사용할 수 있다.
    - 이때 부모클래스를 슈퍼클래스, 자식클래스를 서브클래스라고 부른다.

- 다형성 (Polymorphism)
  - 하나의 객체나 메소드가 여러가지 다른 형태를 가질 수 있는 것
  - 오버라이딩(overriding)과 오버로딩(overloading), 그리고 상속받은 객체의 참조변수 변환등이 있다.
    - 오버라이딩(overriding) : 부모클래스로부터 상속받은 메소드를 자식클래스에서 재정의하여 사용하는 것.
    - 오버로딩(overloading) : 메소드의 이름은 동일하나 매개변수의 타입이나 개수를 달리하여 중복 정의함으로써 매개변수에 따라 특정 메소드가 호출되는 것.

### 객체 지향적 설계 원칙

1. SRP(Single Responsibility Principle) : 단일 책임 원칙
   - 클래스는 단 하나의 책임을 가져야 하며 클래스를 변경하는 이유는 단 하나의 이유이어야 한다.
2. OCP(Open-Closed Principle) : 개방-폐쇄 원칙
   - 확장에는 열려 있어야 하고 변경에는 닫혀 있어야 한다.
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
   - 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.
4. ISP(Interface Segregation Principle) : 인터페이스 분리 원칙
   - 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
5. DIP(Dependency Inversion Principle) : 의존 역전 원칙
   - 고수준 모듈은 저수준 모듈의 구현에 의존해서는 안된다.

### 참고

- [KADOSHoly/[Java] 객체지향언어란? 특징(캡슐화, 상속, 다형성)과 클래스, 객체, 인스턴스](https://kadosholy.tistory.com/88)
- [JaeYeopHan/Interview_Question_for_Beginner/Object Oriented Programming](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Development_common_sense#object-oriented-programming)
