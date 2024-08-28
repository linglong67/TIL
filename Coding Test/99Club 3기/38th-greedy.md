# 99클럽 코테 스터디 38일차 TIL + Greedy

### 학습 키워드
- Greedy

### 오늘의 문제
- 프로그래머스 → [디펜스 게임](https://school.programmers.co.kr/learn/courses/30/lessons/142085)

### 풀이 접근 방식
- 최대힙을 사용한 풀이
  ```java
  public int solution(int n, int k, int[] enemy) {
      int answer = 0;
      int sum = 0;
      PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);

      for (int e : enemy) {
          answer++;
          sum += e;
          pq.add(e);

          if (sum <= n) continue;

          if (k > 0) {
              sum -= pq.remove();
              k--;
              continue;
          }

          answer--;
          break;
      }

      return answer;
  }
  ```
  - Math.max → List.sort → PriorityQueue 사용으로 점차 풀이를 개선함
  - 1번째에서는 최대값을 제대로 가져올 수 없는 경우가 있었고, 2번째는 시간 초과 이슈 발생했음
- (그 외) 다른 사람 풀이 → 최소힙 (ChatGPT)
  ```java
  public int solution(int n, int k, int[] enemy) {
      PriorityQueue<Integer> pq = new PriorityQueue<>(); // 최소 힙 (적 수가 작은 순서대로 정렬)
      
      for (int i = 0; i < enemy.length; i++) {
          pq.offer(enemy[i]); // 현재 라운드의 적의 수를 큐에 추가
          if (pq.size() > k) {
              n -= pq.poll(); // 가장 적은 수의 적을 실제로 병사로 막음
          }
          
          if (n < 0) {
              return i; // 병사 수가 부족해 더 이상 방어할 수 없는 라운드를 반환
          }
      }
      
      return enemy.length; // 모든 라운드를 방어할 수 있으면 전체 라운드 수를 반환
  }
  ```
  - (나와 반대로) 최소힙을 사용
  - 이 로직을 생각할 수 있었다면 for문 구현이 좀 더 간결해지는 장점이 있는 듯 
### 오늘의 회고
    - 오늘은 시간 안에 풀이를 개선하면서 해결할 수 있었음
    - 우선순위 큐를 바로 떠올리지 못해서 시행착오를 일부 거쳤지만 그래도 결국엔 풀어내서 좋았음 🙂

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``