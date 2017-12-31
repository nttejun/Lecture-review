# Process Concept #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  프로세스는 OS에서 가장 중요한 정보단위로 CPU할당과 동작을 수행하는데 사용되며, OS를 공부할 때 프로세스를 먼저 이해해야 한다

<br>

## Process Concept ##
- Program Execution (Process state, Execution Stream)
- 컴퓨터 시스템의 원인과 결과를 귀속시킨 것을 프로세스라 할 수 있다
- 프로세스는 OS에서 프로그램을 실행 (Runtime) 시키는 기본 주최
- 복잡도를 감소시키는 Decomposition 역할

<br>

### 복잡도를 감소시키는 방법 ###
1. Abstraction
2. Decomposition

<br>

### Decomposition ###
복잡한 문제를 단순한 여러 개의 문제로 나누어 처리하는 방법

<br>

### Decomposition Processes ###
Decomposition된 것이 개별로 수행시킬 수 있는 하나의 작업 단위가 되었다면 프로세스라 할 수 있다

<br>

### Process state ###
프로그램이 수행되는 동안 기억해야 할 정보를 저장한 것
> 프로세스가 수행되는데 영향을 주거나 영향 받을 수 있는 모든 정보를 저장한 것을 의미

<br>

### 프로세스 실행에 필요한 정보 ###
Process state에서 저장하고 있어야 하는 정보

1. Memory 저장되어 있는 것
- 코드 (기계어)
- 데이터 (프로그램 전역변수)
- 스택 (지역변수, 함수 호출을 위한 공간)
- 힙
2. Hardware context
- CPU registers
- I/O registers
3. System context (Per-Processes Kernel Information 커널이 관리하는 정보)
- Process table
- open file
- page table

<br>

### Execution Stream ###
프로세스가 현재까지 수행한 모든 명령어 순서

<br>

### Multi Programming ###
메인 메모리에 있는 여러 개의 프로세스가 동시에 수행되고 있는 것을 의미

<br>

### Unit Programming ###
메인 메모리에 있는 실행하고 있는 프로세스가 하나라는 것을 의미

<br>

### Multi Processing ###
CPU가 여러 개의 프로세스에 의해 수행되는 것을 의미 (CPU 관점)

<br>

### Swapping ###
메모리 부족 문제를 해결하기 위해 CPU를 사용하지 않는 프로세스 데이터를 메모리에서 다른 저장 장치로 내보내고 CPU를 사용할 프로세스 데이터를 메모리에 로드하는 과정을 의미

<br>

### 프로세스 유용성 ###
- OS의 메모리를 할당하고 수행하는 주체 

<br> 

### Software System Develop ###
1. 설계
	- 요구사항 명세서
	- 설계 (Decomposition)
	- Tasks (독립적인 구성)
2. 구현
	- Tasks 구현 결과물 : Programs (Process)
	- Programs는 컴파일 되고 OS에 의해 실행 (OS는 컴파일 시점에 매핑된 프로세스를 실행 : 컴파일 시점에 OS가 Process를 갖고 있는 이유)

<br>

---

<br>

## Process Control Block ##
운영체제에서 필요한 프로세스의 정보를 갖고 있는 운영 체제 커널의 자료구조를 의미 

<br>

### Programming 이란 ###
Program = Data Structure + Algorithm
데이터 구조를 어떻게 만들고 이 구조는 어떤 알고리즘을 사용해야 하는지 이해한다면 프로그램을 구현할 수 있다는 의미

### 

### Process를 OS로 구현하는 방법 ###
OS 안에서 Process는 어떤 Data Structure를 갖고 있는지 확인하고 어떤 알고리즘을 사용해야 하는지 이해하면 된다 

### Context 3가지 ###
1. Memory context
2. Hardware context
3. System context

<br>

### System Context ###
OS Kernel이 프로세스를 위해 유지해야 하는 정보

<br>

### State Transition ###
여기서의 State는 특정 프로세스가 어떤 상황에 있는지를 의미하는
Process가 생성되고 종료되는 일련의 과정에서 나타나는 상황

- Ready : CPU를 받지 못해 아직 실행하지 못하고 있는 프로세스
	- Running 되기 위해서는 운영체제 스케줄러가 수행되어야 한다
> Ready Queue : Ready 상태의 프로세스를 관리하기 위한 Queue 형태의 자료 구조
> Ready Queue 구현은 미리 만들어놓은 Process Control Block을 Linked List로 연결하여 구현

- Running : OS가 선택하여 CPU를 할당받은 상태 (Running 상태 : 0 또는 1개)
	- Ready로 상태가 변하려면 Interrupt 가 발생되어 CPU자원을 빼앗기게 된 것을 의미한다
	- Waiting으로 상태가 변하려면 Request 이벤트가 호출되야 한다

- Waiting : 예를 들어 I/O Request로 입력 데이터를 기다린다면 계속 Running 상태에 있으면 CPU 자원을 사용하게 되므로 Waiting 상태로 변환
> Waiting 상태의 프로세스는 여러개 있을 수 있다 (OS에서 Waiting 이유에 따라 별도의 Queue를 사용해 여러 개가 존재할 수 있다)

- Ready : Waiting 상태에서 원하는 이벤트가 실행되어 데이터를 전달받으면 다시 Ready 상태로 변환

위 과정이 State Transition을 의미

<br>

---

<br>

## Process Scheduling ##

- 목적 : 프로세스가 상대적 공평하게 CPU 자원을 공유하기 위해 순차적으로 수행시킬 프로세스를 선택
- 원리 : CPU를 여러 프로세스가 공유하고 있다 그리고 사용하던 한 프로세스의 CPU자원을 다른 프로세스에게 전달하게 된다
	- Policy : 다음에 어떤 교체 가능한 프로세스를 선택할 것인가
	- Mechanism : CPU 자원을 전달하기 위한 Mechanism

<br>

### Dispatcher Mechanism ###

OS 안에서 반복해서 실행하고 있다
- 프로세스 실행을 중단하라는 요청이 들어오면 Waiting으로 이동한다
- 선택한 프로세스를 수행시킨다 (수행 전에 이전 데이터를 전부 로드 후 재 실행하게 된다)

### User에서 Dispatcher를 실행시키는 방법 ###
Dispatcher Mechanism 실행을 위해서는
User에서 Kernel로 그리고 다시 실행할 User로 모드 체인지를 해야한다
그리고 모드 체인지를 하기 위한  방법으로 Interrupt를 발생시키는 것이다
(Interrupt가 발생되면 실행을 중단하라는 요청이 전달된다)

<br>