동영상 강의 : 서울대학교 평생교육원 [운영체제의 기초](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=623) Introduction to OS 1(1,2,3) - 홍성수

<h4>operating sysyem의 생활화</h4>

컴퓨터에서 확장되어 스마트폰, 자동차 일상생활 곳곳에 사용되고 있다


<h4>OS 공부는 왜 중요한가?</h4>

나는 항상 어떤 공부를 시작하기 전에 왜? 라는 질문을 굉장히 자주한다

공부한 지식을 어느 곳에 어떻게 사용할 지 정확히 알고

이에 필요한 지식을 이해하고 정확히 적용하기 위함이다

<h4>OS는 가장 복잡한 소프트웨어이므로</h4>

구성된 기능과 내부 구조를 복잡하지만 잘 이해한다면

앞으로 어려운 소프트웨어의 복잡한 설계도 이해하고 올바르게 사용할 수 있기 때문이다

<h4>OS가 등장하게된 이유는?</h4>

하드웨어의 단점을 보완하기 위해 OS가 발전해왔다

---

<h4>Phase1</h4>


<h4>OS 첫번째 시기(7094)</h4>

비싼 하드웨어 따라서, CPU를 최대화 시키는 것을 목적으로 했다


<h4>Operator 역할</h4>

1] 기계가 사용자로부터 카드 덱을 수령

2] 카드 덱을 컴퓨터 시스템에 로딩하고 수행

3] 수행 결과를 프린터로 출력

4] 출력된 결과물을 사용자에 전달


<h4>OS 두번째 시기(1401, Batch Monitor)</h4>

최초의 OS가 등장했다 (Job-to-Job 문제해결을 위해)

= operator의 느린 Job-to-Job 전환 속도로 인한 컴퓨터 시스템의 비효율성을 해결하기 위해


<h4>최초의 OS의 역할</h4>

1] 사용자는 카드덱 형태를 컴퓨터에 제출한다 (컴퓨터는 바로 처리하지 않는다)

2] 컴퓨터는 테이프에 저장한다 (마그네틱에 읽혀진 Job을 여러개 저장)

3] 다 받은 여러개의 저장된 Job을 한번의 한개씩 처리한다

4] 컴퓨터는 수행한 결과를 테입에 출력한다

5] 사용자는 결과테입을 사용한다


<h4>성과</h4>

여러개의 카드덱(Batch of Jobs)을 하나의 Tape에 기록하고,

컴퓨터 시스템은 이 Tape에 있는 Job들을 순차적 수행을 통해

Operator의 느린 Job-to-Job 전환 속도 문제를 해결했다.

이를 통해 CPU의 효율성을 증가시키는 성과를 만들었다


<h4>OS 세번째 시기 (IO Channel)</h4>

<h4>등장배경</h4>

= operation IO 입출력까지 CPU의 역할이었다.

= CPU와 IO operation을 오버랩 할 수 있는 메커니즘을 개발했다

= 개발된 매커니즘이 (당시)IO Channel이다. (현재)IO Device controller라 칭한다

= CPU를 대신해 IO Device의 IO Opertion을 관리하고 IO Opertion의 시작과 끝만 CPU가 관리하는 방식으로 CPU는 IO Command(시작과 끝)만 IO Channel에 전달하고 CPU는 다른 업무를 처리할 수 있다


<h4>용어정리</h4>

1] IO Channel

= 채널이 IO Device의 IO Opertion을 관리하고, 시작과 끝만 CPU가 관리하게 하는 방식

2] Interupt

= I/O가 끝나고 CPU가 데이터를 읽어갈 수 있도록 메커니즘을 작동한다

그렇다면 CPU가 IO Operation의 시작과 끝은 어떻게 알 수 있는가?

시작과 끝을 알기 위해 Interupt가 최초로 등장한다

Interupt IO Controller가 IO Operation이 끝나면 CPU가 입력된 데이터를 읽어갈 수 있도록

CPU가 입력된 데이터를 읽어갈 수 있도록 Interupt 메커니즘을 작동시킨다

(Interupt는 I/O의 작동이 끝났음을 알려주는 역할을 했다)


문제 : I/O가 진행되는 동안 CPU가 I//O 작업을 관리하면서 기다려야 된다

해결방안 : I/O 작업을 관리해주는 I/O Channel의 도입은

CPU가 I/O의 시작과 끝만 관리하며 그 동안 다른 작업을 할 수 있도록 만들어준다.

업무가 끝나면 데이터를 읽어갈 수 있도록 Interupt 메커니즘이 실행되는데

Interupt 메커니즘의 실행은 Batch Monitor 지원한다.


<h4>여기서 잠깐!</h4>

이제 동기적 I/O와 비동기적 I/O의 개념이 필요하게 된다


<h4>동기적 I/O (Asynchronous)</h4>

CPU가 어떤 연산을 수행하다가 다른 I/O가 만들어졌을 때

수행하고 있던 연산이 종료되어야 다른 I/O의 연산을 실행할 수 있는 것을 말한다

<h4>비동기적 I/O (Asynchronous)</h4>

CPU가 수행중인 I/O 연산의 결과를 기다리지 않고 동시에 다른 I/O 연산을 수행하는 것을 말한다

생각해보면,  (나) 밥을 먹고 있다. (나) 전화가 왔다

동기 = 밥을 다 먹어야 전화통화를 할 수 있다 (여유롭다 - 적은 일을 수행한다)

비동기 = 밥을 먹다가 전화를 받을 수 있다 전화를 받으며, 밥을 먹을 수 있다

(정신없다 - 많은 일을 수행한다)


빠르게 원하는 것을 얻고자 하는 컴퓨터 상에서 클라이언트 입장에서 생각해보면

비동기적으로 프론트 화면에서 여러가지를 동시에 수행할 수 있을 때 사용자 만족감이 높다

중요한 업무를 수행하는 것 외에는 비동기적으로 수행이 많이 된다고 생각한다

중요한 업무로는 브라우저에서 생각해보면 클라이언트가 로그아웃 시 로그아웃 업무는 동기적으로 처리해 로그아웃 중에는 로그아웃이 완료된 결과를 확인하기 전까지 다른 업무를 수행할 수 없도록 하는 경우가 있다


<h4>Batch Monitor 한계</h4>

비동기적 I/O의 경우 CPU Utilization을 높일 수 있지만, 동기적 I/O는 여전히 낮은 CPU가 I/O동안 다른 작업을 수행할 수 없어 효율성이 낮았다


동기적의 경우 한번에 하나의 Job만 수행할 수 있어 효율성이 낮았다

효율성을 높이기 위해 Multi programming 등장한다


<h4>용어정리 (용어의 정의는 정확하게 아는 것이 좋다)</h4>

1] Mulit programming

한번에 하나 이상의 Job을 수행한다

2] Degree of Multiprogramming

현재 메인 메모리에 존재하는 Active Job의 갯수

3] Active Job

수행을 시작했지만 아직 종료되지 않은 업무를 컴퓨터 메인 메모리에 동시에 존재하는 것


<h4>Multi programming 등장</h4>

Multi programming 메인메모리 구조

메인 메모리에 Operationg system과 다수의 job이 존재하고 있다

예를들어 메인메모리(내부)에 Operating system(존재), job1(존재), job2(존재), job3(존재)


<h4>Multi programming Batch Monitor 등장</h4>

등장배경 : 동기적 I/O의 CPU 효율성이 낮은 문제를 해결하기 위해 Multiprogramming 지원이 필요했다

새로운 문제 3가지 등장 : Memory Protection, Memory Relocation, Current Programming


문제 1] Memory Protection

Multi programming을 작동하면서 발생하게 된다

포인터 에러와 같은데 다른 메모리를 건드리는 것을 말한다

예를들어 메모리 구조 내 Job1 업무를 수행하는데 Job1이 Job2를 침범해 실행시키게 되던가

operating system을 실행시키게 되면 큰 문제가 발생한다


문제 2] Memory Relocation

job1 업무가 어디에 위치하는지 알 수 없다 즉, 언제 interupt와 같은 업무를 실행해야 하는가를 알 수 없었다


<h4>Base register</h4>

Base register는 시작 주소를 해당 Job의 시작주소로 설정한다. 그리고 업무는 0번지부터 시작된다

예를들어 job2가 수행중이라면 주소는 job2의 시작주소를 가르키게 된다. 그리고 주소의 0번지를 가리킨다


<h4>Memory Protection</h4>

job이 사용하는 메인 메모리 시작 주소와 job이 사용하는 메모리의 크기(Bound Register에 저장)를 사용하여 현재 접근하려는 주소값이 Bese Register와 Base Register+Bound Register 사이에 있는지 확인한다


<h4>Memory Relocation</h4>

프로그램 작성 시에는 항상 0번지에 로드된다고 가정하여 주소값을 계산한다

Job 수행 시 주소값 계산은 Base Register의 값을 더하여 실제 물리적인 메모리 주소를 계산한다


<h4>생성되는 주소 2가지</h4>

1] CPU에서 프로그램을 통해 바로 생성된 주소 (=논리적 주소 - 런타임 과정을 거친다)

Base register 값을 구하여 Bound Register 내에 있는지 확인한다

- 논리 주소 = 프로그램에 의해 CPU가 바로 생성하는 주소이다

- 물리 주소 = 일련의 변환을 거친 최종 메인 메모리 주소이다

특정 메커니즘이 하드웨어 메커니즘인지 소프트웨어 메커니즘인지 알고 넘어가자


<h4>MMU(Memory Management Unit)</h4>

논리주소를 물리주소로 변경해주는 메커니즘이다

MMU는 하드웨어로 구성하는 것이 옳다

MMU를 소프트웨어로 생성 시 문제점

1] 성능의문제 - 하나의 instruction이 수행 되려면 최소 1개 이상의 instruction 주소가 생성된다

instruction이 메모리에 있는 것을 가져올 때 메모리 주소가 한번 더 발생하므로 메모리 효율이 낮아진다

2] MMU 주소 또한 instruction으로 구성되어 mapping 과정이 필요하며 자기를 반복 호출하는 재귀적 현상이 나타나므로 좋지 않다


<h4>Privilage instruction</h4>

= Operation system만 주소에 접근이 가능하다

MMU주소에 Opertion system 외에 Job의 접근이 가능하다면

Job이 MMU register를 자유롭게 변경하면 register의 주소가 마음대로 변경될 수 있다


문제 3] Current Programming

여러 Job이 동시에 수행 시 공유 자원과 공유 데이터를 동시에 접근하면서 문제가 발생한다

---

<h4>Phase2</h4>

해당 시기는 하드웨어가 발전한 시기다

1] 트랜지스터 발명

2] 집적회로 기술 발전

컴퓨터가 작아지면서 가격이 낮아진 시점 그리고 인건비가 상승했다

따라서, phase2 시기의 관심은 사람들의 생산성을 어떻게 증가시킬 것인가 HOW TO


<h4>용어정리</h4>

1] Terminal

1개의 CPU를 여러명의 유저에게 쪼개어 유저로부터 데이터나 명령을 입력받는다 (interative)

2] Time sharing operating system (Phase2시기의 큰 특징)

여러명의 유저가 CPU 사용시간을 쪼개어 갖는다

이는 컴퓨터와 프로그래머가 대화할 수 있는 interative가 가능하도록 만들었다

이는 현대 operating system의 기반이기도 하다

3] File system

사용자별로 파일로 구분

4] response time

operting sysytm 성능 평가의 척도는 사람들의 사용감

입력 시 결과가 얼마나 빠르게 전달하는가

Operating System = 복잡한 system\

추상화 = 복잡한 OS의 문제를 해결하는 역할을 갖는다

Phase 1 , Phase2 , Phase3의
원인과 결과를 파악하여 OS가 발전된 흐름을 이해해야 한다
OS의 스토리 라인을 갖고 학습할 때 OS의 공부는 완성된다


<h4>추상화 (blackbox abstract)</h4>
operating system이 갖고 있는 추상화까지 뚫고 들어가야 한다

<h4>왜 추상화를 알아야 하는가?</h4>

추상화를 하는 이유와 목적이 있다

추상화를 표현하는 용어의 의미는 정확하게 이해해야 한다

---

<h4>Phase3 (1990~현재)</h4>


<h4>Phase3 시기의 특징</h4>

1. 3C Convergence

    - Communication, Computer, Consumter Electronics 경계가 무너졌다

    - 인터넷 사용이 선택이 아닌 필수가 된 시대이다

    - 그 이유는 phase2 시기부터 하드웨어가 저렴해지면서 많은 사람들이 서비스를 사용하고 있기 때문에도 OS는 더욱 복잡하게 되었다.

<br>

<h4>Multimedia support</h4>

미디어가 여러개 있다는 것이 Multimedia

유니(텍스트)미디어에서 멀티미디어로 처리하는 대상이 변화하면서

멀티미디어의 중요한 특징은 Continuous Media

* Continuous media : 시간적 제약에 맞춰 연속적으로 처리해야 하는 데이터 (Ex : 동영상)

<br>

<h4>Continuous Media</h4>

특정 시간에 맞춰 연속적으로 처리해야하는 데이터

<br>

<h4>Downloading과 Streaming</h4>

1] Downloading

내가 원하는 전체 데이터를 확보한 다음에 작업을 진행하는 것입니다

2] Streaming

일부 데이터만 확호한 상태에서도 작업을 진행하는 것입니다

<br>

<h4>BandWidth 스케줄링 등장</h4>

- 스케줄링 방식의 변화

    - 중요한 일을 먼저 처리하는 우선순위 기반 스케줄링에서 Continous Media를 원활한 처리를 하기위해

    - BandWidth 스케줄링으로의 변화가 일어난다

    - 그 이유는 멀티미디어는 스케줄링이 잘못되면 사용자가 금방 저품질을 알게되어 "일정한 BandWidth"를 제공하는 스케줄링이 필요하다

<br>

<h4>Phase3 시기의 특징</h4>

2. Operating system(OS)이 전문적인 분야에서 보편적 자원으로의 변화를 했다

