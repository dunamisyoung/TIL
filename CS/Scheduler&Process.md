# 기초 CS 지식 알아보기

## 🌱 부족한 개념들이 많아 계속 수정할 예정입니다 :)

### 스케쥴러, 프로세스

컴퓨터는 어느 순서대로 프로세스를 실행 시킬까?

스케쥴링 알고리즘에 대해 알아보자.

### 스케쥴러

**FIFO 스케쥴러 - First in first out 선입선출**

먼저 메모리에 올린것을 먼저 실행하는 것이 가장 일반적이라고 할 수 있다.

프로세스가 저장 매체를 읽는 다든지, 프린팅을 한다든지 하는 작업 없이 쭉 cpu를 처음부터 끝까지 사용한다.

**가장 간단한 스케쥴러는? → (배치 처리 시스템)**
어떠한 일이 다 끝날때 까지 기다렸다가 끝난이후에 실행하는것

**SJF 스케쥴러 - 최단 작업 우선 스케쥴러**
가장 프로세스 실행시간이 짧은 프로세스 부터 먼저 실행 시키는 알고리즘

🎇 **RealTime OS(RTOS)**

응용 프로그램 실시간 성능 보장 목표로 하는 OS 정확하게 프로그램 시작, 완료시간을 보장한다.

- Hardware RTOS, Software RTOS

🎇 **General Purpose OS(GPOS)**

프로세스 실행시간에 민감하지 않고, 일반적인 목적으로 사용되는 OS - window, Linux

## **우선순위 기반 스케쥴러**

**정적 우선순위**

- 프로세스 별로 우선순위를 미리지정

예를 들어 맥 OS에서 파이널컷프로를 우선순위 1 나머지 프로세스는 뒤로..

- **동적 우선순위**
- 프로세스를 더욱 필요로하는것을 동적으로 결정해서 실행한다.

실행이 오래걸리는것을 우선순위를 높게 설정해 프로세스 반응속도를 높여줄수 있게끔 한다.

- **Round Robin 스케쥴러**

프로세스 실행시 일정 부분만 실행시키고 다시 큐에 넣어준다.

- **CFS**

프로세스의 수가 많아지더라도 일정한 시간을 걸리게 한다.

프로세스 상태 기반 스케쥴러

- running state : 현재 CPU에서 실행 상태
- ready state : CPU에서 실행 가능 상태
- block state : 특정 이벤트 발생 대기 상태

`프로세스 생성(new Q) -> 실행가능(ready Q) -> 실행 중(running Q) -> 대기(blocked Q) -> 종료(exit Q)`

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/11fde25f-81f9-407f-afd4-1c05f024d07e/processState.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/11fde25f-81f9-407f-afd4-1c05f024d07e/processState.jpg)

_이미지 출처 - 잔재미 코딩_

프로세스 실행시 바로 readyQ로 들어간다고 해도 무방하다.

Q에서 pop된 아이를 CPU에 전달후 실행후 다시또

지금 바로 CPU에 넣어도 실행할수있는 상태가 ready state

하드웨어를 읽거나 다른동작을 하게되면, blocked Q

결국 스케쥴러가 하는일은 팝한다. -> CPU에 전달

Ready Q에 아무것도 없다면, CPU는 놀고있다.

그렇게 Ready Q에 아무것도 없을때 스케쥴러는 프로세스가 있는지 계속 확인한다.

- 스케쥴러가 이벤트 루프 같은거다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38046de8-4306-4f50-b7d8-7146c63e85e4/processAlgorithm.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38046de8-4306-4f50-b7d8-7146c63e85e4/processAlgorithm.jpg)

_이미지 출처 - 잔재미 코딩_

프로그램 성능을 높이고 싶을때 알아두면 좋을 팁

- [IO-bound : IO](https://jhnyang.tistory.com/25) 관련 기능이 주로 사용하는 프로그램 - 데이터베이스 같은것이다.
- CPU-bound : CPU / 메모리를 사용하는 프로그램

레디스(Redis)는 메모리로만 데이터를 주고 받는다.

수시로 파일등을 접근한다면,

한번에 데이터를 메모리에 올려 놓고 접근하도록 만드세요.

### 프로세스

**프로세스 구조**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44e280db-adc0-41c0-97dd-50f4eb0f04aa/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44e280db-adc0-41c0-97dd-50f4eb0f04aa/Untitled.png)

_이미지 출처 - 잔재미 코딩_

프로세스는 일반적으로 어떻게 구성되어있을까?

- text : 코드 - [바이너리](https://ko.wikipedia.org/wiki/%EB%B0%94%EC%9D%B4%EB%84%88%EB%A6%AC) 코드가 올라간다.
- data : 하나의 값을 담기위한 메모리공간 / 변수 초기화된 데이터 / 전역변수
- heap : 동적메모리를 위한 공간 / 코드에서 동적으로 만들어지는 데이터
- stack : 함수처리를 위한 공간 / 임시 데이터(함수 호출, 로컬 변수)

**프로세스와 컴퓨터 구조**

- pc (program counter) + sp(stack pointer)
- pc : 다음 실행할 코드주소가 들어가있다.
- sp : 스택 최상단주소

CPU는 최상단 주소에서 1씩 증가 시키면서 프로그램을 실행하며 다음주소를 가르킨다.

함수 선언은 별도의 공간을 만들지 않는다

`순차적으로 주소를 따라가면서 코드를 실행한다. - 리턴위치 = 함수 실행이 끝나고 돌아갈 위치 -> 그위치를 스택에 담는다.`

변수도 스택에 하나씩 담긴다.

코드 실행이 끝나면 리턴위치까지 스택 값을 비워준다.(POP)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18f01571-327d-4cdd-8be2-1015ac2b9b0d/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18f01571-327d-4cdd-8be2-1015ac2b9b0d/Untitled.png)

_이미지 출처 - 잔재미 코딩_

결국 프로그램은 프로세스다.

**데브옵스**

시스템 관리자, 서버 개발자 - 관리 + 개발 = DEV OPS 팀 -> 서버 관리프로그램을 개발

배포나 관리를 좀더 원할하게끔 하는 프로그램을 만드는 개발자.

**Agile**

이전에는 계획을 짜고 나서 개발을 하는것이엇다면,

기능을 작게만들어서 사용자에게 피드백을 받아 개발하는것이다.

기능개발 -> 사용자 피드백 -> 개발

**컨텍스트 스위칭**

프로세스가 교체될시점에

CPU가 어딘가의 공간에 PC와 SP 값을 저장해놓는다.

**PCB (process Control Block)**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61d15468-b6a8-4b3e-a20f-7b8beb160cf6/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/61d15468-b6a8-4b3e-a20f-7b8beb160cf6/Untitled.png)

_이미지 출처 - 잔재미 코딩_

- PCB에 다음 프로세스 정보 저장

프로세스 ID, 레지스터 (pc, sp 등) 등

프로세스가 실행중인 상태를 캡쳐/ 구조화 해서 저장.

**컨텍스트 스위칭 세부동작**

컨텍스트 스위칭은 10ms마다 프로세스를 바꿔가며실행

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcd6bb81-b394-4c4b-9a00-30771bda92a9/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcd6bb81-b394-4c4b-9a00-30771bda92a9/Untitled.png)

_이미지 출처 - 잔재미 코딩_

1. 실행 중지할 프로세스 정보를 해당 프로세스의 PCB에 업데이트 해서 메인 메모리에 저장.

2. 다음 실행할 프로세스 정보를 메인 메모리에 있는 해당 PCB 정보(PC, SP)를 CPU의 레지스터에 넣고 실행

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66524b0a-b95c-40c6-a01b-80e85a9519c8/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/66524b0a-b95c-40c6-a01b-80e85a9519c8/Untitled.png)

이미지 출처 - 잔재미 코딩

우리가알고있는 레코드 판과 연관지어 생각해보면, 그 레코드 침을 어디서 놓냐에 따라서 실행 시점이 결정된다.

**어셈블리어**

기계어랑 1대1 매칭이되는거가 어셈블리어 라는게있다. - 매우 복잡하고 어렵다.

어셈블리어의 진화 → c언어

**프로세스간 커뮤니케이션 (InterProcess Communication)**

프로세스가 하나가 아니고 여러개라고 했을때?

프로세스는 다른 프로세스의 공간을 접근할 수 없다.

- 프로세스간 접근불가 - 프로세스간의 통신은 필요하다라고 느낌

CPU 입장에서 OS를 통해 바라보는 프로세스의 주소는 각각의 프로세스 마다 동일하다.

즉, 모든 프로세스가 번지수가 같다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7dad3e31-7a57-48f3-bb23-1154c44115fa/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7dad3e31-7a57-48f3-bb23-1154c44115fa/Untitled.png)

_이미지 출처 - 잔재미 코딩_

프로세스가 두개라고 가정했을때 A프로세스가 B프로세스에 접근할수 있는 방법은 아예없다.

서로를 지정할수 없는 번호가없다.

하나의 운영프로그램은 여러개의 프로세스가 있어도된다.

즉, 프로세스간 통신이 필요하다.

**IPC기법을 통해 극복**

프로세스간 서로 접근할수없지만, 프로세스간의 통신은 필요할경우 IPC 기법을 통해 극복

IPC 기법은 프로세스간 통신 방법을 제공한다.

- ex) 내컴퓨터와 다른 컴퓨터간의 통신
  프로그램 두개가 서로통신을 해야할때
- 파일을 처리, 네트워크

파일을 하나 만들어놓고 컴퓨터 끼리 그 만든 파일에 데이터를 올리고 사용하고 하는것도 IPC 기법이라고 할수있다.

**아파치 웹서버**

하나의 요청에 의해서, 하나의 역할만 해야한다고 한다면, 우리는 그것을 기다릴수없다.

그렇기에 웹서버를 멀티 프로세스로 만드는 방법을 생각해 놓았다.

멀티 프로세스를 만들어놓고 많은 요청을 받아 실행할수 있게끔 되었다.

**프로세스간 커뮤니케이션**

어떤 프로세스나 0 - 4 GB 까지의 메모리 주소를 가진다.

4GB에 공간에는 운영체제를 위한 공간이 있다.

운영체제는 하나의 프로세스 처럼 동작한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4ff7a72-3a22-4a3d-8071-3382e395c564/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4ff7a72-3a22-4a3d-8071-3382e395c564/Untitled.png)

_이미지 출처 - 잔재미 코딩_

커널모드로 들어갔을때만 접근할수있는 공간이 있으며, 우리가 입력한 것에 따라서 공간을 확보하여 데이터를 쓰고 읽을수 있다.

프로세스 A와 프로세스 B는 커널 공간을 서로 공유한다.

커널 공간에 메모리공간을 만들고 데이터를 읽고 쓰게되면 프로세스간 통신이 가능하다.

file을 사용하면 실시간으로 직접 원하는 프로세스에 데이터 전달이 어렵다.

그렇기에 다양한 IPC 기법이 나왔는데,

- **Message Queue,**
- **Shared Memory**
- **Pipe**
- **Signal**
- **Semaphore**
- **Socket**

공유 메모리를 예를들면,

사용자 모드에서는 직접적으로 커널 공간에 접근이 불가하고 커널 모드에서만 커널 공간으로의 접근이 가능하다.

공유메모리는 어떤 함수를 호출하면 그 함수는 특별히 시스템 콜로 호출이되어 커널공간의로써의 접근이 가능하게되는것.

즉, kernel space에 메모리 공간을 만들고 해당 공간을 변수처럼 사용하게 된다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4704f343-e693-4a95-a936-57860726388d/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4704f343-e693-4a95-a936-57860726388d/Untitled.png)

_이미지 출처 - 잔재미 코딩_

### ✨**정리**

여러 프로세스 동시 실행을 통한 성능을 개선하고, 복잡한 프로그램을 위해 프로세스간 통신이 필요했다.

- 프로세스간 공간이 분리되어있음
- 프로세스간 통신을 위한 특별한 기법 필요 - IPC기법만듬
- 대부분의 IPC 기법은 결국 프로세스간 커널 공간을 활용하는 것임
- 커널(운영체제) 공간은 공유하기 때문

**가비지 컬렉션**

객체들은 heap에 들어가있다.

heap도 제한된 공간이다.

가비지 컬렉터가 하는일은 쓰지 않는 메모리 공간을 해제해서 heap 공간을 늘린다.

**소켓 -** 네트워크와 통신할수있는 함수 (네트워크와 관련된 함수)

**노티피케이션(notification)** - 알람같은거라고 생각하면된다.

**`프로세스는 주소공간이 완전이 동일하며 , 프로세스공간이 완전히 분리되어있기에 프로세스 통신을위한 특별한 기능이있고, 다양한 기능을 통칭하는것이 IPC공간이고, IPC 공간의 핵심은 커널공간을 공유해서 프로세스간 데이터를 주고 받는것을 말한다.`**

한장의 그림으로 정리 해보기

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e4f8a9d-66dc-456f-b81d-f726a9e6ee1d/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e4f8a9d-66dc-456f-b81d-f726a9e6ee1d/Untitled.png)

_이미지 출처 - 잔재미 코딩_

### **Thread (스레드)**

Light weiht Process 라고도 함

- 프로세스
  프로세스간에는 각 프로세스의 데이터 접근이 불가 - IPC로만 가능
- 스레드
- 하나의 프로세스 안에서 스레드 여러개를 생성할수 있고, 각각의 스레드들이 병렬로 실행할수있다. ( 동일한 역할을 하는 프로세스가 여러개이다 라고 생각하자)
- 프로세스 안에 있으므로 프로세스의 데이터를 모두 접근 가능
- 스레드는 함수다 - 스레스 함수를 통해 스레드를 만들수있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/349809d3-98e2-4caf-a261-38191694e3aa/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/349809d3-98e2-4caf-a261-38191694e3aa/Untitled.png)

_이미지 출처 - 잔재미 코딩_

함수는 스택에서 실행된다.

CODE안에 스레드를 생성할수있는 함수가있다.

함수만을 별도스택에서 실행할수있는 기능을 갖춘것이 스레드다.

CODE랑 DATA랑 HEAP은 부모프로세스 공간에 접근할수있기에 하나의 프로세스 안에서 여러 스레드를 생성하면 각각의 코어에 스레드를 넣어 주면 병렬처리가 가능 하며 부모프로세스에 접근이가능하다.

스레드는 IPC 기법이 필요없다.

**멀티 스레드**

프로세스 병렬 처리를 위해 사용한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0bb91799-d177-42d2-859a-082ec189cfe0/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0bb91799-d177-42d2-859a-082ec189cfe0/Untitled.png)

_이미지 출처 - 잔재미 코딩_

**멀티 프로세싱이란?**

하나의 프로세스중 각각의 기능들을 분리하여 분리한 기능을 CPU나 코어에 별도로 할당해서 병렬로 실행하게끔 하여 처리속도를 높이는 스케쥴링기법이다.

최근 CPU는 멀티 코어를 가지므로 Thread를 여러개 만들어 멀티코어 활용도를 높였다.

최근에는 짧은 반응 시간이 우선이기에 성능 개선에 신경을 많이쓰므로

- 멀티 프로세스 또는 멀티 스레드를 고려한다.

**멀티 프로세스와 멀티 태스킹**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1249981-ec6f-4905-b5a7-6eb11628fc7d/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1249981-ec6f-4905-b5a7-6eb11628fc7d/Untitled.png)

_이미지 출처 - 잔재미 코딩_

**thread 장점1**

사용자에 대한 응답성을 향상한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/96ccf745-08b4-4591-b725-82f0e7da8b09/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/96ccf745-08b4-4591-b725-82f0e7da8b09/Untitled.png)

_이미지 출처 - 잔재미 코딩_

- IO 처리
- 사용자 통신 등등

병렬적으로 처리가 가능하다.

**thread 장점 2**

자원공유가 효율적이다.

프로세스안에서 실행되기에 프로세스의 데이터를 모두 접근가능하며, 자원을 효율적으로사용한다.

IPC 기법을 사용하지 않기에 자원 공유를 위해 번거로운 작업이 필요없다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57e95106-5639-47df-89bf-5b77bf084712/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57e95106-5639-47df-89bf-5b77bf084712/Untitled.png)

_이미지 출처 - 잔재미 코딩_

**thread 장점 3**

작업이 분리되어 코드가 간결

- 작성 나름

**thread 단점**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc681b4b-ccba-42d7-bcdc-10e6cc4587da/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc681b4b-ccba-42d7-bcdc-10e6cc4587da/Untitled.png)

_이미지 출처 - 잔재미 코딩_

하나의 기능을 하나의 프로세스로 만들지 않고 멀티 프로세스로 만든다면?

하나의 기능이 죽는다고 해도 다른 프로그램에 영향을 주지 않는다.

**멀티 스레드는**

스레드중 한 스레드만 문제가 있어도 전체 프로세스가 영향을 받는다.

스레드를 많이 생성하면 Context Switching이 많이 일어나 성능 저하를 일으킨다.

리눅스 OS에서는 thread를 process와 같이 다룬다.

**멀티 프로세스**

- 하나의 프로세스가 다운되어도 프로그램에 영향을 주지않음

**멀티 스레드**

- 하나의 스레드가 다운되어도 프로그램에 영향을 준다.

**thread의 가장큰 단점**

스레드를 많이 생성하면 모든 스레드를 스케쥴링해야하므로 컨텍스트스위칭이 많이 일어난다.

동기화 이슈로인해서 비정상적으로 동작가능하다.

동기화 기법을 통해서 극복해야된다.

### process VS thread

- 프로세스 독립적이다.
- 스레드는 프로세스안에 있으며 자원을 공유할수있다.
- 프로세스는 자기만의 주소를 가진다.
- 스레드는 프로세스 주소영역을 공유 한다.
- 프로세스간에는 IPC 기법으로 통신해야한다. 스레드는 필요없다.

✨**thread 개념 정리**

프로세스와 달리 스레드간 자원을 공유한다.

**스레드 장점**

- CPU 활용도를 높이고,
- 성능 개선 기능
- 응답성 향상
- 자원공유 효율 (IPC를 안써도된다.)

**스레드 단점**

- 하나의 스레드 문제가 전반적인 영향을 미친다.
- 여러 스레드 생성시 성능 저하 기능
