## CORS(Cross-Origin-Resoure-Sharing)

다른 출처의 리소스에 접근할 수 있는 권한을 부여받기위해 브라우저에게 알려주는 정책이다.
SOP(Same-Origin-Policy)에 따라, 보안 상의 이유로 브라우저는 스크립트 상의 교차 출처로의 HTTP 요청을 제한한다. 예를 들어 한 사이트에서 Fetch API를 이용해 다른 출처에 요청을 전송할 경우 요청이 제한된다.

CORS 정책은 다른 출처간의 안전한 리소스 교환을 지원한다.

### 다른 출처를 구분하는 법

요청 출처와 응답 출처 간에 프로토콜, 도메인, 포트번호를 비교하여 이들 중
하나라도 다를 때 다른 출처라고 판단한다.

| 요청                   | 응답                     | 결과      |
| ---------------------- | ------------------------ | --------- |
| http://example.com     | http://examples.com      | 다른 출처 |
| http://example.com     | https://example.com      | 다른 출처 |
| http://examples.com    | http://examples.com      | 같은 출처 |
| http://examples.com:80 | http://examples.com:8000 | 다른 출처 |

만약 한 쪽 출처의 포트만 명시된 경우에는, 브라우저 출처 비교 방식에 따라 비교 결과가 달라진다.

### CORS 에러 발생시 해결 방법

다른 출처로 리소스 요청 시 CORS정책에 의한 에러가 발생한다.
이를 해결하기 위해서 아래의 응답헤더와 요청헤더를 설정하면된다.

**응답 헤더**

- Access-Control-Allow-Origin: 지정된 출처의 교차 요청을 허용
- Access-Control-Allow-Method: 리소스 접근 시 허용할 HTTP 메소드
- Access-Control-Allow-Headers: 리소스 접근 시 허용할 HTTP 헤더

**요청 헤더**

- Origin: 요청이 시작된 URL로 경로 정보는 포함하지 않음
- Access-Control-Request-Method: 실제 요청에 사용할 HTTP 메소드
- Access-Control-Request-Headers: 실제 요청에 사용할 HTTP 헤더

클라이언트 측에서 CORS를 회피할 수도 있다. 프록시 서버를 통해 요청하거나, 브라우저 정책을 회피하는 확장프로그램을 사용할 수 있다.

하지만, 안전한 교차 출처 간 리소스 공유를 위해서는 서버와 클라이언트가 협력하여 HTTP 헤더를 사용해야한다.

### CORS 유의점

응답헤더인 Access-Control-Allow-Origin의 값을 \*(와일드카드)로 설정할 경우, 모든 교차 출처로부터 요청을 허용한다. 이 경우 CSRF(교차 사이트간 요청 위조)에 취약할 수 있다. 따라서 이에 민감한 경우에는 단일 출처를 지정하도록해야한다.

```
Access-Control-Allow-Origin: http://example.com
```
