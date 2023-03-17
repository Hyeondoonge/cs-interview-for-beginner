## TCP
TCP는 연속성보다 신뢰성있는 전송이 중요할 때에 사용하는 프로토콜 (파일 전송 등)

**특징**

- 연결 지향적
  - 3-way handshake를 통해 연결 설정, 4-way handshake를 통해 해제
- 흐름 제어 및 혼잡 제어
  - 흐름 제어 및 혼잡 제어를 하지 않는 UDP 보다 속도가 느리다.
- 높은 신뢰성을 보장
- 전이중, 점대점 방식

<img src="https://user-images.githubusercontent.com/72093196/225388042-c0d25a1b-572f-4c99-b916-217ed28a7bec.png" width=300>


### **흐름 제어**

- 송신 측과 수신 측의 데이터 처리 속도가 다를 수 있음
    - 송신 측이 빠를 때 수신 측 버퍼가 넘치는 오버플로우 문제 발생
- 이러한 문제를 줄이기 위해 윈도우 크키로 송신 측의 데이터 전송량을 조절
- stop and wait
    - 상대방에게 데이터를 보낸 후 잘 받았다는 응답이 올 때까지 기다리는 방식
- sliding window
    - 송신 측이 수신 측에서 받은 윈도우 크기를 참고해서 데이터의 흐름을 제어하는 방식

### 오류 제어

- TCP는 통신 중에 오류가 발생하면 해당 데이터를 재전송 한다.
- stop and wait 방식
    - ACK를 받고 나서 다음 데이터를 보내는 방식
- Go Back N
    - 연속으로 데이터를 보내다가 오류가 발생한 지점부터 재전송
    - 성공적으로 전송된 데이터까지 재전송하기 때문에 비효율적
- Selective Repeat
    - 오류가 발생한 데이터만 재전송

### 혼잡 제어

- 네트워크 내의 패킷 수가 과도하게 증가하는 현상을 방지하고 제거하기 위한 기능
- AIMD (Additive Increase / Multicative Decrease)
    - 패킷을 보내고 문제 없이 도착하면 윈도우 크기를 1씩 증가시키며 전송
      만약, 전송에 실패하면 윈도우의 크기를 반으로 줄인다.
    - 윈도우 크기를 너무 조금씩 늘리기 때문에 네트워크 모든 대역을 활용하여 제대로된 속도로 통신하기까지 시간이 오래걸리는 단점이 있다.
    - `window size : 1 → 2 → 3 → 4 → 5 → … → 32 → 혼잡 발생 → 16 → 17 → …`
- Slow Start (느린 시작)
    - 윈도우 크기를 1, 2, 4, 8, … 과 같이 지수적으로 증가시키다가 혼잡이 감지되면 윈도우 크기를 1로 줄이는 방식
    - `window size : 1 → 2 → 4 → 8 → 16 → 32 → 혼잡 발생 → 1 → 2 → 4 → …`
- Fast Recovery (빠른 회복)
    - 혼잡한 상태가 되면 윈도우 크기를 1로 줄이지 않고 반으로 줄이고 선형 증가시키는 방법
      한 번 혼잡 상황을 겪고 나면 이후 AIMD 방식으로 동자
    - `window size : 1 → 2 → 3 → … → 32 → 혼잡 발생 → 16 → 17 → 18 → …`
- TCP Tahoe

  <img src="https://user-images.githubusercontent.com/72093196/225388393-fe729b52-f148-4853-9a54-d9a4f932c89d.png" width=300>

    - 처음 Slow Start를 사용하여 자신의 윈도우 크기를 지수적으로 빠르게 증가시키다가 ssthresh(Slow Start Thresh)를 만난 이후부터 AIMD를 사용하여 선형적으로 윈도우 크기를 증가시킨다.
    - ACK Duplicated 이나 Timeout이 발생하면 네트워크에 혼잡이 발생했다고 판단하고, ssthresh와 자신의 윈도우 크기를 수정한다.
    - 혼잡 상황이 발생한 지점을 기억하고 그 지점이 가까워지지 않도록 합리적으로 조절 가능
      → sshthresh 값을 조절
    - 단점 : 초반의 Slow Start 구간에 윈도우 크기를 늘릴 때 오래 걸린고 혼잡 상황 발생 시 다시 윈도우 크기를 1에서부터 시작해야 한다는 단점이 있다.
- TCP Reno

  <img src="https://user-images.githubusercontent.com/72093196/225388483-82c3b2ea-618e-4049-ba48-97d4c7ac8144.png" width=300>

    - Tahoe와는 다르게 3 ACK Duplicated와 Time out 혼잡 상황을 구분한다.
    - 3 ACK Duplicated → 윈도우 크기를 반으로 줄이고 sshtresh를 줄어든 윈도우 값으로 설정
    - Time out → 윈도우 크기를 1로 줄이고 Slow Start 진행 , sshtresh는 변하지 않는다.