# 99클럽 코테 스터디 1일차 TIL + 배열

### 학습 키워드
- 배열

### 오늘의 문제
- 프로그래머스 → [n^2 배열 자르기](https://school.programmers.co.kr/learn/courses/30/lessons/87390)

### 풀이 접근 방식
- 1차 시도 (단순 브루트포스 방식 → 메모리 초과 🫨)
  ```java
  public int[] solution(int n, long left, long right) {
      int[][] arr = new int[n][n];

      for (int i = 0; i < n; i++) {
          Arrays.fill(arr[i], i + 1);
          for (int j = i; j < n; j++) {
              arr[i][j] = j + 1;
          }
      }

      int[] flatArr = Arrays.stream(arr).flatMapToInt(Arrays::stream).toArray();
      int[] answer = new int[(int) (right - left + 1)];

      int index = 0;
      for (int i = (int) left; i <= right; i++) {
          answer[index++] = flatArr[i];
      }

      return answer;
  }
  ```
- 2차 시도 (식을 세워 접근)
  ```java
  public int[] solution(int n, long left, long right) {
      int[] answer = new int[(int) (right - left + 1)];

      int index = 0;
      for (long i = left; i <= right; i++) {
          long x = i / n;
          long y = i % n;

          answer[index++] = (int) Math.max(x, y) + 1;
      }

      return answer;
  }
  ```
    (사실 이 와중에 원래 ``int x = (int) i / n``처럼 써서 실패..)

### 오늘의 회고
    - 지난 번보다 레벨을 한 단계 올렸는데 바로 차이가 느껴져서 조금 당황스러웠다. (역시 아직 갈 길이 멀어 🥲)
    - 1차 시도 후에 문제해결은 이중 for문이 아닌 단일로 해야한다는 건 알았지만 바로 식이 떠오르지 않아 다른 글들을 조금씩 참고하게 되었다.
    - 배열 만만하게 보지 말자..
    - 주어진 값의 범위를 보고 구현할 방식을 좀 더 고민해볼 것!

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``