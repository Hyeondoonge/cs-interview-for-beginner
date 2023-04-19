## 2-3 트리란?

- 트리의 높이가 균형을 이루며, 내부노드의 차수가 2 또는 3인 균형 탐색 트리이다.
- 차수가 3인 B-트리

## 시간 복잡도

- Search : O(log N)
- Insert : O(log N)
- Delete : O(log N)


## Condition

1. **Inter Node, External Node**
    - Internal Node: 데이터(Key)가 들어있는 내부 노드
    - External Node: 데이터(Key)가 들어있지 않는 노드 (가상의 노드)

    <img width="764" alt="1" src="https://user-images.githubusercontent.com/72093196/233000797-2c197306-238d-4a2b-9742-b471b343f2c0.png">

2. **중복된 Key는 허용하지 않는다.**
3. **leftChild (Key)** < leftKey
   leftKey < **middleChild (Key)** < rightKey
   rightKey < **rightChild (Key)**

   <img width="640" alt="2" src="https://user-images.githubusercontent.com/72093196/233000793-cb159db4-ea3b-4f27-b453-3d7b3ed7f0e1.png">

4. 2- 3 트리에서 각각의 내부 노드는 **2-Node** 이거나 **3-Node** 이다.

    > **2-Node**
    >

    <img width="488" alt="3" src="https://user-images.githubusercontent.com/72093196/233000791-e3cbac5a-bddb-4d9d-8a53-22407d09789b.png">

    > **3-Node**
    >

    <img width="473" alt="4" src="https://user-images.githubusercontent.com/72093196/233000789-1d849592-f4e8-40f3-bc62-029a7bfa4796.png">

1. **모든 외부 노드는 같은 레벨**에 있다.

## Search

**search(Root, target);**

1. 노드에 값이 존재

   target == leftKey || target == rightKey → 트리에 존재!

2. target < leftKey → 왼쪽 자식 트리 확인 `search(leftChild, target);`
3. leftKey < target && target < rightKey → 가운데 자식 트리 확인 `search(middleChild, target);`
4. rightKey < target → 오른쪽 자식 트리 확인 `search(rightChild, target);`

## Insert

**반드시 Leaf Node에 데이터를 삽입**한다. (부모 노드가 비어있어도 삽입하지 않음)

- **예시**

  <img width="675" alt="5" src="https://user-images.githubusercontent.com/72093196/233000788-f33cdc01-0d5f-4303-b81b-994e279cbfad.png">

    - ‘60’ 삽입

      <img width="606" alt="6" src="https://user-images.githubusercontent.com/72093196/233000787-8d8c4fc6-3b27-42be-83a1-69f4876be91f.png">


middleChild가 2-Node, 3-Node 이어야 하는 조건 만족 X → **Split**

> **Split**
>
> 1. 노드 3개 중 가운데 값을 부모노드로 가지는 서브트리 생성
>
> <img width="613" alt="7" src="https://user-images.githubusercontent.com/72093196/233000782-d13c9464-a057-4c28-aace-81de75abceac.png">
>
> 1. 서브트리를 부모의 Node에 추가
>
> <img width="576" alt="8" src="https://user-images.githubusercontent.com/72093196/233000777-ff981c80-7c8d-4a88-9988-5ec1273a2457.png">
>
> 1. **부모 Node에 추가하였을 때 부모 노드의 Key가 3개일 경우, 부모노드에서 Split과정 반복**

## Delete

*가정) 최좌측일 경우에만 오른쪽 노드를 확인하고 그렇지 않을 경우 왼쪽 노드를 확인*

> **Rotation (회전) [형제 노드 중 3-Node 존재 O]**
>
>
> Key가 삭제되는 노드를 기준으로 삭제되는 노드의 형제노드의 원소 하나를 부모 노드로, 부모 노드의 원소 하나를 자신의 노드로 가져와 회전 시킨다.
>
> <img width="606" alt="9" src="https://user-images.githubusercontent.com/72093196/233000774-65c7827f-a50d-4b15-8655-6b6998f00742.png">
>

> **Merge (병합) [형제 노드 중 3-Node 존재 X]**
>
>
> Key가 삭제된 노드를 기준으로, 삭제되는 원소의 직후 형제노드와 자신 사이에 포함되는 부모 원소를 합치는 것
>
> <img width="736" alt="10" src="https://user-images.githubusercontent.com/72093196/233000771-049d799d-22a8-48b2-8d8b-34733e912c4d.png">
>
> 병합 이후 노드의 용량이 초과할 경우 → **Split**
>

### **삭제의 4가지 경우**

- 3-Node인 Leaf Node 삭제
- 2-Node인 Leaf Node 삭제
- 3-Node인 Non Leaf Node 삭제
- 2-Node인 Non Leaf Node 삭제

### **3-Node인 Leaft Node 삭제**

- 원소 삭제
- rightKey가 있을 경우 rightKey를 leftKey로 옮겨 줌

<img width="537" alt="11" src="https://user-images.githubusercontent.com/72093196/233000768-584b15d9-bda0-417e-bf96-c99e45bf4593.png">

### **2-Node인 Leaf Node 삭제**

- 형제 노드(왼쪽노드)가 3-Node(O) → Rotation

  <img width="551" alt="12" src="https://user-images.githubusercontent.com/72093196/233000764-6a655459-627f-43df-bda7-f5c86d26ca85.png">

- 형제 노드(왼쪽노드)가 3-Node(X) → Merge

  <img width="711" alt="13" src="https://user-images.githubusercontent.com/72093196/233000763-8de97a17-a5ca-4e28-8355-51394a5aca59.png">


### **3-Node인 Non Leaf Node 삭제**

1. ‘80’ 삭제

   <img width="733" alt="14" src="https://user-images.githubusercontent.com/72093196/233000761-4d7498ee-87c7-4fa0-9d22-8e022088ef4b.png">

2. 삭제되는 노드의 왼쪽 서브트리 중 가장 큰 값으로 채운다. (Leaf Node가 삭제되는 경우로 변환)

   <img width="733" alt="15" src="https://user-images.githubusercontent.com/72093196/233000759-ac0e147b-e63f-48c1-9f9d-4601e2ceb4b0.png">

3. 삭제되는 리프 노드의 형제 노드(왼쪽 노드)가 3-Node(X) → Merge

   <img width="733" alt="16" src="https://user-images.githubusercontent.com/72093196/233000755-5d1704e4-62cf-453c-bf9c-374f804ee6e9.png">

4. 삭제되는 리프 노드의 형제 노드(왼쪽 노드)가 3-Node(O) → Rotation

   <img width="733" alt="17" src="https://user-images.githubusercontent.com/72093196/233000754-67e421c7-06b3-4858-9aad-ac0b3018826c.png">

5. 결과

   <img width="733" alt="18" src="https://user-images.githubusercontent.com/72093196/233000753-60c3d663-8f09-4fc4-a3d7-5de60ad0c1c0.png">


### **2-Node인 Non Leaf Node 삭제**

1. ‘40’ 삭제

   <img width="733" alt="19" src="https://user-images.githubusercontent.com/72093196/233000750-1feaacc0-b35f-46e7-8ec6-ebc11a796bc2.png">

2. 삭제되는 노드의 왼쪽 서브트리 중 가장 큰 값으로 채운다. (Leaf Node가 삭제되는 경우로 변환)

    <img width="733" alt="20" src="https://user-images.githubusercontent.com/72093196/233000747-1989108b-b560-4ea0-ae05-644b6044ec87.png">

3. 삭제되는 리프 노드의 형제 노드(오른쪽 노드)가 3-Node(O) → Merge

   <img width="733" alt="21" src="https://user-images.githubusercontent.com/72093196/233000745-231fc5a1-ad79-4f76-9d81-1a76076ff0dd.png">

4. 삭제되는 리프 노드의 형제 노드(왼쪽 노드) 중 3-Node(X) → Merge

   <img width="733" alt="22" src="https://user-images.githubusercontent.com/72093196/233000741-412d37b6-8968-49a6-969b-c7bbb8a8c6df.png">

3. 결과

   <img width="733" alt="23" src="https://user-images.githubusercontent.com/72093196/233000734-4b9c88ea-bb5f-42b6-ac97-e6c37cfffa95.png">
