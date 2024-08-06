# 99클럽 코테 스터디 16일차 TIL + 완전탐색

### 학습 키워드
- 완전탐색

### 오늘의 문제
- 프로그래머스 → [모음사전](https://school.programmers.co.kr/learn/courses/30/lessons/84512)

### 풀이 접근 방식
- 단순하게 완탐 시도
  ```java
  public int solution(String word) {
      String[] alphabet = {"A", "E", "I", "O", "U"};
      Map<String, Integer> map = new HashMap<>();

      int idx = 1;
      for (String s1 : alphabet) {
          map.put(s1, idx++);

          for (String s2 : alphabet) {
              map.put(s1 + s2, idx++);

              for (String s3 : alphabet) {
                  map.put(s1 + s2 + s3, idx++);

                  for (String s4 : alphabet) {
                      map.put(s1 + s2 + s3 + s4, idx++);

                      for (String s5 : alphabet) {
                          map.put(s1 + s2 + s3 + s4 + s5, idx++);
                      }
                  }
              }
          }
      }

      return map.get(word);
  }
  ```
  - 성능이 좋다는 생각은 들지 않지만, 그래도 문제없이 통과!
- (그 외) 다른 사람 풀이1
  ```java
  List<String> list = new ArrayList<>();
  void dfs(String str, int len) {
      if (len > 5) return;
      list.add(str);

      for (int i = 0; i < 5; i++) {
          dfs(str + "AEIOU".charAt(i), len + 1);
      }
  }

  public int solution(String word) {
      dfs("", 0);
      return list.indexOf(word);
  }
  ```
  - DFS를 활용한 방식으로 접근
  - 코드가 한결 간결해지지만, 여전히 전체 경우의 수를 탐색해야 함
- (그 외) 다른 사람 풀이2
  ```java
  public int solution(String word) {
      int answer = 0;
      int max = 3905;
  
      for(String s : word.split("")){
          answer += "AEIOU".indexOf(s) * (max /= 5) + 1;
      }

      return answer;
  }
  ```
  - 연산을 통해 위치를 계산
  - 전체 경우의 수를 만들지 않고, 수학적으로 접근해서 해결
### 오늘의 회고
    - 쉽게 풀려고 하니 어렵지 않게 해결했으나, 성능을 고려한 좋은 풀이는 아니었던 것 같음
    - 문제를 풀고 나서 보는 다른 사람 풀이가 꽤나 흥미진진함 😁

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``