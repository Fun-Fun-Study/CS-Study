# PCB와 Context Switching

## PCB(Process Control Block)란?

> 운영체제가 프로세스를 제어하기 위해 정보를 저장해 놓는 곳으로 프로세스의 상태 정보를 저장하는 구조체이다.

- 프로세스에 대한 정보가 저장된 구조체
- 프로세스 상태 관리와 문맥교환에 사용된다.
- 프로세스 생성 시 만들어지며 주기억장치에 유지된다.
- 프로세스가 교체되어 실행될 때 이전의 프로세스의 정보를 기억했다가 다시 불러오기 위한 BLOCK.

## PCB 저장 정보(Process Metadata)

- PID: 프로세스의 고유 번호
- Process state: 준비, 대기, 실행 등의 상태
- Process counter: 다음 실행될 명령의 포인터
- CPU register: CPU에서 사용한 레지스터 값을 저장
- CPU scheduling information: 프로세스의 우선순위, 최종 실행 시간, 스케줄링 큐를 가리키는 포인터 등
- Memory management information: 레지스터, 페이지 테이블, 세그먼트 테이블의 base, limit값에 대한 정보
- Accounting information: CPU 사용 시간, 실제 사용된 시간, 시간 제한 등
- I/O status information: 프로세스에 할당된 I/O 기기에 해당하는 정보

## PCB 관리 방법

- 연결 리스트(Linked List) 방식으로 관리한다.
- 새로운 프로세스가 실행되면 PCB를 생성하여 PCB List Head에 데이터를 연결한다.
- 연결 리스트 방식이기 때문에 삽입과 삭제가 용이하다.

### 프로세스 생성 과정

1. 새로운 프로세스를 위한 식별자를 할당한다.
2. 새로운 프로세스에 한 주소 공간과 프로세스 제어블록(PCB)를 할당한다.
3. 새로운 프로세스의 프로세스 제어 블록을 초기화한다.(상태정보, 카운터 ,우선순위 등)
4. 새로운 프로세스를 스케줄링 큐의 준비/보류 리스트에 연결한다.

## Context Switching이란?

> CPU가 현재 작업 중인 프로세스에서 다른 프로세스로 넘어갈 때 지금까지의 프로세스 상태를 저장하고, 새 프로세스의 저장된 상태를 다시 적재하는 작업
> <br>
> ` 프로세스가 Ready → Running, Running → Ready, Running → Waiting처럼 상태 변경 시 발생`

- 멀티 태스킹
  - 실행 가능한 프로세스들이 운영체제의 스케줄러에 의해 조금씩 번갈아가며 수행되는 것을 말한다.
  - 번갈아 가며 프로세스가 CPU를 할당받는데, 이 때 문맥교환이 이루어진다.
- 인터럽트 핸들링
  - 인터럽트가 발생하면 문맥교환이 이루어진다.
- 사용자와 커널모드 전환
  - 필수는 아니지만 운영체제에 따라서 발생할 수 있다.

## 오버헤드

> 문맥교환에 소요되는 시간과 메모리를 의미한다.

- 문맥교환이 발생하면 시간과 메모리가 소요되므로 잦은 문맥교환은 성능 저하를 가져온다.
- I/O 이벤트가 발생했을 때, 해당 이벤트가 끝날 때까지 작업을 할 수 없다.
  -> 오버헤드를 감수하더라도 다른 프로세스가 작업을 하는 것이 더 효율적이다.

- 멀티 태스킹에서 시간 할당량이 적어지면
  - 문맥교환 횟수와 오버헤드 증가
  - 동시에 수행가능한 프로세스 수 증가
- 시간 할당량이 커지면
  - 문맥교환 횟수과 오버헤드 감소
  - 동시에 수행가능한 프로세스 수 감소

## 문맥교환 시나리오

![문맥교환 시나리오](https://github.com/Fun-Fun-Study/CS-Study/assets/37894963/b133fa32-3d73-462a-a6c1-a25a15669167)

1. `P0` 프로세스가 인터럽트를 받으면서 `PCB0`에 `P0` 프로세스의 상태 정보를 저장한다.
2. 다음 수행될 `P1` 프로세스의 `PCB1`에서 `P1` 프로세스의 상태 정보가 CPU에 재로딩 된다.
3. `P1` 프로세스를 일정 시간 수행한다.
4. `P1` 프로세스가 인터럽트를 받으면서 `PCB1`에 `P1` 프로세스의 상태 정보를 저장한다.
5. 다음 수행할 `P0` 프로세스의 `PCB0`에서 `P0` 프로세스의 상태정보가 CPU에 재로딩 된다.
6. `P0` 프로세스를 일정 시간 수행한다.
