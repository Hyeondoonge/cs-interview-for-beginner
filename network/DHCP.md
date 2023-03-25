## DHCP란?

⇒ DHCP(Dynamic Host Configuration Protocol)은 호스트의 IP 주소와 각종 TCP/IP 프로토콜의 기본 설정을 클라이언트에게 자동적으로 제공해주는 프로토콜 

### DHCP를 사용하는 이유

1. IP 주소 관리 편의성 : DHCP 사용시 IP 주소 할당과 관리가 중앙 서버에서 이루어지기 때문에, 네트워크 관리자는 각 호스트에 대해 수동으로 IP 지정할 필요가 없어 IP 주소 할당과 관리에 대한 효율성과 정확성을 높일 수 있음
2. 유연한 IP 주소 할당 : 호스트의 수요나 변경사항에 따라 IP 주소, 서브넷 마스크, 기본 게이트웨이, DNS 서버 등의 정보를 클라이언트에게 자동으로 할당해 호스트의 이동성을 높이고 유연하게 대응 가능
3. IP 충돌 방지 : DHCP를 사용하면 IP 주소가 중앙 서버에서 할당되므로 IP 충돌 문제를 예방하여 네트워크의 안정성과 신뢰성을 높임
4. 호스트 이동성 : 호스트가 네트워크에서 이동하더라도 IP 주소 할당이 자동으로 이루어지므로, 호스트의 이동성을 높여 네트워크 사용성 향상
5. 보안 : DHCP 서버에서 IP 주소를 할당하지 않은 호스트는 네트워크에 접속할 수 없어 보안에 대한 신뢰성을 높임 

### DHCP 장점

PC의 수가 많거나 PC 자체 변동사항이 많은 경우 IP 설정이 자동으로 되기 때문에 효율적으로 사용 가능하고, IP를 자동으로 할당해주기 때문에 IP 충돌을 막을 수 있음

### DHCP 단점

DHCP 서버에 의존되기 때문에 서버가 다운되면 IP 할당이 제대로 이루어지지 않음 

(의존성이 크다)

### DHCP 구성

1) DHCP 서버 : DHCP서버는 네트워크 인터페이스를 위해서 IP주소를 가지고 있는 서버에서 실행되는 프로그램으로 일정한 범위의 IP주소를 다른 클라이언트에게 할당하여 자동으로 설정하게 해주는 역할을 합니다. DHCP서버는 클라이언트에게 할당된 IP주소를 변경없이 유지해 줄 수 있습니다.

( 클라이언트에게 IP 할당 요청이 들어오면 IP를 부여해주고 할당 가능한 IP들을 관리해줌 )

2) DHCP 클라이언트 : 클라이언트들은 시스템이 시작하면 DHCP서버에 자신의 시스템을 위한 IP주소를 요청하고, DHCP 서버로부터 IP주소를 부여받으면 TCP/IP 설정은 초기화되고 다른 호스트와 TCP/IP를 사용해서 통신을 할 수 있게 됩니다.

( 서버에게 IP를 할당받으면 TCP/IP 통신을 할 수 있음 )

### DHCP 동작원리

![image](https://user-images.githubusercontent.com/77667212/227723354-8cdf19f0-e004-4e9f-b175-bcd27eb2b71b.png)


1. DHCP Discover
    - 먼저 장치가 네트워크에 연결되면 브로드캐스트 DHCP Discover 메시지를 보내 사용 가능한 DHCP 서버를 검색
2. DHCP OFFER
    - DHCP 서버는 Discover 메시지를 수신하고, 사용 가능한 IP 주소 및 기타 네트워크 설정을 포함한 DHCP OFFER 메시지로 응답 
3. DHCP Request
    - 장치는 제안 메시지를 수신하고 제안된 IP 주소 중 하나를 선택하고 DHCP 서버에 선택한 IP 주소를 할당받기 위해 DHCP Request 메시지를 보냄
4. DHCP Ack
    - DHCP 서버는 해당 요청 메시지를 수신하고 IP주소 및 기타 설정들의 할당을 확인하는 DHCP 승인 메시지로 응답
5. DHCP는 할당된 IP주소, 서브넷 마스크, 게이트웨이 및 DNS 서버를 포함하여 네트워크 설정을 구성 

Reference

[https://jwprogramming.tistory.com/35](https://jwprogramming.tistory.com/35)

[https://www.cisco.com/c/ko_kr/support/docs/switches/catalyst-9300-series-switches/217366-configure-dhcp-in-ios-xe-evpn-vxlan.html](https://www.cisco.com/c/ko_kr/support/docs/switches/catalyst-9300-series-switches/217366-configure-dhcp-in-ios-xe-evpn-vxlan.html)
