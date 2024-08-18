# 99클럽 코테 스터디 28일차 TIL + 스택/큐

### 학습 키워드
- 스택/큐

### 오늘의 문제
- 프로그래머스 → [괄호 회전하기](https://school.programmers.co.kr/learn/courses/30/lessons/76502)

### 풀이 접근 방식
- 스택 사용
  ```java
  public int solution(String s) {
      int answer = 0;
      int length = s.length();

      for (int i = 0; i < length; i++) {
          String str = s.substring(i, length) + s.substring(0, i);
          Stack<Character> stack = new Stack<>();
          boolean isValidate = true;

          for (char ch : str.toCharArray()) {
              if (ch == '(' || ch == '{' || ch == '[') {
                  stack.push(ch);
                  continue;
              }

              if (stack.isEmpty()) {
                  isValidate = false;
                  break;
              }

              char peek = stack.peek();
              if ((peek == '(' && ch != ')') ||
                  (peek == '{' && ch != '}') ||
                  (peek == '[' && ch != ']')) {
                  isValidate = false;
                  break;
              }

              stack.pop();
          }

          if (isValidate && stack.isEmpty())
              answer++;
      }

      return answer;
  }
  ```
  - 스택에 '열린 괄호'만 넣으면서 올바른 '닫힌 괄호'를 만날 때만 스택을 비워주는 식으로 진행
  - 다른 풀이를 보니 peek보다는 바로 pop을 하는 게 좀 더 효율적인 듯
- (그 외) 다른 사람 풀이
  ```java
    public int solution(String s) {
        int answer = 0;
        int n = s.length();
        
        for (int i = 0; i < n; i++) {
            if (isValid(s)) {
                answer++;
            }

            s = s.substring(1) + s.charAt(0);
        }
        
        return answer;
    }
    
    private boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                
                char top = stack.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }
        
        return stack.isEmpty();
    }
  ```
  - 기본적인 방식은 비슷하지만 pop을 해서 비교하기 때문에 내 풀이처럼 별도의 boolean 변수가 필요 없음
  - 메서드 분리를 해서 코드를 이해하기에 좀 더 용이한 것 같음

### 오늘의 회고
    - 예전에 풀어봤던 문제라 풀이가 쉽게 생각난 편이었다.
    - 이런 유형의 스택 문제는 그래도 익숙해진 듯 👍

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``