# 동시성 문제와 해결 방법

동시성(`Concurrency`) 동시에 여러 작업이 실행되는 컴퓨터 시스템의 특성을 가리킵니다. 이는 멀티쓰레드, 비동기 프로그래밍, 병렬 컴퓨팅 등 다양한 형태로 구현될 수 있습니다. 동시성은 성능 향상과 응답성 향상을 위해 중요하지만, 잘못 다룰 경우 예기치 않은 문제들을 발생시킬 수 있습니다.

## 동시성 문제

##### 경쟁 조건(Race Condition)

경쟁 조건은 여러 프로세스 또는 스레드가 공유된 자원에 접근할 때 발생할 수 있는 문제입니다. 두 개 이상의 프로세스 또는 스레드가 동시에 공유된 자원을 변경하려고 할 때 발생합니다. 이때 어떤 프로세스 또는 스레드가 먼저 자원을 변경할지 예측할 수 없기 때문에 잘못된 결과가 발생할 수 있습니다.

##### 교착 상태(Deadlock)

교착 상태는 둘 이상의 프로세스나 스레드가 서로의 작업이 끝나기를 기다리며 무한히 대기하는 상태를 가리킵니다. 이는 각각의 프로세스 또는 스레드가 다른 프로세스 또는 스레드가 점유한 자원을 기다리는 동안 발생합니다.

## 해결 방법

##### 상호 배제(Mutual Exclusion)

상호 배제는 공유된 자원에 대한 동시 접근을 막는 기법입니다. 한 시점에 오직 하나의 프로세스 또는 스레드만이 공유된 자원을 사용할 수 있도록 합니다. 이를 통해 경쟁 조건을 방지할 수 있습니다.

##### 동기화(Synchronization)

동기화는 여러 프로세스나 스레드 간의 작업을 조율하여 원활한 실행을 보장하는 기법입니다. 상호 배제를 통해 공유된 자원에 대한 접근을 조절하고, 교착 상태를 방지합니다.

#### 예제 코드

```py
import threading

# 공유 자원
shared_resource = 0

# Lock 객체 생성
lock = threading.Lock()

# 공유 자원을 변경하는 함수
def modify_shared_resource():
    global shared_resource
    # Lock을 획득
    lock.acquire()
    try:
        # 공유 자원 변경
        shared_resource += 1
    finally:
        # Lock 해제
        lock.release()

# 여러 스레드 생성 및 실행
threads = []
for _ in range(10):
    t = threading.Thread(target=modify_shared_resource)
    threads.append(t)
    t.start()

# 모든 스레드 종료 대기
for t in threads:
    t.join()

# 결과 출력
print("최종 공유 자원 값:", shared_resource)
```

- 10개의 스레드가 동시에 `modify_shared_resource` 함수를 호출하여 `shared_resource`를 증가시키는 예제입니다.
- Lock 객체를 사용하여 상호 배제를 구현했습니다. 이를 통해 여러 스레드가 동시에 공유 자원에 접근하더라도 안전하게 동작합니다.
