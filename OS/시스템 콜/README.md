# 시스템 콜

> 시스템 콜이란 응용 프로그램에서 운영 체제의 커널이 제공하는 서비스에 접근하기 위한 인터페이스이다.

- 시스템 호출이라고도 한다.
- 사용자 프로그램이 디스크 파일에 접근하거나 화면에 출력하는 등의 작업이 필요할 때, 운영체제에 특권 명령의 대행을 요청하는 것을 말한다.

### CPU 모드

- 유저 모드
  - 사용자 프로그램이 실행되는 모드
  - 사용자가 접근할 수 있는 영역을 제한하여 자원을 보호하기 위함
  - 일반 명령: 유저 모드에서 사용자가 실행하는 명령
- 커널 모드
  - 운영체제 커널이 실행되는 모드
  - 시스템의 모든 자원(드라이버, 메모리, CPU 등)에 접근 가능
  - 특권 명령: 운영체제가 실행하는 명령

## 시스템 콜의 종류

- 시스템 콜은 크게 6가지로 분류할 수 있다.

1. 프로세스 제어(Process Control)
   - 끝내기(exit), 중지(abort)
   - 적재(load), 실행(execute)
   - 프로세스 생성(create process) - fork
   - 프로세스 속성 획득 및 설정
   - 시간 대기(wait time)
   - 사건 대기(wait event)
   - 사건을 알림(signal event)
   - 메모리 할당 및 해제
2. 파일 조작(File Manipulation)
   - 파일 생성 / 삭제(create, delete)
   - 열기 / 닫기 / 읽기 / 쓰기(open, close, read, write)
   - 위치 변경(reposition)
   - 파일 속성 획득 및 설정(get file attribute, set file attribute)
3. 장치 관리(Device Manipulation)
   - 하드웨어의 제어와 상태 정보를 얻음(ioctl)
   - 장치를 요구(request device), 장치를 방출(release device)
   - 장치 속성 획득 및 설정
   - 장치의 논리적 부착 및 분리
4. 정보 유지(Information Maintenace)
   - getpid, alarm, sleep
   - 시간과 날짜의 설정과 획득(time)
   - 시스템 데이터의 설정과 획득(date)
   - 프로세스 파일, 장치 속성의 획득 및 설정
5. 통신(Communication)
   - pipe, shm_open, mmap
   - 통신 연결의 생성, 제거
   - 메세지의 송신, 수신
   - 상태 정보 전달
   - 원격 장치의 부착 및 분리
6. 보호(Protection)
   - chmod
   - umask
   - chown
