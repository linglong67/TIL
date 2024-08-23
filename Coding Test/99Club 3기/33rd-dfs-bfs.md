# 99클럽 코테 스터디 33일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 프로그래머스 → [리코쳇 로봇](https://school.programmers.co.kr/learn/courses/30/lessons/169199)

### 풀이 접근 방식
- BFS로 접근
  ```java
  public int solution(String[] board) {
      // 방향 벡터: 상, 하, 좌, 우
      int[] dx = {0, 0, -1, 1};
      int[] dy = {-1, 1, 0, 0};
  
      int rows = board.length;
      int cols = board[0].length();
      
      // 각 위치까지의 최소 이동 거리를 저장할 배열, 초기값은 -1로 설정
      int[][] dist = new int[rows][cols];
      for (int[] row : dist) {
          Arrays.fill(row, -1);
      }

      Queue<int[]> queue = new LinkedList<>();

      // 로봇(R)의 시작 위치를 찾아 큐에 추가하고, 해당 위치의 거리를 0으로 설정
      for (int i = 0; i < rows; i++) {
          for (int j = 0; j < cols; j++) {
              if (board[i].charAt(j) == 'R') {
                  queue.add(new int[]{i, j});
                  dist[i][j] = 0;
              }
          }
      }

      // BFS 탐색 시작
      while (!queue.isEmpty()) {
          int[] polled = queue.poll(); // 큐에서 현재 위치를 꺼냄
          int y = polled[0];
          int x = polled[1];

          // 상, 하, 좌, 우 네 방향에 대해 탐색
          for (int i = 0; i < 4; i++) {
              int ny = y;
              int nx = x;

              // 현재 방향으로 벽('D')이나 격자의 경계에 닿을 때까지 이동
              while (ny + dy[i] >= 0 && nx + dx[i] >= 0
                      && ny + dy[i] < rows && nx + dx[i] < cols
                      && board[ny + dy[i]].charAt(nx + dx[i]) != 'D') {
                  ny += dy[i];
                  nx += dx[i];
              }

              // 아직 방문하지 않은 위치라면 방문 처리하고, 큐에 추가
              if (dist[ny][nx] == -1) {
                  dist[ny][nx] = dist[y][x] + 1;
                  
                  // 목표 지점(G)에 도달하면, 그때의 거리 반환
                  if (board[ny].charAt(nx) == 'G') return dist[ny][nx];
                  
                  queue.add(new int[]{ny, nx});
              }
          }
      }

      // 목표 지점(G)에 도달할 수 없는 경우 -1 반환
      return -1;
  }
  ```
  - 문제를 읽고나서 로봇이 움직이는 방식을 바로 이해하지 못했음 -> 끝이나 장애물을 만나지 않으면 계속 나아감
  - 참고한 풀이를 봤을 때, 2번째 while문이 위 내용을 구현한 코드로 보임
### 오늘의 회고 
    - 시간 내에 풀지 못했고 이후에도 풀이를 바로 떠올리지 못하고 오답을 내는 상황이라 풀이를 검색함
    - 아직은 DFS/BFS 유형에서 조금의 응용도 쉽게 받아들이지 못하는 상태인 듯 😵‍💫

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``