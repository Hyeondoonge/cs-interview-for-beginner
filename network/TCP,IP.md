### TCP / IP 란?

인터넷에서 컴퓨터들이 서로 정보를 주고 받는데 쓰이는 프로토콜 집합

### 4계층

- Application Layer
  - 특정 서비스를 제공하기 위해 애플리케이션 끼리 정보를 주고 받을 수 있음
  - **FTP, HTTP**, SSH, Telnet, DNS, SMTP 등
- Transport Layer
  - 송신된 데이터를 수신측 애플리케이션에 확실히 전달하게 함
  - PORT 번호를 사용해서 애플리케이션을 찾아주는 역할
  - **TCP, UDP**, RTP, RTCP 등
- Internet Layer
  - 수신측 까지 데이터를 전달하기 위해 사용
  - IP 주소 활용
  - **IP**, ARP 등
- Network Access Layer
  - 네트워크에 직접 연결된 기기 간 전송을 할 수 있도록 함
  - MAC 주소 활용
  - Eternet, PPP 등