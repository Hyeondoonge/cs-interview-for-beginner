## PCB

![PCB](https://zitoc.com/wp-content/uploads/2019/02/process-control-block-PCB.png)

프로세스를 관리하기 위해서 운영체제가 프로세스마다 할당한 데이터.

PID: 프로세스 식별자

Process state: 프로세스 상태

CPU Registers: PC, IR, AC 등의 레지스터 값

CPU 스케쥴링 정보: 우선순위, 최종 실행 시각, CPU 점유시간 등

메모리 관리 정보: 주소 공간 정보 등

## Context Switching

![Context Switching](https://t1.daumcdn.net/cfile/tistory/994590345BB1B4DB2F)

멀티 태스킹 환경에서, 진행 중이던 작업을 해당 작업의 PCB에 저장하고
다음 작업의 PCB를 로드하는 현상을 의미.

### Context Switching 발생 상황

1. Timer에 의한 인터럽트 발생
2. I/O 요청 System call에 의한 인터럽트 발생
