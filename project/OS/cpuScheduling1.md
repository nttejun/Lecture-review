# CPU Scheduling1 #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  POSIX 스레드 API 이론과 Pthreads가 적용되는 순환구조을 학습하며, CPU 스케쥴링의 개념과 정책 및 등장이유와 이를 이해하기 위해 필요한 기본적인 CS 용어 및 개념에 대해 학습

<br>

## Pthreads ##
- POSIX standard for threads
- Pthreads API
	- 스레드 생성 시 수행할 코드가 제공된다
	- 이 코드는 c프로그래밍 함수의 function 포인트로 전달된다
	- 스레드 생성 시 entry point는 특정함수가 된다
	- 이 함수의 function 포인터가 Pthreads_create()에 제공된다
	- 포인터 
	- 특정 함수가 된다. 특정 함수에 function 포인트가 Pthreads 
	- pthread_create()
	- pthread_exit()
	- pthread_join()
	- pthread_yield()

<br>

### POSIX (Portable Operating System Interface) ###
- 다양한 UNIX 계열 운영체제들의 API를 표준화하기 위해 IEEE가 정의한 인터페이스

<br>

### pthread_create() ###
- 스레드를 생성할 때 수행할 코드가 제공된다
- 제공된 코드는 C 프로그래밍 함수의 함수 포인터로 전달된다. 
> 스레드 생성 시 그 스레드의 entry point는 특정함수가 된다
>  특정함수의 포인터가 pthread_create()에 제공된다

- pthread_create() 스레드 생성하기 전에 main thread 1개는 존재한다

<br>

### entry point ###
- 제어가 운영체제에서 컴퓨터 프로그램으로 이동하는 것을 의미

<br>

### pthread_exit() ###
- 호출한 스레드를 종료시킨다

<br>

### pthread_join() ###
- wait system call 흡사하다
- 스레드가 종료될 때까지 기다릴 때 사용하는 함수

<br>

### pthread_yield() ###
- 비선점형(non-preemptive) 스케줄링을 포기하기 위해 사용하는 함수

<br>

### pthread 적용 순환구조 (thread life cycle) ###
- 메인 스레드가 존재한다
- 메인 스레드는 스레드를 생성(create())한다
- 생성된 스레드는 2가지 경우가 있다
	- 중간에 수행을 포기, 중단(yield())하는 경우도 있고
	- 수행을 마치고 스레드를 종료(exit())하는 경우도 있을 것이다
	- (스레드 상태변화는 운영체제가 관리한다)
- 그럼 이제 메인 스레드는 스레드 생성 외 어떤 역할이 있는지 궁금해진다
- 메인 스레드는 생성한 스레드들을 모니터링(join()) 한다 
- (스레드가 종료되기까지 모니터링 하기 위해 메인 스레드는 join())
- 메인 스레드가 생성한 스레드들이 모두 종료되면 메인 스레드도 종료(exit())한다
- 프로세스가 종료된다

스레드 라이브러리를 이용해 멀티스레드 프로그래밍을 어떻게 하는 것인가를 확인할 수 있었고, 메인 스레드가 생성되고 종료되기 까지의 과정에 pthread가 어떻게 사용되는지 확인할 수 있었다

<br>

---

<br>

## Resources ##
- preemptible Resource : 
	- 한 프로세스가 점유한 상태에서 다른 프로세스에게 양보할 수 있는 자원을 의미
- non-preemptible Resource :
	- 한 프로세스가 점유하면 사용을 마칠 때 까지 다른 프로세스에게 양보할 수 없는 자원을 의미

<br>

### Resources allocation ###
1. CPU를 누구에게 줄 것인가
2. CPU 할당을 얼마나 허용할 것인가

<br>

### Batch Monitor에서의 Job ###
- 한번 수행이 시작되면 완료될 때까지 계속 수행되는 작업

<br>

### CPU Burst ###
- 프로그램 수행 중에 연속적으로 CPU를 사용하는 연속적인 구간
- CPU를 할당 받아서 수행하는 부분

<br>

### I/O Burst ###
- 프로그램의 수행 중에 I/O의 완료를 기다리며 블록되는 구간
- I/O를 차지해서 수행하는 부분

<br>

### CPU Scheduling ###
- 한 프로세스 단위가 아닌 그 프로세스가 수행하는 CPU Burst 단위로 스케줄링을 구성한다
- CPU Burst에 따라 scheduling이 달라져야 한다
- 연산 작업
- device I/O

<br>

### CPU Scheduling  ###
- Process state transition 주요 3가지
	1.	ready
	2.	running
	3.	waiting

- state transition 시점
	- ready -> running : dispatcher
	- running -> ready : hardware interrupt
	- running -> waiting : non-preemptive scheduling
	- running -> terminate : non-preemptive scheduling
	- waiting -> ready : preemptive scheduling (Asynchronous)

<br>

### Scheduling Objectives ###
- Maximize resource utilization
> utilization : 존재하는 리소스를 전체 컴퓨터 가동시간 중 의미있게 수행한 시간이 얼마나 되는가

- Minimize overhead
	- Operating system 코드 수행량이 작아야 한다
- Minimize context switches
- Distribute CPU cycles equitably

<br>

### Aging ###
- 태스크가 CPU를 기다리는 시간에 비례하여 우선순위를 점차적으로 높이는 기법

<br>

### Throughput ###
- 네트워크 상 노드나 터미널로 단위 시간 당 디지털 데이터 전송으로 처리하는 양을 의미

<br>

### Turnaround time ###
- 부분적으로 프로세스가 실행되는 시간을 의미

<br>

### Waiting time ###
-  프로세스가 ready queue에서 waiting 상태로 있는 시간을 의미

<br>

### Response time ###
- 시스템이나 실행단위에 입력이 주어지고 응답을 받기까지 걸리는 시간을 의미

<br>

## Scheduling policy ##
1. First In First Out
2. Shortest Job First
3. Round robin

<br>

### First In First Out ###
- 동일한 job 들어오면 먼저 들어온 순서대로 처리 
- process scheduling :
	- 프로세스 스케줄링 단위는 하나의 프로세스가 점유하는 것이 아니다
	- 다음 I/O를 할 때까지만 CPU를 점유한다
	- CPU Burst 단위로 스케줄링한다

- FIFO 장점 : 단순하고 직관적
- FIFO 단점 : 독점(Monopolize)이 가능하다
	- 예를들어 무한루프가 존재하는 태스크
	- 독점 방지 : Round Robin 

<br>

### SJF 스케쥴링의 문제점
- 스케쥴링 목표 중 하나로 Maximize resource utilization 달성하는 것에 문제가 있다
 	- 스케쥴링 최적화를 이루기 위해선 Shortest Job이 먼저 실행되야 한다
 	- Shortest Job인지를 확인하기 위해서는 CPU Burst 정보가 필요하다
	- 하지만, 운영체제가 태스크의 남은 CPU Burst Size를 예측할 수 없다

<br>

### Shortest Job First ###
- Two variations
	1. Preemptive
	2. Non-preemptive
- preemptive SJF 스케쥴링 시점
	- 현재 수행중인 태스크가 종료되는 시점에 re-scheduling 수행
	- 새로운 태스크가 생성되거나 깨어날 때 re-scheduling 수행
- Non-preemptive 스케쥴링 시점
	- 하나의 CPU Burst가 끝나면 Non-preemptive는 re-scheduling을 수행한다

<br>

### Round Robin ###
- FIFO 방식에 CPU Burst Timeout interrupt 적용
- 문제점 : timeout 값 설정
- 해결방안 : Time Slice
 
<br>
 
### Round Robin에서의 Time Slice (Time Quantum) ###
- 태스크에게 CPU가 할당된 후 다음 스케쥴링을 위한 Time Interrupt가 발생할 때까지의 시간
- 적절한 Time Quantum (Ex : timeout) 중요하다
	- Time Quantum 이 0과 같이 너무 낮다면 빈번한 interrupt 호출로 interrupt service routine 매번 실행되어 overhead 발생할 수 있고, Time Quantum이 무한대면 Round Robin이 FIFO 큰 차이가 없게 된다