# 99클럽 코테 스터디 20일차 TIL + Greedy

### 학습 키워드
- Greedy

### 오늘의 문제
- 프로그래머스 → [큰 수 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/42883)

### 풀이 접근 방식
- Stack 사용
  ```java
  public String solution(String number, int k) {
      Stack<Character> stack = new Stack<>();

      for (char c : number.toCharArray()) {
          while (!stack.isEmpty() && k > 0 && stack.peek() < c) {
              stack.pop();
              k--;
          }
          stack.push(c);
      }

      while (k > 0) {
          stack.pop();
          k--;
      }

      return stack.stream().map(String::valueOf).collect(Collectors.joining());
  }
  ```
  - 쉽게 생각했는데 마지막 입출력 예시에서 막혔고, 스택 풀이를 떠올리지 못함
  - 다른 풀이를 참고해서 제출.. 😂
### 오늘의 회고
    - 그리디는 최선의 선택을 반복해 최적의 해를 구하는 방법이라 그런지 정형화된 풀이는 없는 듯..!
    - 최선의 선택을 생각해내기 위해서는 자료구조 학습과 여러 유형을 경험해보면서 코테 경험치를 쌓는 게 중요한 것 같음

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``