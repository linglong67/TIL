# 99클럽 코테 스터디 32일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 프로그래머스 → [무인도 여행](https://school.programmers.co.kr/learn/courses/30/lessons/154540)

### 풀이 접근 방식
- DFS로 접근
  ```java
  private int[] dx = {0, 0, -1, 1};
  private int[] dy = {-1, 1, 0, 0};
  private boolean[][] visited;

  public int[] solution(String[] maps) {
      int mapsLen = maps.length;
      int mapLen = maps[0].length();
      visited = new boolean[mapsLen][mapLen];
      int[][] numMap = new int[mapsLen][mapLen];

      for (int i = 0; i < mapsLen; i++) {
          for (int j = 0; j < mapLen; j++) {
              int num = maps[i].charAt(j) - '0';
              numMap[i][j] = num < 10 ? num : 0;
          }
      }

      List<Integer> list = new ArrayList<>();
      for (int i = 0; i < mapsLen; i++) {
          for (int j = 0; j < mapLen; j++) {
              if (numMap[i][j] == 0 || visited[i][j]) continue;

              int count = dfs(i, j, numMap);
              if (count > 0) list.add(count);
          }
      }

      return list.isEmpty() ? new int[]{-1} : list.stream().sorted().mapToInt(Integer::intValue).toArray();
  }

  private int dfs(int y, int x, int[][] numMap) {
      if (visited[y][x]) return 0;
      visited[y][x] = true;

      int count = numMap[y][x];
      for (int i = 0; i < dy.length; i++) {
          int ny = y + dy[i];
          int nx = x + dx[i];

          if (ny >= 0 && nx >= 0 && ny < numMap.length && nx < numMap[0].length && numMap[ny][nx] > 0 && !visited[ny][nx]) {
              count += dfs(ny, nx, numMap);
          }
      }

      return count;
  }
  ```
  - 접근은 거의 했지만 몇 가지 포인트에서 정답과 멀어짐
    1) visited[y][x] = true → 루프 안에 존재했음 (* 루프 밖으로 이동)
    2) count 값을 dfs 결과로 반환하지 않았음 (* dfs 반환값으로 변경)
    3) dfs 종료 조건이 잘못됨 → 4개의 방향 중 어느 한 방향으로 더 갈 수 없거나 막혔다면 0 반환 
       (* 반대로 dfs 할 수 있는 조건을 정하고 dfs 메서드 호출)
  - 결과적으로는 시간 내 풀이를 마치지 못하고 잘못된 부분에 대해 ChatGPT를 통해 개선했음
  - 그래도 접근 방향에 대해서는 어느 정도 감을 잡았다는 느낌이 들어 그 부분은 만족 😅
- (그 외) 다른 사람 풀이 → DFS (ChatGPT)
  ```java
  // 방향 벡터 (상, 하, 좌, 우)
  private static final int[] dx = {-1, 1, 0, 0};
  private static final int[] dy = {0, 0, -1, 1};

  // 지도와 방문 여부를 나타내는 배열
  private static char[][] map;
  private static boolean[][] visited;
  private static int rows, cols;

  public int[] solution(String[] maps) {
      rows = maps.length;
      cols = maps[0].length();
      map = new char[rows][];
      visited = new boolean[rows][cols];

      // 지도 초기화
      for (int i = 0; i < rows; i++) {
          map[i] = maps[i].toCharArray();
      }

      List<Integer> foodList = new ArrayList<>();

      // 모든 위치를 탐색
      for (int i = 0; i < rows; i++) {
          for (int j = 0; j < cols; j++) {
              if (!visited[i][j] && map[i][j] != 'X') {
                  // 새로운 무인도를 발견하면 DFS로 식량 합산
                  int food = dfs(i, j);
                  foodList.add(food);
              }
          }
      }

      // 결과를 오름차순으로 정렬
      if (foodList.isEmpty()) {
          return new int[]{-1};
      }

      Collections.sort(foodList);
      return foodList.stream().mapToInt(i -> i).toArray();
  }

  // DFS를 사용하여 무인도의 총 식량을 계산
  private int dfs(int x, int y) {
      visited[x][y] = true;
      int food = map[x][y] - '0';

      // 네 방향으로 탐색
      for (int i = 0; i < 4; i++) {
          int nx = x + dx[i];
          int ny = y + dy[i];

          if (nx >= 0 && ny >= 0 && nx < rows && ny < cols && !visited[nx][ny] && map[nx][ny] != 'X') {
              food += dfs(nx, ny);
          }
      }

      return food;
  }
  ```
  - 기본적으로는 많이 다르진 않았지만, map 배열을 만드는 부분이 한결 간결해서 좋았음
  - dfs 호출 전에 visited[i][j]를 체크하기 때문에 dfs 메서드 내부에서는 if문을 두지 않는 것도 👍
- (그 외) 다른 사람 풀이 → BFS (ChatGPT)
  ```java
  public int[] solution(String[] maps) {
      ... (동일한 내용 생략)

      // 모든 위치를 탐색
      for (int i = 0; i < rows; i++) {
          for (int j = 0; j < cols; j++) {
              if (!visited[i][j] && map[i][j] != 'X') {
                  // 새로운 무인도를 발견하면 BFS로 식량 합산
                  int food = bfs(i, j);
                  foodList.add(food);
              }
          }
      }

      ...
  }

  // BFS를 사용하여 무인도의 총 식량을 계산
  private int bfs(int startX, int startY) {
      Queue<int[]> queue = new LinkedList<>();
      queue.add(new int[]{startX, startY});
      visited[startX][startY] = true;
      int totalFood = 0;

      while (!queue.isEmpty()) {
          int[] current = queue.poll();
          int x = current[0];
          int y = current[1];
          totalFood += map[x][y] - '0';

          // 네 방향으로 탐색
          for (int i = 0; i < 4; i++) {
              int nx = x + dx[i];
              int ny = y + dy[i];

              if (nx >= 0 && ny >= 0 && nx < rows && ny < cols && !visited[nx][ny] && map[nx][ny] != 'X') {
                  visited[nx][ny] = true;
                  queue.add(new int[]{nx, ny});
              }
          }
      }

      return totalFood;
  }
  ```
  - DFS처럼 재귀가 아니므로 while문 안에서 totalFood += map[x][y] - '0'와 visited[nx][ny] = true 처리
  - BFS 풀이도 익숙해지면 (지금의 나에겐) 재귀보다 사고하기 더 편할 것 같음 
### 오늘의 회고 
    - 전형적인 DFS/BFS 문제를 만난 듯
    - 풀 수 있을 것 같았는데 마무리까지 짓지 못해서 아쉬움이 남은 문제 🫠

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``