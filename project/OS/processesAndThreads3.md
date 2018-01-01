# Context Switching #

출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습 목표 :  개념적 틀을 가지고 구현을 학습

<br>

## Abstraction And Decomposition ##

### Complexity ###
1. Abstraction
	- 아래 계층의 복잡성을 추상화하여 단순화한 인터페이스를 상위 계층에 보내는 것 (그 결과 Layered Architecture 존재) 
2. Decomposition

<br>

### Layered Architecture ###
Abstraction을 System Architecture에 반영하면 Layered Architecture가 나오게 된다
(하위) 하드웨어 --> OS --> Middle ware --> Application1, Application2... (상위)

<br>

### Layering Principle ###
Abstraction이 완벽하게 구현되기 위해서는 Layered Principle 만족해야한다
상위 계층은 아래 계층이 제공하는 기능만을 사용할 수 있으며 반대의 경우는 발생하지 않아야 한다

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

---

<br>