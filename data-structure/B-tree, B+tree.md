## B-Tree란

- 데이터베이스와 파일 시스템에서 널리 사용되는 트리 자료구조의 일종
- 외부장치(디스크)에서 데이터를 가져올 때 한번에 여러개의 데이터를 가져옴으로써 **데이터 로드의 효율성**이 좋다. (*디스크에 접근해서 데이터를 가져오는 것은 비싼 작업)*

## 시간 복잡도

- Search : O(log N)
- Insert : O(log N)
- Delete : O(log N)

## Condition

1. Root 노드는 최소 2개 이상의 자식을 갖는다.
2. M차 B트리 (최대 M개의 자식을 가질 수 있는 B 트리)
    1. 노드는 최대 M개부터 M/2개 까지 자식을 가질 수 있다.
    2. 노드는 최대 M-1개 부터 M/2-1개 까지 키를 가질 수 있다.
3. **Inter Node, External Node**
    - Internal Node: 데이터(Key)가 들어있는 내부 노드
    - External Node: 데이터(Key)가 들어있지 않는 노드 (가상의 노드)

   <img width="764" alt="1" src="https://user-images.githubusercontent.com/72093196/233029983-df34be3f-192c-4867-8e99-7c013675cd0d.png">

4. **모든 외부 노드는 같은 레벨**에 있다.

## Search (M=4)

<img width="766" alt="2" src="https://user-images.githubusercontent.com/72093196/233029979-af3b59fc-7861-495f-9838-0c311809328f.png">

**`search(Root, target);`**

1. 노드에 값이 존재

   target == valueN → 트리에 존재!

2. target < value1 → `search(Child1, target);`
3. value1 < target < value2 → `search(Child2, target);`
4. value2 < target < value3 → `search(Child3, target);`
5. value3 < target → `search(Child4, target);`

## Insert

**반드시 Leaf Node에 Key를 삽입**한다. (부모 노드가 비어있어도 삽입하지 않음)

- 예시

  <img width="717" alt="3" src="https://user-images.githubusercontent.com/72093196/233029977-d27fdff9-d92e-4a53-a850-248f08d8d32d.png">

    - ‘70’ 삽입

        <img width="717" alt="4" src="https://user-images.githubusercontent.com/72093196/233029973-66424691-9811-401b-8a25-c20cfabdaaa4.png">

    - ‘80’ 삽입
  
        <img width="717" alt="5" src="https://user-images.githubusercontent.com/72093196/233029972-7fceaf93-dd99-4f2c-b2e8-acb46b36484e.png">


> **Split**
>
> 1. 노드 3개 중 가운데 값을 부모노드로 가지는 서브트리 생성
     >
     >     <img width="633" alt="6" src="https://user-images.githubusercontent.com/72093196/233029970-1ef918fe-18f0-4bed-a3d1-3a37f75121f5.png">
>
> 2. 서브트리를 부모의 Node에 추가
     >
     >     <img width="717" alt="7" src="https://user-images.githubusercontent.com/72093196/233029967-ca62a1cb-b892-4e13-8a82-291eb48eaf20.png">
>
> 3. **부모 Node에 추가하였을 때 부모 노드의 Key가 M개일 경우, 부모노드에서 Split과정 반복**

## Delete

*가정) 최좌측일 경우에만 오른쪽 노드를 확인하고 그렇지 않을 경우 왼쪽 노드를 확인*

> **Rotation (회전) [형제 노드 중 (M/2-1) 개 이상의 Key를 가져야 한다.]**
>
>
> Key가 삭제되는 노드를 기준으로 삭제되는 노드의 형제노드의 원소 하나를 부모 노드로, 부모 노드의 원소 하나를 자신의 노드로 가져와 회전 시킨다.
>
> <img width="606" alt="8" src="https://user-images.githubusercontent.com/72093196/233029966-b290b1eb-868e-4778-9298-cdac66d76c57.png">
>

> **Merge (병합) [형제 노드 중 (M/2-1) 개 이상의 Key를 가지지 않는다.]**
>
>
> Key가 삭제된 노드를 기준으로, 삭제되는 노드의 직후 형제노드와 자신 사이에 포함되는 부모 원소를 합치는 것
>
> <img width="736" alt="9" src="https://user-images.githubusercontent.com/72093196/233029963-e0bf7d8d-7c40-40b5-9490-64007d1609bf.png">
>
> 병합 이후 노드의 용량이 초과할 경우 → **Split**
>

### Delete **Case**

- Leaf Node에서 삭제
- Non Leaf Node에서 삭제
    - 왼쪽 서브트리에서 최댓값을 가져와서 Leaf Node가 삭제되는 경우로 변환
    - 오른쪽 서브트리에서 최솟값을 가져와서 Leaf Node가 삭제되는 경우로 변환

### **Leaf Node 삭제 (삭제 후 키 갯수: 최소 Key 갯수(M/2 - 1) 이상)[M = 3]**

- 바로 Key 삭제
- 오른쪽에 Key가 존재할 경우 왼쪽으로 옮겨 줌

<img width="537" alt="10" src="https://user-images.githubusercontent.com/72093196/233029958-a147d999-fabe-416a-9d3b-c018732f0fe4.png">

### Leaf Node 삭제 (삭제 후 키 갯수: 최소 Key 갯수(M/2 - 1) 미만)[M = 3]

- 형제 노드(왼쪽 노드)가 (M/2-1)개 이상의 Key를 가지는 경우  → **Rotation**

  <img width="551" alt="11" src="https://user-images.githubusercontent.com/72093196/233029955-7a0b5053-ef1a-4194-9395-da09d4df6a86.png">

- 형제 노드(왼쪽 노드)가 (M/2-1)개 이상의 Key를 가지지 않는 경우 → **Merge**

  <img width="711" alt="12" src="https://user-images.githubusercontent.com/72093196/233029952-da4ead15-f4f1-4941-bf9a-473112c2ea67.png">


### **Non Leaf Node 삭제 (삭제 후 키 갯수: 최소 Key 갯수(M/2 - 1) 이상)[M = 3]**

1. ‘80’ 삭제

   <img width="733" alt="13" src="https://user-images.githubusercontent.com/72093196/233029946-2613a48b-4fa4-47aa-a570-05c61633059a.png">

2. 삭제되는 노드의 왼쪽 서브트리 중 가장 큰 값으로 채운다. (Leaf Node가 삭제되는 경우로 변환)

   <img width="733" alt="14" src="https://user-images.githubusercontent.com/72093196/233029937-00142c12-cf3e-4d43-8d81-259799fd819e.png">

3. 삭제되는 리프 노드의 형제 노드(왼쪽 노드)가 (M/2-1)개 이상의 Key를 가지지 않으므로 **Merge**

   <img width="733" alt="15" src="https://user-images.githubusercontent.com/72093196/233029934-111efc42-225e-48a6-9e0d-cb0e43333c9c.png">

4. 삭제되는 리프 노드의 형제 노드(왼쪽 노드)가 (M/2-1)개 이상의 Key를 가지므로 **Rotation**

   <img width="733" alt="16" src="https://user-images.githubusercontent.com/72093196/233029925-86fde38e-3eff-474f-9925-98a1f108436d.png">

5. 결과

   <img width="733" alt="17" src="https://user-images.githubusercontent.com/72093196/233029921-b521f027-53f0-4ecb-a669-7e9a9939aa4e.png">


### **Non Leaf Node 삭제 (삭제 후 키 갯수: 최소** Key **갯수(M/2 - 1) 미만)[M = 3]**

1. ‘40’ 삭제

   <img width="733" alt="18" src="https://user-images.githubusercontent.com/72093196/233029916-fa734c65-4191-4b28-aca4-93b219826b37.png">

2. 삭제되는 노드의 왼쪽 서브트리 중 가장 큰 값으로 채운다. (Leaf Node가 삭제되는 경우로 변환)

   <img width="733" alt="19" src="https://user-images.githubusercontent.com/72093196/233029911-f8d5bce5-76c3-45c9-833d-fc0fee2fa9c6.png">

3. 삭제되는 리프 노드의 형제 노드(오른쪽 노드)가 (M/2-1)개 이상의 Key를 가지지 않으므로 **Merge**

   <img width="733" alt="20" src="https://user-images.githubusercontent.com/72093196/233029909-a7c087b2-5b38-407e-9363-a6ea5269f6f4.png">

4. 삭제되는 리프 노드의 형제 노드(왼쪽 노드)가 (M/2-1)개 이상의 Key를 가지지 않으므로 **Merge**

   <img width="733" alt="21" src="https://user-images.githubusercontent.com/72093196/233029904-65dd5f2d-54c6-4dbb-b48f-46e62bf89877.png">

5. 결과

   <img width="733" alt="22" src="https://user-images.githubusercontent.com/72093196/233029893-c5d9de37-1f7d-42cf-ace2-019f1da8c02a.png">

## B+Tree란
데이터의 빠른 접근을 위한 인덱스 역할만 하는 비단말 노드가 추가로 있는 구조

기존의 B-Tree와 데이터의 연결리스트로 구현된 색인 구조 (B-Tree의 데이터 순차 접근 문제를 개선하기 위해)

![2](https://user-images.githubusercontent.com/72093196/233034178-8f175c5d-4818-44df-809d-01ec3bfbb9d6.png)

<img width="721" alt="1" src="https://user-images.githubusercontent.com/72093196/233032988-eada1254-9f8c-4ea0-9e7e-c378e806522a.png">

Leaf Node 끼리 연결리스트로 연결되어 있어 범위 탐색에 유리함

## Condition

- 모든 데이터는 Leaf Node에만 존재한다.
- 모든 Leaf Node는 연결리스트로 구성된다.
- 모든 Leaf Node의 첫 번째 key는 index set에 존재한다.