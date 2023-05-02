### 과정

1. 주어진 배열 중에서 최소값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체한다.
3. 맨 처음 위치를 뺀 나머지 리스트를 같은 방법으로 교체한다.
4. 하나의 원소만 남을 때 까지 1~3 과정을 반복한다.

### 예시

![1](https://user-images.githubusercontent.com/72093196/235566551-2133daf6-ba30-49ab-ab74-43eb2e169a70.png)

### 시간복잡도

```math
T(n) = (n-1) + (n-2) + ... + 2 + 1 = n(n-1)/2 = O(n^2)
```


### Reference

[https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)