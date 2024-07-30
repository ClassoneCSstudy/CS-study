## 동기화 & 비동기화와 메모리 관리 

1. 동기화와 비동기화의 개념
2. 상호 배제 (Mutex, Semaphore)  교착 상태 (Deadlock)

### 동기화, 비동기화

1. 동기화(Synchronous)

* 작업이 순차적으로 실행(프로세스의 비선점 스케줄링과 유사)
* 다음 작업은 현재 작업이 끝나고 시작
* Javascript의 일반적인 함수들

2. 비동기화(Asynchronous)

* 작업이 병렬적으로 실행(프로세스의 선점 스케줄링과 유사)
* 다음 작업은 현재 작업과 관계없이 시작 가능
* Javascript의 callback, promise, async등으로 이용 

### 상호배제, 교착상태

1. 상호배제(Mutual Exclusion, Mutex)

* 여러 스레드는 동시에 공유 자원에 접근 불가
* 교착상태의 필요조건 중 하나
* 주로 데이터 경합 등을 방지하기 위해 이용

2. 교착상태(DeadLock)

* 두 개 이상의 스레드 or 프로세스가 상대의 자원을 기다리며 무한히 대기
* 4개의 조건
  1. 상호 배제(Mutex)
  2. 점유 대기(Hold & Wait)
  3. 비선점(No Preemption)
  4. 환형 대기(Circular Wait)