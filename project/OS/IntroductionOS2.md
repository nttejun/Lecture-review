동영상 강의 : 서울대학교 평생교육원 [운영체제의 기초](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=627) Introduction to OS 2(2-1, 2-2) - 홍성수

<h4>Operating System은 어떤 기능을 해야하는가?</h4>

<h4>OS의 성격</h4>

굉장히 크며 복잡한 시스템이다 ( 컴퓨터 시스템을 관리하기 때문에 )

<br>

<h4>OS의 기능</h4>

- Coordinator
   - 여러 태스크가 자원을 차지하기 위해 충돌이 일어날 때 이를 중재하는 역할
- 추상화
    - 여러 유저가 사용하기 쉽도록 추상화를 통해 손쉬운 런타임 환경을 제공해주는 것
    - operating system이 복잡해 지면서 복잡성을 감소시키기 위한 방법으로 사용
- standard library
    - 시스템을 관리하는데 필요한 코드(모듈)를 제공하여 프로그래밍을 쉽게 할 수 있도록 제공하는 기본기능

<br>

<h4>OS의 역할</h4>

CPU 관리 시스템, IO device 관리 시스템, Memory 관리 시스템 3가지를 관리한다

추가로 File 시스템, 네트워크 시스템까지 총 5가지를 관리한다

<br>

<h4>유닉스에서 나눈 세 가지의 I/O시스템 구분</h4>

- Character I/O device
    - I/O의 단위가 작은 데이터인 byte 단위 ( 키보드, 마우스 )
- Block I/O device
    - I/O의 단위가 Block인 단위 ( 하드디스크 )
- Network I/O device
    - Network를 제어하는 장치 ( 소켓 )

<br>

<h4>I/O 시스템을 3가지로 구분하는 이유는?</h4>

I/O 관리에 따라서 성능의 차이가 크게 나타난다

중요한 데이터의 경우에는 별도의 큐를 제공해 전송하는 것이 효율적이다

<br>

<h4>Illusion</h4>

복잡한 것을 추상화를 통해 사용하기 쉽도록 만든 후 여러 유저에게 동일하게 제공한다


<h4>freshing</h4>

Illusion의 단점 : 추상화를 잘못 제공했을 경우를 말한다

<br>

<h4>Time-Sharing 시스템에서의 Thrashing</h4>

사용자의 수가 특정 임계점을 넘는다면 순간 응답 시간이 급격하게 증가하는 현상이다




