# 99클럽 코테 스터디 30일차 TIL + 이분탐색

### 학습 키워드
- 이분탐색

### 오늘의 문제
- 리트코드 → [Find Right Interval](https://leetcode.com/problems/find-right-interval/description/)

### 풀이 접근 방식
- 이분탐색 방식 사용
  ```java
  public int[] findRightInterval(int[][] intervals) {
      int length = intervals.length;
      if (length == 1) {
          return intervals[0][0] == intervals[0][1] ? new int[]{0} : new int[]{-1};
      }

      Map<Integer, Integer> map = new HashMap<>();
      int[] startArr = new int[length];

      for (int i = 0; i < length; i++) {
          int startPoint = intervals[i][0];
          map.put(startPoint, i);
          startArr[i] = startPoint;
      }

      Arrays.sort(startArr);
      int[] answer = new int[length];

      for (int i = 0; i < length; i++) {
          int left = 0, right = startArr.length;

          while (left < right) {
              int mid = (left + right) / 2;

              if (startArr[mid] < intervals[i][1]) {
                  left = mid + 1;
              } else {
                  right = mid;
              }
          }

          answer[i] = left >= length ? -1 : map.get(startArr[left]);
      }

      return answer;
  }  
  ```
  - 오늘은 이분탐색을 사용해 시간 내 푸는 데에는 성공!
  - 시작점들로 배열을 만들어 정렬 후 탐색 범위로 잡고, 종료점 값들에 대해 각각 이분탐색 진행
- (그 외) 다른 사람 풀이
  ```java
  public int[] findRightInterval(int[][] intervals) {
      int n = intervals.length;
      int[] result = new int[n];

      // 구간의 시작점과 원래 인덱스를 저장한 배열 생성
      int[][] starts = new int[n][2];
      for (int i = 0; i < n; i++) {
          starts[i][0] = intervals[i][0]; // 시작점
          starts[i][1] = i; // 원래 인덱스
      }

      // 시작점을 기준으로 정렬
      Arrays.sort(starts, (a, b) -> a[0] - b[0]);

      // 각 구간에 대해 오른쪽 구간 찾기
      for (int i = 0; i < n; i++) {
          int end = intervals[i][1];

          int left = 0, right = n;
          while (left < right) {
              int mid = left + (right - left) / 2;
              if (starts[mid][0] >= end) {
                  right = mid;
              } else {
                  left = mid + 1;
              }
          }

          // 만약 찾았다면 원래 인덱스를 결과에 기록
          result[i] = (left < n) ? starts[left][1] : -1;
      }

      return result;
  }
  ```
  - ChatGPT를 통해 받은 다른 풀이 방식 → 사실 큰 틀에서는 다르지 않음
  - 개인적으로는 Map이 아닌 2차원 배열로 만든 부분이 좋았음
### 오늘의 회고
    - 어제 문제가 이분탐색이어서 오늘 문제를 조금 더 수월하게 접근할 수 있었던 것 같음 🙂
    - 그래도 아직 좀 더 익숙해질 필요는 있음!

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``