## OSI 7계층이란?

⇒ 네트워크에서 통신이 일어나는 과정을 7단계로 정의한 국제 통신 표준 규약 

![image](https://user-images.githubusercontent.com/77667212/224915791-1a2d6dcf-57c0-4074-8128-60c4a49babd0.png)

Application (응용) 계층 : 사용자가 네트워크에 접근할 수 있도록 서비스 제공

- 프로토콜을 이용해서 서비스 제공
- HTTP (Hypertext Transfer Protocol)
- FTP (File Transfer Protocol)
- SMTP (Simple Mail Transfer Protocol)
- DNS (Domain Name System)

Presentation (표현) 계층 : 세션 계층 간의 인터페이스를 일관성 있게 제공

- 알아 볼 수 있도록 다른 형식 간의 데이터 변환 ( 응용 계층 → 세션 계층, 세션 계층 → 응용 계층 )
- 코드 변화, 데이터 암호화, 데이터 압축, 정보 형식 변환 등

Session (세션) 계층 : 송수신간의 연결을 유지 및 설정

- 송수신간의 대화 제어를 담당

Transport (전송) 계층 : 두 host 시스템으로부터 발생하는 데이터 흐름 제공 ( 게이트 웨어 )

- 데이터가 실제로 전송되는 구간

Network (네트워크) 계층 : 패킷을 네트워크 IP를 통해 데이터 전달 ( 라우팅  )

- 네트워크 연결을 관리
- 데이터 교환의 중계
- 라우팅 : 최적의 경로 찾아줌

Data Link (데이터링크) 계층 : 송/수신 확인, MAC 주소를 가지고 통신함 ( 브릿지,  스위치 )

- 신뢰성 있고 효율적인 정보 전송을 가능하게 함
- 흐름 제어, 오류 제어, 순서 기능, 프레임 동기화 등

Physical (물리) 계층 : 전송하는데 필요한 기능 ( 통신 케이블, 허브 )


    
<details>
<summary> ex)  X라는 프로그램을 통해서 사용자 A,B가 통신할 때  A가 B에게 Data 를 보냄</summary>
  
    응용 계층 : X 프로그램 
    
    표현 계층 : Data를 암호화 및 압축
    
    세션 계층 : 인증 체크 ( B가 통신이 가능한지 확인 ) 
    
    전송 계층 : TCP / UDP 
    
    네트워크 계층 : IP (B의 주소)
    
    데이터링크 계층 : MAC 주소 ( B의 주소를 찾고 그 안에서 device 주소)
    
    물리 계층 : 적외선(광 케이블) 을 통해 B에게 보냄
</details>
    

    
    

Reference

[https://hanamon.kr/네트워크-기본-프로토콜이란-osi-7-계층-별-프로토콜/](https://hanamon.kr/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EA%B8%B0%EB%B3%B8-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%EC%9D%B4%EB%9E%80-osi-7-%EA%B3%84%EC%B8%B5-%EB%B3%84-%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C/)
