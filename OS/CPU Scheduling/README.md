# CPU Scheduling

## ❓ CPU Scheduling 이란

### 개념

> 프로세스가 생성되어 실행될 때 최적의 성능을 내기 위해서, 필요한 시스템의 자원들을 **어떤 프로세스**에 **얼마나 할당**하는지를 정하는 작업

### 목적

- **공평성** : 프로세스 자원 배분 과정이 공평
- **효율성** : 처리량의 극대화 (시스템 자원을 쉬게 하지 않음)
- **안정성** 및 확장성 : 시스템 자원 또는, 프로세스가 늘어나도 시스템 정상 반영, 정상 동작
- **반응 시간 보장** : 프로세스의 요구가 있을 때 반환 시간이 예측이 가능
- **실행의 무한 연기 배제** : 특정 프로세스의 작업 무한 연기 X

<br>

### 시스템별 스케쥴링 요구사항

> **Batch System**
>
> - 한 번에 하나의 프로그램만 수행
> - 응답시간, turnaround time 등은 중요하지 않음
> - **가능하면 많은 일을 수행**하기 위해 utilization 최대화

<br>

> **Interactive System**
>
> - **사용자와 컴퓨터의 대화로 동작**
> - 가장 중요한 것이 response time, 다음이 waiting time
> - waiting time을 줄이기 위해 time sharing 방법 고려

<br>

> **Real Time Systems**
>
> - 인풋 아웃풋 계산이 끝이 아닌, 시간 제약 조건이 추가
> - hard real time systems : 시간 제약 조건을 만족 못 하면 문제 발생함
> - soft real time systems : 시간 제약 조건을 만족 못 하면 지금까지의 결과가 무의미해짐
> - **시간 제약 조건을 만족시키는 스케쥴링**이 가장 큰 목표

---

## 💡 Tip. 프로세스 상태 전이

<img src=https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/a323fdf5-2c95-4859-abe2-a942345c50bd>

<br>

**✓ 승인 (Admitted)** : 프로세스 생성이 가능하여 승인됨

**✓ 스케줄러 디스패치 (Scheduler Dispatch)** : 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것

**✓ 인터럽트 (Interrupt)** : 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태로 바꾸고, 해당 작업을 먼저 처리하는 것

**✓ 입출력 또는 이벤트 대기 (I/O or Event wait)** : 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태로 만드는 것

**✓ 입출력 또는 이벤트 완료 (I/O or Event Completion)** : 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것

---

## 🎲 CPU 스케쥴링의 종류

### 선점형 스케쥴링

> 운영체제가 필요하다고 판단하면, **_실행 상태에 있는 프로세스의 작업을 중단하고 새로운 작업을 시작_**

- 우선 순위가 높은 프로세스를 빠르게 처리해야 하는 경우 유용
- 응답이 빠르지만, 처리 시간을 예측하기 힘듬
- 빈번한 **Context Switching** 으로 인한 오버헤드 발생 가능

#### 선점 알고리즘

##### Round Robin

- 프로세스마다 같은 크기의 CPU 시간을 할당 (시간 할당량 / Time Slice / Quantum) - 보통 10 ~ 100ms 정도
- 프로세스가 할당된 시간 내에 처리완료 못하면 준비 큐 리스트의 가장 뒤로 보내지고, CPU는 대기중인 다음 프로세스로 넘어감
- 균등한 CPU 점유 시간을 보장하며, 시분할 시스템에 사용

##### SRT (Shortest Remaining Time First)

- 가장 짧은 시간이 소요되는 프로세스를 먼저 수행
- 남은 시간이 더 짧다고 판단되는 프로세스가 준비 큐에 생기면 언제라도 프로세스가 점령됨

##### 다단계 큐 (Multi Level Queue)

- 작업들을 여러 종류 그룹으로 분할, 여러 개의 큐를 이용하여 상위 단계 작업이 선점
- 각 큐는 자신만의 독자적인 스케쥴링을 가짐

##### 다단계 피드백 큐 (Multi Level Feedback Queue)

- 입출력 위주와 CPU 위주인 프로세스의 특성에 따라 큐마다 서로 다른 CPU 시간 할당량 부여
- FCFS와 라운드 로빈 기법혼합
- 새로운 프로세스는 높은 우선순위를 가지지만 프로세스의 실행 시간이 길어질 수록 점점 낮은 우선순위 큐로 이동하며, (이 때, 우선 순위가 낮을 수록 시간할당량을 크게 줌으로써 보완 가능) 마지막 단계에서 FCFS 방식을 적용
- 유연성 뛰어남, turnaround 시간과 response time에 최적화

<br>

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/ce8cd21f-8761-4e3f-a126-e3c97192ea7e" />

<br>

### 비선점형 스케쥴링

> 어떤 프로세스가 실행 상태에 들어가면 그 프로세스가 끝나거나, 자원을 자진 반납하는 경우가 아니면 계속 실행

- 오버헤드도 적고 스케쥴러의 비중도 줄어들어 효율적일 수 있지만, **전체 시스템의 처리율** 이 떨어짐

#### 비선점 알고리즘

##### FCFS 스케쥴링 (First Come First Serve Scheduling)

- CPU를 먼저 요청한 프로세스가 먼저 CPU를 배정 받는 스케줄링 방법
- 프로세스가 대기 큐에 도착한 순서에 따라 CPU 할당

##### SJF (Shortest Job First)

- 프로세스가 도착하는 시점에 따라 그 당시 가장 작은 서비스 기간을 갖는 프로세스가 종료 시 까지 선점
- 준비 큐 작업중 가장 짧은 작업부터 수행하므로 평균 대기시간 최소
- CPU 요구시간이 긴 작업과 짧은 작업간의 불평등이 심하여, CPU 요구시간이 긴 프로세스는 기아 현상발생

##### 우선순위 (Priority)

- 각 프로세스 별로 우선순위가 주어지고, 우선순위에 따라 CPU 할당
- 우선순위가 같을 경우 FCFS 적용
- 설정, 자원 상황등에 따른 우선순위를 선정해 주요/긴급 프로세스에 대한 우선처리 가능

##### 기한부 (Deadline)

- 작업들이 명시된 기간이나 기한 내에 완료되도록 계획

##### HRN (Highest Response Ratio Next)

- 대기 중인 프로세스 중 현재 Response Ratio가 가장 높은 것을 선택
- (Response Ratio = (대기시간 + 서비스시간) / 서비스시간)
- 대기시간이 긴 프로세스일 경우 우선순위가 높아짐
- 긴 작업과 짧은 작업 간의 지나친 불평등을 해소할 수 있음

<br>

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/73164347/cc1f1ffb-1f64-43e7-85be-64f49083154b" />

<br>