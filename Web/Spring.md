# Spring

## 용어

- 컨테이너
  - 인스턴스의 생명 주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것
  - 작성한 코드의 처리과정을 위임받은 독립적 존재
  - bean 객체들이 들어있는 통
- bean
  - 스프링 컨테이너 상에서 생성된 객체

## 특징

- **경량 컨테이너**로서 자바 객체를 직접 관리
  - 각 <u>객체의 생성 및 소멸과 같은 life cycle을 관리</u>하며 스프링으로부터 필요한 객체를 얻어올 수 있음
- **POJO(Plain Old Java Object)** 방식의 프레임워크
  - 구현을 위해 특정한 인터페이스를 구현하거나 상속을 받을 필요가 없어 기존 라이브러리들을 지원하기 쉬우며, 객체가 가볍다
- **제어 반전(IoC)** 지원
  - 컨트롤의 제어권이 프레임워크에 있다
  - 필요에 따라 스프링에서 사용자의 코드를 호출함
- **의존성 주입(DI)** 지원
  - 각각 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결시켜줌
- **관점 지향 프로그래밍(AOP)** 지원
  - 트랜잭션, 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 관리할 수 있음
- **영속성**과 관련된 다양한 서비스 지원
  - iBATIS, 하이버네이트 등 이미 완성도 높은 DB처리 라이브러리와 연결할 수 있는 인터페이스 제공
- **확장성**이 높음
  - 스프링 프레임워크에 통합하기 위해
  - 간단하게 기존 라이브러리를 감싸는 식으로 하면 스프링에서 사용 가능!

### IoC(Inversion of Control, 제어 반전)

- 목표: 낮은 결합도와 높은 응집도

- 스프링은 IoC를 통해 어플리케이션을 구성하는 객체간의 낮은 결합도를 유지

- 객체 생성 및 객체간 의존관계를 컨테이너가 처리

- 비교

  - 개발자가 직접 객체를 생성하여 코드를 제어

    ```java
    public class A {
    
        private B b;
    
        public A()
            b = new B();
        }
    }
    ```

  - 컨테이너에 의해서 생성한 객체를 사용

    ```java
    public class A {
    
        @Autowired
        private B b;
    
    }
    ```

### DI(Dependency Injection, 의존성 주입)

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201201032803348.png" alt="image-20201201032803348" style="zoom: 67%;" /> 

- 의존성 관계: 객체 간의 결합 관계 
- 의존성 주입: 객체가 필요로 하는 객체를 생성자 또는 setter를 통해 주입하는 것!
- 하나의 객체에서 다른 객체의 변수나 메서드를 이용해야 한다면 이용하려는 객체에 대한 객체를 생성해야 하고, 생성된 객체의 레퍼런스 정보가 필요함
- 의존 관계는 new라는 키워드를 통해 생성되는데
  - A obj = new B(); 와 같이 짜면 A는 B에 의존하게 됨(깡한 결합도)
    - 
  - A라는 객체에서 B를 생성하는 것이 아니라
  - 외부에서 생성된 B를 A에 주입함으로써 의존관계를 없앤다!
  - ctx.getBean(...);
  - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201201031014729.png" alt="image-20201201031014729" style="zoom: 67%;" />
  - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201201031131316.png" alt="image-20201201031131316" style="zoom:67%;" />
  - <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201201031026065.png" alt="image-20201201031026065" style="zoom:67%;" />

#### 의존성 주입 방법

- XML을 통한 의존성 주입
  - 분리
    - <u>유지보수성</u>에 의의
    - 그러나 xml이 너무 많아지면 오히려 유지보수성이 낮아짐..
    - **시스템 전반에 영향을 주고, 이후에 변경 가능성이 있는 것은 xml로 설정**
  - 주입 방법
    - 생성자를 통한 의존성 주입
      - 생성자에 인자로 주입하고자 하는 객체를 넣어준다.
      - \<constructor-arg\> 태그의 ref 속성
    - java config를 통한 의존성 주입
      - set method 사용
      - \<property\> 태그에서 name 속성
- Annotation을 통한 의존성 주입
  - 결합
    - <u>생산성</u>에 의의
    - 의미를 갖는 주석?
    - 프로그램 규모가 커짐에 따라 XML이 가지는 설정정보의 양이 많아지는데, annotation은 직관적인 메타데이터 설정이 가능
    - **설계시 확정되는 부분은 annotation 기반으로 설정**
  - 주입 방법
    - @Autowired(Spring)
      - 속성의 설정자 메서드에 해당하는 역할을 자동으로 수행
      - 객체의 <u>타입 → 이름 → Qualifier</u>를 기준으로 bean을 찾음
    - @Resource(Java)
      - setter, 속성값에 붙일 수 있으며, 생성자에는 못 붙임
      - 객체의 <u>타입 → 이름 → Qualifier</u>을 기준으로 bean을 찾음

### AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)

## 동작 순서 및 구조

![image-20201130233144222](C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201130233144222.png)

Request → DispatcherServlet → HandlerMapping → Controller → Service → DAO → DB

→ DAO → Service → Controller → DispatcherServlet → ViewResolver → View → Response

1. 클라이언트가 **request**를 하면 **DispatcherServlet**이 이 request를 가로챔
   - web.xml의 \<url-pattern\>에 등록된 내용만 가로챔
2. **DispatcherServlet**이 가로챈 요청을 **HandlerMapping**에게 보내 해당 요청을 처리할 수 있는 **Controller**를 찾음
3. 로직 처리 (**Controller** → **Service** → **DAO** → **DB** → **DAO** → **Service** → **Controller**)
4. 로직 처리 후 **ViewResolver**를 통해 **View** 화면을 찾음
5. View 화면을 최종 클라이언트에게 **response**함

## Spring Security

## 기타

### XSS

- 게시판이나 웹메일 등에 js와 같은 스크립트 코드를 삽입해 개발자가 고려하지 않은 기능이 작동하게 하는 공격.

- 클라이언트를 대상으로 한 공격

#### 위험성

- 쿠키 정보 및 세션 ID 획득
- 시스템 관리자 권한 획득
- 악성코드 다운로드
- 거짓 페이지 노출

#### 방지법

- script 문자 필터링
  - 스크립트를 실행하기 위한 <, >, ", ' 등의 문자
- htmlentities 사용(php)
  - 모든 특수문자를 HTML 엔티티로 변환
- JSTL의 \<c:out\> 태그 사용
  - 모든 값이 문자열로 출력됨
  - 모든 view 페이지에 작성해야 하므로 적용해야 할 페이지 수가 많다면 작업량이 많아짐
- script 코드 검사
  - DB 입력 전 FE/BE에서 입력값에 script 코드가 포함되어 있는지 확인하는 방식
  - script가 포함되었을 경우 등록 불가!
  - indexOf, contains, startWith, 정규식 등 활용
- **XSS Filter 적용**
  - Servlet Filter에 파라미터에 포함된 HTML 엔티티를 escape 문자로 치환하는 XSS Filter 적용
  - 가장 손쉽게 처리할 수 있는 방법
  - Ex) 네이버의 lucy-xss
  - 동작 원리
    1. ServletRequest를 wrapping할 클래스를 생성
    2. getParameter, getParameterValues를 escape 문자로 치환하도록 재정의하고
    3. Filter간 Filter Chain 특성을 이용하여 wrapping한 객체를 다음 filter로 전달