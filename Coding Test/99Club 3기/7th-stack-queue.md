# 99클럽 코테 스터디 7일차 TIL + 스택/큐

### 학습 키워드
- 스택/큐

### 오늘의 문제
- 프로그래머스 → [하노이의 탑](https://school.programmers.co.kr/learn/courses/30/lessons/12946)

### 풀이 접근 방식
- 재귀 함수 사용
  ```java
  public int[][] solution(int n) {
      int[][] answer = new int[(int) Math.pow(2, n) - 1][2];

      hanoi(n, 1, 3, 2, answer);

      return answer;
  }

  private int index = 0;
  private void hanoi(int n, int from, int to, int temp, int[][] answer) {
      if (n == 1) {
          answer[index++] = new int[]{from, to};
          return;
      }

      hanoi(n - 1, from, temp, to, answer);
      answer[index++] = new int[]{from, to};
      hanoi(n - 1, temp, to, from, answer);
  }
  ```
  - 1~3번 기둥이 있다고 할 때, 맨 아래 원판을 목표 지점에 가져다 놓는다고 하면 1→2, 1→3, 2→3 반복
    - 원판의 개수가 많아져도 1→2, 1→3, 2→3 동일하므로 이 부분이 재귀 대상
    - 이동 횟수는 2^n - 1

### 오늘의 회고
    - 난 역시 재귀에 취약한 것 같다.. 도저히 감이 안 와서 참고자료 찾아봄 🥲
    - 조금 이해하고 나니 할 만 했긴 하지만 그래도 몇일 뒤면 잊을 듯.. (다시 찾아서 해보자!)

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``