# Multithreading #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  Multithreading 개념과 필요성을 이해하고 3가지 구현 방법에 대한 학습

<br>

## 서버 유형 ##
1. Iterative Server
2. Concurrent Server

<br>

### Iterative Servre Architecture ###
- 서버가 깨어나서 Request Queue에서 자신이 스스로 Request를 해결하고 다시 확인해서 있다면 Request를 해결하는 것을 반복
- 장점 : 단순하여 프로그램 하기 쉽다
<br>

### Concurrent Server Architecture ###
- 병렬 처리 형식
- Message에서 Request Queue를 가져오면 서버가 직접 처리하지 않고 요청을 처리할 하나의 Child Process Worker를 fork해서 처리하도록 시킨다
- Concurrent Server 역할은 Server는 별도의 해야할 일은 없으며 반복해서 Message가 있는지 확인하여 Child Process Worker를 fork하는 역할이다

<br>

### Request Queue ###
여러 요청이 발생되어 Queue를 사용하여 발생하는 Request를 쌓는다

<br>

### Architecture ###
 디자인 패턴으로 시스템 전체 설계에 사용할 수 있는 패턴을 의미한다

<br>

### Concurrent Server 운영방식 ###
- Request가 들어오면 Process를 생성해야 한다
- Process 생성 과정이 어렵기 때문에 운영에 부담을 주어 사용하는 개발자가 부담을 느낄 수 있다
- 이 문제를 해결한 것이 Multithreading

<br>

### Multithreading 목적 ###
Concurrency는 높이고 Execution Unit을 생생 혹은 수행하는데 드는 부담을 줄일 수 있다

<br>

### Process ###
- 프로세스에는 2가지가 있다
1. Context (Resource)
2. Execution Stream or Threads of Control

<br>

### Process 구분 ###
- Context(자원)와 Threads of Control로 나누어서 생각을 하게 되면
- 왜 하나의 Process 안에 하나의 Threads of Control만 있어야 하는가 라는 의문을 갖게 되었다
- Threads of Control을 따로 분리하여 거대한 Process와 구분되도록 lightweight process 혹은 Threads로 부르기 시작
- 그 결과 하나의 Process에 여러개의 Threads 존재하기 시작
- Process에게 부여된 자원은 1개만 유지하며, 여러 개의 Threads가 이 자원을 공유하게 된 것으로 Multithreading 등장

<br>

### Threads ###
- Threads가 이제는 Execution의 대상, CPU를 할당받는 주체가 된다
- 그리고 트랜지션에서 이야기됬던 Process State를 ready, running, waiting 상태를 갖는다고 했는데 Threads에서도 상태를 가질 수 있게 됬다
> Threads 간에 관계에 따른 실행하고 있는 Threads, 실행하고 있는 Threads  등으로 상태를 갖게 된다

<br>

### Threads 구현에 필요한 것 ###
1. Stack
2. Thread ID
3. Thread Control Block (TCB)

### Threads 구현 ###
- Stack으로 구현된다
- Threads는 Execution Stream이며, Execution Stream은 Sequence of Executive Instruction으로 이야기할 수 있으며 Sequence of Executive Function이라고 할 수 있다
> Multithreading을 사용하는 Process와 하나의 Thread만 사용했던 Process의 차이점 : 하나의 Process가 여러 개의 Stack을 갖게 된다

- 각각의 Thread를 Process가 명령할 수 있도록 각 Thread는 ID를 부여받게 된다
- ID에 소속된 정보를 저장하기 위한 Thread Control Block (TCB)와 정보를 표현하기 위한 Table이 필요하게 된다
- Thread 구현에 필요한 것들을 갖게 되면서 Thread를 구현할 수 있게 된다

### Threading ###
Process : Process Control Block, User Address Space
User Stack, Kernel Stack
단일 스레드는 프로세스 PCB에 있는 정보를 혼자 사용하기 때문에, 바로 접근해서 사용하면 되므로 Multithreading 처럼 따로 Control block을 가질 필요가 없다

<br> 

### Multithreading ###
Process : Process Control Block, User Address Space
Thread1 : **Thread Control Block**, User Stack, Kernel Stack
Thread2 : **Thread Control Block**, User Stack, Kernel Stack

<br>

### Threading, Multithreading 차이 ###
Threading은 하나의 블록을 갖고, Multithreading은 각 Thread별 여러 개의 Thread Stack을 갖고 별도의 Thread Control Block을 갖는다

<br>

### Process 2가지 모습 ###
1. Design Time Process : 복잡한 시스템 설계 시 Decomposition 때문에 설계 결과로 독립적으로 수행 가능한 개체(Entity)가 등장하게 되는 것을 의미
2. Run Time Process : Operating System에서 자원을 할당하고 수행시키는 주체를 Run Time Process라 칭한다
> Multithreading에서 Run Time Entity가 더 세분화 되어 Thread 각각에 Run Time Entity가 존재한다

<br>

### Task ###
Design Time Process를 흔히 Task라 칭한다
> 복잡한 시스템을 Decomposition으로 설계하게 되면 독립적으로 **수행가능한 Entity를 Task**라 칭한다

<br>

### Multithreading 사용이유 ###
1. 값싸게 Concurrency(병행성)를 얻기 위해
-  또는 Reactive 개발 시 Response 처리를 빠르게 하기 위해
2. Massively Parallel Scientific Programming 할 때 발생하는 오버헤드를 줄이기 위해
- 왜 오버헤드가 적는가? Process는 1개만 두고 Thread와 Thread Stack만 만들면 되기 때문이다
- 만약 Thread가 아닌 Process를 수십 수만개 만들면 각각 메모리 할당부터 주소 Mapping 까지 전부 이루어져야 하므로 상당한 자원이 사용된다
3. Concurrency를 손쉽게 확장할 수 있다. Process 자신 내부에서 Thread만 만들면 되고 Parent Process에서 Child Process를 생성하기 위해 진행된 Context Switching(fork, exec, exit, wait) 과정을 전부 할 필요가 없어진다. 그러므로 반응을 빠르게 만들 수 있다

<br>

> 메모 : 개념을 배우고 필요성을 배웠다면 실제로 어떻게 구현하는지 확인할 단계

<br>

---

<br>

## Multithreading는 어떻게 구현하는가 ##
- 구현 방법은 3가지가 있다
1. User-Level : Kernel 전혀 모르도록 구현하는 방법
2. Kernel-Level : Kernel이 100% 알고 있도록 구현하는 방법
3. Combined User-Level / Kernel-Level 구현 : 두 가지를 섞어서 구현하는 방법

<br>

## User-Level Implementation(구현) 방법 ##
- Conventional Unit Process만 지원한다
- Process 1개만 존재하고 Threads of Control 1개만 존재한다
- 이 안에 Multithreading을 구현하는 방법이다

Kernel은 전혀 고치지 않고 User-Level에서 수행한다
1. Stack 구현
2. Thread Control Block을 각 스레드별로 생성
- Thread Control Block 위치 : User-Level에 있어야 한다
- Thread 간 Switching을 한다 (스케줄링을 한다) 이 의미는 User-Level에 스케줄러가 있어야 한다

그 동안 Kernel-Level로 알고 있던 것들을 User-Level에 구현해야 한다

<br>

### User-Level에는 어떻게 구현하는가 ###
- 기존에는 Kernel 안에 Dispacher와 Scheduler는 함수로 구현되어 있었다
- User-Level 구현하는 방법을 사용 할 때는 **User-Level에서** Dispatcher와 Scheduler를 함수로 구현한다 
- 그리고 이 함수들을 묶어서 User-Level **Thread Library** 로 만들어서 사용하면 된다
- 여기서 Thread는 100% User-Level에 위치하며 Kernel 아무런 사실도 전혀 알 수 없는 상태이다
> Thread Library에 들어있는 내용은 : Thread 생성과 소멸을 구현하는 코드, Thread Context를 저장하는 코드, Thread 간 커뮤니케이션을 할 수 있는 함수가 담겨있다

<br>

### Thread Scheduling ###
1. Preemptive
2. Non-Preemptive
<br>

### Multithreading에서 Preemptive Scheduling 문제점 ###
1. Interrupt 전달 불가
- Preemptive : Preemptive 스케줄링이 발생하려면 반드시 Interrupt가 필요하다
- Interrupt가 오면 Kernel 방식에서는 Interrupt Service Routine을 통해 해당 Control를 넘겨준다
- 하지만 User-Level 구현 방법에서는 Interrupt가 **User-Level 안에있는 Thread까지 넘어가서 접근해야** 한다
- 하지만 Thread 내부에서는 그 Interrupt에 대해서 알고 있지 못해 처리할 수가 없다

2. 해당 Process를 Block으로 모든 Multithread가 Block되는 문제
- 다른 하나의 문제는 Interrupt가 발생해서 Thread가 System Call을 통해 System Call Handler에서 Kernel 함수를 호출하는 경우 해당 Process의 모든 Thread가 Block는 현상이 발생한다
- 정리하면 User-Level 구현 방법은 Kernel이 Multithreading의 존재를 전혀 알지 못하기 때문에 하나의 Thread가 Blocking System Call을 하더라도 Kernel에서는 하나의 Thread만 존재하는 것으로 알고 Thread를 정지시키면 실제로 존재하고 있던 모든 Multithread가 전부 정지하게 되는 문제가 있다

<br>

## Kernel-Level 구현(Implementation) 방법 ##
- Thread Creation(생성), Termination(소멸)을 Kernel에서 모두 수행해 준다
- Thread Control Block 또한 Kernel이 관리한다
- Scheduling 또한 Kernel Entity를 가지고 진행하게 된다
- locking 문제도 해결
- User-Level의 문제점은 전부 해결하지만 Kernel 단의 수행 시간이 증가하면서 추가적인 오버헤드가 발생하게 된다
> System Call을 하게되면 System Call Handler가 수행되야 하고 Kernel 함수가 Dispatch 되야하며 Kernel 수행하게 되므로 오버헤드가 발생할 수 있지만 반응성은 상당히 좋다

<br>

## Combined User-Level / Kernel-Level Implementation(구현) 방법##
1. 상당 부분의 처리는 User-Level에서 처리하며, 단지 Interrupt가 발생하면 User-Level Interrupt를 전달해서 어떤 Thread를 깨워야 하는지 알려주는 기능이 추가됬다
2. 어떤 System에서 System Call Block을 하게되면 해당 스레드는 중단시키고 새로운 Kernel Stack을 할당해서 User Process에 전달한다. 그 결과 User-Level에 있는 Thread Scheduler가 다른 Thread를 선택하여 실행하므로 전체가 Block되는 문제도 해결된다

<br>