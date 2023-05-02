# Quick Sort

⇒ **분할 정복 방법**을 통해 정렬하는 방식

( 분할 정복 ⇒ 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략 )  

- Quick Sort는 불안정 정렬
- Merge Sort와 달리 Quick Sort는 배열을 비균등하게 분할

## Process

1. 배열 가운데에 하나의 원소를 골라 pivot으로 설정
2. pivot 앞에는 pivot 보다 작은 값들이 오고, pivot 뒤에는 pivot 보다 큰 값들이 오도록 pivot을 기준으로 **분할**
3. 분할된 두 개의 작은 배열에 대해 재귀적으로 반복  

```java

  public static int[] sort(int[] arr){

        sort(arr,0,arr.length-1);

        return arr;
    }

   public static void sort(int[] arr, int start, int end){ // 처음과 끝을 기준으로 정렬
	   
        int partitionIndex=partition(arr,start,end); // 피봇 설정 

        if(start<partitionIndex-1){
            sort(arr,start,partitionIndex-1); // 분할정복으로 0번 인덱스부터 분할된 앞의 인덱스-1까지 정렬
        }
        if(partitionIndex<end) { // 분할정복으로 분할된 앞의 인덱스부터 마지막 인덱스까지 정렬
            sort(arr, partitionIndex, end);
        }
    }

    public static int partition(int[] arr,int start,int end){
        int pivot=arr[(start+end)/2];

        while(start<=end){
            while (arr[start]<pivot){ // pivot 보다 앞에 있는 원소들 중에서 큰 값을 찾음
                start++;
            }
            while (arr[end]>pivot){ // pivot 보다 뒤에 있는 워소들 중에서 작은 값을 찾음
                end--;
            }
            if(start<=end){ // 서로 교환
                int temp=arr[start];
                arr[start]=arr[end];
                arr[end]=temp;
                start++;
                end--;
            }
        }
        return start; // 서로 교환한 바로 앞의 index 를 반환
    }
```

## 시간 복잡도

- 최선의 경우 ⇒ 순환 호출의 깊이 * 각 순환 호출 단계의 비교 연산 = O(NlogN)

![image](https://user-images.githubusercontent.com/77667212/235563780-308f3556-c44b-487f-ba31-3eae3eab5cdc.png)


- 최악의 경우 ⇒ O(N^2) ( 이미 정렬된 리스트에 대해서 퀵 정렬을 실행하는 경우 )

![image](https://user-images.githubusercontent.com/77667212/235563810-8b9ed0be-f7ce-4d2d-80ea-443d427fdd4c.png)

- 평균의 경우 ⇒ O(NlogN)

## 장점

- **속도가 빠르다 (다른 O(NlogN)의 시간복잡도를 가지는 정렬 알고리즘과 비교해도 빠름)**
- 추가 메모리 공간이 필요하지 않음

## 단점

- 불안정 정렬 (Unstable Sort)
- 정렬된 리스트에서는 불균형 분할에 의해 시간이 더 오래걸림
- 퀵 정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할할 수 있는 데이터를 선택한다.
    
    ex) 리스트 내의 몇 개의 데이터 중에서 크기순으로 중간 값을 피벗으로 선택한다.
    
    ( 이 방법으로 개선한다해도 Quick Sort의 최악의 시간복잡도가 O(NlogN)이 되는 것은 아니다. )
    

## 소트와의 차이점

- 퀵정렬 : 우선 피벗을 통해 정렬(partition) → 영역을 쪼갬(quickSort)
- 합병정렬 : 영역을 쪼갤 수 있을 만큼 쪼갬(mergeSort) → 정렬(merge)
