# 99클럽 코테 스터디 11일차 TIL + 정렬

### 학습 키워드
- 정렬

### 오늘의 문제
- 프로그래머스 → [카드 뭉치](https://school.programmers.co.kr/learn/courses/30/lessons/159994)

### 풀이 접근 방식
- 이중 for문 사용
  ```java
  public String solution(String[] cards1, String[] cards2, String[] goal) {
      int idx1 = -1;
      int idx2 = -1;
    
      for (String s : goal) {
          for (int j = 0; j < cards1.length; j++) {
              if (!s.equals(cards1[j])) continue;
              if (j < idx1) return "No";
        
              idx1 = j;
          }
    
        for (int k = 0; k < cards2.length; k++) {
            if (!s.equals(cards2[k])) continue;
            if (k < idx2) return "No";
      
            idx2 = k;
        }
      }
      
      return goal.length < (idx1 + 1) + (idx2 + 1) ? "No" : "Yes";
  }
  ```
  - goal 배열을 돌 때 각각의 카드 뭉치별로 한번 더 돌면서 순서에 어긋나는지 확인
    - 순서가 어긋나는 경우 이중 for문에서 확인해서 "No" 리턴 가능
    - 하지만 이 구조만으로는 중간에 있는 카드를 사용하지 않은 경우를 체크할 수 없음
      - 그래서 마지막에 goal의 길이를 통해 한번 더 검증
- (그 외) 다른 사람 풀이
  ```java
  public String solution(String[] cards1, String[] cards2, String[] goal) {
      int cardIdx1 = 0;
      int cardIdx2 = 0;

      for (int i = 0; i < goal.length; i++){
          String target = goal[i];

          if (cardIdx1 < cards1.length && target.equals(cards1[cardIdx1]))
              cardIdx1++;
          else if (cardIdx2 < cards2.length && target.equals(cards2[cardIdx2]))
              cardIdx2++;
          else
              return "No";
      }
      
      return "Yes";
  }
  ```
  - 자료구조를 사용하지 않은 풀이 중에서는 가장 간결하고 좋았다고 생각함
  - if~else 부분을 보면 각 카드 뭉치에 순차적으로 접근하지 않을 경우 "No"를 리턴하게 되어있음

### 오늘의 회고
    - 정렬이 키워드였는데 개인적으로 정렬을 활용한 느낌은 아니었음
    - 쉬운 문제를 쉽게 풀지 못해 아쉬움이 남는 문제..🥲

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``