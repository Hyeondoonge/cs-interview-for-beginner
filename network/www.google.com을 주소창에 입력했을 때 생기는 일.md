1. 사용자가 브라우저에 **[http://www.google.com](http://www.google.xn--com-of0o/)** 을 입력합니다.
2. 브라우저는 로컬 DNS 캐시를 검색하여 입력된 도메인명인 **[www.google.com](http://www.google.xn--com-568n/)** 에 해당하는 IP 주소를 찾습니다. 만약 캐시에서 찾을 수 없다면, 브라우저는 인터넷에 연결된 DNS 서버에 **[www.google.com](http://www.google.com/)** 도메인명에 해당하는 IP 주소를 요청합니다.
3. DNS 서버는 **[www.google.com](http://www.google.com/)** 도메인명에 해당하는 IP 주소를 응답합니다.
    - ISP(ex. SK 브로드밴드, KT...)를 통해 DNS서버가 호스팅하고 있는 서버의 IP주소를 찾기 위해DNS query를 전달합니다.
    - DNS query는현재 DNS서버에 원하는 IP주소가 존재하지 않으면다른 DNS 서버를 방문하는 과정을원하는 IP주소를 찾을 때까지 반복합니다.
    - DNS 쿼리는 응용 계층에서 실행되고, DNS 리졸버가 IP 주소를 반환 받은 후, 반환 된 IP 주소는 전송 계층에서 처리됩니다.
    - iterative 쿼리 : local DNS server가 계속해서 root DNS server, TLD DNS server등 여러 서버와 최종 IP 주소를 받을 때까지 요청 &응답을 계속해서 local name server가 반복하는 방법
    - recursive 쿼리 : local DNS server에서 root DNS server에 query를 보내고 root DNS server에서 계층적으로 다른 서버에 요청해서 최종 IP를 찾는 방법
4. 브라우저는 웹 서버와 TCP 연결을 시도합니다. 이때, TCP/IP 3-way handshake 과정을 거칩니다.
5. TCP 연결이 성공하면 웹브라우저가 웹서버에게 IP주소를 이용하여 html 문서를 요청
    - 브라우저는 HTTP GET 요청을 서버에 보냅니다.
6. 웹 서버는 요청에 대한 응답으로 HTML 문서를 생성하고, 클라이언트에게 응답합니다.
    - 1XX : 정보 응답
    - 2XX : 요청 성공
    - 3XX : 리다이렉션 메시지
    - 4XX : 클라이언트 오류
    - 5XX : 서버 오류
7. 브라우저는 응답받은 HTML 문서를 파싱하여 DOM 트리를 생성하고, CSS 파일과 같은 필요한 리소스를 요청합니다. 이때 필요한 리소스가 캐시에 저장되어 있으면 서버에 요청하지 않고 캐시에서 로드합니다.
    - DOM 트리는 HTML 문서를 구조화하여, 브라우저에서 웹 페이지의 요소들을 처리하고 조작할 수 있도록 만들어주는 것
8. 브라우저는 웹 페이지를 렌더링합니다. 이 과정에서 DOM 트리와 CSSOM 트리를 조합하여 렌더링 트리를 생성합니다.
9. 브라우저는 렌더링 트리를 사용하여 웹 페이지를 화면에 그리고, 사용자에게 보여줍니다.
