## Array, ArrayList, LinkedList

|                   | Array    | ArrayList | LinkedList     |
| ----------------- | -------- | --------- | -------------- |
| **길이**          | 고정길이 | 동적길이  | 동적길이       |
| **리사이징 여부** | X        | O         | X              |
| **접근시간**      | O(1)     | O(1)      | O(N)           |
| **삽입시간**      | O(N)     | O(N)      | O(1)           |
| **삭제시간**      | O(N)     | O(N)      | O(1)           |
| **항목 구성요소** | 데이터   | 데이터    | 데이터, 포인터 |

- LinkedList는 삽입, 삭제를 위한 위치를 알고있다는 가정 하에, 각각 O(1)의 시간복잡도를 가진다.
