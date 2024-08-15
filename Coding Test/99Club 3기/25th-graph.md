# 99클럽 코테 스터디 25일차 TIL + 그래프

### 학습 키워드
- 그래프

### 오늘의 문제
- 리트코드 → [Evaluate Division](https://leetcode.com/problems/evaluate-division/description/)

### 풀이 접근 방식
- DFS로 접근 (재귀)
  ```java
  public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
      Map<String, Map<String, Double>> graph = new HashMap<>();

      for (int i = 0; i < equations.size(); i++) {
          String from = equations.get(i).get(0);
          String to = equations.get(i).get(1);
          double value = values[i];

          graph.computeIfAbsent(from, k -> new HashMap<>()).put(to, value);
          graph.computeIfAbsent(to, k -> new HashMap<>()).put(from, 1 / value);
      }

      double[] answers = new double[queries.size()];

      for (int i = 0; i < queries.size(); i++) {
          String from = queries.get(i).get(0);
          String to = queries.get(i).get(1);
          Set<String> visited = new HashSet<>();

          answers[i] = dfs(graph, from, to, visited);
      }

      return answers;
  }

  private double dfs(Map<String, Map<String, Double>> graph, String from, String to, Set<String> visited) {
      if (!graph.containsKey(from)) {
          return -1.0;
      }

      if (from.equals(to)) {
          return 1.0;
      }

      visited.add(from);

      for (Map.Entry<String, Double> neighbor : graph.get(from).entrySet()) {
          if (!visited.contains(neighbor.getKey())) {
              double result = dfs(graph, neighbor.getKey(), to, visited);
              if (result != -1.0) {
                  return result * neighbor.getValue();
              }
          }
      }

      return -1.0;
  }
  ```
  - 역시 어제가 쉬웠던건가.. 어렵다! 😂
  - ChatGPT가 준 풀이로 문제를 좀 더 이해할 수 있었음..
### 오늘의 회고
    - 머릿 속에 그려지는 풀이는 간단해도 코드로 옮기는 게 아직 쉽지 않음
    - 그래도 풀이를 보고 이해는 잘 되는 것 같아 그나마 다행 🥲

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``