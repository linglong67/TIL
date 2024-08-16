# 99클럽 코테 스터디 26일차 TIL + 시뮬레이션

### 학습 키워드
- 시뮬레이션

### 오늘의 문제
- 프로그래머스 → [달리기 경주](https://school.programmers.co.kr/learn/courses/30/lessons/178871)

### 풀이 접근 방식
- 1차 시도 (완전탐색)
  ```java
  public String[] solution(String[] players, String[] callings) {
      String[] answer = players.clone();

      for (String calling : callings) {
          for (int j = 0; j < players.length; j++) {
              String temp = "";
              if (answer[j].equals(calling)) {
                  temp = answer[j - 1];
                  answer[j - 1] = calling;
                  answer[j] = temp;
              }
          }
      }
      return answer;
  }
  ```
  - 쉽게 풀렸다고 생각했지만 callings 수가 많아서 그런지 시간초과 발생..!
- 2차 시도 (Map 활용)
  ```java
  public String[] solution(String[] players, String[] callings) {
      Map<String, Integer> nameMap = new HashMap<>();
      Map<Integer, String> rankMap = new HashMap<>();

      for (int i = 0; i < players.length; i++) {
          nameMap.put(players[i], i);
          rankMap.put(i, players[i]);
      }

      for (String calling : callings) {
          int rank = nameMap.get(calling);
          String player = rankMap.get(rank - 1);

          nameMap.put(calling, rank - 1);
          nameMap.put(player, rank);
          rankMap.put(rank - 1, calling);
          rankMap.put(rank, player);
      }

      String[] answer = new String[players.length];
      for (int i = 0; i < rankMap.size(); i++) {
          answer[i] = rankMap.get(i);
      }

      return answer;
  }
  ```
  - Map을 이중으로 사용해서 풀었고 시간 초과는 발생하지 않음
  - 하지만 코드를 봤을 때 아직 만족스럽지는 않은 편 (비효율적인 것 같은..)
- (그 외) 다른 사람 풀이 (swap + Map 활용)
  ```java
  public String[] solution(String[] players, String[] callings) {
      String[] answer = players.clone();

      Map<String, Integer> map = new HashMap<>();
      
      for(int i = 0; i < answer.length; i++) {
          map.put(answer[i], i);
      }

      int curRank = 0;
      String swapTarget = "";
      
      for(String calling : callings) {
          curRank = map.get(calling);
          swapTarget = answer[curRank - 1];
          
          answer[curRank - 1] = calling;
          map.put(calling, curRank - 1);
              
          answer[curRank] = swapTarget;
          map.put(swapTarget, curRank);
      }
      
      return answer;
  }
  ```
  - 사실 내가 예전에 풀었던 방식인데 이게 셋 중에서는 가장 나은 듯 🙂 
  - 1차, 2차의 방식을 적절히 조합한 느낌이랄까..?! (시간도 제일 적게 소요됨)
### 오늘의 회고
    - 문제를 이해하는 데는 크게 어렵지 않았음
    - 역시 문제가 간단하면.. 시간 복잡도 이슈가 생길 수 있구나 싶었음 😂

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``