# 시스템 콜

운영체제의 커널이 제공하는 서비스에 대해, 응용 프로그램의 요청에 따라 커널에 접근하기 위한 인터페이스.

유저 프로그램이 운영체제의 서비스를 받기 위해 커널 함수를 호출할 때 쓴다!

유저 프로그램이 I/O 요청으로 trap을 발동하면 올바른 I/O 요청인지 확인한 후 유저 모드가 시스템 콜을 통해 커널 모드로 변환되어 실행.

![Untitled](https://file.notion.so/f/f/7475e982-b1c2-48f4-b4e6-407994dfdc27/97d88d7e-1b7b-4243-b050-87d91e18dbf6/Untitled.png?id=39e48933-c7d9-4b1f-b192-ad42d05aa193&table=block&spaceId=7475e982-b1c2-48f4-b4e6-407994dfdc27&expirationTimestamp=1721865600000&signature=sk2VVAq0z-rgURd_r8S5YkUll_sVxiUyR8qj_8Hc1sQ&downloadName=Untitled.png)

### 운영체제 구조

![Untitled](https://file.notion.so/f/f/7475e982-b1c2-48f4-b4e6-407994dfdc27/9829b774-687a-42d0-a5ee-53e78d3b6485/Untitled.png?id=f8587b4f-40a2-418b-b000-42b2897e7b4f&table=block&spaceId=7475e982-b1c2-48f4-b4e6-407994dfdc27&expirationTimestamp=1721865600000&signature=c0NhrF2loV_7F9M9YaBYinj3_1LYn7NMm3_y4whjw4I&downloadName=Untitled.png)

- 커널
  - 운영체제 중 항상 필요한 부분만을 전원이 켜짐과 동시에 메모리에 올려놓고, 그렇지 않은 부분은 필요할 때 메모리에 올려서 사용하게 된다. 이때 메모리에 상주하는 운영체제의 부분
- 유저모드
  - 유저가 접근할 수 있는 영역을 제한적으로 두며 컴퓨터 자원에 함부로 침범하지 못하는 모드
- 커널모드
  - 모든 컴퓨터 자원에 접근할 수 있는 모드

### 시스템 콜 종류

정말정말 하나도 안중요하다고 생각하지만…이게 진짜진짜 많고…. 나올리가 없고….일단 정리는 한다만….흠…. 대분류만 알아도 될 듯!

- 프로세스 관리 (Process Management)
  - fork(): 새로운 프로세스를 생성합니다.
  - exec(): 실행 중인 프로세스를 다른 프로그램으로 교체합니다.
  - wait(): 자식 프로세스가 종료될 때까지 부모 프로세스를 대기 상태로 둡니다.
  - exit(): 프로세스를 종료합니다.
  - getpid(): 현재 프로세스의 프로세스 ID를 반환합니다.
- 파일 관리 (File Management)
  - open(): 파일을 엽니다.
  - read(): 파일에서 데이터를 읽습니다.
  - write(): 파일에 데이터를 씁니다.
  - close(): 파일을 닫습니다.
  - lseek(): 파일의 읽기/쓰기 위치를 변경합니다.
  - stat(): 파일의 상태 정보를 얻습니다.
- 장치 관리 (Device Management)
  - ioctl(): 장치의 입출력 제어 작업을 수행합니다.
  - read(): 장치에서 데이터를 읽습니다.
  - write(): 장치에 데이터를 씁니다.
- 정보 유지 (Information Maintenance)
  - gettimeofday(): 현재 시간을 얻습니다.
  - settimeofday(): 현재 시간을 설정합니다.
  - uname(): 시스템 정보를 얻습니다.
  - getrusage(): 자원 사용 정보를 얻습니다.
- 통신 (Communication)
  - pipe(): 파이프를 생성합니다.
  - shmget(): 공유 메모리를 할당합니다.
  - shmat(): 공유 메모리를 프로세스 주소 공간에 연결합니다.
  - shmdt(): 공유 메모리를 분리합니다.
  - msgget(): 메시지 큐를 생성하거나 접근합니다.
  - msgsnd(): 메시지 큐에 메시지를 보냅니다.
  - msgrcv(): 메시지 큐에서 메시지를 받습니다.
- 네트워크 관리 (Network Management)
  - socket(): 소켓을 생성합니다.
  - bind(): 소켓에 주소를 바인딩합니다.
  - listen(): 소켓을 연결 대기 상태로 만듭니다.
  - accept(): 연결을 수락합니다.
  - connect(): 원격 호스트에 연결합니다.
  - send(): 소켓을 통해 데이터를 보냅니다.
  - recv(): 소켓을 통해 데이터를 받습니다.

### 시스템 콜 과정

- 프로세스는 사용자 모드로 실행되다가 커널에 처리를 요청할 때 시스템 콜을 호출합니다.
- CPU에서는 인터럽트 이벤트가 발생하고 CPU가 사용자 모드에서 커널 모드로 변경되며 요청한 내용을 처리하기 위해 커널이 동작합니다.
- 요청한 내용 처리가 끝내면 커널 내의 시스템 콜 처리가 종료되고 다시 사용자 모드로 돌아가 프로세스의 동작을 계속 진행합니다.

# **CPU Scheduling**

CPU가 다음에 수행할 프로세스의 실행 순서를 정하는 것

CPU scheduling 결정은 프로세스가 다음과 같은 경우일 때

1. running에서 waiting으로 전환
2. running에서 ready로 전환 : 시간 다 써서 강제적으로 끌려 내려옴 (interrupt)
3. waiting에서 ready로 전환 : 강제로 running에 있은 애 끌려 나옴 (completion of I/O)
4. terminates(종료)

→ 1, 4일 때는 비선점(강제권 없음). 2, 3은 선점

### 스케줄링 종류

- 비선점
  CPU가 현재 실행중인 프로세스가 완료될 때까지 다른 프로세스들은 대기하는 스케줄링

  현재 실행중인 프로세스가 종료되거나 입/출력을 위하여 waiting으로 들어가는 경우에만!

  - FCFS (First Come First Served)
    - 큐에 도착한 순서대로 CPU 할당
    - 실행시간이 짧은 게 뒤로 가면 평균 대기시간이 길어짐 → CPU의 효율화를 떨어뜨림(호송 효과)
  - SJF (Shortest Job First)
    - 수행시간이 가장 짧다고 판단되는 작업을 먼저 수행
    - FCFS보다 평균 대기 시간 감소, 짧은 작업에 유리
    - 다음 CPU 요청 길이를 알 수 없음에 어려움
  - HRM (Highest Response-ratio Next)
    - 우선순위를 계산하여 점유 불평등을 보완한 방법(SJF 단점 보완)
    - 우선순위 = (대기시간 + 실행시간) / 실행시간

- 선점
  CPU가 현재 프로세스를 실행중일 때 스케줄러에 의해 현재 프로세스의 CPU 제어권을 다른 프로세스한테 넘기는 스케줄링

  실행중인 프로세스가 다른 프로세스에게 CPU 제어권을 선점당하면 running에서 ready 상태로 변하고 입/출력을 위하여 대기 중인 상태에서 다른 프로세스가 CPU를 선점하면 ready 상태로 전환

  - Priority
    - 정적/동적으로 우선순위를 부여하여 우선순위가 높은 순서대로 처리
    - 우선순위가 낮은 프로세스는 무한정 기다리는 starvation이 생길 수 있음
  - Round Robin
    - ready queue는 circular queue로 동작하며, CPU 스케줄러는 ready queue를 돌면서 한번에 한 프로세스에게 한번의 time slice동안 CPU 할당.
    - 프로세스의 burst가 time slice보다 작은경우 실행이 끝나면 자발적으로 cpu 방출
    - 프로세스의 burst가 time slice보다 큰 경우 context switch가 일어나고 실행하던 프로세스는 ready queue의 꼬리 (tail)에 넣어짐
    - RR은 최적의 결과를 가져오지 않는다.
    - 만약 time slice가,
      - 크다면 FIFO와 같음 = 즉, FCFS와 같아짐
      - 작다면 매우 많은 context switch 발생. → overhead 높음
