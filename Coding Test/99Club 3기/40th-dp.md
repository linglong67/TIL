# 99클럽 코테 스터디 40일차 TIL + 동적계획법

### 학습 키워드
- 동적계획법

### 오늘의 문제
- 리트코드 → [Unique Paths](https://leetcode.com/problems/unique-paths/description/)

### 풀이 접근 방식
- DP 메모이제이션 방식 사용
  ```java
  private final int[][] dp = new int[101][101];

  public int uniquePaths(int m, int n) {
      return move(m - 1, n - 1);
  }

  private int move(int y, int x) {
      if (y == 0 || x == 0) {
          return 1;
      }

      if (dp[y][x] != 0) {
          return dp[y][x];
      }

      dp[y][x] = move(y, x - 1) + move(y - 1, x);

      return dp[y][x];
  }
  ```
  - 풀이를 떠올리고 난 후에는 생각보다 어렵지 않게 풀어낼 수 있었음
  - 어떤 부분을 DP로 풀어낼 것인지만 잘 떠올릴 수 있다면 될 듯
### 오늘의 회고
    - 문제가 조금 쉬웠던 편이었을지 모르지만 시간 내에 잘 풀어서 뿌듯 😊
    - 전보다 DP 문제 접근이 편해진 느낌

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``