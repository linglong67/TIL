# 99클럽 코테 스터디 24일차 TIL + 그래프

### 학습 키워드
- 그래프

### 오늘의 문제
- 프로그래머스 → [대충 만든 자판](https://school.programmers.co.kr/learn/courses/30/lessons/160586)

### 풀이 접근 방식
- 알파벳 맵을 만들어 알파벳별 최소 키 입력 횟수를 저장하고 target 계산 시 사용
  ```java
  public int[] solution(String[] keymap, String[] targets) {
      Map<Character, Integer> map = new HashMap<>();

      for (int i = 'A'; i <= 'Z'; i++) {
          map.put((char) i, Integer.MAX_VALUE);
      }

      for (String s : keymap) {
          char[] chArr = s.toCharArray();

          for (int i = 0; i < chArr.length; i++) {
              map.put(chArr[i], Math.min(map.get(chArr[i]), i + 1));
          }
      }

      int[] answer = new int[targets.length];

      for (int i = 0; i < targets.length; i++) {
          char[] chArr = targets[i].toCharArray();

          for (char c : chArr) {
              int count = map.get(c);

              if (count == Integer.MAX_VALUE) {
                  answer[i] = -1;
                  break;
              }

              answer[i] += count;
          }
      }

      return answer;
  }
  ```
  - 일부 코드는 좀 더 단순하게 풀어낼 수 있을 것 같다!
  - 한 번에 잘 풀어서 좋긴 한데, for문이 너무 많아보이는 아쉬움..
### 오늘의 회고
    - 그래프에 대한 개념을 미리 찾아봤었는데, 이 문제와는 연결을 잘 못 시키는 중 😵‍💫
    - 최소 키 입력 횟수라는 점에서 그래프와 연결지을 수 있으려나? 🤔 

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``