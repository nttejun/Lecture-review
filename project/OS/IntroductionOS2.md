동영상 강의 : 서울대학교 평생교육원 [운영체제의 기초](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=627) Introduction to OS 2(2-1, 2-2) - 홍성수

<h4>Operating System은 어떤 기능을 해야하는가?</h4>

<br>

<h4>OS의 성격</h4>

- 일반적인 성격은 굉장히 크며 복잡한 시스템이다 ( 컴퓨터 시스템을 관리하기 때문에 )

- 기존 제품을 개발하고 있던 개발자가 떠나도 OS는 계속 발전하게 된다

<br>

<h4>OS의 기능</h4>

- Coordinator
   - 여러 태스크가 자원을 차지하기 위해 충돌이 일어나게 됩니다. 이때 OS가 적절한 중재자 역할을 합니다

- 추상화
    - 추상화를 제공합니다
        > Ex : PC 에서 Hello world 를 출력한다고 하면 프로그래밍 하기 쉬운 런타임 시스템을 통해 OS는 자기를 사용하는 유저가 손쉽게 사용할 수 있도록 추상화를 제공한다

    - operating system 이 복잡해 지면서 복잡성을 감소시키기 위한 방법으로 사용

- standard library

    - 시스템을 관리하는데 필요한 코드(모듈)를 제공하여 프로그래밍을 쉽게 할 수 있도록 제공하는 기본기능

<br>

<h4>OS의 역할</h4>

- CPU 관리 시스템

- IO device manager 관리 시스템

- Memory 관리 시스템 3가지를 관리한다

- 추가로 서브 역할 2가지가 더 존재한다
    - File 시스템
        - File 은 하드디스크 드라이브라는 볼륨 스토리지에 저장되어있는 데이터로 즉, File은 하드디스크 IO를 관리하는 시스템
    - 네트워크 시스템까지

- 5가지를 관리한다

<br>

<h4>유닉스에서 나눈 세 가지의 I/O시스템 구분</h4>

- Character I/O device
    - 데이터 I/O의 단위가 작은(소량) 데이터인 byte 단위 ( 키보드, 마우스 )

- Block I/O device
    - 데이터 I/O의 단위가 Block인 단위 ( 하드디스크 )

- Network I/O device
    - Network를 제어하는 장치 ( 소켓 )

<br>

<h4>I/O 시스템을 3가지로 구분하는 이유는?</h4>

- I/O 관리에 따라서 성능의 차이가 크게 나타납니다

- 중요한 데이터의 경우에는 별도의 큐를 제공해 전송하는 것이 효율적입니다

    > 속도에 민감한 것은 별도의 길을 제공해야 합니다
    이것에 따른 성능의 차이가 많이 차이가 나게 되기 때문입니다

<br>

<h4>OS Illusion Generator</h4>

Application --- Operating System --- Hardware

Proc1, Proc2, Proc3... --- Operating System --- Hardware


<h4>Illusion</h4>

복잡한 것을 추상화를 통해 사용하기 쉽도록 만든 후 여러 유저에게 동일하게 제공한다


<h4>freshing</h4>

Illusion의 단점 : 추상화를 잘못 제공했을 경우를 말한다

<br>

<h4>Time-Sharing 시스템에서의 Thrashing</h4>

사용자의 수가 특정 임계점을 넘는다면 순간 응답 시간이 급격하게 증가하는 현상이다

<h4>Time-Sharing</h4>

OS가 제공하는 추상화 기능 중 하나입니다. 실제 컴퓨터는 1개지만 여러명이 모두 개인 컴퓨터를 부여받은 느낌을 제공합니다

단, OS가 제공하는 자원의 범위를 적정수준 이상이 되면 Thrashing 발생



