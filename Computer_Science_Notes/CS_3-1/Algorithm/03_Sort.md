# # 알고리즘

## 03. 정렬 (1)

- 컴퓨터과학과 이관용 교수님

### (1) 기본 개념

- 정렬 : 주어진 데이털르 값의 크기 순서에 따라 재배치하는 것
    - 오름차순, 내림차순
- 정렬구분 -> 정렬 수행 시점에 데이터가 어디에 저장되어 있는가?
    - 내부 정렬
        - 전체 데이터를 주기억장치에 저장한 후 정렬을 수행하는 방식
    - 외부 정렬
        - 모든 데이터를 주기억장치에 저장할 수 없는 경우, 모든 데이터를 보조기억장치에 저장해 두고
        - 그중 일부 데이터만을 반복적으로 주기억장치로 옮겨와서 정렬을 수행하는 방식
- 내부 정렬
    - 비교 기반 알고리즘
        - O(n<sup>2</sup>)
            - 선택 정렬
            - 버블 정렬
            - 삽입 정렬
            - 셀 정렬
        - O(nlogn)
            - 퀵 정렬
            - 합병 정렬
            - 힙 정렬
    - 데이터 분포 기반 알고리즘
        - O(n)
            - 계수 정렬
            - 기수 정렬
            - 버킷 정렬
- 정렬 관련 개념
    - 안정적 정렬 (stable)
        - 동일한 값을 갖는 데이터가 여러 개 있을 때 정렬 전의 상대적 위치가 정렬 후에도 그대로 유지되는 정렬
    - 제자리 정렬 (in-place)
        - 입력 배열 이외에 별도로 필요한 저장 공간이 상수 개를 넘지 않는 정렬
            - 입력 크기 n이 증가함에도 불구하고 추가적인 저장 공간은 증가하지 않음

### (2) 선택 정렬

- 예시 (가장 작은 숫자를 찾아서 앞으로 하나씩 배치)

```aiignore
for (i = 0; i < n-1; i++) {
    min = i;
    for (j = i+1; j<n; j++) {
        if (A[min] > A[j]) {
            min = j;
        }
    }
}
return A;
```

- 성능과 특징
    - 입력 데이터의 순서에 민감하지 않음
        - 최소값 찾기 -> 미정렬 부분A[i...n-1]에서 항상 (i-1)-i번의 비교가 필요
            - 입력 데이터의 상태와 상관없이 항상 동일한 성능 O(n<sup>2</sup>)을 가짐
        - 제자리 정렬 알고리즘
            - 입력 배열 A[] 이외에 상수 개의 저장 공간(예 : i, j, min, tmp)만 필요
        - 안정적이지 않은 정렬 알고리즘

### (3) 버블 정렬

- 모든 인접한 두 데이터를 차례대로 비교하여 왼쪽 데이터가 더 큰 경우에는 오른쪽 데이터와 자리를 바꾸는 과정을 반복해서 정렬을 수행하는 방식
    - 비교를 진행하는 방향
        - 왼쪽에서 오른쪽으로 진행
            - 가장 큰 값부터 찾아서 오른쪽 끝에서부터 위치시킴
        - 오른쪽에서 왼쪽으로 진행
            - 가장 작은 값부터 찾아서 왼쪽 끝에서부터 위치시킴

```aiignore
for(i=0; i < n-1; i++) {        // 단계 : (n-1)번 반복
    for (j=0; j < n-1; j++) {   // 왼쪽에서 오른쪽으로 진행하는 경우
        if (A[j] > A[j+1]) {    // 왼쪽 데이터 > 오른쪽 데이터이면
            A[j]와 A[j+1]의 자리 바꿈
        }
    }
}
return A;
```

- 성능과 특징
    - 안정적인 정렬 알고리즘
        - 인접한 두 데이터가 동일한 경우 -> 위치 교환이 미발생
    - 제자리 정렬 알고리즘
        - 입력 배열 A[] 이외에 상수 개의 저장 공간(예: i, j, tmp)만 필요
    - 선택 정렬에 비해 데이터 교환이 많이 발생
        - 선택 정렬보다 비효율적
- 개선된 버블 정렬 알고리즘
    - 각 루프의 반복 횟수를 줄여서 개선 가능
        - 처리 단계의 수
            - 자리바꿈이 발생하지 않으면 이미 정렬된 상태이므로 이후의 처리 단계를 수행하지 않고 종료
        - 인접한 두 데이터의 비교 횟수
            - 각 단계에서 무조건 오른쪽/왼쪽 끝까지 이동하면서 인접한 두 데이터의 비교가 불필요
            - 이미 제자리를 잡은 데이터에 대해서는 비교를 수행하지 않도록 함

```aiignore
for(i=0; i < n-1; i++) {
    Sorted = TRUE;
    for (j=0; j < (n-1)-i; j++) {
        if (A[j] > A[j+1]) {
            A[j]와 A[j+1]의 자리 바꿈
            Sorted = FALSE;
        }
        if (Sorted == TRUE) break;
    }
}
return A;
```

### (4) 삽입 정렬

- 미정렬 된 첫번째 데이터를 정렬 된 데이터에 알맞는 위치를 찾아 삽입
- 주어진 데이터를 하나씩 뽑은 후 이미 나열된 데이터가 항상 정렬된 상태를 유지하도록 뽑은 데이터를 바른 위치에 삽입해서 나열하는 방식
- 입력 배열을 정렬 부분 A[0...k-1]과 미정렬 부분 A[k..n-1]으로 구분해서 처리
    - A[0]를 정렬 부분, A[1..n-1]은 미정렬 부분으로 취급하여 시작
    - k=1, ..., n-1까지 반복
        - 미정렬 부분 A[k..n-1]의 첫 번째 데이터 A[k]를 뽑고,
        - A[0..k]가 정렬 상태를 유지하도록 만듦

```aiignore
for (i=1; i<n; i++) {                   // A[0] 정렬 부분; 1,..., (n-1)까지 (n-1)번 반복
    val = A[i];                         // 미정렬 부분 A[i.. n-1]의 첫 번째 데이터 선택
    for (j=i; j>0 && A[j-1] >val; j--) {    // 삽입할 위치 찾기
        A[j] = A[j-1];                  // 정렬 부분의 A[j-1]이 크면 뒤로 한 칸 이동
    }
    A[j] = val;                         // 찾아진 위치에 선택된 데이터 삽입
}
return (A);
```

- 성능과 특징
    - 안정적인 정렬 알고리즘
        - 인접한 두 데이터가 정렬되지 않은 경우에만 위치 교환이 발생
    - 제자리 정렬 알고리즘
        - 입력 배열 A[] 이외에 상수 개의 저장 공간(예: i, j, val)만 필요
    - 입력 데이터의 원래 순서에 민감
        - 원하는 정렬 순서의 역순으로 주어지는 경우
        - 원하는 순서의 정렬된 상태로 주어지는 경우

### (5) 셀 정렬

- 삽입 정렬의 단점 보완
    - 현재 삽입하고자 하는 데이터가 삽입될 제 위치에서 많이 벗어나 있어도 한 번에 한 자리씩만 이동해서 찾아가야 함
- 기본 아이디어
    - 멀리 떨어진 데이터와의 비교, 교환으로 한 번에 이동할 수 있는 거리를 늘려서 처리 속도 향상
        - 처음에는 멀리 떨어진 두 데이터를 비교해서 필요시 위치를 교환하고, 점차 가까운 위치의 데이터를 비교, 교환한 뒤, 맨 마지막에는 인접한 데이터를 비교, 교환하는 방식
        - 입력 배열을 부분배열로 나우어 삽입 정렬을 수행하는 과정을 부분배열의 크기와 개수를 변화시켜 가면서 반복

```java
public static void shellSort(int[] arr) {
    int n = arr.length;

    // 초기 gap 설정, 점점 줄여나감
    for (int gap = n / 2; gap > 0; gap /= 2) {
        // gap 만큼 떨어진 요소들을 삽입 정렬
        for (int i = gap; i < n; i++) {
            int temp = arr[i];
            int j = i;

            // gap 간격으로 앞쪽의 요소들과 비교하며 정렬
            while (j >= gap && arr[j - gap] > temp) {
                arr[j] = arr[j - gap];
                j -= gap;
            }

            arr[j] = temp;
        }
    }
}
```