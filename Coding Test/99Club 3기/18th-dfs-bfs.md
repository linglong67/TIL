# 99클럽 코테 스터디 18일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 백준 → [단지번호붙이기](https://www.acmicpc.net/problem/2667)

### 풀이 접근 방식
- BFS로 접근
  ```java
  private static int N;
  private static int[][] map;
  private static boolean[][] visited;
  private static int[] dx = {0, 0, -1, 1};
  private static int[] dy = {-1, 1, 0, 0};

  public static void main(String[] args) throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      N = Integer.parseInt(br.readLine());
      map = new int[N][N];
      visited = new boolean[N][N];

      for (int i = 0; i < N; i++) {
          map[i] = Arrays.stream(br.readLine().split(""))
                         .mapToInt(Integer::parseInt)
                         .toArray();
      }

      List<Integer> answer = new ArrayList<>();

      for (int i = 0; i < N; i++) {
          for (int j = 0; j < N; j++) {
              if (map[i][j] == 1 && !visited[i][j]) {
                  answer.add(bfs(i, j));
              }
          }
      }

      Collections.sort(answer);
      System.out.println(answer.size());
      answer.forEach(System.out::println);
  }

  public static int bfs(int y, int x) {
      Queue<int[]> queue = new LinkedList<>();
      queue.add(new int[]{y, x});
      visited[y][x] = true;
      int count = 1;

      while (!queue.isEmpty()) {
          int[] pos = queue.poll();

          for (int i = 0; i < 4; i++) {
              int ny = pos[0] + dy[i];
              int nx = pos[1] + dx[i];

              if (ny >= 0 && nx >= 0 && ny < N && nx < N) {
                  if (map[ny][nx] == 1 && !visited[ny][nx]) {
                      queue.add(new int[]{ny, nx});
                      visited[ny][nx] = true;
                      count++;
                  }
              }
          }
      }

      return count;
  }
  ```
  - 시간 내에 풀지 못함
  - ChatGPT를 통해 문제 풀이를 받아서 이해한 후 다시 풀어봄
  - DFS 방식도 사용한 자료구조 외에는 크게 다른 부분이 없었음
### 오늘의 회고
    - 이번 학습 키워드.. 쉽게 풀이를 떠올리지 못하겠음 😂 (어떡하지..?)

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``