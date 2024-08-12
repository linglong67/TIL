# 99클럽 코테 스터디 22일차 TIL + 동적계획법

### 학습 키워드
- 동적계획법

### 오늘의 문제
- 프로그래머스 → [멀리 뛰기](https://school.programmers.co.kr/learn/courses/30/lessons/12914)

### 풀이 접근 방식
- DP 메모이제이션 방식 사용
  ```java
  private final int[] dp = new int[2001];

  public int jump(int n) {
      if (dp[n] != -1) return dp[n];
      if (n < 3) return n;

      dp[n] = (jump(n - 2) + jump(n - 1)) % 1234567;

      return dp[n];
  }

  public long solution(int n) {
      Arrays.fill(dp, -1);

      return jump(n);
  }
  ```
  - 어제 문제 풀이와 크게 다를 게 없었음
  - _n 증가에 따른 멀리 뛰기 방법의 수_ 규칙을 알아내면 끝-!
### 오늘의 회고
    - 비슷한 문제가 나와서 전날 풀었던 문제에 대한 복습이 되는 것 같아 좋았다! 😊

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``