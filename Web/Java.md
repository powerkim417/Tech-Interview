# Java

## 특징

### 장점

- **JVM**을 사용하므로 OS 및 플랫폼에 독립적
- 객체지향의 여러 개념을 잘 적용한 **객체지향 언어**
- **Garbage collector** 지원
  - 동적할당된 메모리 영역(heap) 중 더이상 필요없는 영역을 탐지하여 자동으로 해제
  - 프로그래머가 메모리 관리를 따로 할 필요가 없음!
- 라이브러리를 통해 **멀티스레드와 동기화를 쉽게 구현 가능**
  - Thread 스케줄링은 java 인터프리터가 담당
- 오픈소스 라이브러리가 풍부하다
  - 고급 기능을 구현하는 코드를 작성하는 대신 검증된 오픈소스 라이브러리를 사용하면 안정성을 높일 수 있으며, 개발 기간을 단축하여 생산성도 높일 수 있다
  - 긴 시간동안 검증되고 쌓여온 라이브러리 → 신뢰성 확보
- **Dynamic Loading**
  - 프로그램 실행 시 모든 클래스를 로딩하지 않고 필요한 시점에 적절히 로드하여 사용

### 단점

- 속도가 **느리다**
  - Java는 한번의 컴파일링으로 실행 가능한 기계어가 만들어지지 않음
  - JVM에 의해 기계어로 번역되고 실행되는 과정을 거치므로 느리다
  - 그러나 하드웨어의 성능 향상과 JIT 컴파일러(바이트코드를 기계어로 번역) 기술 등의 적용으로 JVM의 기능이 향상되어 속도 격차가 많이 줄어들음
- **예외처리가 불편**하다
  - 예외가 발생할 가능성이 있다면 무조건 프로그래머가 선언을 해줘야 함

## Java의 실행 과정

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129202822284.png" alt="image-20201129202822284" style="zoom:67%;" /> 

Java 코드(.java) → 컴파일러(javac) → java byte code(.class) → JVM

- JVM(Java Virtual Machine)

  - Class Loader + Execution Engine(Interpreter + JIT) + Garbage Collector + Runtime Data Area

  - 스택 기반의 가상머신

  - OS가 java byte code를 이해할 수 있게 돕는다.

  - Byte code는 JVM 위에서 OS-dependent하게 실행됨

  - 포인터 대신 reference 활용

  - Class Loader

    - Runtime 시점에 클래스를 로드하며, 인스턴스 생성시 메모리에 로드됨

    1. 로드: 클래스 파일을 가져와서 JVM 메모리에 로드
    2. 검증: 자바언어 명세 및 JVM 명세에 명시된 대로 구성되어 있는지 검사
    3. 준비: 클래스가 필요로 하는 메모리 할당
    4. 분석: 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경
    5. 초기화: 클래스 변수들을 적절한 값으로 초기화(static 필드)

  - 실행 엔진

    - 인터프리터
      - byte code 명령어를 하나씩 읽어서 해석하고 실행
      - 하나하나의 실행은 빠르나, 전체적인 실행 속도는 느림
    - JIT 컴파일러(Just-In-Time Compiler)
      - 인터프리터의 단점을 보완하기 위해 도입된 방식
      - byte code 전체를 컴파일하여 바이너리 코드로 변경하고, 이후에는 헤딩 메서드를 더이상 인터프리팅하지 않고 바이너리 코드로 직접 실행하는 방식

## OOP

### 특징

- 객체(Object)

  - 현실세계의 실체 및 개념을 반영하는 상태(Status)와 행위(Behavior)를 정의한 데이터의 집합

- 객체지향 프로그래밍(Object-Oriented Programming)

  - 각자의 역할을 지닌 객체들끼리 서로 메시지를 주고받으며 동작할 수 있도록 프로그래밍 하는 것

- 장점

  - 사람의 관점에서 프로그램을 이해하고 파악하기 쉬움
  - 강한 응집력과 약한 결합력을 가짐
  - 재사용성, 확장성, 융통성이 높음

  이러한 장점 덕분에 디버깅과 유지보수가 용이하고, 설계와 분석이 비교적 쉽다

- 단점

  - 객체간 정보 교환이 모두 메시지 교환을 통해 일어나므로 오버헤드 많이 발생
    - 처리속도가 느려짐
    - 그러나 이러한 단점은 하드웨어의 발전으로 인해 어느정도 해소
  - 객체가 상태를 가지므로 예상치 못한 부작용 발생
    - 변수가 존재하고, 이 변수를 통해 객체가 예측할 수 없는 상태를 가지면 프로그램 내부에서 버그 발생 가능
    - 이로 인해 함수형 프로그래밍이 생김

### 객체지향과 절차지향의 차이

- 절차지향 프로그래밍
  - 실행하고자 하는 절차를 정하고, 이 절차대로 프로그래밍
  - **일의 흐름**에 중점
- 객체지향 프로그래밍
  - 실세상의 물체를 객체로 표현하고, 이들 사이의 관계와 상호작용을 프로그래밍
  - 연관된 변수와 메서드를 하나의 그룹으로 묶어서 그룹핑
  - 하나의 클래스를 바탕으로 서로 다른 상태를 가진 인스턴스를 만들면 서로 다른 행동을 하게 됨(재활용성)

### OOP의 4가지 특징

1. **추상화(Abstraction)**

   <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129205643850.png" alt="image-20201129205643850" style="zoom:50%;" /> 

   - 구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념(집합)으로 다룸

   - 예시

     - 구체적인 개념에 의존하는 경우

       ```java
       switch (자동차 종류) {
           // 각 차종 별로 엔진 오일을 교환하는 과정을 기술
           case 아우디:
           case 벤츠:
           case BMW:
               
       	// 새로운 종류의 자동차가 나오면 계속해서 추가해야 한다.
       }
       ```

     - 추상적인 개념에 의존하는 경우(추상화 적용)

       ```java
       void changeEngineOil(Car c) {
       	c.changeEngineOil(); // 추상 메서드이므로 새로운 자동차가 나와도 이 부분을 변경할 필요가 없음
       }
       ```

       - 새로운 자동차가 나오면 해당 클래스에서 changeEngineOil()을 오버라이드해 메서드를 구현하면 됨

2. **캡슐화(Encapsulation)**

   - 정보 은닉을 통해 높은 응집도와 낮은 결합도를 유지할 수 있도록 설계해주는 원리

     - 정보 은닉: 필요없는 정보는 외부에서 접근하지 못하도록 제한(private)
     - 응집도: 클래스나 모듈 안의 요소들이 얼마나 밀접하게 관련되어 있는지
     - 결합도: 어떤 기능을 실행하는 데 다른 클래스나 모듈들에 얼마나 의존적인지

   - 예시

     - 강한 결합

       ```java
       /* 자료구조 int[](배열)를 사용하여 Stack을 구현한 클래스 */
       public class ArrayStack {
         // 외부에 공개되어 있다.(public)
         public int top;
         public int[] itemArray; //
         public int stackSize;
         // 생성자
         public ArrayStack(int stackSize){}
         // Stack 관련 메서드들
         public boolean isEmpty(){}
         public boolean isFull(){}
         public void push(int item){}
         public int pop(){}
         public int peek(){}
       }
       
       /* 은닉 내용(자료구조 형태)을 직접 사용한 클래스 */
       public class StackClient {
         public static void main(String[] args) {
           ArrayStack st = new ArrayStack(10);
           st.itemArray[++st.top] = 20; //
           System.out.println(st.itemArray[st.top]);
         }
       }
       ```

       - 이렇게 구현하고, 나중에 Stack의 자료구조를 배열에서 ArrayList로 바꾸려 한다면 <u>클라이언트의 코드까지 다 바꿔야 함</u>

     - 약한 결합

       ```java
       /* 자료구조 int[](배열)를 사용하여 Stack을 구현한 클래스 */
       public class ArrayStack {
         // 은닉되어 있다.(private)
         private int top;
         private int[] itemArray; //
         private int stackSize;
         // 생성자
         public ArrayStack(int stackSize){}
         // Stack 관련 메서드들
         public boolean isEmpty(){}
         public boolean isFull(){}
         public void push(int item){}
         public int pop(){}
         public int peek(){}
       }
       
       /* 은닉 내용(자료구조 형태)을 직접 사용한 클래스 */
       public class StackClient {
         public static void main(String[] args) {
           ArrayListStack st = new ArrayListStack(10);
           st.push(20);
           System.out.println(st.peek());
         }
       ```

       - 이렇게 메서드만 사용하는 방식으로 클라이언트에서 사용하면 private된 자료구조들이 어떻게 바뀌어도 클라이언트는 손댈 필요 없다

   - private

     - 변하기 쉬운 것은 감출 것
     - 외부에서 변해도 영향을 받지 않도록
     - Ex) 멤버 변수, 자료구조

   - public

     - 변하기 어려운 것은 드러낼 것
     - 변하기 어려우므로 외부에서 사용하는데 변경될 일이 적음
     - Ex) Stack 관련 메서드들(push, pop, ...)

3. **일반화 관계(Inheritance, 상속)**

   - 상위 개념의 특징(property, method)을 하위 개념이 물려받는 것
   - 추상화가 하위 클래스들의 공통점을 묶어서 상위 클래스를 만드는 것이라면, 상속은 상위 클래스를 물려주며 더욱 자세한 하위 클래스를 다시 작성할 필요 없이 재사용으로 효율성을 늘림

4. **다형성(Polymorphism)**

   - 서로 다른 클래스의 객체가 같은 메시지를 받았을 때, 각자의 방식으로 동작하는 능력

   - 상속과 연계되어 동작하면 매우 강력한 힘을 발휘

   - 다형성과 일반화 관계는 코드를 간결하게 할 뿐 아니라 변화에도 유연하게 대처할 수 있게 함

   - 예시

     - 다형성을 사용하지 않는 경우

       ```java
       public class Cat {
         public void meow(){ System.out.println("야옹"); }
       }
       public class Dog {
         public void bark(){ System.out.println("멍멍"); }
       }
       public class Parrot {
         public void sing(){ System.out.println("안녕"); }
       }
       
       public class Main {
         public static void main(String[] args) {
           Cat cat = new Cat();
           Dog dog = new Dog();
           Parrot parrot = new Parrot();
           // 애완동물 세 마리의 울음소리 호출
           cat.meow(); dog.bark(); parrot.sing();
         }
       }
       ```

     - 다형성을 사용한 경우

       ```java
       // 부모 클래스
       public abstract class Pet {
         public abstract void talk();
       }
       // 자식 클래스
       public class Cat extends Pet {
         public void talk(){ System.out.println("야옹"); }
       }
       public class Dog extends Pet {
         public void talk(){ System.out.println("멍멍"); }
       }
       public class Parrot extends Pet {
         public void talk(){ System.out.println("안녕"); }
       }
       
       public class Main {
         public static void main(String[] args) {
           Pet[] pets = { new Cat(), new Dog(), new Parrot() };
           // 애완동물 세 마리의 울음소리 호출
           for (int i = 0; i < 3; i++){
             // 실제 참조하는 객체에 따라 talk 메서드가 실행된다.
             pets.talk();
           }
         }
       }
       ```

   - 단, 부모 클래스의 참조변수가 접근할 수 있는 것은 부모 클래스가 물려준 변수와 메서드 뿐이다..

### OOP의 5대 원칙

> **SOLID(객체 지향 설계 원칙)**
>
> 프로그래머가 시간이 지나도 유지보수/확장이 쉬운 소프트웨어를 만들기 위해 이 원칙을 적용한다.

1. **Single** Responsibility Principle (SRP, 단일 책임 원칙)

   - <u>소프트웨어의 설계 부품(클래스, 함수 등)</u>은 <u>단 하나의 책임(기능)</u>만을 가져야 함
   - <u>객체의 단일 책임</u>

   - 즉, 응집도는 높고 결합도는 낮게!
     - 응집도: 한 프로그램의 요소가 얼마나 뭉쳐있는지
     - 결합도: 요소들 사이의 의존도
     - 한 객체에 책임이 많아질 수록 클래스 내부에서 서로 다른 역할을 수행하는 코드끼리 강하게 결합될 가능성이 높아짐..
   - 각 객체들이 하나의 책임만 갖도록 잘 분배한다면, <u>시스템에 변화가 생기더라도 그 영향을 최소화</u>할 수 있다.
   - Ex) 계산기
     - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129023730371.png" alt="image-20201129023730371" style="zoom:50%;" />
     - calculator() 함수에 사칙연산이 다 들어가는 것은 비효율적!
     - 대신 add(), sub(), mul(), div() 함수를 가진 Calculator 객체로 만든다.
     - 알람 기능을 넣어야 할 경우..
     - Calculator 객체는 사칙연산만 해야 하므로 여기에 alarm()를 구현하지 말고
     - Alarm 객체를 따로 만든 뒤, 두 객체를 모두 포함하는 한 객체를 새로 만드는 것이 낫다.

2. **Open** - Closed Principle (OCP, 개방 - 폐쇄 원칙)

   - <u>기존의 코드를 변경하지 않고</u>(closed) <u>기능을 수정하거나 추가</u>(open)할 수 있도록 설계해야 함

   - 즉, 확장에 대해서는 개방적(open)이고 (코드의) 수정에 대해서는 폐쇄적(closed)이어야 한다.

   - <u>캡슐화</u>를 통해 여러 객체에서 사용하는 같은 기능을 인터페이스에 정의

     - 캡슐화: 연관이 있는 변수와 함수를 클래스로 묶는 것

   - Ex) 동물 울음소리

     - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129033449547.png" alt="image-20201129033449547" style="zoom:50%;" />

     - crying() 메서드를 가지는 Animal 인터페이스를 만들고, 이를 implement한 각 동물 클래스 내에서 crying() 함수를 각 동물의 울음 방식에 맞게 재정의한다.

     - 이렇게 캡슐화를 하면 동물이 추가되어도 클라이언트가 crying() 함수를 호출하는 부분을 건드릴 필요가 없으면서 쉽게 확장이 가능

     - ```java
       public class Client {
           public static void main(String args[]){
               Animal cat = new Cat();
               Animal dog = new Dog();
               
               cat.crying();
               dog.crying();
           }
       } 
       ```

3. **Liskov** Substitution Principle (LSP, 리스코프 치환 원칙)
   - <u>자식 클래스</u>는 최소한 자신의 <u>부모 클래스에서 가능한 행위는 수행할 수 있어야</u> 함
   - 즉, 자식 클래스는 언제나 부모 클래스의 역할을 대체할 수 있어야 한다.
     - 그러기 위해서는 부모의 기능에 대해 오버라이드되지 않도록 해야 한다.
     - 즉, <u>부모 클래스의 기능을 무시하거나 재정의하지 않고 확장만!</u>
   - Ex) 도형 클래스를 구현하고, LSP를 만족하는지 확인
     - 도형 클래스를 "도형은 둘레를 가짐 / 도형은 넓이를 가짐 / 도형은 각을 가짐" 으로 구현
     - 이를 상속받는 사각형 클래스의 경우 '도형'을 '사각형'으로 대체했을 때 문제가 되지 않음
     - 그러나, 원 클래스가 이를 상속받으려 할 때 '원은 각을 가짐'이 되지 않으므로 위와 같이 도형 클래스를 구현한 것은 LSP를 만족하지 못함 

4. **Interface** Segregation Principle (ISP, 인터페이스 분리 원칙)
   - <u>사용하지 않는 인터페이스는 구현하지 말아야</u> 함
   - 즉, 하나의 거대한 인터페이스보다는 여러 개의 구체적 인터페이스가 낫다.
   - <u>인터페이스의 단일 책임</u>
   - Ex) 같은 기능들을 필요로 하는 옛날 폰과 현재 스마트폰에 대한 인터페이스 구현
     - Phone() 이라는 인터페이스를 정의해 두 폰 클래스가 이 인터페이스를 구현한다면 아래처럼 된다.
     - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129025858865.png" alt="image-20201129025858865" style="zoom:50%;" />
     - 그러나, 이는 ISP를 만족하지 않음(Phone 인터페이스가 여러 기능을 담고 있음)
     - ISP를 만족하려면, 각 기능에 대한 인터페이스를 정의하고, 두 폰 클래스가 이 인터페이스들을 구현하도록 하면 된다.
     - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129030041799.png" alt="image-20201129030041799" style="zoom:50%;" />
     - 이러면 각 인터페이스의 메서드들이 서로 영향을 미치지 않게 할 수 있다!

5. **Dependency** Inversion Property (DIP, 의존 역전 원칙)
   - 객체들이 서로 정보를 주고받을 때 의존 관계가 형성되는데, 이 때 객체들은 나름대로의 원칙을 갖고 정보를 주고 받아야 한다.
     - 나름대로의 원칙: "<u>추상성이 더 높은 클래스</u>(인터페이스 또는 추상 클래스)<u>와 의존 관계를 맺어야 한다</u>" → 캡슐화
     - 의존성 주입
   - Ex) 동물 울음소리
     - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129033010687.png" alt="image-20201129033010687" style="zoom:50%;" />
     - Client 객체가 추상성이 낮은 클래스(Cat, Dog, Bird)의 crying() 메서드에 직접 접근하지 않고, 추상성이 높은 클래스(Animal 인터페이스)의 crying() 메서드를 호출함으로써 DIP 만족

## 기타

데이터 타입

클래스-객체-인스턴스

접근제어자



static

final

generic

serialize

오버로딩-오버라이딩

cbr, cbv

인터페이스, 추상클래스

map

set

list

annotation

string-stringbuilder-stringbuffer

동기화

==, equals

reflection

stream

lambda



