# 99클럽 코테 스터디 35일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 프로그래머스 → [게임 맵 최단거리](https://school.programmers.co.kr/learn/courses/30/lessons/1844)

### 풀이 접근 방식
- BFS로 접근
  ```java
  public int solution(int[][] maps) {
      int[] dx = {0, 0, -1, 1};
      int[] dy = {-1, 1, 0, 0};
      int rows = maps.length;
      int cols = maps[0].length;
      boolean[][] visited = new boolean[rows][cols];

      Queue<int[]> queue = new LinkedList<>();
      queue.add(new int[]{0, 0, 1});

      while (!queue.isEmpty()) {
          int[] polled = queue.poll();
          int y = polled[0];
          int x = polled[1];
          int dist = polled[2];

          if (y == rows - 1 && x == cols - 1) {
              return dist;
          }

          if (visited[y][x]) continue;
          visited[y][x] = true;

          for (int i = 0; i < dx.length; i++) {
              int ny = y + dy[i];
              int nx = x + dx[i];

              if (ny >= 0 && nx >= 0 && ny < rows && nx < cols && !visited[ny][nx] && maps[ny][nx] != 0) {
                  queue.add(new int[]{ny, nx, dist + 1});
              }
          }
      }

      return -1;
  }
  ```
  - 큐에 좌표 외에 거리를 추가로 담는 방법을 처음에 떠올리지 못해 시간이 많이 소요됨
  - 그래도 풀고 나서 보니 생각보다 풀 만한 문제였던 것 같음
### 오늘의 회고 
    - 이번처럼 여러 경로가 존재할 수 있다면 경로별 거리를 계산할 수 있도록 구현하기!
    - 이번 기회에 DFS/BFS에 익숙해지고 있어서 좋음 🤭

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``