# 99클럽 코테 스터디 31일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 백준 → [점프 점프](https://www.acmicpc.net/problem/14248)

### 풀이 접근 방식
- DFS로 접근
  ```java
  public static void main(String[] args) throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      int n = Integer.parseInt(br.readLine());
      int[] jumps = Arrays.stream(br.readLine().split(" "))
                          .mapToInt(Integer::parseInt)
                          .toArray();
      int s = Integer.parseInt(br.readLine());

      boolean[] visited = new boolean[n];
      dfs(s - 1, jumps, visited);

      int answer = 0;
      for (boolean v : visited) {
          if (v) answer++;
      }

      System.out.println(answer);
  }

  private static void dfs(int start, int[] jumps, boolean[] visited) {
      if (visited[start]) return;

      int jump = jumps[start];
      visited[start] = true;

      if (start - jump >= 0) {
          dfs(start - jump, jumps, visited);
      }

      if (start + jump < jumps.length) {
          dfs(start + jump, jumps, visited);
      }
  }
  ```
  - DFS 방식으로 접근 → 방문하지 않은 돌이라면 좌우로 점프할 수 있는지 확인하며 반복
### 오늘의 회고 
    - 드디어 DFS/BFS 유형 문제를 시간 내에 풀이 성공! 👊
    - 다만, 스스로 풀이를 완벽히 설명할 정도는 못 되는 것 같음..

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``