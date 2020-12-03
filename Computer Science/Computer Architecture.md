# Computer Architecture 컴퓨터 구조

### 컴퓨터의 구성

하드웨어 + 소프트웨어

- 하드웨어: 컴퓨터를 구성하는 기계적 장치
- 소프트웨어: 하드웨어의 동작을 지시하고 제어하는 **명령어의 집합**
  - 시스템 소프트웨어: 운영체제, 컴파일러
  - 응용 소프트웨어: 워드프로세서, 스프레드시트

#### 하드웨어

<img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201013190232322.png" alt="image-20201013190232322" style="zoom: 67%;" />

중앙처리장치 + 기억장치 + 입출력장치

- 시스템 버스로 연결되어 있음
  - 데이터와 명령 제어 신호를 각 장치로 실어나르는 역할

##### 중앙처리장치(CPU)

산술논리연산장치(ALU) + 제어장치 + 레지스터

- 컴퓨터의 두뇌에 해당하는 부분
- 주기억장치에서 명령어와 데이터를 읽어와 처리, 명령어의 수행 순서 제어
- **ALU**: 비교와 연산 담당
- **제어장치**: 명령어의 해석/실행 담당
- **레지스터**: 속도가 빠른 데이터 기억 장소

##### 기억장치

주기억장치 + 보조기억장치

- 프로그램, 데이터, 연산 중간 결과를 저장하는 장치
- **주기억장치**
  - Ex) RAM, ROM
  - 실행중인 프로그램과 같은 <u>프로그램에 필요한 데이터를 일시적으로 저장</u>
- **보조기억장치**
  - Ex) HDD
  - 주기억장치보다 <u>느리지만</u> 많은 자료를 <u>영구적으로 보관</u>할 수 있음

##### 입출력장치

입력장치 + 출력장치

- **입력장치**: 컴퓨터 내부로 자료 입력(Ex. 키보드, 마우스, ...)
- **출력장치**: 컴퓨터 외부로 자료 표현(Ex. 프린터, 모니터, ...)

#### 시스템 버스

하드웨어 구성요소를 <u>물리적으로 연결</u>하는 선

##### 데이터 버스

<u>중앙처리장치</u>와 <u>기타 장치</u>(기억장치, 입출력장치) 사이에서 데이터 전달

- <u>양방향</u> 버스

##### 주소 버스

데이터를 정확하게 나르기 위해서 <u>기억장치의 주소를 전달</u>하는 통로

- 중앙처리장치 → 주기억장치, 입출력장치(<u>단방향</u> 버스)

##### 제어 버스

중앙처리장치가 기타 장치에 제어 신호를 전달하는 통로

- 데이터 버스와 주소 버스는 모든 장치에 공유되므로 이를 제어하는 수단

- 읽기, 쓰기 모두 수행(<u>양방향</u> 버스)
- 제어 신호 종류: 기억장치 읽기 및 쓰기, 버스 요청 및 승인, 인터럽트 요청 및 승인, 클락, 리셋, ...

#### 컴퓨터의 데이터 처리

읽고 처리한 뒤 저장 READ → PROCESS → WRITE

- 이 과정에서 끊임없이 주기억장치(RAM)과 소통
- 운영체제가 64bit라면 CPU는 RAM으로부터 데이트를 한번에 64bit씩 읽어옴 

### 중앙처리장치(CPU) 작동 원리

#### 각 장치의 특징 및 역할

##### 연산 장치(ALU)

- 산술 연산과 논리 연산 수행
- 연산에 필요한 데이터를 레지스터에서 가져오고, 연산 결과를 다시 레지스터로 보냄

##### 제어 장치

- 명령어를 순서대로 실행할 수 있도록 제어
- 주기억장치에서 명령어를 꺼내 해독하고, 그 결과에 따라 명령어 실행에 필요한 제어 신호를 기억장치, 연산장치, 입출력장치로 보냄
- 장치들이 보낸 신호를 받아 다음에 수행할 동작을 결정

##### 레지스터

- 고속 기억장치
- 명령어 주소, 코드, 연산에 필요한 데이터, 연산 결과 등을 임시로 저장
- CPU 종류에 따라 사용할 수 있는 레지스터 갯수와 크기가 다름
- 범용 레지스터: 연산에 필요한 데이터나 연산 결과를 임시로 저장
- 특수목적 레지스터: 특별한 용도로 사용하는 레지스터
  - MAR(메모리 주소 레지스터): <u>읽기/쓰기 연산을 수행할 주기억장치 주소</u> 저장
  - PC(프로그램 카운터): <u>다음에 수행할 명령어 주소</u> 저장
  - IR(명령어 레지스터): <u>현재 실행중인 명령어</u> 저장
  - MBR(메모리 버퍼 레지스터): <u>주기억장치에서 읽어온 데이터 또는 주기억장치에 저장할 데이터</u>를 임시로 저장
  - AC(누산기): <u>연산 결과를 임시로</u> 저장

#### CPU의 동작 과정

1. 주기억장치: 입력장치에서 입력받은 데이터 or 보조기억장치에 저장된 프로그램을 읽어옴
2. CPU: 프로그램을 실행하기 위해 주기억장치에 저장된 명령어와 데이터를 읽어와 처리. 그 결과를 다시 주기억장치에 저장
3. 주기억장치: 처리 결과를 보조기억장치에 저장하거나 출력장치로 보냄
4. 제어장치: 1~3 과정에서 명령어가 순서대로 실행되도록 각 장치를 제어

#### 명령어 세트

CPU가 실행할 명령어의 집합, 연산 코드(Operation Code) + 피연산자(Operand)로 이루어짐

- 연산 코드: 실행할 연산
  - 연산, 제어, 데이터 전달, 입출력 기능
- 피연산자: 데이터 or 저장 위치
  - 주소, 숫자/문자, 논리 데이터 등 저장
- CPU는 프로그램을 실행하기 위해 '주기억장치에서 명령어를 순차적으로 인출하여 해독하고 실행하는 과정'을 반복
- 명령어 사이클: CPU가 주기억장치에서 한번에 하나의 명령어를 인출하여 실행하는데 필요한 일련의 활동
  - Fetch / Execute / Indirect / Indirect 사이클로 나누어짐
  - 주기억장치의 지정된 주소에서 하나의 명령어를 가져오고, Execute 사이클에서는 명령어를 실행함. 하나의 명령어 실행이 완료되면 그 다음 명령어에 대한 Fetch 사이클 시작

##### Fetch 사이클과 Execute 사이클에 의한 명령어 처리 과정

###### Fetch

1. PC에 저장된 주소를 MAR로 전달
2. 저장된 내용을 토대로 주기억장치의 해당 주소에서 명령어 인출
3. 인출한 명령어를 MBR에 저장
4. <u>다음 명령어를 인출하기 위해 PC값 증가</u>
5. MBR에 저장된 내용을 IR에 전달

```assembly
T0 : MAR ← PC
T1 : MBR ← M[MAR], PC ← PC+1
T2 : IR ← MBR
```

###### Fetch 이후 Execute

- PC 증가할 필요 X
- IR에 MBR의 값이 이미 저장되어있는 상태
- AC에 MBR를 더해주기만 하면 됨

``` assembly
T0 : MAR ← IR(Addr)
T1 : MBR ← M[MAR]
T2 : AC ← AC + MBR
```

### 캐시 메모리(Cache Memory)

속도가 빠른 장치와 느린 장치에서 <u>속도 차이에 따른 병목 현상을 줄이기 위한</u> 메모리

Ex) CPU 코어 - 메모리 사이의 병목 현상 완화, (웹 브라우저 캐시 파일) 하드디스크 - 웹페이지 사이 병목 현상 완화

- CPU가 주기억장치에 저장된 데이터를 읽어올 때, 자주 사용하는 데이터를 캐시 메모리에 저장한 뒤 다음에 이용할 때는 주기억장치가 아닌 캐시 메모리에서 먼저 가져오면서 속도를 향상시킨다.
- 장점: 속도가 향상됨 / 단점: 용량이 적고, 비용이 비쌈
- CPU에서는 2~3개의 캐시 메모리가 사용됨(L1, L2, L3)
  - 속도와 크기에 따라 분류
  - L1 캐시부터 먼저 사용
  - 듀얼 코어 프로세서의 경우 각 코어가 독립된 L1을 가지고, 두 코어가 L2를 공유함
    - L1 캐시가 128kb면 64kb에 명령어를 처리하기 직전의 명령어를 저장하고, 나머지 64kb에는 실행 후 명령어를 임시 저장
      - 명령어 세트로 구성, L cache - D cache
    - L1: CPU 내부에 존재, L2: CPU와 RAM 사이에 존재, L3: 보통 메인보드에 존재
    - 캐시 메모리 크기가 작은 이유: SRAM 가격이 매우 비쌈
    - 디스크 캐시: 주기억장치(RAM)와 보조기억장치(HDD) 사이에 존재하는 캐시

#### 작동 원리

- **시간 지역성**: 반복문에 사용되는 조건변수(for while에서 i, j)처럼 한번 참조된 데이터는 잠시 후 또 참조될 가능성이 높음
- **공간 지역성**: A[0], A[1]과 같은 연속 접근 시, 참조된 데이터 근처에 있는 데이터가 잠시 후 또 사용될 가능성이 높음
  - 이러한 참조 지역성을 최대한 활용하기 위해 해당 데이터뿐만 아니라, 옆 주소의 대에터도 가져와 같이 미래에 쓰일 것을 대비한다.
- CPU가 요청한 데이터가 캐시에 있으면 'Cache Hit', 없어서 DRAM에서 가져오면 'Cache Miss'

#### 캐시 미스의 경우 3가지

1. **Cold miss**
   - 해당 메모리 주소를 처음 불러서 나는 미스
2. **Conflict miss**
   - 캐시 메모리에 두 데이터를 저장해야 하는데, 두 데이터가 같은 캐시 메모리 주소에 할당되어 있어서 나는 미스(direct mapped cache에서 주로 발생)
   - Ex) 항상 핸드폰과 열쇠를 오른쪽 주머니(캐시)에 넣고 다니는데, 잠깐 친구가 준 물건을 받느라 손에 들고 있던 핸드폰을 가방에 넣었음. 그 이후 핸드폰을 찾으려 오른쪽 주머니에서 찾는데 없는 상황
3. **Capacity miss**
   - 캐시 메모리의 공간이 부족해서 나는 미스
   - Conflict가 주소 할당 문제라면, Capacity는 공간 문제
   - 캐시 크기를 키워서 문제를 해결하려 하면 캐시 접근 속도가 느려지고 파워를 많이 먹는 단점이 생김

#### 구조 및 작동 방식

- **Direct Mapped Cache**

  DRAM의 여러 주소가 캐시 메모리의 한 주소에 대응되는 다대일 방식

  <img src="C:\Users\KJH\AppData\Roaming\Typora\typora-user-images\image-20201013220532221.png" alt="image-20201013220532221" style="zoom: 67%;" />

  - 가장 기본적인 구조
  - 캐시 메모리 = 인덱스 필드(000) + 태그 필드(01) + 데이터 필드
  - 장점: 간단하고 빠르다
  - 단점: Conflict miss가 발생(같은 색깔의 데이터를 동시에 사용해야 할 때 발생)

- **Fully Associative Cache**

  비어있는 캐시 메모리가 있으면 마음대로 주소를 저장하는 방식

  - 장점: 저장할 때 매우 간단하다
  - 단점: 찾을 때가 어렵다, 가격이 비싸다
    - 저장할 때의 조건이나 규칙이 없어서 특정 캐시 set 안에 있는 모든 블럭을 한번에 찾아 원하는 데이터가 있는지 검색해야 함.. 비효율적
    - CAM이라는 특수한 메모리 구조를 사용해야 하는데, 이게 비쌈

- **Set Associative Cache**

  Direct + Fully 방식

  - 특정 행을 지정하고, 그 행 안의 어떤 열이든 비어있을 때 저장하는 방식
  - Direct보다 검색 속도는 느리지만, 저장이 빠르고
  - Fully에 비해 저장이 느린 대신 검색이 빠르다

### 고정 소수점 & 부동 소수점

컴퓨터에서 실수롤 표현하는 두가지 방식

#### 고정 소수점(Fixed Point)

소수점이 찍힐 위치를 미리 정해놓고 소수를 표현하는 방식

- 정수 + 소수
- 장점: 실수를 정수와 소수부로 표현하여 단순
- 단점: 표현의 범위가 너무 적어서 활용하기 힘듦(정수부 15bit, 소수부 16bit)

#### 부동 소수점(Floating Point)

지수의 값에 따라 소수점이 움직이는 방식을 활용한 방식

- 가수 + 지수
- 장점: 표현할 수 있는 수의 범위가 넓어짐(현재 대부분 시스템에서 활용중)
- 단점: 오차가 발생할 수 있다(부동소수점으로 표현할 수 있는 방법이 매우 다양)

### 패리티 비트 & 해밍 코드

#### 패리티 비트

정보 전달 과정에서 오류가 생겼는지 검사하기 위해 추가하는 비트

- 전송하고자 하는 데이터의 각 문자에 1비트를 더하여 전송
- 전체 비트에서 짝홀에 맞도록 비트를 정함
- Ex) 짝수 패리티(짝수로 맞춰야 한다)일 때 7비트 데이터가 1010001 이라면
  - 짝수를 맞춰주기 위해 1을 더해서 '1'1010001 (맨 앞이 패리티비트인 경우)

#### 해밍 코드

데이터 전송 시 1비트의 에러를 정정할 수 있는 자기 오류 정정 코드

- 패리티비트를 보고, 1비트에 대한 오류를 정정할 곳을 찾아 수정할 수 있음
- 패리티비트는 오류를 검출하기만 할 뿐, 수정하지는 않으므로 해밍 코드 활용
- 방법
  - 2의 n승번째 자리(1,2,4)가 패리티 비트일 때
    - 각 자리에 따라 확인하는 비트의 규칙이 정해져 있음
  - 3개의 패리티 비트가 짝수인지 홀수인지 기준으로 판별
  - Ex) 0011011, 짝수 패리티일 때 오류가 수정된 코드는?
    - 1번째 비트: 1, 3, 5, 7번째 비트 확인. 0101. 짝수(0)
    - 2번째 비트: 2, 3, 6, 7번째 비트 확인. 0111. 홀수(1)
    - 4번째 비트: 4, 5, 6, 7번째 비트 확인. 1011. 홀수(1)
    - 즉 4-2-1 순서대로 이으면 110. 이를 10진법으로 바꾸면 6이므로 6번째 비트를 수정하면 된다
    - 답: 00110'0'1

### ARM 프로세서

- 프로세서: 메모리에 저장된 명령어들을 실행하는 유한 상태 오토마톤
- ARM: Advanced RISC Machine
  - RISC: Reduced Instruction Set Computing
  - 단순한 명령 집합을 가진 프로세서가 복잡한 명령 집합을 가진 프로세서보다 훨씬 더 효율적이지 않을까? 로 탄생함
  - 명령 집합의 수가 적기 때문에 트랜지스터 수가 적고, 이를 통해 크기가 작고 전원 소모가 낮은 ARM CPU가 스마트폰, 태블릿PC와 같은 모바일 기기에 많이 사용됨
- ARM을 위해 설계된 프로세서는 오직 ARM 프로세서가 탑재된 기기에서만 실행 가능
  - ARM에서 실행되던 프로그램을 x86 프로세서에서 실행되도록 하려면 수정을 해야됨(그 반대도)
- 하지만 하나의 ARM 기기에 동작하는 OS는 다른 ARM 기반 기기에서도 잘 동작함
  - 덕분에 수많은 버전의 안드로이드가 탄생
  - HP나 블랙베리의 타블렛에도 안드로이드가 탑재될 가능성이 생김
- ARM을 만드는 기업들은 ARM을 통해 전력 소모를 줄이고 성능을 높이기 위해 설계를 개선하며 노력함