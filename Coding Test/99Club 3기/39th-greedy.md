# 99클럽 코테 스터디 39일차 TIL + Greedy

### 학습 키워드
- Greedy

### 오늘의 문제
- 프로그래머스 → [광물 캐기](https://school.programmers.co.kr/learn/courses/30/lessons/172927)

### 풀이 접근 방식
- 우선순위 큐를 사용한 풀이
  ```java
  public int solution(int[] picks, String[] minerals) {
      int diamondCnt = 0;
      int ironCnt = 0;
      int stoneCnt = 0;
      PriorityQueue<Group> pq = new PriorityQueue<>();
      int picksSum = Arrays.stream(picks).sum();

      for (int i = 0; i < minerals.length; i++) {
          if (picksSum == pq.size()) {
              break;
          }

          if (minerals[i].equals("diamond")) {
              diamondCnt++;
          } else if (minerals[i].equals("iron")) {
              ironCnt++;
          } else {
              stoneCnt++;
          }

          if (i % 5 == 4 || i == minerals.length - 1) {
              pq.add(new Group(diamondCnt, ironCnt, stoneCnt));
              diamondCnt = 0;
              ironCnt = 0;
              stoneCnt = 0;
          }
      }

      int answer = 0;
      while (!pq.isEmpty()) {
          Group polled = pq.poll();

          if (picks[0] > 0) {
              answer += (polled.diamond + polled.iron + polled.stone);
              picks[0]--;
          } else if (picks[1] > 0) {
              answer += (polled.diamond * 5 + polled.iron + polled.stone);
              picks[1]--;
          } else if (picks[2] > 0) {
              answer += (polled.diamond * 25 + polled.iron * 5 + polled.stone);
              picks[2]--;
          }
      }

      return answer;
  }

  static class Group implements Comparable<Group> {
      int diamond;
      int iron;
      int stone;

      public Group(int diamond, int iron, int stone) {
          this.diamond = diamond;
          this.iron = iron;
          this.stone = stone;
      }

      @Override
      public int compareTo(Group o) {
          if (this.diamond != o.diamond) {
              return o.diamond - this.diamond;
          }

          if (this.iron != o.iron) {
              return o.iron - this.iron;
          }

          if (this.stone != o.stone) {
              return o.stone - this.stone;
          }

          return 0;
      }
  }
  ```
  - 광물들을 5개씩 나눠 우선순위에 맞게 정렬 후 최소 피로도 계산하도록 구현
  - 전체 곡괭이 수가 큐의 개수와 같아진다면 더이상의 그룹은 만들지 않아야 함 (제약을 두지 않으면 테스트케이스에 걸림)
### 오늘의 회고
    - 시간은 조금 초과했으나 어제 문제 풀이 방식을 응용해서 풀어낼 수 있어서 좋았음
    - 우선순위 큐에 대한 복습이 되어 앞으로는 더 기억이 잘 날 듯! 

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``