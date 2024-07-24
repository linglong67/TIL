# 99클럽 코테 스터디 3일차 TIL + 문자열

### 학습 키워드
- 문자열

### 오늘의 문제
- 프로그래머스 → [문자열 내 마음대로 정렬하기](https://school.programmers.co.kr/learn/courses/30/lessons/12915)

### 풀이 접근 방식
- Stream의 sorted 사용 (사전순 정렬 후, n번째 문자 기준으로 재정렬)
  ```java
  public String[] solution(String[] strings, int n) {
      return Arrays.stream(strings)
                   .sorted()
                   .sorted(Comparator.comparingInt(s -> s.charAt(n)))
                   .toArray(String[]::new);
  }
  ```
  - 다만, 이 방식은 2번의 정렬을 하기 때문에 비효율적인 부분이 존재
- (그 외) ChatGPT의 추천
  ```java
  public String[] solution(String[] strings, int n) {
      Arrays.sort(strings, Comparator.comparing((String s) -> s.charAt(n)).thenComparing(s -> s));
      return strings;
  }
  ```
  - n번째 문자를 첫 번째 기준, 사전순을 두 번째 기준으로 정렬
  - 직관적이고 좋은 방법인 듯

### 오늘의 회고
    - 정렬 문제는 매번 풀이 방법이 곧바로 떠오르지 않는다..🥲
    - 이번 알고리즘 문제에 대해서 ChatGPT에게 여러 풀이를 제공해달라고 했는데, 잘 활용하면 도움이 많이 될 듯!
    - 오늘 알아야 할 추가 키워드 → Comparator | Comparable | Collections.sort | Arrays.sort | Stream.sorted

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``