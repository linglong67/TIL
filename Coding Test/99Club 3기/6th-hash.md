# 99클럽 코테 스터디 6일차 TIL + 해시

### 학습 키워드
- 해시

### 오늘의 문제
- 프로그래머스 → [의상](https://school.programmers.co.kr/learn/courses/30/lessons/42578)

### 풀이 접근 방식
- 해시 사용
  ```java
  public int solution(String[][] clothes) {
      Map<String, Integer> map = new HashMap<>();
      for (String[] cloth : clothes) {
          map.put(cloth[1], map.getOrDefault(cloth[1], 0) + 1);
      }
  
      int answer = 1;
      for (String key : map.keySet()) {
          answer *= map.get(key) + 1;
      }
  
      return answer - 1;
  }  
  ```
  - 의상 종류별(안 입기, 의상 1, ...)로 고려해 계산 후 마지막에 모두 안 입은 경우 빼주기

### 오늘의 회고
    - 이전에 풀었던 문제라 쉽게 생각이 난 편
    - 이 문제 풀면서 해시에 대해 많이 알게 된 기억이 남 👍

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``