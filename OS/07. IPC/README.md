# IPC (Inter-Process Communication)

    프로세스들 사이에 서로 데이터를 주고받는 행위 또는 그에 대한 방법이나 경로

![alt](https://camo.githubusercontent.com/ae371b6a70f7e11ebfbbd4cda052d103e6cf8c7e39b8ae3fd81e5396ef9bb9a8/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f393944423843343935433443353730343137)
<br>

- 프로세스는 완전히 독립된 실행객체라 다른 프로세스의 영향을 받지 않습니다.
- 독립되어 있는 만큼 별도의 설비 없이 서로 통신이 어렵다는 문제가 있기 때문에 `커널영역`에서 IPC를 제공하고 이를 이용해 프로세스 간 통신을 가능하게 합니다.

<br>

> ❔ 커널이란 <br>
> 커널은 운영체제의 핵심적인 부분으로, 파일입출력, 프로세스관리 등과 같이 운영체제의 기능을 담당 하지만 일반 사용자모드에선 커널에 접근할 수 없기 때문에 원칙적으로는 파일 입출력, 프로세스 생성등 커널의 기능을 사용하지 못합니다. 그래서 운영체제에서는 시스템 콜을 제공합니다.

<br>

## IPC 필요성
---
> - 정보 공유 : 여러 사용자가 동일한 정보에 엑세스 할 필요가 있다.
> - 가속화 : 특정 작업을 여러 개의 서브 작업으로 쪼개어 프로세스의 병렬성을 키움으로써 처리 속도를 높일 수 있다. 이때 메인, 서브 Task는 서로 통신의 필요성이 생김
> - 모듈화 : 특정 시스템 기능을 별도의 프로세스(스레드)로 구분하여 모듈화된 시스템을 구성할 수 있다.
> - 편의성: 다수의 사용자가 동시에 여러가지 작업을 수행할 수 있다. 

## 🔌IPC 설비

    IPC 종류로는 크게 메시지 전달(Message Passing)과 공유 메모리(Shared Memory)로 나뉩니다.

## 메시지 전달

|                                  내용                                   |                      장점                      |                       단점                        |
| :---------------------------------------------------------------------: | :--------------------------------------------: | :-----------------------------------------------: |
| 커널을 통해 메시지를 전달하는 방식으로 <br> 자원이나 데이터를 주고 받음 | 커널을 이용하기 때문에 <br> 구현이 비교적 쉬움 | 시스템 콜이 필요하며 <br> 이로 인해 오버헤드 발생 |

### PIPE (익명 PIPE)

- 단방향 통신, 반이중 통신
- 하나의 통신선로는 읽기나 쓰기 중 하나만 가능합니다.<br> 즉, 송/수신을 모두 원한다면 두 개의 파이프를 만들어야 가능합니다.
- 매우 간단하게 사용 가능하지만 <br> 반이중 통신이므로 프로세스가 읽기, 쓰기 모두를 해야 한다면 구현이 복잡해 질 수 있습니다.
- **통신을 할 프로세스를 명확하게 알 수 있는 경우** 사용합니다. <br> ex. 자식과 부모 프로세스간 통신
- **같은 PPID(같은 부모)를 가지는** 프로세스들 사이에서만 통신이 가능합니다.

<br>

### Named PIPE(FIFO)

- **전혀 모르는 상태의 프로세스들 사이의 통신에 사용**됩니다.
- 익명 PIPE의 확장으로 프로세스 통신을 위해 이름이 있는 파일을 사용하기 때문에 **부모 프로세스와 무관**하게 전혀 다른 모든 프로세스들 사이에서 통신이 가능합니다.
- mkfifo를 통해 Named PIPE를 생성합니다.
- 읽기/쓰기가 동시에 가능하지 않지만 통신 선로가 파일로 존재하기 때문에 하나를 읽기 전용으로 열고 다른 하나를 쓰기 전용으로 열어서 이러한 문제를 해결할 수 있습니다. <br> 즉, 전이중 통신을 위해서는 결국 두개의 FIFO 파일이 필요합니다.

<br>

### Message Queue

- 선입선출의 자료구조를 가지는 통신설비로 커널에서 관리합니다.
- Named PIPE는 데이터의 흐름이지만 메세지 큐는 메모리 공간이고, 어디서나 물건을 꺼낼 수 있는 컨테니어 벨트라고 보면 쉽습니다.
- 메시지가 발생하면 고정 크기의 메시지를 연결리스트를 통해 프로세스 간 통신을 수행합니다.
- 메세지 큐에서 사용할 데이터에 번호를 붙임으로서 여러 개의 프로세스가 동시에 데이터를 쉽게 다룰 수 있습니다.

<br>

### Socket

- 프로세스와 시스템의 기초적인 부분이며, 프로세스 둘 사이의 통신을 가능하게 합니다.
- 같은 도메인에서의 경우에만 연결될 수 있습니다.

  <br>

### Signal

- 프로세스 ID를 통해 특정 프로세스에 메세지를 전달하는 방식입니다.

<br>

## 공유 메모리

|                                     내용                                     |                             장점                             |                         단점                          |
| :--------------------------------------------------------------------------: | :----------------------------------------------------------: | :---------------------------------------------------: |
| 공유 메모리 영역을 구축하고 <br> 공유영역을 통해 자원이나 데이터를 주고 받음 | 커널 의존도가 낮기 때문에 <br> 속도가 빠르고 통신이 자유로움 | 자원과 데이터를 공유하기 때문에 <br> 동기화 이슈 발생 |

### Shared Memory

- PIPE, Named PIPE, Message Queue는 통신을 이용한 설비라면, Shared Memory는 공유메모리가 데이터 자체를 공유하도록 지원하는 설비입니다.
- 프로세스간 메모리 영역을 공유해서 사용할 수 있도록 허용하며<br> 프로세스가 공유 메모리 할당을 커널에 요청하면 커널은 해당 프로세스에 메모리 공간을 할당해주어 어떤 프로세스든 해당 메모리 영역에 접근이 가능하게 합니다.
- 중개자 없이 곧바로 메모리에 접근할 수 있기 때문에 모든 IPC들 중에서 **가장 빠르게** 작동합니다.

<br>

### Memory Map

- 공유메모리와 마찬가지로 메모리를 공유하지만 열린파일을 메모리에 맵핑시켜서 공유한다는 점에서 차이점이 있습니다.
- 파일은 모두 공유할 수 있는 자원이므로 다른 프로세스들끼리 데이터를 공유하는데 문제가 없습니다.

<br>

### Semaphore

- **Named PIPE, PIPE, Message Queue와 같은 다른 IPC 설비들이 대부분 프로세스간 메세지 전송을 목적으로 하지만,<br> Semaphore는 프로세스 간 데이터를 동기화 하고 보호하는 것이 목적입니다.**
- 프로세스 간 메시지 전송을 하거나, Shared Memory를 통해서 특정 데이터를 공유하게 될 경우 공유된 자원에 여러 개의 프로세스가 동시에 접근하면 안됩니다.<br> 이 때, **Semaphore, Mutex가 한 번에 하나의 프로세스만 접근 가능**하도록 만들어 줍니다.
