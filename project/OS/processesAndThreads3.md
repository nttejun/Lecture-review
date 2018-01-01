# Context Switching #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  Abstraction, Decomposition을 Layered Principle 원리에 부합되게 추상적 문제를 구체화 하는 것처럼 이와 같은 개발 방법론을 소프트웨어를 개발하고 거대한 문제를 해결하는데 사용해야 하는 이유를 이해할 수 있는 내용 

<br>

## Abstraction And Decomposition ##

### Complexity ###
1. Abstraction
	- 아래 계층의 복잡성을 추상화하여 단순화한 인터페이스를 상위 계층에 보내는 것 (그 결과 Layered Architecture 존재) 
2. Decomposition

<br>

### Layered Architecture ###
- Abstraction을 System Architecture에 반영하면 Layered Architecture가 나오게 된다
- (하위) 하드웨어 --> OS --> Middle ware --> Application1, Application2... (상위)

<br>

### Layering Principle ###
- Abstraction이 완벽하게 구현되기 위해서는 Layered Principle 만족해야한다
- 상위 계층은 아래 계층이 제공하는 기능만을 사용할 수 있으며 반대의 경우는 발생하지 않아야 한다

<br>

### Layer 계층별 역할 ###
(하위) 하드웨어 --> OS --> Middle ware --> Application1, Application2... (상위)
> OS의 경우 : 하단에 복잡한 하드웨어를 보이지 않도록 하고 반드시 필요한 인터페이스만 상단으로 전달하는 것이 목적
> 계층간 통신은 API를 통해 이루어진다

<br>

### API (Application Programming Interface) ###
계층과 계층 사이의 통신을 위해 정의된 호출 규약
API는 각 레이어가 만나는 지점에 존재
커널 안에있는 함수 호출하는 방법이 시스템콜 OS의 API도 시스템 콜 
>  예를들어 OS에서 Middle ware와 통신하는 경우
> (하단) 하드웨어 --> OS --> (API) --> Middle ware --> Application1, Application2... (상단)

<br>

### Layered Principle 존재 이유 ###
Application 개발자가 OS와 하드웨어를 몰라도 개발할 수 있도록 만들어주기 때문에 존재한다

### Synthesis (설계), Implementation (구현) ###
Computer System 설계에서 Layering Principle의 Layered Architecture를 만나게 되면 가장 이해하기 쉬운 상위 Layer에서 하위 Layer로 구체화 시키며 내려가야 한다
> 위 과정을 이해한다면 Operating System을 이해하는데 많은 도움이 되며, 추상적 문제를 구체화하는 과정을 할 수 있을 때 지식을 생산할 수 있으며 지식을 소비하는 입장에서도 인사이트 있게 지식을 소비할 수 있다

- OS를 공부하는 것도 커다란 문제를 구체화하여 진행하면 효과적이다
- 이러한 방법론과 프로세스를 갖고 있는 사람이 창조적인 사람이 될 수 있다
- 예를들어 OS를 공부할 경우에도 OS를 5가지로 구분할 수 있다
1. CPU 스케줄러
2. 파일 시스템
3. 메모리 관리
4. I/O 관리
5. 네트워크 관리

<br>

### Interrupt Type ###
1. Hardware : Preemptive
2. Software : Non-Preemptive

### Preemptive ###
- 하드웨어 Interrupt에 의해 CPU를 빼앗기면 Preemptive Scheduling by Hardware Interrupt
- Operating System 수행되야 하므로 Asynchronous 방식이 필요

<br>

### Non-Preemptive
- Software Interrupt에 의해 발생
- 예를들어 I/O 작업이 끝나기를 기다려야 하는 경우 내가 CPU를 점유하고 있을 필요가 없으므로 CPU를 양보하기 위해 Software Interrupt를 발생시켜 CPU 자원을 가져갈 수 있도록 한다

<br>

---

<br>

## Process Creation and Termination ##

<br>
### Creation ###
Context Switching을 위한 

<br>

### Process Creation ###
Data Segment, Stack Segment 과정이 필요

1. Data Segment
- Orating System이 Data Structure를 모두 할당받아 초기화 한다 (Process Creation)
- 예들들어 Process를 만들기 위해서는 File System은 Execution File(실행 파일)이 있어야 한다
- 그리고 실행 파일의 경로명을 Operating System에 전달하면 Operating System이 전달된 경로에 위치한 파일 내 코드를 Code Segment로 읽어드리게 됩니다
> Global Variable 선언된 정보와 기술을 **Data Segment 영역에 지정**해줘야 한다
> Data Segment 영역에 지정하는 과정은 실행 파일을 읽어 코드와 데이터 Segment를 만드는 과정이며 이것을 **Program load** 라고 한다

2. Stack Segment
- 초기에는 Empty Stack, Empty Heap 생성된다
- 프로세스 정보를 담은 PCB를 메모리 할당하여 생성한다
- 할당이 완료된 PCB를 Ready Queue에 준비한다

<br>

### 유닉스 환경 Process Creation
**단, 유닉스, 리눅스는 Cloning 기능을 통해 복사하여 처음 부팅할 때 1회만 ID값을 0으로 생성하고 나머지는 복사했던 것을 Fork해서 사용한다**

- 유닉스는 프로세스 생성하는 명령을 내리는 다른 프로세스가 필요
- 자신을 만든 프로세스를 Parent Process
- 만들어진 프로세스를 Child Process
- Parent Process가 Child Process 만들기 위해서는 Fork System Call을 호출하게 된다
- Operating System에서 Fork한 Parent Process를 완전히 중단시킨다
- Parent Process가 갖고 있는 Context를 전부 Snapshot으로 찍는다
- 그리고 Context를 모두 복사하여 Child Process를 생성된다
- Process 고유 값인 ID를 제외하고는 모든 Context 내용이 동일하게 복사된 Child Process 가 생성된다
- 그리고 Child Process의 (복사된)Process Control Block을 Ready Queue로 보내면 Fork System Call 수행을 마치고 Parent Process 로 복귀한다

<br>

### fork() System Call 문제점 ###
- 맨 처음 만든 Process와 다른 Process는 수행할 수 없다
- 처음 수행한 프로세스만 수행할 수 있다

<br>

### fork() System Call 해결책 ###
1. Another System Call로 exec()을 호출한다
2. exec() Parameter가 생성된 프로그램의 실행파일(Execution File)의 경로다
3. 생성된 프로그램 실행파일의 코드와 데이터를 이미 Parent를 복사해서 갖고 있는 Context(코드와 데이터)에 오버라이드 해서 새로운 프로그램으로 실행 시킨다
4. 단, 성능적인 문제가 있다

<br>

## Process Creation 과정 ##
> Fork --> (Parent) --> wait ()  --> resumes
> Fork --> (Child) --> exec() --> exit() --> wait()  
> 단, Parent Process가 항상 for() 후에 wait()를 호출해야 하는 건 아니다
> 그리고 Parent Process가 Child Process 종료 상태에 관심있는 경우에만 wait() 호출을 한다
 
1. Parent Process가 Fork하는 시점에 Child Process가 Parent Context를 복사하고 exec()을 수행한다
2. exec() 수행되면서 Parent Process와 Child Process는 다른 프로그램을 실행하게 되어지는 것이다
3. Parent Process와 Child Process가 다시 만나는 지점이 생기는데 이곳이 wait() System Call 지점이다

<br>

### Parent ###
- Fork한 후에 wait() System Call 한다
- wait()는 Parent Process 자신이 생성한 Child Process ID 다
- 그러므로, wait는 Parameter로 준 Process가 수행을 종료할 때까지 Parent 자신을 기다리게 하도록 만드는 것이 wait() System Call 입니다

<br>

### Child ###
Child는 exec에서 코드를 얻은 후 전부 수행이 완료되면 exit() System Call을 수행합니다
> exit() System Call : 어떤 프로세스를 종료하는 시스템 콜 
> 모든 프로세는 정상 종료하게 되면 exit() 실행되도록 되어 있다

exit()을 수행하게 되면 그 Process가 갖고 있던 Data Structure, Resource를 Operating System에서 전부 걷어간다
> 단, exit() 정상적으로 수행 되었는지 결과 코드 하나는 남기게 된다

exit() 수행하고 난 결과 코드는 자신을 wait하고 있는 Process에게 전달해주고 Parent Process는 깨어나서 나머지 작업(resume)을 수행을 하게 됩니다

이러한 Parent Process와 Child Process 관계에 의해 생성된다

<br>

### Zombi State ###
exit() 마치고 Parent Process가 자신의 Exit Status를 읽어가기를 기다리는 Process의 상태
  
<br>

### Shell, CLI (Command Line Interpreter) ###
사용자가 입력한 명령어를 입력으로 받아들여 새로운 프로세스를 수행시키는 프로그램

<br>

### fork(), exec() 해야만 했던 이유 ###
CPU --> (Logical Address) --> MMU --> (Physical Address) --> Memory
- Logical Address : 실제로 존재하지는 않고 프로그램이 간주하는 가상 메모리
> 32bit 경우 : 0~2^32-1 주소공간 생성가능 --> Logical Address Space
> Logical Address Space : 모든 프로세스가 1개씩 갖고 있다

- Process A는 0 부터 2^32-1 주소를 갖고 있다
- Process B는 0 부터 2^32-1 주소를 갖고 있다
<br>

- Address Space가 다르므로 Process A, Process B의 주소값이 동일한 100번지라고 해도 다른 주소를 의미한다
- 문제가 되는 부분은 Process A, Process B 서로 데이터를 주고 받아야 하는 경우 중첩되므로 별도의 방법이 필요했다
- 이 때 사용한 것이 File을 이용해 Process A는 write하고 Process B는 read해 가는 방식으로 사용
- 이것도 문제가 된다 서로 File 이름을 공유하고 있어야 한다
- 그래서 사용한 방법이 fork()이며 fork()로 발생하는 불필요한 성능저하를 해결하기 위해 COW 사용

### COW(Copy On Write) ###
Process Context를 fork() 시점에 복사하지 않고, Data Segment에 새 값이 쓰여질 때 복사하는 기법

<br>