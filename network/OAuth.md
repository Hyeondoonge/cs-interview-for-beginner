## OAuth 란?

- 우리의 서비스가 우리 서비스를 이용하는 유저의 타사 플랫폼 정보에 접근하기 위해서 권한을 타사 플랫폼으로부터 위임 받는 것

## OAuth 2.0 주체

### Resource Owner

- 리소스 소유자
- 우리의 서비스를 이용하면서 구글, 페이스북 등의 플랫폼에서 리소스를 소유하고 있는 사용자

### Authorization & Resource Server

- Authroization Server
    - Resource Owner를 인증
    - Client에게 액세스 토큰을 발급
- Resource Server
    - 구글, 페이스북, 트위터와 같이 리소스를 가지고 있는 서버

> *Authorization Server와 Resource Server는 공식문서상 별개로 구분되어 있지만, 별개의 서버로 구성할지, 하나의 서버로 구성할지는 개발자가 선택하기 나름*
>

### Client

- Resource Server의 자원을 이용하고자 하는 서비스

## 어플리케이션 등록

OAuth 2.0 서비스를 이용하기 전에 Client를 Resource Server에 등록하는 작업이 선행되어야 한다. 이 때 Redirect URI를 등록한다.

- Redirect URI: 사용자가 OAuth 2.0 서비스에서 인증을 마치고 사용자를 Redirection시킬 URI

### Redirect URI

OAuth 2.0 서비스는 인증이 성공한 사용자를 사전에 등록된 Redirect URI로만 Redirection 시킨다.

### Client ID, Client Secret

등록과정을 마치면, Client ID와 Client Secret을 얻을 수 있다. 발급된 Client ID와 Client Secret은 액세스 토큰을 획득하는데 사용된다. 이 때 Client ID는 공개되어도 상관없지만, Client Secret은 절대 유출되어서는 안된다.

## OAuth 2.0 동작 매커니즘

![111](https://user-images.githubusercontent.com/72093196/227731209-6dba0cc2-8dbf-4db4-bfaa-72a5c2d0abf3.png)

### 로그인 요청 (1,2)

Resource Owner가 우리 서비스의 **`OOO**로 로그인 하기` 등의 버튼을 클릭해 로그인을 요청한다.

Client는 OAuth 프로세스를 시작하기 위해 사용자의 브라우저를 Authorization Server로 보낸다.

Client는 이때 Authorization Server가 제공하는 Authorization URL에 `response_type`, `client_id`, `redirect_uri`, `scope` 등의 매개변수를 쿼리 스트링으로 포함하여 보낸다.

### 로그인 페이지 제공, ID/PW 제공 (3,4)

Client가 빌드한 Authorization URL로 이동된 Resource Owner는 제공된 로그인 페이지에서 ID와 PW 등을 입력하여 인증

### Authorization Code 발급, Redirect URI로 리다이렉트 (5,6)

인증이 성공되었다면, Authorization Server는 제공된 Redirect URI로 사용자를 리다이렉트 시킬 것이다. 이때, Redirect URI에 Authorization Code를 포함하여 사용자를 리다이렉션 시킨다.

- Authorization Code: Client가 Access Token을 획득하기 위해 사용되는 임시 코드

### Authorization Code와 Access Token 교환 (7,8)

Client는 Authorization Server에 Authorization Code를 전달하고, Access Token을 응답받는다.

Client는 발급받은 Resource Owner의 Access Token을 저장하고, 이후 Resource Server에서 Resource Owner의 리소스에 접근하기 위해 Access Token을 사용한다.

### 로그인 성공 (9)

### Access Token으로 리소스 접근(10 ~ 13)

이후 Resource Owner가 Resource Server의 리소스가 필요한 기능을 Client에 요청한다.

Client는 위 과정에서 발급받고 저장해둔 Resource Owner의 Access Token을 사용하여 제한된 리소스에 접근하고, Resource Owner에게 자사의 서비스를 제공한다.

### 참고자료

[OAuth 2.0 개념과 동작원리](https://hudi.blog/oauth-2.0/)