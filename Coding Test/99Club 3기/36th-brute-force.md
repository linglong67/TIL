# 99클럽 코테 스터디 36일차 TIL + 완전탐색

### 학습 키워드
- 완전탐색

### 오늘의 문제
- 프로그래머스 → [전력망을 둘로 나누기](https://school.programmers.co.kr/learn/courses/30/lessons/86971)

### 풀이 접근 방식
- BFS로 접근
  ```java
  public int solution(int n, int[][] wires) {
      int answer = n;

      List<List<Integer>> graph = new ArrayList<>();
      for (int i = 0; i <= n; i++) {
          graph.add(new ArrayList<>());
      }

      for (int[] wire : wires) {
          graph.get(wire[0]).add(wire[1]);
          graph.get(wire[1]).add(wire[0]);
      }

      for (int[] wire : wires) {
          graph.get(wire[0]).remove(Integer.valueOf(wire[1]));
          graph.get(wire[1]).remove(Integer.valueOf(wire[0]));

          int nodeCount = bfs(graph, n, wire[0]);

          answer = Math.min(answer, Math.abs(nodeCount - (n - nodeCount)));

          graph.get(wire[0]).add(wire[1]);
          graph.get(wire[1]).add(wire[0]);
      }

      return answer;
  }

  private int bfs(List<List<Integer>> graph, int n, int start) {
      boolean[] visited = new boolean[n + 1];
      Queue<Integer> queue = new LinkedList<>();
      queue.add(start);
      visited[start] = true;
      int count = 1;

      while (!queue.isEmpty()) {
          int polled = queue.poll();
          for (int neighbor : graph.get(polled)) {
              if (!visited[neighbor]) {
                  visited[neighbor] = true;
                  queue.add(neighbor);
                  count++;
              }
          }
      }

      return count;
  }
  ```
  - 직접 풀이하는 데에는 실패해서 다른 풀이를 참고했음 🥲
  - 전선을 끊고 두 전력망의 송전탑 개수 차이를 계산한 다음 재연결 및 끊는 과정을 반복해 최소값을 찾는 방식
### 오늘의 회고 
    - 완전탐색 키워드를 보자마자 바로 방심해서 DFS/BFS 풀이 방식을 바로 떠올리지 못함
    - 하.. 역시 아직 멀었다 🫠

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``