# 99클럽 코테 스터디 4일차 TIL + 문자열

### 학습 키워드
- 문자열

### 오늘의 문제
- 프로그래머스 → [JadenCase 문자열 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/12951)

### 풀이 접근 방식
- String, Character, Stream 활용
  ```java
  public String solution(String s) {
      return Arrays.stream(s.split(" ", -1))
                   .map(sp -> {
                       if (sp.isBlank()) {
                           return sp;
                       }
  
                       char[] charArr = sp.toCharArray();
                       for (int i = 0; i < charArr.length; i++) {
                           if (!Character.isAlphabetic(charArr[i])) continue;
  
                           if (i == 0) {
                               charArr[i] = Character.toUpperCase(charArr[i]);
                               continue;
                           }
  
                           charArr[i] = Character.toLowerCase(charArr[i]);
                       }
                       
                       return String.valueOf(charArr);
                   })
                   .collect(Collectors.joining(" "));
  }
  ```
  - 문제 대비 풀이 복잡도가 많이 올라간 느낌
  - 예외 케이스에 부딪혀 시간 내 제출이 어려웠음 (문자열 마지막 공백에 대해 실패 → ex. "3people Unfollowed Me   ")
  - s.split(" ")처럼 작성하면 마지막 공백에 대해 처리할 수 없음 → 원하는 동작을 위해서는 s.split(" ", -1)와 같이 작성 필요
- (그 외) 다른 사람 풀이
  ```java
  public String solution(String s) {
        String answer = "";
        String[] sp = s.toLowerCase().split("");
        boolean flag = true;

        for (String ss : sp) {
            answer += flag ? ss.toUpperCase() : ss;
            flag = ss.equals(" ") ? true : false;
        }

        return answer;
  }
  ```
  - 공백을 포함해 문자열 전체를 1글자씩 나눔
  - 풀이가 더 이해가 잘 되고 간단 (다만, 시간은 이게 조금 더 걸렸음)
  - 이렇게 할 경우 마지막 공백에 대한 고민을 하지 않아도 됨 → 이 부분이 좋은 듯 

### 오늘의 회고
    - String.split(regex, limit)에 대해 좀 더 알게 됨
    - Collectors.joining(delimiter)도 사용 안 하고 잘 몰랐는데 실용적인 듯!
    - 풀이를 바로 하려고 하기 보다는 좀 더 효율적이거나 직관적인 풀이가 있는지 좀 더 고민해보고 시작하자 😂

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``