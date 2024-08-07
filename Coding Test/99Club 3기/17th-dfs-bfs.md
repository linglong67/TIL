# 99클럽 코테 스터디 17일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 백준 → [촌수계산](https://www.acmicpc.net/problem/2644)

### 풀이 접근 방식
- BFS로 접근
  ```java
  public static void main(String[] args) throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      int peopleCount = Integer.parseInt(br.readLine());
      int[] target = Arrays.stream(br.readLine().split(" "))
                           .mapToInt(Integer::parseInt)
                           .toArray();
      int relationCount = Integer.parseInt(br.readLine());

      List<List<Integer>> graph = new ArrayList<>();
      for (int i = 0; i <= peopleCount; i++) {
          graph.add(new ArrayList<>());
      }

      for (int i = 0; i < relationCount; i++) {
          int[] relation = Arrays.stream(br.readLine().split(" "))
                                 .mapToInt(Integer::parseInt)
                                 .toArray();
          graph.get(relation[0]).add(relation[1]);
          graph.get(relation[1]).add(relation[0]);
      }

      System.out.println(bfs(graph, target[0], target[1], peopleCount));
  }

  public static int bfs(List<List<Integer>> graph, int from, int to, int peopleCount) {
      Queue<int[]> queue = new LinkedList<>();
      queue.add((new int[]{from, 0}));

      boolean[] visited = new boolean[peopleCount + 1];
      visited[from] = true;

      while (!queue.isEmpty()) {
          int[] polled = queue.poll();
          int person = polled[0];
          int depth = polled[1];

          if (person == to) {
              return depth;
          }

          for (int neighbor : graph.get(person)) {
              if (!visited[neighbor]) {
                  visited[neighbor] = true;
                  queue.add(new int[]{neighbor, depth + 1});
              }
          }
      }

      return -1;
  }
  ```
  - BFS로 접근해서 풀이를 시작했으나 시간 내에 풀지 못함
  - 이후 ChatGPT에게 BFS 방식의 풀이를 받아서 일부 적용 후 성공!
- (그 외) ChatGPT의 DFS 풀이 활용
  ```java
  private static int answer = -1;
  
  public static void main(String[] args) {
      ... (동일 내용 생략)

      boolean[] visited = new boolean[peopleCount + 1];
      dfs(graph, target[0], target[1], visited, 0);
      System.out.println(answer);      
  }

  public static void dfs(List<List<Integer>> graph, int from, int to, boolean[] visited, int depth) {
      visited[from] = true;

      for (int neighbor : graph.get(from)) {
          if (!visited[neighbor]) {
              if (neighbor == to) {
                  answer = depth + 1;
                  return;
              }

              dfs(graph, neighbor, to, visited, depth + 1);
          }
      }
  }
  ```
  - DFS로 접근한 풀이로 일부 수정함
  - BFS 방식보다 실행시간이 조금 더 소요됨
### 오늘의 회고
    - 역시 지금의 난 DFS/BFS에 취약함.. 풀이를 보고는 어느 정도 이해하지만 스스로 풀기 쉽지 않음
    - 개념과 동일 유형 문제 풀이를 많이 접해봐야할 것 같음 😵‍💫

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``