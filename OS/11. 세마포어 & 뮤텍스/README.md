# Mutex & Semaphore

🧑‍💻 **_동시성 프로그래밍_** 의 가장 큰 숙제는 **공유 자원 관리** 입니다. 공유 자원을 안전하게 관리하기 위해서는, 프로세스 간 메시지를 전송하거나, 공유된 자원에 여러 개의 프로세스가 동시에 접근하지 못하게 하기 위해 한 번에 하나의 프로세스만 접근할 수 있도록 제한을 두는 **동기화**가 필요합니다.
<br>

대표적인 동기화 기법에는 **뮤텍스(Mutex), 세마포어(Semaphore)** 가 있습니다.

> ❔ 동기화 (Synchronization) <br>
> 공유되고 있는 변수를 사용해 한 프로세스가 작업을 하고 있을 때, 다른 프로세스가 그 변수의 이용이 끝나기 전까지 사용하는 것을 막아주는 것

<br>

## 🔥뮤텍스 Mutex

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/3bfdda07-3521-4411-b7a4-bd6b1f906e18" alt="뮤텍스">

<br>

공유된 자원의 데이터 혹은 임계영역 등에 하나의 프로세스 혹은 스레드가 접근하는 것을 막아줍니다. <br> **동기화 대상이 하나**

- 임계구역을 가진 스레드들의 실행시간이 서로 겹치지 않고 각각 단독으로 실행(상호배제) 되도록 하는 기술입니다.
- 한 프로세스에 의해 소유될 수 있는 Key를 기반으로 한 상호배제 기법이며, Key에 해당하는 객체를 소유한 스레드/프로세스만이 공유자원에 접근할 수 있습니다.
- 다중 프로세스들의 공유 리소스에 대한 접근을 조율하기 위해 동기화 or 락을 사용함으로써 뮤텍스 객체를 두 스레드가 동시에 사용할 수 없습니다.
- 2진 세마포어 기법, Locking 기법으로도 불립니다.

<br>

ex) 식당 화장실 키를 A가 들고 들어간 순간, B는 A가 화장실 키를 반납할 때까지 해당 화장실을 이용할 수 없음

<br>

> ❔ 임계구역 (Critical Section) <br>
>
> Race Condition 경쟁 상태 현상이 발생할 수 있는 코드/부분/영역 <br>
> "상호배제, 진행, 한정된 대기" 3가지 조건으로 임계구역의 문제 해결 가능

> ❔ 상호배제 (Mutual exclusion) <br>
>
> 특정 프로세스가 공유자원을 사용하고 있을 경우, 다른 프로세스가 해당 공유 자원을 사용하지 못하게 제어하는 기법 <br>
> 여러 프로세스가 동시에 공유자원을 사용할 때, 각 프로세스가 번갈아가며 자원을 사용하게끔 임계 구역을 유지

> ❔ 진행 (Progress) <br>
>
> 임계영역에 진행 중인 프로세스가 없을 경우에, 임계영역에 진입을 요구할 경우 유한한 시간내에 진입해야 하며, 정당한 진입 프로세스를 막으면 안됨

> ❔ 한정된 대기 (bounded waiting) <br>
>
> 임계영역에 대한 진입을 요청 했을 경우, 무한히 기다리지 않고 유한한 시간내에 진입해야 함

<br><br>

## 🔥세마포어 Semaphore

<img src="https://github.com/Fun-Fun-Study/CS-Study/assets/96433955/f146921c-fc7b-4a1d-9267-776a6ba7d12f" alt="세마포어">

<br>

공유된 자원의 데이터 혹은 임계영역 등에 하나의 프로세스 혹은 스레드가 접근하는 것을 막아줍니다. <br> **동기화 대상이 하나 이상**

- 사용하고 있는 스레드/프로세스의 수를 공통으로 관리하는 하나의 값을 이용해 상호배제를 달성합니다.
- 공유 자원에 접근할 수 있는 프로세스의 최대 허용치만큼 동시에 사용자가 접근할 수 있고, 각 프로세스는 세마포어의 값을 확인하고 변경할 수 있습니다.
- 자원을 사용하지 않는 상태가 될 때, 대기하던 프로세스가 즉시 자원을 사용하고, 이미 다른 프로세스에 의해 사용중이라는 사실을 알게 되면, 재시도 전에 일정시간 대기해야 합니다.
- 비교적 긴 시간을 확보하는 리소스에 대해 사용하게 됩니다.
- 각 프로세스에 제어 신호를 전달하여 순서대로 작업을 수행하도록 합니다.
- wait(), signal()로 접근이 가능합니다.

<br>

ex) 3칸의 화장실이 존재한다면, A가 화장실을 가려고 할 때 카운터에서 빈 화장실의 개수를 체크해야함. 빈 화장실이 있으면, A는 빈 화장실 개수를 -1 하여 최신화하고 화장실을 이용함. 나올 때는 +1 로 최신화함.

<br><br>

## 💡차이점

|                                               Mutex                                               |                       Semaphore                        |
| :-----------------------------------------------------------------------------------------------: | :----------------------------------------------------: |
|                                         동기화 대상 하나                                          |                동기화 대상이 하나 이상                 |
|                                      자원 소유 가능, 책임 O                                       |                    자원 소유 불가능                    |
| 상태가 0, 1 뿐이므로 <br> Lock을 가질 수 있으며, <br> 소유하고 있는 스레드만 해당 Mutex 해제 가능 | Semaphore를 소유하지 않는 스레드가 Semaphore 해제 가능 |
|                  프로세스의 범위를 가지며 프로세스가 종료될 때 자동으로 Clean Up                  | 시스템 범위에 걸쳐 있고, 파일 시스템 상의 파일로 존재  |
|                                    뮤텍스는 세마포어가 될 수 X                                    |              세마포어는 뮤텍스가 될 수 O               |

<br>
<br>

[출처](https://heeonii.tistory.com/14)
