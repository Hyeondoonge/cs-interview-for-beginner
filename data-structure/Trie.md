### 트라이 (Trie)란?

**문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조**

트라이 자료구조에 저장된 문자열들은 트리의 루트에서부터 자식들을 따라가면서 생성된 문자열들이다.

<img width="619" alt="1" src="https://user-images.githubusercontent.com/72093196/233884853-61db5521-34d6-4872-9077-d197412c2300.png">

### 시간복잡도

- L : 자료구조에 저장된 가장 긴 문자열의 길이
- M : 자료구조에 저장된 문자열들의 수
- 삽입 : `O(L)`
- 탐색 : `O(L)`
- 삭제 : `O(L)`
- 생성 : `O(M*L)`

### 사용되는 경우

- 자동완성/사전
- 맞춤법 검사기
- 가장 긴 접두사 일치

### 장점

문자열을 탐색할 때, 하나하나씩 전부 비교하는 것보다 시간 복잡도 측면에서 훨씬 효율적!

### 단점
각 노드는 자식에 대한 포인터를 모두 저장하므로 공간을 많이 차지한다.

`O(포인터 크기 * 포인터 개수 * 총 노드의 개수)`