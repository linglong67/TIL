# 99클럽 코테 스터디 21일차 TIL + 동적계획법

### 학습 키워드
- 동적계획법

### 오늘의 문제
- 프로그래머스 → [피보나치 수](https://school.programmers.co.kr/learn/courses/30/lessons/12945)

### 풀이 접근 방식
- DP 메모이제이션 방식 사용
  ```java
  private final int[] dp = new int[100001];

  public int fibonacci(int n) {
      if (dp[n] != -1) return dp[n];
      if (n < 2) return n;

      dp[n] = (fibonacci(n - 2) + fibonacci(n - 1)) % 1234567;

      return dp[n];
  }

  public int solution(int n) {
      Arrays.fill(dp, -1);

      return fibonacci(n);
  }
  ```
  - 예전에 풀어봤던 문제인데 DP를 잘 모를 때 풀고 잊고 있었다..
  - 재귀로 계산한 값을 저장해 중복 계산을 막는 것이 포인트!
### 오늘의 회고
    - DP가 코테 유형에 많이 나오는 편이라고 알고 있는데 아직 미숙한 듯
    - 비슷한 유형의 문제를 많이 풀어보면서 익숙해져보기 👊

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``