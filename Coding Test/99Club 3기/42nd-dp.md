# 99클럽 코테 스터디 42일차 TIL + 동적계획법

### 학습 키워드
- 동적계획법

### 오늘의 문제
- 리트코드 → [First Day Where You Have Been in All the Rooms](https://leetcode.com/problems/first-day-where-you-have-been-in-all-the-rooms/description/)

### 풀이 접근 방식
- DP 메모이제이션 방식 사용
  ```java
  public int firstDayBeenInAllRooms(int[] nextVisit) {
      int mod = 1_000_000_007;
      int size = nextVisit.length;
      long[] dp = new long[size];
      dp[0] = 0;

      for (int i = 1; i < size; i++) {
          dp[i] = (dp[i - 1] + 2 + dp[i - 1] - dp[nextVisit[i - 1]] + mod) % mod;
      }

      return (int) dp[size - 1];
  }
  ```
  - 시간 내에 구현을 못함 🥲
  - 규칙을 알고 나니 dp를 구하는 계산식은 생각보다 간단한 편 
### 오늘의 회고
    - 지난 며칠동안 dp를 사용하면서 익숙해진 느낌이 듦 🤭
    - 그래도 좀 더 익숙해져야 풀이를 떠울리기 용이할 듯!

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``