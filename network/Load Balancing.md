### 로드밸런싱

- 서버가 처리해야 할 업무 혹은 요청을 여러 대의 서버로 나누어 처리하는 것
- 방식
    - Scale-up
        - 기존의 서버 성능을 확장
    - Scale-out
        - 서버를 증설
        - 로드 밸런싱 필요
- 기법
    - 라운드로빈 방식
        - 서버에 들어온 요청을 **순서대로 돌아가며 배정**하는 방식
        - 클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합
    - 가중 라운드로빈 방식
        - 각각의 서버마다 가중치를 매기고 **가중치가 높은 서버에 클라이언트 요청을 우선적**으로 배분
        - 주로 서버의 트래픽 처리 능력이 상이한 경우 사용되는 부하 분산 방식이다.
    - IP 해시 방식
        - **클라이언트의** **IP 주소를 특정 서버로 매핑**하여 요청을 처리하는 방식
        - 사용자의 IP를 해싱해 로드를 분배하기 때문에 **사용자가 항상 동일한 서버로 연결되는 것을 보장**한다
    - 최소 연결 방식
        - 요청이 들어온 시점에 **가장 적은 연결상태를 보이는 서버에 우선적**으로 트래픽을 분배
        - 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식
    - 최소 응답 시간 방식
        - 서버의 현재 **연결 상태와 응답 시간을 모두 고려**하여 트래픽을 배분
        - 가장 적은 연결 상태와 가장 짧은 응답 시간을 보이는 서버에 우선적으로 로드를 배분하는 방식

- L4 로드밸런서, L로드밸런서
    - **L4 로드밸런서**
        - 특징
            - Layer4 (Transport Layer)에서 처리
            - TCP/UDP 포트 정보를 바탕으로 함
        - 장점
            - 데이터 안을 들여다보지 않고 패킷 레벨에서만 로드를 분산하기 때문에 속도가 빠르고 효율이 높음
            - 데이터의 내용을 복호화할 필요가 없기 때문에 안전함
            - L7 로드밸런서보다 가격이 저렴
        - 단점
            - 패킷의 내용을 살펴볼 수 없기 때문에 섬세한 라우팅이 불가능 함
            - 사용자의 IP가 수시로 바뀌는 경우라면 연속적인 서비스를 제공하기 어려움
    - **L7 로드밸런서**
        - 특징
            - Layer7 (Application Layer)에서 처리
            - TCP/UDP 정보는 물론, HTTP의 URI, FTP의 파일명, 쿠키 정보 등을 바탕으로 함
        - 장점
            - 상위 계층에서 로드를 분산하기 때문에 훨씬 더 섬세한 라우팅이 가능
            - 캐싱 기능을 제공
            - 비정상적인 트래픽을 사전에 필터링할 수 있어 서비스 안전성이 높음
        - 단점
            - 패킷의 내용을 복호화해야 하기에 더 높은 비용을 지불해야 함
            - 클라이언트가 로드밸런서와 인증서를 공유해야하기 때문에 공격자가 로드밸런서를 통해서 클라이언트의 데이터에 접근할 보안 상의 위험성이 존재