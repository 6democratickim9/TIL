# 스케줄링 알고리즘

## 프로세스 상태와 스케줄링



### 멀티 프로그래밍과 wait

- 멀티 프로그래밍: **CPU 활동도를 극대화** 하는 스케쥴링 알고리즘
- Wait: 저장매체로부터 **파일 읽기를 기다리는 시간**으로 가정

### 프로세스 상태

- running state: 현재 CPU에서 **실행** 상태
- ready state: CPU에서 **실행가능** 상태
- block state: 특정 이벤트 **발생 대기** 상태

![image-20211126233220824](C:\Users\MIN\TIL\zero-base\1126_OS_SchedulingAlgorithm.assets\image-20211126233220824.png)



### 프로세스 상태간 관계

- ![image-20211126233433985](C:\Users\MIN\TIL\zero-base\1126_OS_SchedulingAlgorithm.assets\image-20211126233433985.png)

![image-20211126233551423](C:\Users\MIN\TIL\zero-base\1126_OS_SchedulingAlgorithm.assets\image-20211126233551423.png)