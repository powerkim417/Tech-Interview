# Operating System 운영체제

### 운영체제란?

하드웨어 관리 & 응용프로그램-하드웨어 간 인터페이스 & 시스템 동작 제어

**시스템의 자원과 동작을 관리하는 소프트웨어**

#### 프로세스 관리

프로세스, 스레드 / 스케줄링 / 동기화 / IPC 통신

- OS에서 작동하는 응용 프로그램을 관리
- 프로세서(CPU) 관리로도 볼 수 있음
  - 현재 CPU를 점유해야 할 프로세스를 결정하고,
  - CPU를 프로세스에 할당하며
  - 프로세스 간 공유자원 접근과 통신 관리

#### 저장장치 관리

메모리 관리 / 가상 메모리 / 파일 시스템

- 1차 저장장치(메인 메모리)
  - 프로세스에 할당하는 메모리 영역 할당/해제
  - 메모리 영역 간 침범 방지
  - 메인 메모리 효율적 활용을 위한 가상 메모리 기능
- 2차 저장장치(HDD, NAND 플래시 메모리 등)
  - 파일 형식 데이터 저장
  - 파일 데이터 관리를 위한 파일시스템을 os에서 관리

#### 네트워킹

TCP/IP / 기타 프로토콜

- 인터넷에 연결하거나 네트워크 사용을 위해 **네트워크 프로토콜 지원**
- 사용자와 하드웨어 사이에서 제어/관리하는 셈



#### 사용자 관리

계정 관리 / 접근권한 관리

- 각 계정을 관리할 수 있는 기능
  - 사용자별 프라이버시 및 보안을 위해
- 파일이나 시스템 자원에 접근 권한 지정

#### 디바이스 드라이버

순차접근 장치 / 임의접근 장치 / 네트워크 장치

- 시스템에 연결된 하드웨어를 운영체제에서 인식하고 관리
  - 응용프로그램이 하드웨어를 사용할 수 있도록!
- 하드웨어를 추상화 해주는 계층 필요(= 디바이스 드라이버)
- 이러한 디바이스 드라이버를 관리

### 프로세스와 스레드

- **프로세스**: 프로그램을 메모리 상에서 실행중인 작업

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120202801434.png" alt="image-20201120202801434" style="zoom:67%;" /> 

  - 각각 별도의 독립적 주소공간 할당
    - Code: 코드 자체를 구성하는 메모리 영역(프로그램 명령)
    - Data: 전역변수, 정적변수, 배열 등(초기화된 데이터)
    - Heap: 동적 할당 시 사용(new(), malloc() 등)
    - Stack: 지역변수, 매개변수, 리턴값(임시 메모리 영역)
      - 스레드마다 따로 할당

- **스레드**: 프로세스 안에서 실행되는 여러 흐름 단위

  - 하나의 프로세스가 생성될 때 기본적으로 하나의 스레드가 같이 생성됨
  - 스택만 따로 할당받고, 나머지 영역은 스레드들끼리 공유

- 차이점) 프로세스는 자신만의 고유 공간과 자원을 할당받아 사용하지만, 스레드는 다른 스레드와 공간과 자원을 공유하면서 사용

#### 멀티프로세스

하나의 컴퓨터에 여러 CPU(프로세서), 즉 여러 프로세스를 동시에 처리(병렬)

- 장점: 안전성(메모리 침범 문제를 OS차원에서 해결)
- 단점: 각각 독립된 메모리 영역을 갖고 있어 작업량 많아질 수록 오버헤드 발생, Context switching으로 인한 성능 저하
  - Context Switching: 프로세스의 상태 정보를 저장 및 복원하는 과정
  - 프로세스가 각 독립된 메모리 영역을 할당받아 사용하므로, 캐시 메모리 초기화와 같은 무거운 작업이 진행되면 오버헤드가 발생할 수 있음..



#### 멀티스레드

하나의 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리

- 스레드들이 공유 메모리를 통해 여러 작업을 동시에 처리
- 장점: 공유 메모리를 사용함에 따른 시간 및 자원 손실이 감소, 전역/정적 변수에 대한 자료 공유 가능
- 단점: 안전성 문제, 하나의 스레드가 데이터 공간을 망가뜨리면 모든 스레드가 작동 불능(공유 메모리를 가지므로)
  - 안전성 문제는 Critical section 기법(하나의 스레드가 공유 데이터값을 변경하는 시점에 다른 스레드가 그 읽으려할 때 발생하는 문제를 해결하기 위한 동기화 과정)을 통해 대비할 수 있음
    - 상호 배제, 진행, 한정된 대기를 충족해야 함

### 프로세스 주소 공간

프로그램이 CPU에 의해 실행되면, 프로세스가 생성되고 메모리에 프로세스 주소공간이 할당된다.

- 코드 + 데이터 + 스택으로 이루어져 있음
  - 코드 segment: 프로그램 소스 코드 저장
  - 데이터 segment: 전역변수 저장
  - 스택 segment: 함수, 지역변수 저장
  - 최대한 데이터를 공유하여 메모리 사용량을 줄이기 위해 구역을 나눈다.
    - 코드의 경우 같은 프로그램에서는 다 같은 내용일 것

### 인터럽트(Interrupt)

##### 정의

프로그램 실행 도중 예기치 못한 상황(더 중요한 일.. ex. 입출력, 우선순위 연산 등)이 발생했을 경우

현재 실행중인 작업을 즉시 중단하고

발생된 상황을 우선 처리한 후

실행중이던 작업으로 복귀하여 계속 처리하는 것

- 하드웨어 인터럽트
  - CPU 외부 하드웨어장비에 의해 발생
  - 타이머, I/O장비 등
- 소프트웨어 인터럽트(= Exception)
  - 명령어 실행 도중 CPU에 의해 발생
  - 0으로 나누기, 세그폴트, 페이지폴트, 부동소수점 오류, 시스템콜, ...

#### 인터럽트 발생 처리 과정

![image-20201120223158362](C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120223158362.png) 

##### 만약 인터럽트 기능이 없었다면?

컨트롤러는 특정 task를 수행할 시기를 알기 위해 계속 체크를 해야 함(폴링, polling)

→ 이 경우 원래 하는 일에 집중할 수 없게 되어 많은 기능을 제대로 수행하지 못함

인터럽트는 실시간 대응에 있어서 필수적인 기능!

### 시스템 콜(System Call)

- fork(), exec(): 새로운 프로세스 생성
  - parent의 fork()값: child의 pid값, child의 fork()값: 0
- wait(): 프로세스(부모)가 만든 다른 프로세스(자식)가 긑날 때까지 기다리는 명령어

### PCB와 Context Switching

<span style="color:red">X</span>

### IPC(Inter Process Communication)

<span style="color:red">X</span>

### CPU 스케줄링

CPU의 효율적인 사용을 위해 프로세스를 잘 배정해야 한다.

- 조건: 오버헤드, starvation ↓ / 사용률 ↑
- 목표
  1. Batch system: 가능한 많은 일 수행.. 처리량
  2. Interactive system: 빠른 응답 시간 및 적은 대기 시간
  3. Real-time system: 데드라인 맞추기

#### 선점/비선점 스케줄링

- 선점(preemptive): OS가 CPU의 사용권을 선점 및 강제 회수 가능
  - Ex) I/O, Event wait
- 비선점(non-preemptive): 프로세스가 종료되거나 I/O 이벤트가 있을 때까지 실행 보장
  - 처리시간 예측이 어려움
  - Ex) Interrupt, Scheduler Dispatch

#### 상태

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120224637181.png" alt="image-20201120224637181" style="zoom:67%;" /> 

#### 스케줄링의 종류

- 비선점 스케줄링
  - FCFS(First Come First Served)
  - SJF(Shortest Job First)
- 선점 스케줄링
  - Priority Scheduling
    - starvation 문제 발생 가능
  - Round Robin
  - Multilevel-Queue
  - Multilevel-Feedback-Queue

#### 스케줄링 척도

- Response Time: 작업이 처음 실행되기까지 걸린 시간
- Turnaround Time: 대기시간과 실행시간을 모두 합한 시간(작업 완료까지 걸린 시간)

### 데드락(Deadlock)

프로세스가 자원을 얻지 못해서 다음 처리를 하지 못하는 상태

#### 발생 조건

1. **상호 배제(Mutual exclusion)**: 자원은 한번에 한 프로세스만 사용 가능
2. **점유 대기(Hold and wait)**: 최소 하나의 자원을 점유하고 있으면서 다른 프로세스에 할당된 자원을 추가적으로 점유하기 위해 대기하는 프로세스가 존재해야 함
3. **비선점(No preemption)**: 다른 프로세스에 할당된 자원은 강제로 빼앗을 수 없음
4. **순환 대기(Circular wait)**: 프로세스의 집합에서 순환 형태로 자원을 대기하고 있어야 함

#### 처리

- 예방(Prevention)
  - 데드락 발생 조건 중 하나를 제거하면서 해결
    - 상호배제 부정 : 여러 프로세스가 공유 자원 사용
    - 점유대기 부정 : 프로세스 실행전 모든 자원을 할당
    - 비선점 부정 : 자원 점유 중인 프로세스가 다른 자원을 요구할 때 가진 자원 반납
    - 순환대기 부정 : 자원에 고유번호 할당 후 순서대로 자원 요구
  - 단점: 자원 낭비가 심함
- 회피(Avoidance)
  - 데드락 발생 시 피해나가는 방법
  - Ex) 은행원 알고리즘
    - 모든 고객의 요구가 충족되도록 현금 할당
    - 프로세스가 자원을 요구할 때, 시스템은 <u>자원을 할당한 후에도 안정 상태인지 사전에 검사</u>하여 교착 상태를 회피
    - 안정 상태면 자원 할당, 아니면 자원 해지까지 대기
- 탐지(Detection)
  - 자원 할당 그래프를 통해 데드락 탐지
  - 단점: 자원 요청 시 탐지 알고리즘을 실행시켜 그에 대한 오버헤드 발생
- 회복(Recovery)
  - 데드락을 일으킨 프로세스를 종료하거나, 할당된 자원을 해제시켜 회복
  - 프로세스 종료의 경우
    - 데드락 상태의 모든 프로세스를 중지
    - 데드락이 제거될 때까지 데드락 상태의 프로세스를 하나씩 중지
  - 자원 선점의 경우
    - 데드락 상태의 프로세스가 점유하고 있는 자원을 선점해 다른 프로세스에 할당(해당 프로세스 일시정지)
    - priority가 낮은 프로세스나 수행 횟수 적은 프로세스 위주로 프로세스 자원 선점

### 경쟁 상태(Race Condition)

<span style="color:red">X</span>

### 세마포어와 뮤텍스

### 페이징과 세그먼테이션

### 페이지 교체 알고리즘

페이지 부재 발생 → 새로운 페이지를 할당해야 함 → 현재 할당된 페이지 중 어떤 것 교체할 지 결정하는 방법

- FIFO(First-in First-out) 알고리즘: 가장 먼저 올라온 페이지를 먼저 내보냄

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120235322260.png" alt="image-20201120235322260" style="zoom:67%;" />

- OPT(Optimal) 알고리즘: 앞으로 가장 사용하지 않을 페이지를 먼저 내보냄(**미래**)

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120235338896.png" alt="image-20201120235338896" style="zoom:67%;" />

  - 4번째에서 7,0,1 중 가장 나중에 다시 사용되는 7을 빼고 2를 불러온다.

  - 장점: FIFO에 비해 페이지 결함의 수를 감소시킬 수 있음
  - 단점: 그러나 실질적으로 페이지가 앞으로 잘 사용되지 않을 것이라는 보장을 할 수 없으므로 수행이 어렵다

- LRU(Least-Recently-Used) 알고리즘: 최근에 사용하지 않은 페이지를 먼저 내보냄(**과거**)

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201120235445319.png" alt="image-20201120235445319" style="zoom:67%;" />

  - 6번째 페이지 폴트에서 2,0,3 중 가장 예전에 사용된 2가 교체됨
  - Global 교체: 메모리 상의 모든 프로세스 페이지에 대해 교체
  - Local 교체: 메모리 상의 자기 프로세스 페이지에서만 교체
  - 자기 프로세스 페이지에서만 교체를 하면 교체 시 각각 모두 교체를 해야 하므로 실제로는 Global 교체가 더 효율적임

### 메모리(Memory)

<span style="color:red">X</span>

### 파일 시스템(File System)

<span style="color:red">X</span>