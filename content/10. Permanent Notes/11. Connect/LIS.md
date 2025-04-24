---
CMDS: "[[103 Algorithm]]"
creation date: 2025-04-08 11:30
modification date: 2025-04-08 11:30:56
type:
  - note
tags:
  - "#LIS"
관련 문서:
  - "[[DP]]"
category: content
---

# LIS

<center><i><b>L</b>ongest <b>I</b>ncreasing <b>S</b>ubsequence</i></center>

### 개요
최장 증가 부분 수열(LIS)은 주어진 수열에서 원소들의 순서를 유지하면서 증가하는 부분 수열 중 가장 긴 것을 찾는 알고리즘입니다. LIS는 여러 응용 분야에서 활용되며, 대표적으로 데이터 분석, 생물정보학, 최적화 문제 등에 사용됩니다.

### 예시
예를 들어, 다음과 같은 수열이 주어졌다고 합시다:

```
수열: 10, 9, 2, 5, 3, 7, 101, 18
```

이 수열의 LIS는 `2, 3, 7, 101`로 길이는 4입니다. 이 부분 수열은 원래 수열에서 순서를 유지하면서 증가하고 있으며, 가능한 가장 긴 길이를 가지고 있습니다.

### LIS 알고리즘 구현 방법
LIS 알고리즘은 동적 계획법(Dynamic Programming, DP)을 사용하여 효율적으로 구현할 수 있습니다. 기본적인 접근 방식은 다음과 같습니다:

1. 각 원소에서 끝나는 LIS의 길이를 계산하기 위해 DP 배열을 사용합니다.
2. 배열의 각 요소에 대해, 이전의 모든 요소를 확인하고 현재 요소보다 작은 요소들 중 가장 긴 LIS에 현재 요소를 추가하여 새로운 LIS 길이를 갱신합니다.
3. 모든 요소에 대해 이 과정을 반복한 후, DP 배열에서 가장 큰 값을 찾습니다.

#### 시간 복잡도
기본적인 동적 계획법을 사용한 LIS 알고리즘의 시간 복잡도는 O(N²)입니다. 하지만 이보다 더 효율적인 O(N log N) 시간 복잡도를 가지는 알고리즘도 존재합니다.

### Java로 LIS 알고리즘 구현하기

아래는 동적 계획법을 사용하여 LIS를 구하는 Java 코드입니다.

```java
import java.util.Arrays;

public class LongestIncreasingSubsequence {
    public static int lengthOfLIS(int[] nums) {
        if(nums == null || nums.length == 0) return 0;
        
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1); // 각 요소는 최소한 자기 자신으로 이루어진 수열을 가짐
        
        for(int i = 1; i < n; i++) {
            for(int j = 0; j < i; j++) {
                if(nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        // dp 배열에서 가장 큰 값을 찾음
        int max = 1;
        for(int length : dp) {
            if(length > max) {
                max = length;
            }
        }
        return max;
    }
    
    // LIS의 실제 수열을 추적하는 함수
    public static int[] getLIS(int[] nums) {
        if(nums == null || nums.length == 0) return new int[0];
        
        int n = nums.length;
        int[] dp = new int[n];
        int[] prev = new int[n];
        Arrays.fill(dp, 1);
        Arrays.fill(prev, -1);
        
        for(int i = 1; i < n; i++) {
            for(int j = 0; j < i; j++) {
                if(nums[j] < nums[i] && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                    prev[i] = j;
                }
            }
        }
        
        // dp 배열에서 가장 큰 값과 그 인덱스를 찾음
        int max = 1;
        int index = 0;
        for(int i = 1; i < n; i++) {
            if(dp[i] > max) {
                max = dp[i];
                index = i;
            }
        }
        
        // LIS를 역추적하여 저장
        int[] lis = new int[max];
        int k = max - 1;
        while(index != -1) {
            lis[k--] = nums[index];
            index = prev[index];
        }
        
        return lis;
    }
    
    public static void main(String[] args) {
        int[] sequence = {10, 9, 2, 5, 3, 7, 101, 18};
        
        // LIS의 길이 구하기
        int length = lengthOfLIS(sequence);
        System.out.println("LIS의 길이: " + length); // 출력: 4
        
        // 실제 LIS 수열 구하기
        int[] lis = getLIS(sequence);
        System.out.print("LIS 수열: ");
        for(int num : lis) {
            System.out.print(num + " ");
        }
        // 출력: LIS 수열: 2 3 7 101 
    }
}
```

### 코드 설명

1. **lengthOfLIS 함수:**
   - **입력:** 정수 배열 `nums`.
   - **출력:** LIS의 길이.
   - **동작:** 각 위치 `i`에 대해, 이전의 모든 위치 `j`를 확인하고 `nums[j] < nums[i]`인 경우 `dp[i]`를 업데이트합니다. 최종적으로 `dp` 배열의 최대값이 LIS의 길이입니다.

2. **getLIS 함수:**
   - **입력:** 정수 배열 `nums`.
   - **출력:** 실제 LIS 수열을 담은 배열.
   - **동작:** `prev` 배열을 사용하여 각 위치에서 이전에 어떤 요소가 LIS를 이루는지 추적합니다. 최종적으로 역추적하여 LIS 수열을 구성합니다.

3. **main 함수:**
   - 예시 수열 `[10, 9, 2, 5, 3, 7, 101, 18]`에 대해 LIS의 길이와 실제 수열을 출력합니다.

### 최적화된 O(N log N) 알고리즘
위의 구현은 O(N²) 시간 복잡도를 가지지만, 이보다 더 효율적인 O(N log N) 알고리즘을 구현하는 것도 가능합니다. 이 알고리즘은 이진 탐색을 활용하여 `dp` 배열을 관리합니다. 그러나 기본적인 이해를 위해 먼저 O(N²) 구현을 익히는 것이 좋습니다.

#### 예시 코드 (O(N log N) 알고리즘)

```java
import java.util.Arrays;

public class LongestIncreasingSubsequenceOptimized {
    public static int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        int len = 0;
        for(int num : nums) {
            int i = Arrays.binarySearch(dp, 0, len, num);
            if(i < 0) i = -(i + 1);
            dp[i] = num;
            if(i == len) len++;
        }
        return len;
    }
    
    public static void main(String[] args) {
        int[] sequence = {10, 9, 2, 5, 3, 7, 101, 18};
        int length = lengthOfLIS(sequence);
        System.out.println("최적화된 LIS의 길이: " + length); // 출력: 4
    }
}
```

### 요약
- **LIS 알고리즘**은 주어진 수열에서 증가하는 부분 수열 중 가장 긴 것을 찾는 알고리즘입니다.
- **동적 계획법**을 사용하여 O(N²) 시간 복잡도로 구현할 수 있으며, `dp` 배열을 사용하여 각 위치에서의 LIS 길이를 저장합니다.
- **O(N log N)** 시간 복잡도의 최적화된 알고리즘도 존재하지만, 기본적인 동적 계획법을 이해하는 것이 선행되어야 합니다.
- **Java 구현**에서는 `Arrays` 클래스를 활용하여 배열을 관리하고, 이진 탐색을 통해 효율적인 LIS 길이 계산이 가능합니다.

위의 예제 코드를 통해 LIS 알고리즘의 동작 원리와 구현 방법을 이해할 수 있을 것입니다. 필요에 따라 추가적인 최적화나 기능을 구현하여 활용할 수 있습니다.