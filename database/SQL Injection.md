## SQL Injection

⇒ 해커에 의해 조작된 SQL문이 데이터베이스에 그대로 전달되어 비정상적으로 명령을 실행시키는 공격 기법 

ex) 2017년 3월 발생한 "여기어때" 고객 정보 및 고객 투숙 정보 노출 사고, 2015년 "뽐뿌" 개인정보 노출 사고가 SQL Injection 공격이 원인

## 공격 방법

1. **인증 우회**
    
    공격자는 인증 절차를 우회하고 인가되지 않은 사용자가 시스템에 접근하는 것 
    
    ex) OR '1'='1' 를 사용하여 users 테이블에 있는 모든 정보를 출력하게 됨 
    
    ```sql
    SELECT * FROM users WHERE username='[입력된 사용자 이름]' AND password='[입력된 암호]';
    
    SELECT * FROM users WHERE username='김아무개' OR '1'='1'--;
    ```
    
2. **데이터 노출**
    
    시스템에서 발생하는 에러 메시지를 이용해 공격하는 방법이다. 보통 에러는 개발자가 버그를 수정하는 면에서 도움을 받을 수 있는 존재다. 해커들은 이를 역이용해 악의적인 구문을 삽입하여 에러를 유발시킨다.
    
    ex) GET 방식으로 동작하는 URL 쿼리 스트링을 추가하여 에러를 발생
    
    ```html
    http://example.com/index.php?username=john&password=1234
    
    http://example.com/index.php?username='' OR 1=1 --
    ```
    

## 방어 방법

1. **input 값을 받을 때, 특수문자 여부 검사하기 ( 블랙리스트 & 화이트 리스트 기반 필터링 )**
    
    ⇒ 로그인 전, 검증 로직을 추가하여 미리 설정한 특수 문자들이 들어왔을 때 요청을 막아냄
    
    - 블랙리스트 기반 필터링 ⇒ 입력값에서 특정 문자열이나 패턴을 필터링하여, 악성 입력값을 차단
    - 화이트리스트 기반 필터링 ⇒ 입력값에서 특정 문자열이나 패턴을 허용하여, 안전한 입력값만을 받는 것
2. **SQL 서버 오류 발생 시, 해당하는 에러 메시지 출력 제한** 
    
    ⇒ view를 사용하여 원본 데이터베이스 테이블에 접근권한을 높임, 일반 사용자는 view로만 접근하여 에러를 볼 수 없도록 함 
    
    - view ⇒ 하나 이상의 테이블에 대한 쿼리 결과를 대신하여 사용할 수 있는 가상 테이블
    - view를 사용하면 사용자는 원본 테이블에 직접 액세스하지 않고, view를 통해 액세스할 수 있습니다. ( 원본 테이블에 접근 할 수 없게 돼서 보안성이 높아짐 )
3. **preparestatement 사용하기** 
    
    ⇒ preparestatement를 사용하면, 특수문자를 자동으로 escaping 해준다. (statement와는 다르게 쿼리문에서 전달인자 값을 ?로 받는 것) 이를 활용해 서버 측에서 필터링 과정을 통해서 공격을 방어한다.
    
    ex) sql 문 안에 ? 파라미터 값을 setString() 메서드를 사용하여 추가하기 때문에 사용자 입력값이 SQL 쿼리 문자열에 포함되지 않으므로 SQL Injection 공격을 방어할 수 있습니다.
    
    ```java
    String username = request.getParameter("username");
    String password = request.getParameter("password");
    
    Connection conn = null;
    PreparedStatement pstmt = null;
    
    try {
        conn = getConnection(); // 데이터베이스 연결을 설정하는 코드
        String sql = "SELECT * FROM users WHERE username = ? AND password = ?";
        pstmt = conn.prepareStatement(sql);
        pstmt.setString(1, username);
        pstmt.setString(2, password);
        ResultSet rs = pstmt.executeQuery();
    
        if (rs.next()) {
            // 인증 성공
        } else {
            // 인증 실패
        }
    } catch (SQLException e) {
        // 예외 처리
    } finally {
        close(conn, pstmt); // 데이터베이스 연결을 닫는 코드
    }
    ```
    
    **Reference**
    
    [https://gyoogle.dev/blog/computer-science/data-base/SQL Injection.html](https://gyoogle.dev/blog/computer-science/data-base/SQL%20Injection.html)
