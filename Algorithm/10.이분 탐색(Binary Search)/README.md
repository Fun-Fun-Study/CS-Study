# 👀 이분 탐색 (Binary Search)

> 순차적 탐색보다 빠른 탐색을 위해 나온 탐색 방법

**순차적 탐색**

- 정렬된 배열 안에서 특정 원소를 찾기 위해 인덱스 0부터 차례로 탐색
- 원소를 건너뛰는 일 없이 순차적으로 탐색

<br>

**이분 탐색**

- 정렬된 배열 안에서 특정 원소를 찾을 때 인덱스 i부터 j의 중간값과 비교
- 중간값이 찾는 원소가 아니라면 인덱스 i와 j를 다시 정해줌
- 인덱스 i와 j를 정할 때마다 탐색 범위가 반으로 줄어든다.

<br>

## 이분 탐색 방법

1. 처음 범위는 인덱스 0부터 끝까지이며, 중간 인덱스를 mid로 한다.

```java
int left = 0, right = n-1, mid = (left+right)/2;
```

2. mid의 값고 찾는 원소를 비교한다.

- 찾는 원소와 mid가 같으면 탐색을 종료한다.
- mid 값 < 찾는 원소 일 때 left는 mid+1로 이동시킨다.
- mid 값 > 찾는 원소 일 때 right는 mid-1로 이동시킨다.

3. 만약 right > left 가 된다면 해당 배열에는 찾는 원소가 없는 것이다.

<br>

## 시간 복잡도

⏰ 순차적 탐색 - 최악의 경우 배열의 끝까지 탐색해야 하므로 O(n)
⏰ 이분 탐색 - 범위를 새로 정할 때마다 탐색 범위는 1/2로 줄어든다. O(log n)

<br><br>

### 문제

[입국심사](https://school.programmers.co.kr/learn/courses/30/lessons/43238)

```java
import java.io.*;
import java.util.*;

class Solution {
    public long solution(int n, int[] times) {
        Arrays.sort(times);
        int size = times.length;
        long min = 0, max = (long)times[size-1]*n;
        while(min<=max){
            long mid = (min+max)/2, tmp = 0;

            for(int i=0;i<size;i++)
                tmp+=mid/times[i];

            if(tmp>=n) max = mid-1;
            else min = mid+1;
        }

        return min;
    }
}
```
