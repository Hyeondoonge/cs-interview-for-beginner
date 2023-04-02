## 조인(Join)

여러개의 테이블을 연결하는 방법이다. 일반적으로 하나 이상의 컬럼을 기준으로두어 연결한다.

그 결과 하나의 결과 셋(튜플 집합)이 생성된다.

### INNER JOIN

두 집합을 교집합한 결과와 같다. 특정 컬럼을 기준으로, 각 테이블간에 일치하는 값들이 있는 튜플을 반환한다.

```sql
SELECT *
FROM T1
INNER JOIN T2
ON T1.id = T2.id;
```

INNER JOIN 키워드를 생략하고 작성할 수 있다.

```sql
SELECT *
FROM T1, T2
WHERE T1.id = T2.id;
```

### LEFT OUTER JOIN

두 집합 사이의 교칩합에다가 왼쪽 집합을 기준으로한 차집합을 더한 결과와 같다.

따라서 왼쪽 테이블에는 존재하지만 오른쪽 테이블에는 존재하지않는 튜플이 결합될 수 있다. 이때의 오른쪽 테이블의 컬럼 값들은 null로 채워진다.

```sql
SELECT *
FROM T1
LEFT OUTER JOIN T2
ON T1.id = T2.id;
```

### RIGHT OUTER JOIN

두 집합 사이의 교칩합에다가 오른쪽 집합을 기준으로한 차집합을 더한 결과와 같다.

따라서 오른쪽 테이블에는 존재하지만 왼쪽 테이블에는 존재하지않는 튜플이 결합될 수 있다. 이때의 왼쪽 테이블의 컬럼 값들은 null로 채워진다.

```sql
SELECT *
FROM T1
RIGHT OUTER JOIN T2
ON T1.id = T2.id;
```

### FULL OUTER JOIN

두 집합 사이의 교칩합에다가 양쪽 집합을 기준으로한 차집합을 모두 더한 결과와 같다.

```sql
SELECT *
FROM T1
FULL OUTER JOIN T2
ON T1.id = T2.id;
```

### CROSS JOIN

두 집합 사이의 곱칩합을 한 결과와 같다. 테이블의 모든 튜플들 간에 결합하는 방식이다.

두 개의 테이블이 있다고 가정할 때, 결과 셋의 개수는 (A테이블의 튜플 수) x (B테이블의 튜플 수)와 같다.

```sql
SELECT *
FROM T1
CROSS JOIN T2
```
