## DNS 란?

Domain Name System

도메인 네임 시스템으로, 사람이 읽을 수 있는 도메인 이름을 IP 주소로 변환하는 시스템

상위 기관과 하위 기관과 같은 **계층 구조**를 가지는 **분산 데이터베이스 구조**를 가진다.

## DNS서버에 IP를 요청하고 응답받는 과정

![11](https://user-images.githubusercontent.com/72093196/227731104-02e83a7a-344a-4bf0-8918-7ab0aa3611f2.png)

1. 브라우저는 브라우저 캐시에 IP가 있는지 확인
2. 컴퓨터에 저장되어 있는 host파일과 캐시 확인
3. DNS 서버에 요청
4. DNS 서버 캐시 확인
5. Root NS에 IP 주소 요청 .`com NS 주소` 응답
6. TLD NS에 IP 주소 요청, `sub domain NS 주소` 응답
7. Sub domain NS에 IP주소 요청, `IP 주소` 응답
8. DNS 서버에서 IP 응답

![22](https://user-images.githubusercontent.com/72093196/227731111-9d55c2e8-460c-43e7-9212-c6589842f6c5.png)

### DNS는 서버를 계층적으로 관리해 서버를 분리

- 트래픽과 데이터를 분산

도메인을 계층적으로 관리

![33](https://user-images.githubusercontent.com/72093196/227731117-6639de14-af8c-4ec0-9aa8-73b8106773a2.png)

### 참고자료
[[10분 테코톡] 엘리의 DNS](https://www.youtube.com/watch?v=sDXcLyrn6gU)