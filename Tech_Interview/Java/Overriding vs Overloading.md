# Java

## Overloading vs Overriding

### 오버라이딩(Overriding)

- 상위 클래스의 메서드와 이름과 용례(signature)가 같은 함수를 하위 클래스에 재정의하는 것을 말한다.
- 즉, 상속 관계에 있는 클래스 간에 같은 이름의 메서드를 정의하는 것을 말한다.
- 상위 클래스 혹은 인터페이스에 존재하는 메소드를 하위 클래스에서 필요에 맞게 재정의하는 것을 의미한다.
- 자바의 경우는 오버라이딩 시 동적바인딩된다.

```java
public class Computer2 {

  protected String manufacturer; 
  protected String processor; 
  protected int ramSize; 
  protected int diskSize; 
  protected double processorSpeed; 

  public Computer2(String man, String proc, int ram, int disk, double procSpeed) { 
    manufacturer = man; 
    this.processor = proc; 
    ramSize = ram; 
    diskSize = disk; 
    processorSpeed = procSpeed; 
  }

  public String toString() {
    String result = "Manufacturer: " + manufacturer + 
            "\nCPU: " + processor + 
            "\nRAM: " + ramSize + " megabytes" + 
            "\nDisk: " + diskSize + " gigabytes" + 
            "\nProcessor speed: " + processorSpeed + " gigahertz";
    return result;
  }
}

public class Notebook2 extends Computer2{
  public double screenSize;
  public double weight;
  public Notebook2(String man, String proc, int ram, int disk, double speed, double screen, double weight) {
    super(man, proc, ram, disk, speed);
    screenSize = screen;
    this.weight = weight;
  }
  public String toString() {
    String result = 
            super.toString() +
            //의미 : Notebook2의 toString() 메서드가 Computer2의 toString() 메서드를 override 하였다.
            //Notebook2의 super클래스 메서드를 호출로 생략
        
            //"Manufacturer: " + manufacturer + 
            //"\nCPU: " + processor + 
            //"\nRAM: " + ramSize + " megabytes" + 
            //"\nDisk: " + diskSize + " gigabytes" + 
            //"\nProcessor speed: " + processorSpeed + " gigahertz" +
            
            //Notebook2의 변수를 추가
            "\nScreen Size: " + screenSize + " inches" +
            "\nWeight: " + weight + " kg.";
    return result;
  }
  public static void main(String[] args) {
    Notebook2 note = new Notebook2("windows", "14", 4, 1000, 3.2, 15.6, 1.2);
    System.out.println(note.computePower());
    
    System.out.println(note.toString());
  }
}

```

---

### 오버로딩(Overloading)

- 두 메서드가 같은 이름을 갖고 있으나 인자의 수나 자료형이 다른 경우를 말한다.
- return 타입은 동일하거나 다를 수 있지만, return 타입만 다를 수는 없다.
- 매개변수의 타입이나 갯수가 다른 메소드를 만드는 것을 의미한다.
- 다양한 상황에서 메소드가 호출될 수 있도록 한다.
- 자바의경우 오버로딩은 다른 시그니쳐를 만드는 것으로, 아예 다른함수를 만든것과 비슷하다고 생각하면 된다.
- 시그니쳐가 다르므로 정적바인딩으로 처리 가능하며, 자바의 경우 정적으로 바인딩된다.

```java
public int overloading(int a){}
public int overloading(int a, int b){}
public int overloading(String str){}
```

---

### 참고

- [https://github.com/JaeYeopHan/Interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Java#overriding-vs-overloading)
- [[Java] 오버로딩과 오버라이딩의 차이(Overloading VS Overriding)](https://gmlwjd9405.github.io/2018/08/09/java-overloading-vs-overriding.html)
- [Java로 배우는 자료구조 - 권오흠님](https://github.com/newbieccc/TIL-Today-I-Learned-/blob/ce13cee8ceb34ed164835da541d196875ec5a2d0/Java/Algorithms_to_learn_in_Java/07.inheritance/07_2.md)
