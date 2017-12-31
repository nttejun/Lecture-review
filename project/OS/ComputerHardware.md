# Computer Hardware #
출처 : [서울대학교 평생교육원 - 운영체제의 기초, 홍성수](http://snui.snu.ac.kr/ocw/index.php?mode=view&id=684)

학습목표 : Operating Stystem 공부에 필요한 기본적인 하드웨어 시스템을 학습

## Computer System Architecture(컴퓨터 시스템 아키텍처) ##
1. CPU
2. 메모리
3. IO device


## System bus (시스템 버스) ##
하드웨어(컴퓨터 시스템)를 서로 연결해주는 역할

<br>

### System bus (시스템 버스) 기능 ###
메모리 간 데이터 전송 (transaction)

<br>

### System bus Operation ###
1.  read transaction
2.  write transaction

<br>

### System bus 종류 ###
Data bus : 실제 데이터
Address bus : 전송 목적지

<br>

### Bus master ###
bus transaction을 작동시키는 요소
> Bus arbiter : 복수 개의 Bus master 존재하고 있어 특정 System bus 지정이 필요합니다
> 정리하면, System bus를 관리하는 역할을 갖고 있습니다

<br>

### Bus slave ###
데이터를 담는 장치
데이터의 주소(address)를 갖고 있다

<br>

## Bus Master 하드웨어 종류 ##
1. CPU
2. I/O Device Controller
3. DMA Controller 등

<br>

## I/O Operation ##
### Interrupt-Driven I/O ###
I/O 동작이 완료되면 I/O Controller 가 CPU에 비동기적으로 완료된 사실을 전달

<br>

### Polling I/O ###
I/O 동작이 완료될때까지 CPU가 반복해서 I/O Controller Register 상태를 확인

<br>

### Port-mapped I/O ### 
Memory address, Port address 구분 방식

<br>

### Memory-mapped I/O ###
I/O Register 맵핑하는 방법

<br>


## DMA Operation ##
### DMA Controller ###
DMA Controller는 블럭에 있는 데이터를 읽은 후 전송한다 
1. CPU는 데이터를 제공 (전송되야 할 메모리 시작점)
2. CPU는 블럭 크기를 제공 (한 블록의 데이터양)
3. 작업이 완료되면 CPU에게 Interrupt-Driven 방식으로 알림 

<br>

### DMA 블럭 데이터를 옮기는 방식 ###
1. Cycle stealing (CPU가 사용하지 않는 Bus를 사용하는 방식)  
2. Block transfer (CPU와 DMA Controller가 대등하게 경쟁하여 Bus 사용하는 방식)

<br>

---

## Interrupt Mechanism ##
Interrupt는 개념을 이해하고 실제 Software, Hardware Interrupt가 어떻게 구현이 되었는지 확인한다

Interrupt Mechanism은 비동기 구조
OS가 존재하기 위해 컴퓨터 하드웨어가 제공하는 가장 중요한 Mechanism (Interrupt driven system)

<br>

### Interrupt 종류 2가지 ###
1. Hardware Interrupt
2. Software Interrupt

<br>

### Hardware Interrupt ###
CPU 외부에서 CPU가 처리되는 하는 일이 발생되면 신호를 통해 알려주어 문제를 처리할 수 있도록 한다

<br>

### Software Interrupt ###
현재 실행 프로그램에 문제(예외상항)가 발생되면 문제 해결을 진행하기 위해 별도로 지시하여 문제를 처리할 수 있도록 한다

<br>

### Interrupt Source 역할 ###
I/O Controller, DMA Controller 등

<br>

### Interrupt 처리과정 ###
1. Interrupt Signal를 받으면 프로그램이 중단된다
단, 현재 실행되고 있는 Instruction은 완료하고 그 다음 프로그램 실행을 중단시킨다
2. Interrupt 문제를 해결한 후 다시 실행하기 위해 중단된 지점의 주소는 안전하게 저장한다
3. Interrupt Request Number(IRQ 번호)를 통해 Interrupt Source 확인한다
4. Interrupt Vector Table 검색으로 Interrupt Service Routine(ISR) 주소를 확인한다
5. 확인된 주소는 처리해야 할 Handler address가 저장되어 있어 적절한 Handler가 실행된다

<br>

---

## Hardware Protection Mechanisms ##

### Privileged Instruction ###
Operation System만 수행할 수 있는 Instruction

<br>

### Dual Mode Operation ###
Mode 결정은 Micro Process 프로세스 안에 존재하는 Register가 결정한다
수행 모드는 2가지가 존재한다
1. Kernel Mode
2. User Mode


Dual Mode 존재하는 목적은 일반적으로 모든 사용자의 처리를 신뢰할 수는 없어
모든 처리를 허용하는 Kernal Mode, 제한적인 처리만 허용하는 User Mode 2가지로 구분한다
> 컴퓨터의 특성상 사용하지 않는 자원에 접근하려는 성격을 고려하면, I/O Device의 경우 권한이 없는 유저가 자원을 독점한다면 프로그램에 문제가 될 수 있어 권한을 구분하여 문제를 방지할 수도 있다


<br>

### Kernel Mode ###
Privileged Instruction를 수행시킬 수 있는 모드

<br>

### User Mode ###
Privileged Instruction만 수행시킬 수 없는 모드

<br>

### Operating System이 Kernel Mode에서 수행 시 받는 권한 ###
Privileged Instruction 수행시킬 수 있는 권한
모든 메모리 영역 접근할 수 있는 권한
(일반적으로는 자신에게 주어진 메모리 영역에만 접근할 수 있다)


> 메모 : Privileged Instruction 필요하면 Interrupt instruction을 수행시킨다
Interrupt Instruction은 모드를 커널모드로 변경시키는 기능을 갖고 있다
Hardware Interrupt가 발생하면 항상 Mode bit를 0에서 1로 변경시켜 커널모드로 변경시켜준다
Software Interrupt가 발생하면 Interrupt handler가 등장하고 이것이 유저의 권한을 변경해주게 된다

> Interrupt가 발생하면 Mode가 무조건 커널로 변경되고
모드 커널을 Interrupt Service Routine이 시스템을 장악한다
이 구조로 Computer Hardware Protection이 모두 진행되며
Operating System은 이 구조를 기반으로 동작한다

<br>
