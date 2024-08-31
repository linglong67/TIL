# 99클럽 코테 스터디 40일차 TIL + 동적계획법

### 학습 키워드
- 동적계획법

### 오늘의 문제
- 리트코드 → [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/description/)

### 풀이 접근 방식
- DP 메모이제이션 방식 사용
  ```java
  public int uniquePathsWithObstacles(int[][] obstacleGrid) {
      int m = obstacleGrid.length;
      int n = obstacleGrid[0].length;
      
      // dp 테이블 초기화
      int[][] dp = new int[m][n];
      
      // 시작 위치에 장애물이 있다면 경로는 0입니다.
      if (obstacleGrid[0][0] == 1) {
          return 0;
      }
      
      // 시작 위치에 경로를 1로 설정
      dp[0][0] = 1;
      
      // 첫 번째 열의 dp 값을 설정
      for (int i = 1; i < m; i++) {
          dp[i][0] = (obstacleGrid[i][0] == 1) ? 0 : dp[i-1][0];
      }
      
      // 첫 번째 행의 dp 값을 설정
      for (int j = 1; j < n; j++) {
          dp[0][j] = (obstacleGrid[0][j] == 1) ? 0 : dp[0][j-1];
      }
      
      // 나머지 dp 값을 설정
      for (int i = 1; i < m; i++) {
          for (int j = 1; j < n; j++) {
              if (obstacleGrid[i][j] == 1) {
                  dp[i][j] = 0;
              } else {
                  dp[i][j] = dp[i-1][j] + dp[i][j-1];
              }
          }
      }
      
      // 도착 지점의 경로 수를 반환
      return dp[m-1][n-1];
  }
  ```
  - 풀이는 떠올렸는데 시간 내에 구현을 못함 🥲
  - 어제 문제에서 살짝 달라졌는데 못 풀어내서 아쉽다..
### 오늘의 회고
    - 이 문제 풀이는 다시 읽어보고 스스로 풀어보자!

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``