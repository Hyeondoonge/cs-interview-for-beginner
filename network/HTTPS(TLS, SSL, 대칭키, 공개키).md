## HTTPS란?

⇒ **Hypertext Protocol Secure의 약자로 인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약**

**HTTPS** 는 HTTP가 보안에 취약한 것을 보완하는 것으로써 **‘SSL 인증서’** 사용

클라이언트와 서버간의 HTTPS 통신에 사용되는 전자 문서로 클라이언트는 서버에 접속한 직후 서버로부터 이 인증서를 내려받아 검증합니다. 서버를 신뢰할 수 있는지 판단한 후 통신 

인증서에는 서버의 공개키가 담기는데 이 인증서는 CA의 개인키로 암호화

브라우저 모든 CA들의 공개키 가지고 있어서 인증서를 복호화하고 내용을 볼 수 있음

정리해보자면,

1. **인증서에 들어있는 서버의 공개키는 공개키 방식**

2. **서버/클라이언트 양측 모두 pre master secret를 가지고 이 값은 master secret으로 변환되어 최종적으로 session key가 만들어짐.**
 
    **서버와 클라이언트는 실제 데이터 전송 시 이 session key를 사용해서 암호화/복호화를 함. (대칭키)**

### 대칭키

- 하나의 공통된 키를 사용하여 암/복호화를 진행
- 키의 길이가 짧기 때문에 암/복호화 속도가 빠름
- 대칭키의 전달과정에서 키 노출 위험이 있음

### 공개키 (비대칭키)

- 두 개의 키를 사용하여 암/복호화를 진행
- 공개키 ↔ 개인키
    - 공개키로 암호화 후 개인키로 복호화
    - 개인키로 암호화 후 공개키로 복호화 ( 암호화 목적이라기 보단, 검증의 목적 )
- 키의 길이가 길어 암/복호화 속도가 느림

### HTTPS의 통신 흐름

1. **서버**에서 서버의 공개키와 사이트 정보를 **인증 기관(CA)에 전달**
    
    ***CA란?*** 
     : Certificate Authority로, 공개키를 저장해주는 신뢰성이 검증된 민간기업
    
2. **인증 기관**에서 서버의 공개키와 사이트 정보를 **인증기관의 개인키로 암호화(서명) 한 인증서**를 **서버에 전달**
3. **클라이언트**가 **서버**에 https가 아닌 요청시 서버는 클라이언트에 **인증서를 전달**
4. **클라이언트**는 인증서를 복호화해서 **서버의 공개키를 획득**
    
    (**브라우저에 인증기관의 공개키가 저장 돼있음**)
    
5. **클라이언트**는 임의의 난수를 **대칭키로 설정**하고 **서버의 공개키로 암호화**해서 **서버로 전달**
6. **서버**는 서버의 개인키로 복호화해서 **대칭키를 획득**
7. 대칭키를 이용해서 클라이언트,서버간 통신 (SSL 통신)

### HTTPS가 공개키 암호화 방식만 사용하지 않고 대칭키 암호화 방식도 같이 사용하는 이유

⇒ 공개키 암호화 방식은 키의 길이가 길어 암/복호화 속도가 느려 암호화 연산 비용이 크기 때문에 최종적으로 암호화 연산 비용이 적은 대칭키를 사용해서 통신

### SSL/TLS

- TLS는 SSL의 개선된 버전
- HTTPS에서 사용
- SSL/TLS handshake 과정

![image](https://user-images.githubusercontent.com/77667212/226186177-a76ca44b-e579-4c2e-a23b-ae9be9c0b424.png)


1. 클라이언트가 서버에 “Client Hello” 를 보냄
    - 클라이언트 측에서 생성한 랜덤 데이터
    - 클라이언트가 지원하는 암호화 방식들
    - 세션 아이디
2. 서버는 클라이언트에 “Server Hello”를 보냄
    - 서버 측에서 생성한 랜덤 데이터
    - 서버가 선택한 클라이언트의 암호화 방식
    - 인증서
3. 클라이언트는 인증서를 검증함 ( 클라이언트에 내장된 CA 리스트를 확인 )
    - 클라이언트에서 생성한 랜덤 데이터와 서버에서 생성한 랜덤 데이터를 조합해서 ‘pre master secret’ 라는 값(추후에 대칭키의 토대)를 생성
    - 인증서 안에 있는 서버의 공개키를 사용해서  ‘pre master secret’를 암호화 한 뒤 서버에 전송
4. 서버는 암호화 된 ‘pre master secret’ 라는 값를 개인키를 이용해 복호화 
    - ‘pre master secret’ 값 → ‘master secret’ 값 → ‘session key’ 생성 (대칭키)
5. 클라이언트는 handshake 과정이 완료되었다는 ”finished” 메시지를 서버에 보냄
    - 지금까지 보낸 교환 내역들을 해싱 후 그 값을 대칭키로 암호화하여 같이 담아 보내줌
6. 서버도 동일하게 교환 내용들을 해싱한 뒤 클라이언트에서 보내준 값과 일치하는 지 확인하고 일치하면 서버도 마찬가지로 ”finished” 메시지를 이번에 만든 대칭키로 암호화하여 보냄
7. 클라이언트는 해당 메시지를 대칭키로 복호화하여 서로 통신이 가능한 신뢰받은 사용자란 걸 인지하고, 앞으로 클라이언트와 서버는 해당 대칭키로 데이터를 주고받음

### Reference

[https://www.youtube.com/watch?v=lw0qdSqu2eg](https://www.youtube.com/watch?v=lw0qdSqu2eg)

[https://gyoogle.dev/blog/computer-science/network/TLS HandShake.html](https://gyoogle.dev/blog/computer-science/network/TLS%20HandShake.html)
