### Stored Procedure란?

DB 내부에 저장된 일련의 SQL 명령문들을 하나의 함수처럼 실행하기 위한 쿼리의 집합.

DB에 대한 작업을 정리한 절차를 RDBMS에 저장한 쿼리의 집합.

### Stored Procedure 예시

```mysql
delimiter $$
CREATE PROCEDURE change_nickname(user_id INT, new_nick VARCHAR(30))
-> BEGIN
->    insert into nickname_logs(
->		    select id, nickname, now() from users where id = user_id
->    );
->    update users sert nickname = new_nick where id=user_id;
-> END
-> $$
delimiter ;
```

### 장점

- Application에 transparent 하다.
    - 예를들어, MySQL 서버  1 대,Java Spring Application 4 대 작동 시,

      <img width="500" alt="1" src="https://user-images.githubusercontent.com/72093196/231087442-14566f63-5e09-4752-bdc7-75df6a744d58.png">

    - application 마다 같은 비즈니스 로직을 가지고 있으면 비즈니스 로직 수정 시 기존 인스턴스를 내리고 다시 올려아하는 등 번거로움. 하지만, 비즈니스 로직이 프로시저로 관리되면 프로시저만 바꿔주면 됨.

      <img width="500" alt="2" src="https://user-images.githubusercontent.com/72093196/231087452-6de4824d-797a-45be-97fb-f7c0901c3d59.png">


- 네트워크의 부하를 줄일 수 있다.

    <img width="300" alt="3" src="https://user-images.githubusercontent.com/72093196/231087456-b3f8fac7-27c5-4aab-ab5a-810e56885d65.png">

    <img width="300" alt="4" src="https://user-images.githubusercontent.com/72093196/231087462-08072cd5-89d8-4c43-a77c-70496d8243c6.png">


- 보안을 강화할 수 있다. (민감한 정보에 대한 접근을 제한할 수 있다.)
    - 회사 내 개발자가 DataBase에 직접적으로 접근하는 것을 막고, stored procedure를 통해서만 접근
- 여러 서비스에서 재사용 가능하다.

  <img width="649" alt="5" src="https://user-images.githubusercontent.com/72093196/231087475-496c4c56-ecb5-4daf-9d55-c5c15477bba9.png">

    - 서비스 마다 각자의 언어로 비즈니스 로직을 구현해야 하는 것은 번거로움.
    - RDB에 procedure로 저장 시, 여러 서비스에서 재사용 가능

### 단점

- 유지 관리 보수 비용이 증가한다.

  <img width="500" alt="6" src="https://user-images.githubusercontent.com/72093196/231087483-24b901b8-86df-4e81-9cec-525328268482.png">

    - 일부 비즈니스 로직은 소스코드에서 관리, 일부는 프로시저를 통해 관리되면 아무래도 제대로된 로직을 파악하는데 시간이 오래걸림
    - 버전 관리 번거로움 (application, procedure 둘 다 해줘야 함)
    - procedure와 관련된 문법을 알아야 함
- DB 서버를 추가하는 것은 간단한 작업이 아니다.(application을 추가하는 것에 비해서)
    - stored procedure를 사용하면 RDB에서 비즈니스 로직 처리 → CPU 사용량 증가

      <img width="500" alt="7" src="https://user-images.githubusercontent.com/72093196/231087502-40d81d1e-e7f2-4a1f-95cd-011d135ba6cc.png">

    - 애플리케이션은 서버 투입이 MySQL 보다 간단하다.

      <img width="500" alt="8" src="https://user-images.githubusercontent.com/72093196/231087522-e5e8f7ee-4d56-4940-a3a4-8fcb4943b632.png">

- stored procedure이 언제나 transparent 인 것은 아니다.

  <img width="500" alt="9" src="https://user-images.githubusercontent.com/72093196/231087543-fb6a836f-4b9f-445f-b155-a5e26fe6c463.png">

    - procedure의 이름 변경할 경우
        - 새로운 이름의 procedure 등록 → Logic tier 바꿔주고 재시동 → 기존 프로시저 제거
        - 소스 코드에 로직이 있는 것보다 오히려 손 많이 간다.
- transparent 하다고 무조건 좋은 것은 아님
    - 예상치 못한 문제의 영향을 최소화 할 수 있음
        - procedure에 버그가 있을 경우 전체 서버 문제 발생

          <img width="500" alt="10" src="https://user-images.githubusercontent.com/72093196/231087558-5add257a-2c00-4f3a-9fcd-d8a1b8e289a6.png">

        - 몇 개의 서버만 바꾸고 모니터링 하여 버그를 찾음으로써 몇 개의 서버만 문제 발생

          <img width="500" alt="11" src="https://user-images.githubusercontent.com/72093196/231087571-9e02f755-6068-46ef-adb0-a5b56470ddf2.png">

- stored procedure가 민감한 정보에 대한 접근을 완벽히 제한할 수 없다.
    - 민감한 정보를 반환하도록 악용하여 접근할 수도 있음