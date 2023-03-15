### TCP / IP 란?

- TCP / IP는 패킷 통신 방식의 인터넷 프로토콜인 IP와 전송 조절 프로토콜인 TCP로 이루어져 있다.
    - IP는 패킷  전달 여부를 보장하지 않고, 패킷을 보낸 순서와 받는 순서가 다를 수 있다.
    - TCP는 IP 위에서 동작하는 프로토콜로, 데이터 전달을 보증하고 보낸 순서대로 받게 해 준다.
      (IP의 전달 여부, 순서 문제 보완)
- 즉, IP주소 체계를 따르고 ,IP Routing을 이용해 목적지에 도달하며 TCP의 특성을 활용해 송신자와 수신자의 논리적 연결을 생성하고 신뢰성을 유지할 수 있도록 하겠다는 것
- `송신자가 수신자에게 IP주소를 사용하여 데이터를 전달하고 그 데이터가 제대로 갔는지, 너무 빠르지는 않는지, 제대로 받았다고 연락은 오는지에 대한 것.`

### OSI 7계층 중 TCP, IP에 관한 layer

- Transport Layer (4 Layer)
    - 송신자와 수신자의 논리적 연결(Connection)을 담당하는 부분으로, 신뢰성 있는 연결을 유지할 수 있도록 도와준다.
    - 즉 Endpoint(사용자) 간의 연결을 생성하고 데이터를 얼마나 보냈는지, 얼마나 받았는지, 제대로 받았는지 등을 확인한다.
    - 대표적으로 TCP, UDP 가 있다.
- Network Layer (3 Layer)
    - IP(Internet Protocol)이 활용되는 부분으로, 한 Endpoint가 다른 Endpoint로 가고자 할 경우, 경로와 목적지를 찾아줍니다. (Routing)

### IP (Internet Protocol)

- 패킷들의 관계를 이해하지 못하고 그저 목적지를 제대로 찾아가는 것에 중점

### TCP (Transmission Control Protocol)

인터넷 상에서 데이터를 메세지 형태로 보내기 위해 IP와 함께 사용하는 프로토콜

TCP는 연속성보다 신뢰성있는 전송이 중요할 때에 사용하는 프로토콜 (파일 전송 등)

**특징**

- 연결 지향적
    - 3-way handshake를 통해 연결 설정, 4-way handshake를 통해 해제
- 흐름 제어 및 혼잡 제어
    - 흐름 제어 및 혼잡 제어를 하지 않는 UDP 보다 속도가 느리다.
- 높은 신뢰성을 보장
- 전이중, 점대점 방식

<img src="https://user-images.githubusercontent.com/72093196/225388042-c0d25a1b-572f-4c99-b916-217ed28a7bec.png" width=300>

### UDP (User Datagram Protocol)
- 데이터를 데이터그램 단위로 처리하는 프로토콜
- UDP는 신뢰성보다는 연속성이 중요할 때 사용하는 프로토콜 (실시간 서비스 등)
- 비연결형 서비스로 데이터그램 방식을 제공한다.
- 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다.
- UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출
- 신뢰성이 낮다.
- TCP보다 속도가 빠르다.
- 
<img src="https://user-images.githubusercontent.com/72093196/225388596-e01b03f9-dbff-49d8-85e3-4e9b7177254e.png" width=300>