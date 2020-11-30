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

### 분류

|                    생성(Creational) 패턴                     |                    구조(Structural) 패턴                     |                    행위(Behavioral) 패턴                     |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| Abstract Factory<br />Builder<br />Factory Method<br />Prototype<br />**Singleton** | Adapter<br />Bridge<br />Composite<br />Decorator<br />Facade<br />Flyweight<br />Proxy | Chain of Responsibility<br />Command<br />Interpreter<br />Iterator<br />Mediator<br />Memento<br />Observer<br />State<br />Strategy<br />Template Method<br />Visitor |

1. 생성(Creational) 패턴
   - 객체 생성과 관련된 패턴
   - 객체의 생성과 조합을 캡슐화해 특정 객체가 생성 및 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성 제공
   - Ex) 싱글톤(Singleton): 전역변수를 사용하지 않고 객체를 하나만 생성하며, 생성된 객체를 어디서든지 참조할 수 있도록 하는 패턴
2. 구조(Structural) 패턴
   - 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
   - 서로 다른 인터페이스를 지닌 2개의 객체를 묶어 단일 인터페이스를 제공하거나, 새로운 기능을 제공
3. 행위(Behavioral) 패턴
   - 객체나 클래스 사이의 알고리즘이나 책임 분배에 관련된 패턴
   - 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 동시에 객체 간 결합도를 최소화하는 것에 중점

## 싱글톤 패턴

인스턴스가 프로그램 내에서 오직 '하나'만 생성(static)되는 것을 보장하고, 프로그램 어디서든 이 인스턴스에 접근할 수 있도록 하는 패턴

- 인스턴스가 사용될 때 똑같은 인스턴스를 여러개 만들지 않고, 기존에 생성한 인스턴스를 사용

### 구현 방식

```java
public class SingleObj {
    private static SingleObj singleObj = null;

    // 외부에서 직접 생성하지 못하도록 private 선언
    private SingleObj(){ }

    // 오직 1개의 객체만 생성
    public static SingleObj getInstance(){
        if( singleObj == null ){
            singleObj = new SingleObj();
        }

        return singleObj;
    }
}
```

- 생성자를 **private**으로 선언하여 외부에서 생성 불가능하게 하고, getInstance() 메서드를 통해서만 받아 사용하도록 구현
- **static**으로 정의하고 이 메모리에서만 인스턴스가 생기고 작업에 사용된다.

### 특징

- 주로 사용하는 경우
  - <u>공통된 객체를 여러개</u> 생성해서 사용해야 하는 상황
    - Ex) 데이터베이스에서 커넥션풀, 스레드풀, 캐시, 로그 기록 객체 등
  - <u>안드로이드 앱</u>에서 각 액티비티/클래스 마다 주요 클래스들을 하나하나 전달하는 것이 번거롭기 때문에 싱글톤 클래스를 만들어 어디서든 접근하도록 설계
  - 인스턴스가 절대적으로 <u>한 개만 존재하는 것을 보증</u>하고 싶을 때

- 장점
  - 한번의 new만 사용하여 객체를 생성하므로 메모리 낭비 방지
  - 싱글톤 인스턴스는 '전역'이므로 다른 클래스 인스턴스와 데이터 공유 가능
- 단점
  - 싱글톤 인스턴스가 혼자 너무 많은 일을 하거나, 많은 데이터를 공유시키게 된다면 다른 클래스들 간 결합도가 높아져 SOLID 원칙 중 OCP(개방-폐쇄 원칙) 위배
  - 멀티스레드 환경에서 동기화 처리를 하지 않았다면 인스턴스가 여러 개 생길 수 있음
  - **싱글톤은 딱 하나만 존재할 수 있으므로 필드도 하나만 존재한다. 그래서 상태를 가진 객체를 여러개 만들 수 없다.**

### 멀티스레드 환경에서 안전한 싱글톤 구현

1. Lazy Initialization

```java
public class ThreadSafe_Lazy_Initialization{
 
    private static ThreadSafe_Lazy_Initialization instance;
 
    private ThreadSafe_Lazy_Initialization(){}
     
    public static synchronized ThreadSafe_Lazy_Initialization getInstance(){
        if(instance == null){
            instance = new ThreadSafe_Lazy_Initialization();
        }
        return instance;
    }
 
}
```

- private static 인스턴스 변수
- private 생성자
- synchronized 동기화를 활용해 스레드를 안전하게 만듦
  - 그러나, synchronized는 큰 성능저하를 발생시키므로 권장하지 않음

2. Lazy Initialization + Double-checked Locking

```java
public class ThreadSafe_Lazy_Initialization{
    private volatile static ThreadSafe_Lazy_Initialization instance;

    private ThreadSafe_Lazy_Initialization(){}

    public static ThreadSafe_Lazy_Initialization getInstance(){
    	if(instance == null) {
        	synchronized (ThreadSafe_Lazy_Initialization.class){
                if(instance == null){
                    instance = new ThreadSafe_Lazy_Initialization();
                }
            }
        }
        return instance;
    }
}
```

- 1번의 성능저하를 완화시키는 방법
- synchronized에 들어가기 전에 먼저 인스턴스 존재 여부를 확인하고, 인스턴스가 존재하지 않을 경우에만 동기화를 시켜 인스턴스를 생성
  - 즉, 1번 방법은 인스턴스가 있는 경우에도 synchronized에 들어가지만, 2번 방법에서는 인스턴스가 이미 있다면 동기화 과정을 거치지 않음

3. Initialization on demand holder idiom

```java
public class Something {
    private Something() {}
 
    private static class LazyHolder {
        public static final Something INSTANCE = new Something();
    }
 
    public static Something getInstance() {
        return LazyHolder.INSTANCE;
    }
}
```

- 클래스 안에 클래스(holder)를 두어, JVM의 클래스 로더 매커니즘과 클래스 로드 시점을 이용한 방법
- 1, 2번 처럼 개발자가 직접 동기화 문제에 대한 코드를 작성하여 회피하려고 하면 프로그램 구조가 그만큼 복잡해지고 비용 문제 발생
- 그에 반해 3번은 JVM의 클래스 초기화 과정에서 보장되는 원자적 특성을 이용해 싱글톤 초기화 문제에 대한 책임을 JVM에게 넘김
- holder에서 선언된 인스턴스는 static이므로 클래스 로딩 시 한번만 호출되며, final을 사용해서 다시 값이 할당되지 않음!
- **실제로 가장 많이 사용되는 방법**

## MVC 패턴

### 구성 요소

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129161236049.png" alt="image-20201129161236049" style="zoom:50%;" /> 

- Model
  - 애플리케이션의 데이터
  - DB의 **데이터를 처리**하는 부분
- View
  - **사용자에게 보여지는** 인터페이스
  - Ex) 웹의 HTML 문서
- Controller
  - 사용자의 입력을 받아 처리하는 부분, 즉 모든 이벤트를 처리하는 메인 로직 담당
  - **데이터(Model)와 인터페이스(View)간의 상호 동작 관리**
  - Model에 명령을 보내 데이터의 상태를 바꾸거나, 어떤 화면을 사용자에게 보여줄지 View에 명령한다.

### 특징

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129162631470.png" alt="image-20201129162631470" style="zoom:50%;" />

- Model은 가급적 나머지 컴포넌트의 상태를 알지 못하게 해야 한다.
  - 반대로 View나 Controller는 Model의 상태 변화에 대해 자세히 알아야 이를 반영할 수 있다. (Observer Pattern)
  - MVC 패턴의 완성도를 가늠하려면 model 부분이 다른 UI를 위해서도 support가 되는지 테스트해보면 된다.
  - 즉, View와 Controller를 교체해도 Model이 변하지 않으면 MVC 패턴의 완성도가 높은 것!
- View 위젯은 nested 하게 만들어야 한다.
  - div 속에 div가 있고, 그 안에 a와 p가 있는 것처럼! (Composite Pattern)
- View가 Controller에게 gesture를 위임해야 한다. (Strategy Pattern)

- 동작 순서
  1. Controller로 사용자의 입력이 들어옴
  2. Controller는 Model의 데이터를 업데이트하거나 불러오고
  3. Model은 해당 데이터를 보여줄 View를 선택해서 화면에 보여주게 됨
- 장점
  - 전형적인 어플리케이션 OOP 구조로써 가장 단순하며 보편적으로 많이 사용
  - 각자 맡은 일에만 집중할 수 있게 되어 효율성이 높아지고 유지보수가 편리해지며 프로그램의 확장성/유연성이 늘어나고 중복코딩의 문제점이 사라짐
  - 유저 인터페이스 - 비지니스 로직 분리

- 단점
  - Controller가 중간 다리 역할을 해주지만, **View와 Model이 서로 의존적임**
    - 프로그램이 커질수록 복잡하고 유지보수가 어려워질 수 있음

### 구현

- Model

  - 멤버변수와 그에 대한 getter 및 setter를 가지고 있음

  ```java
  public class Student {
      // 멤버 변수
      private String rollNo;
      private String name;
      
      // getter & setter
      public String getRollNo() { return rollNo; }
      public void setRollNo(String rollNo) { this.rollNo = rollNo; }
      public String getName() { return name; }
      public void setName(String name) { this.name = name; }
  }
  ```

- View

  - 전달받은 정보를 표시

  ```java
  public class StudentView {
      public void printStudentDetails(String studentName, String studentRollNo){
          System.out.println("Student: ");
          System.out.println("Name: " + studentName);
          System.out.println("Roll No: " + studentRollNo);
      }
  }
  ```

- Controller

  - Model과 View를 받음
  - Model의 멤버 변수에 대한 getter & setter
  - View를 업데이트하는 함수 존재

  ```java
  public class StudentController {
      
      // Model, View
      private Student model;
      private StudentView view;
      
      // 컨트롤러 생성자
      public StudentController(Student model, StudentView view){
          this.model = model;
          this.view = view;
      }
  
      // Model 멤버변수에 대한 getter & setter
      public void setStudentName(String name){ model.setName(name); }
      public String getStudentName(){ return model.getName(); }
      public void setStudentRollNo(String rollNo){ model.setRollNo(rollNo); }
      public String getStudentRollNo(){ return model.getRollNo(); }
  
      // Model로부터 전달받은 값을 통해 View를 업데이트
      public void updateView(){           
         view.printStudentDetails(model.getName(), model.getRollNo());
      }  
  }
  ```

- Controller를 사용하는 메인 프로그램 부분

  ```java
  public class MVCPatternDemo {
      public static void main(String[] args) {
          // DB로부터 학생 정보를 받아와 저장하는 Model
          Student model  = retriveStudentFromDatabase();
          // View 생성
          StudentView view = new StudentView();
  		// Controller 생성 후 M-V를 연결
          StudentController controller = new StudentController(model, view);
          controller.updateView();
  
          // 사용자 요청으로 데이터 수정
          controller.setStudentName("John");
          controller.updateView();
      }
  
      // DB로부터 정보를 받아옴
      private static Student retriveStudentFromDatabase(){
          Student student = new Student();
          student.setName("Robert");
          student.setRollNo("10");
          return student;
      }
  }
  ```

## MVP 패턴

- MVC 패턴의 단점(V-M 의존성) 보완

- Presenter
  - View에서 요청한 정보를 Model로부터 가공해서 View로 전달하는 부분
  - 사실상 중간 다리 역할

### 특징

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129162950369.png" alt="image-20201129162950369" style="zoom:50%;" /> 

- 동작 순서
  1. <u>View로 사용자의 입력이 들어옴</u>
  2. View가 Presenter에 작업 요청
  3. Presenter에서 필요한 데이터를 Model에 요청
  4. Model은 Presenter에 필요한 데이터를 응답
  5. Presenter는 View에 데이터를 전달
  6. View는 Presenter로부터 받은 데이터를 화면에 보여줌

- Model과 View가 Presenter와 상호동작을 하게 됨
  - **MVC의 단점인 View-Model간 의존성 해소 가능**
  - 하지만 **MVP는 이로 인해 View와 Presenter가 강한 의존성을 가지게 됨**

## MVVM 패턴

- MVP 패턴의 단점(V-P 의존성) 보완

- ViewModel
  - View를 표현하기 위해 만들어진 Model

### 특징

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201129163420733.png" alt="image-20201129163420733" style="zoom:50%;" /> 

- Command 패턴과 Data Binding 패턴으로 인해 V와 VM간의 의존성 제거

- 동작 순서
  1. View에 입력이 들어오면 Command 패턴으로 ViewModel에 명령
  2. ViewModel은 필요한 데이터를 Model에 요청
  3. Model은 필요한 데이터를 ViewModel에 응답
  4. VIewModel은 응답받은 데이터를 가공해서 저장
  5. View는 ViewModel과의 Data Binding으로 인해 자동으로 갱신됨