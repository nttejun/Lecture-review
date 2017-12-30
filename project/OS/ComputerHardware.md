## 운영체제 - Computer Hardware ##

학습목표 : Operating Stystem 공부에 필요한 기본적인 하드웨어 시스템을 학습

###컴퓨터 시스템 아키텍처(Computer System Architecture)###
1.	CPU
2. 메모리
3. IO device

#### System bus (시스템 버스) ####
하드웨어(컴퓨터 시스템)를 서로 연결해주는 역할

#### System bus (시스템 버스) 기능 ####
메모리 간 데이터 전송 (transaction)

#### System bus Operation ####
1.  read transaction
2.  write transaction

#### System bus 종류 ####
Data bus : 실제 데이터
Address bus : 전송 목적지

####Bus master####
bus transaction을 작동시키는 요소
> Bus arbiter : 복수 개의 Bus master 존재하고 있어 특정 System bus 지정이 필요합니다
> 정리하면, System bus를 관리하는 역할을 갖고 있습니다

####Bus slave####
데이터를 담는 장치
데이터의 주소(address)를 갖고 있다

###Bus Master 하드웨어 종류###
1. CPU
2. I/O Device Controller
3. DMA Controller 등

###I/O Operation###
####Interrupt-Driven I/O####
I/O 동작이 완료되면 I/O Controller 가 CPU에 비동기적으로 완료된 사실을 전달

####Polling I/O####
I/O 동작이 완료될때까지 CPU가 반복해서 I/O Controller Register 상태를 확인

####Port-mapped I/O#### 
Memory address, Port address 구분 방식

####Memory-mapped I/O####
I/O Register 맵핑하는 방법


###DMA Operation###
####DMA Controller####
DMA Controller는 블럭에 있는 데이터를 읽은 후 전송한다 
1. CPU는 데이터를 제공 (전송되야 할 메모리 시작점)
2. CPU는 블럭 크기를 제공 (한 블록의 데이터양)
3. 작업이 완료되면 CPU에게 Interrupt-Driven 방식으로 알림 

####DMA 블럭 데이터를 옮기는 방식####
1. Cycle stealing (CPU가 사용하지 않는 Bus를 사용하는 방식)  
2. Block transfer (CPU와 DMA Controller가 대등하게 경쟁하여 Bus 사용하는 방식)

---