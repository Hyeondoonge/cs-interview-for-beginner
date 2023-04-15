## Stack

- LIFO (Last In First Out)
- 활용 예시
    - 웹 브라우저 뒤로가기
    - 문서작업에서 Ctrl+Z
    - 역순 문자열 만들기
    - 후위 표기법 계산
    - 재귀적 알고리즘

## Queue

- FIFO (First In First Out)
- 활용 예시
    - 은행창구 번호표 대기
    - 프린터 출력
    - 컴퓨터 운영체제의 테스크 스케쥴링
    - 너비 우선 탐색 알고리즘

### Deque

- Double Ended Queue
- Stack과 Queue를 합친 것

## 시간복잡도

|  | stack | queue | deque |
| --- | --- | --- | --- |
| 삽입 | O(1) | O(1) | O(1) |
| 삭제 | O(1) | O(1) | O(1) |
| 검색 | O(N) | O(N) | O(N) |