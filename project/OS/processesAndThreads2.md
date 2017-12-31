# Process Implementation #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  프로세스 스케줄링이 진행되는 과정을 이해

<br>

## Process Scheduling ##

<br>

### Dispatcher ###
- Context switching 담당하는 역할
- 사용자 프로그램과 사용자 프로그램 사이에 개입하여 프로세스를 이동 시켜주는 역할
> Dispatcher 시행을 위한  중요한 점 : CPU 점유권을 가져와야 한다 <br>
>  CPU 점유권을 User에서 Dispatcher로 <br>
>  Dispatcher에서 다시 User로 이동되어야 한다

- User, Dispatcher Mode 변경은 Interrupt Mechanism을 사용해서 이루어지며 모드 체인지는 Micro Architecture 구현에 따른다

<br>

### Operating System ###
커널 모드에서 수행되는 라이브러리 함수들(System call)의 집합체

<br>

### System Call ###
운영체제 커널이 제공하는 서비스에 대해, 응용 프로그램 요청에 따라 접근하기 위한 인터페이스
소프트웨어 Interrupt 방식에서 커널함수를 호출하기 위해 소프트웨어 Interrupt를 사용한 Trap을 발생한 특정 부분이 System Call 의미  

<br>

### Interrupt Service Routine ###
 Interrupt가 발생하면 Mode가 변경되며 하드웨어적 정의에 의해 해당 Interrupt Service Routine 호출

<br>

### 커널 함수 ###
커널 함수는 System call, Interrupt Service Routine으로 구성되어 있다
System call 구현하는 함수와 Interrupt가 발생하면 Mode가 변경되며 하드웨어적 정의에 의해 해당 Interrupt Service Routine 호출되며 이것은 커널 모드에서만 동작한다

<br>

### Mode 구분방식 ###
Process Status Word 레지스터 안의 특정 비트를 Mode Bit으로 사용
- Kernel mode 0
- User mode 1

<br>

### Dispatcher로 이동하기 위한 방법 ###
1. Non-preemtive Scheduling
2. Preemptive Scheduling

<br>

### Non-preemptive Scheduling ###
- 프로세스가 자발적으로 CPU를 양보하여 다른 프로세스를 수행하는 스케줄링
- 소프트웨어적 Interrupt 방식(Trap)을 사용하는 스케줄링

<br>

### Preemptive Scheduling ###
- 운영체제가 강제로 프로세스로부터 CPU를 빼앗아 다른 프로세스를 수행하는 스케줄링
- 하드웨어적 Interrupt 방식을 사용하는 스케줄링

<br>

### Mode change of process ###
- read() System call
	- read는 파일을 읽는 것이 아니라 interrupt를 발생하는 역할이다
	- interrupt arguments는 커널의 read 함수를 호출하기 원하다는 요청을 전송한다
- read() System call 시점에 Mode change 수행 (Kernel Mode로 변경)
- Kernel Mode Execution 수행
	- execution을 통해 read 함수가 호출된다
	- Kernel Mode Execution 수행의 주체 프로세스는 System Call 호출한 사용자 프로세스다
- return 하면 다시 User Mode로 이동하게 된다
	- return instruction
	- User mode 이동 시에는 높은 보안 단계에서 낮은 보안 단계로 이동하는 것이므로 별도의 제한을 하지 않는다

<br>

### Mode change of process 사용 스택은 2가지 ###
Process에서 System Call을 하면 커널함수가 실행된다
어떤 함수든 실행되기 위해서는 스택 공간이 필요하다
( 파라미터 값, 로컬 변수 메모리 할당, Return value를 전달하기 위한 메모리 공간이 필요 )

Runtime 스택은 유저 메모리에 두지 않고 커널 메모리에 두게 된다
Process가 유저모드에서 사용할 때는 User Mode Stack을 사용

System Call을 통해 커널 함수가 실행될 때는 Kernel Mode Stack을 사용
정리하면, 유저모드 커널모드에서 사용하는 2가지 스택이 각각 존재하게 된다

Run Time Context가 변해도 유저의 아이디는 동일하다
(시스템 콜을 한 유저 아이디 값으로 프로세스를 끝까지 처리한다)

<br>

### Stack of Process ###
해당 프로세스의 Run-Time Context를 의미


<br>

### Process 요소 2가지 ###
1. State ( = Context )
2. Thread of Control ( = Stack )

<br>

### Debugger 관점 ###
브레이크 포인트로 스택을 확인이 가능하다
> Why? 프로그램 첫 함수부터 현재까지 호출된 함수를 역순으로 나타나게 된다 <br>
> 해당 프로세스의 이력을 확인할 수 있다
> 스택은 유저 메모리 공간에 위치하고 있다

<br>

### 시스템 콜 vs 일반 콜 ###

공통점 : 하나의 Routine에서 다른 Routine으로 이동한다
다른점 : 일반 콜은 모드변경이 없다, 시스템 콜은 모드변경을 한다

