## **Tree**

⇒ `Node`와 `Edge`로 이루어진 자료구조

- 노드들이 나무 가지처럼 연결된 비선형 계층적 자료구조

![https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)

### 트리의 특징

- 트리는 값을 가진 `노드(Node)`와 이 노드들을 연결해주는 `간선(Edge)` 으로 이루어져있다.
- 트리에는 사이클이 존재할 수 없다. (만약 사이클이 만들어진다면, 그것은 트리가 아니고 그래프다)
- 모든 노드는 자료형으로 표현이 가능하다.
- 루트에서 한 노드로 가는 경로는 유일한 경로 뿐이다.
- 노드의 개수가 N개면, 간선은 N-1개를 가진다.

가장 중요한 것은, `그래프`와 `트리`의 차이가 무엇인가인데, 이는 사이클의 유무로 설명할 수 있다.

### 트리의 용어

- `노드(Node)` : 트리의 각 요소로 데이터 값을 가진다.
- `간선(Edge)` : 각 노드들을 연결 해준다.
- `루트(root)`: 트리의 맨 위에 있는 노드(데이터 1을 가진 노드)를 루트 노드라고 부른다.
- `부모 노드(parent node)`: 자신보다 하위 노드(자식 노드)를 가지고 있는 노드의 경우
- `자식 노드(child node)` : 자신보다 상위 노드(부모 노드)를 가지고 있는 경우
- `리프 노드(leaf node)` : 자식 노드를 가지지 않는 노드 (외부 노드, 단말 노드)
- `가지 노드 (branch node)` : 자식 노드를 하나 이상 가진 노드 (내부 노드, 비단말 노드)
- `형제 노드(sibling node)` : 같은 부모를 가지는 노드
- `깊이 (depth)` : 루트에서 어떤 노드까지의 간선의 수
- `높이 (height)` : 어떤 노드에서 리프 노드까지 가장 긴 경로의 간선의 수 (최대 높이)
- `레벨 (level)` : 루트부터 레벨 0, 그 하위 단계를 레벨1, 점차 늘려나감
- `차수 (degree)` : 해당 노드가 포함하는 자식 노드의 갯수
- `경로 (path)` : 노드와 노드 사이간에 나타내는 노드와 엣지의 순서

### **트리 순회 방식**

트리를 순회하는 방식은 총 4가지가 있다. 위의 그림을 예시로 진행해보자

![https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png](https://www.geeksforgeeks.org/wp-content/uploads/binary-tree-to-DLL.png)

1. **전위 순회(pre-order)**
    
    각 루트(Root)를 순차적으로 먼저 방문하는 방식이다.
    
    **(Root → 왼쪽 자식 → 오른쪽 자식)**
    
    > 1 → 2 → 4 → 8 → 9 → 5 → 10 → 11 → 3 → 6 → 13 → 7 → 14
    > 
2. **중위 순회(in-order)**
    
    왼쪽 하위 트리를 방문 후 루트(Root)를 방문하는 방식이다.
    
    **(왼쪽 자식 → Root → 오른쪽 자식)**
    
    > 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 6 → 13 → 3 →14 → 7
    > 
3. **후위 순회(post-order)**
    
    왼쪽 하위 트리부터 하위를 모두 방문 후 루트(Root)를 방문하는 방식이다.
    
    **(왼쪽 자식 → 오른쪽 자식 → Root)**
    
    > 8 → 9 → 4 → 10 → 11 → 5 → 2 → 13 → 6 → 14 → 7 → 3 → 1
    > 
4. **레벨 순회(level-order)**
    
    **루트(Root)부터 계층 별로 방문하는 방식이다.**
    
    > 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 13 → 14
    > 

### **Code**

```cpp
public class Tree<T> {
    private Node<T> root;

    public Tree(T rootData) {
        root = new Node<T>();
        root.data = rootData;
        root.children = new ArrayList<Node<T>>();
    }

    public static class Node<T> {
        private T data;
        private Node<T> parent;
        private List<Node<T>> children;
    }
}
```

Reference

[https://gyoogle.dev/blog/computer-science/data-structure/Tree.html](https://gyoogle.dev/blog/computer-science/data-structure/Tree.html)

[https://velog.io/@kon6443/Data-Structure-자료구조-C-트리#span-stylecolorrgb12217389-binary-tree-span](https://velog.io/@kon6443/Data-Structure-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-C-%ED%8A%B8%EB%A6%AC#span-stylecolorrgb12217389-binary-tree-span)
