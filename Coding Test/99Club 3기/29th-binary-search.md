# 99클럽 코테 스터디 29일차 TIL + 이분탐색

### 학습 키워드
- 이분탐색

### 오늘의 문제
- 리트코드 → [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

### 풀이 접근 방식
- 이분탐색 방식 사용
  ```java
  public int lengthOfLIS(int[] nums) {
      if (nums == null || nums.length == 0) return 0;

      int size = 0;
      int[] result = new int[nums.length];

      for (int num : nums) {
          int left = 0;
          int right = size;

          while (left < right) {
              int mid = (left + right) / 2;
              if (result[mid] < num) {
                  left = mid + 1;
              } else {
                  right = mid;
              }
          }

          result[left] = num;
          if (left == size) size++;
      }

      return size;
  }
  ```
  - 직접 풀진 못해서 풀이를 참고함 → 조금 더 복잡하지만 시간 복잡도가 낮고 효율적인 방식
- (그 외) 다른 사람 풀이
  ```java
  public int lengthOfLIS(int[] nums) {
      if (nums == null || nums.length == 0) return 0;
  
      int n = nums.length;
      int[] dp = new int[n];
      int maxLength = 1;
  
      for (int i = 0; i < n; i++) {
          dp[i] = 1;
  
          for (int j = 0; j < i; j++) {
              if (nums[i] > nums[j]) {
                  dp[i] = Math.max(dp[i], dp[j] + 1);
              }
          }
          maxLength = Math.max(maxLength, dp[i]);
      }
  
      return maxLength;
  }
  ```
  - DP 방식 사용 → 좀 더 직관적이고 이해가 쉽지만 시간 복잡도가 올라감
### 오늘의 회고
    - 문제 내용이 짧고 단순해 보였지만 풀이가 쉽지 않게 느껴졌음 😵‍💫
    - 아직 이분탐색 활용은 쉽지 않다.. 쉽지 않아 🥲

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``