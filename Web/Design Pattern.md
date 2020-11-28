# Design Pattern

일종의 설계 기법

## 개요

### 목적

- SW <u>재사용</u>성
- <u>호환</u>성
- <u>유지보수</u>성

### 특징

- 특정한 구현이 아닌 **"아이디어"** 이다.
- 플젝에 항상 적용해야 하는 것은 아니지만, 추후 재사용/호환/유지보수시 발생하는 **문제를 예방**하기 위해 정한 패턴, 규칙

### 원칙

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

