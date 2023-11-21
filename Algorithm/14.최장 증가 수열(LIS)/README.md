## 최장 증가 부분 수열(LIS, Longest Increasing Subsequence) [📌참고](https://rebro.kr/33)

원소가 n개인 배열의 일부 원소를 골라 만든 부분 수열 중, 각 원소가 이전 원소보다 크다는 조건을 만족하고, 그 길이가 최대인 부분 수열

{6, 2, 5, 1, 7, 4, 8, 3} -> {2, 5, 7 ,8}

### DP

- 시간 복잡도 O(n²)
- 입력 값의 크기가 작을 경우 유용
- 원소와 이전 원소들의 비교하며 원소들 중에서 i번째 원소보다 작은 원소들 중 DP값이 가장 큰 값에 + 1을 하여 dp[i]의 값을 도출

```java
import java.util.Arrays;

public class LIS_DP {
    public static void main(String[] args) {
        int arr[] = {3, 2, 4, 1, 6};
        int dp[] = new int[arr.length];
        dp[0] = 1; // LIS의 첫 번째는 항상 1이다.

        for (int i = 1; i < arr.length; i++) {
            // 첫 원소부터 i원소 전까지 비교
            for (int j = 0; j < i; j++) {
                if (arr[j] < arr[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
                //  증가 부분 수열의 길이는 1부터 시작하므로 0인 값을 1으로 변경해준다.
                if (dp[i] == 0) {
                    dp[i] = 1;
                }
            }
        }

        System.out.println("arr : " + Arrays.toString(arr));
        System.out.println("DP  : " + Arrays.toString(dp));
    }
}
```

- length[i] 는 i번째 인덱스에서 끝나는 최장 증가 부분 수열의 길이

1. 주어진 배열에서 인덱스를 한 칸씩(k+=1) 늘려가면서 확인
2. 내부 반복문으로 k보다 작은 인덱스들을 하나씩 살펴 보면서 arr[i] < arr[k]인 것이 있을 경우, length[k] 를 업데이트

#### 업데이트 기준

아래 둘 중에 더 큰 값으로 length[k] 값을 업데이트

- i번째 인덱스에서 끝나는 최장 증가 부분 수열의 마지막에 arr[k]를 추가했을 때의 LIS 길이
- 추가하지 않고 기존의 length[k] 값

### 이분탐색

- 시간 복잡도 O(nlogn)
- 이분 탐색을 활용하는 경우에는 정확한 LIS가 아닌 LIS의 길이를 구할 때 사용
  ![list_](https://github.com/Fun-Fun-Study/CS-Study/assets/18045556/5a1ec129-7a30-410f-92bb-d3b791e62876)

#### LIS의 길이를 구하는 방법

```java
import java.util.Arrays;

public class LIS_Binarysearch {
    public static void main(String args[]) {
        int[] arr = {3, 5, 7, 9, 2, 1, 4, 8};
        int size = arr.length;

        System.out.println("arr : " + Arrays.toString(arr));
        System.out.println("LIS 길이 : " + binarySearch(arr, size));
    }

    public static int binarySearch(int[] arr, int size) {
        int[] lis = new int[size + 1];    // 가장 긴 증가하는 부분 수열. 가장 뒤에 있는 값은 부분 수열 중 가장 최댓값
        int start = 0;
        lis[start++] = arr[0]; // lis[start] 값을 arr[i]로 변경하고 1증가시킨다.

        for (int i = 1; i < size; i++) {
            // lis값의 맨 마지막 원소가 arr[i] 보다 작을 경우
            if (lis[start - 1] < arr[i]) {
                lis[start++] = arr[i]; // 해당 원소를 arr[i]값으로 변경하고 start를 1 증가 시킨다.
            } else {
                int end = 0;
                while (start <= end) {
                    int mid = start + (end - start) / 2;

                    if (arr[mid] == arr[i]) {
                        return mid;
                    }
                    if (arr[mid] < arr[i]) {
                        start = mid + 1;
                    }
                    if (arr[mid] > arr[i]) {
                        end = mid - 1;
                    }
                }
                // start < end 일 경우 lis[start]의 값은 arr[i]의 값이 된다.
                lis[start] = arr[i];
            }
        }

        return start;
    }
}
```
