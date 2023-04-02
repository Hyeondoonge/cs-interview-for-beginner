## 데이터베이스 이상 개념

테이블을 잘못 설계하여 데이터를 삽입, 갱신, 삭제 할 때 문제가 발생하는 것

> **삽입 이상**
>

새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입하는 문제

> **갱신 이상**
>

중복된 튜플 중 일부만 변경하면 데이터가 불일치하게 되는 모순의 문제

> **삭제 이상**
>

튜플을 삭제할 때 꼭 필요한 데이터까지 함께 삭제되는 데이터 손실의 문제

## 데이터베이스 이상 예시

| Employee_ID | Name | Department | Student_Group |
| --- | --- | --- | --- |
| 123 | J. Longfellow | Accounting | Beta Alpha Psi |
| 234 | B. Rech | Marketing | Marketing Club |
| 234 | B. Rech | Marketing | Management Club |
| 456 | A. Bruchs | CIS | Technology Org. |
| 456 | A. Bruchs | CIS | Beta Alpha Psi |

> **삽입 이상**
>
- 새로운 부서 `Enginnering`이 신설되었고 아직 근무자가 없음
- 이 부서와 관련한 정보는 불필요한 정보를 함께 입력하지 않는 한 위 테이블에 입력할 수 없다.

| Employee_ID | Name | Department | Student_Group |
| --- | --- | --- | --- |
| 123 | J. Longfellow | Accounting | Beta Alpha Psi |
| 234 | B. Rech | Marketing | Marketing Club |
| 234 | B. Rech | Marketing | Management Club |
| 456 | A. Bruchs | CIS | Technology Org. |
| 456 | A. Bruchs | CIS | Beta Alpha Psi |
| ?? | ?? | Enginnering | ?? |

> **갱신 이상**
>
- `A. Bruchs`의 Department가 `CIS → Marketing` 으로 수정
- 4, 5번째 행의 CIS를 전부 갱신하지 않고 하나만 갱신하면 `A. Bruchs`의 Department가 어디인지 알 수 없다.

| Employee_ID | Name | Department | Student_Group |
| --- | --- | --- | --- |
| 123 | J. Longfellow | Accounting | Beta Alpha Psi |
| 234 | B. Rech | Marketing | Marketing Club |
| 234 | B. Rech | Marketing | Management Club |
| 456 | A. Bruchs | Marketing | Technology Org. |
| 456 | A. Bruchs | CIS | Beta Alpha Psi |

> **삭제 이상**
>
- 만약 Accounting 부서에 속한 사람이 `J. Longfellow` 한 명 뿐일 경우
- `J. Longfellow`의 정보를 삭제하면 `Accounting` Department의 정보가 사라지게 된다.

### 이상을 해결하는 방법 → `정규화`