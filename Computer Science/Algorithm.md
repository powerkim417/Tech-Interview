# Algorithm 알고리즘

## 정렬 시간복잡도 표

|                |        Best case        | Average case  |            Worst case            | Stable?  |
| :------------: | :---------------------: | :-----------: | :------------------------------: | :------: |
|  Bubble Sort   |        $O(N^2)$         |   $O(N^2)$    |             $O(N^2)$             |  Stable  |
| Selection Sort |        $O(N^2)$         |   $O(N^2)$    |             $O(N^2)$             | Unstable |
| Insertion Sort | $O(N)$<br />정렬된 경우 |   $O(N^2)$    | $O(N^2)$<br />역으로 정렬된 경우 |  Stable  |
|   Quick Sort   |      $O(N\log{N})$      | $O(N\log{N})$ |  $O(N^2)$<br />이미 정렬된 경우  | Unstable |
|   Merge Sort   |      $O(N\log{N})$      | $O(N\log{N})$ |          $O(N\log{N})$           |  Stable  |
|   Heap Sort    |      $O(N\log{N})$      | $O(N\log{N})$ |          $O(N\log{N})$           | Unstable |

## Bubble Sort(거품 정렬)

### Goal

- [ ] Bubble Sort에 대해 설명할 수 있다.
- [ ] Bubble Sort 과정에 대해 설명할 수 있다.
- [ ] Bubble Sort을 구현할 수 있다.
- [ ] Bubble Sort의 시간복잡도와 공간복잡도를 계산할 수 있다.

### 설명

- 인접한 두 원소의 대소를 비교하여, 조건에 맞지 않는다면 두 원소의 자리를 교환하며 정렬하는 알고리즘
- (오름차순 기준) 첫번째 시행이 끝나면 가장 큰 원소가 가장 오른쪽에 위치하게 됨

![img](https://github.com/GimunLee/tech-refrigerator/raw/master/Algorithm/resources/bubble-sort-001.gif)

### 시간복잡도

- $(n-1) + (n-2) + ... + 1=\dfrac{n(n-1)}{2}$ 이므로 $O(n^2)$

- 조건에 맞는지 여부를 떠나서 2개의 원소를 항상 비교하므로 ==Best, Average, Worst가 모두 $O(n^2)$==

### 공간복잡도

- 주어진 배열 안에서 swap을 통해 정렬을 하므로 ==$O(n)$==