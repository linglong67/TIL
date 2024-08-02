# 99클럽 코테 스터디 12일차 TIL + 정렬

### 학습 키워드
- 정렬

### 오늘의 문제
- 프로그래머스 → [H-Index](https://school.programmers.co.kr/learn/courses/30/lessons/42747)

### 풀이 접근 방식
- 논문별 인용 횟수 정렬 후, h 최댓값 찾기
  ```java
  public int solution(int[] citations) {
      int answer = 0;
      Arrays.sort(citations);

      for (int i = 0; i < citations.length; i++) {
          int h = citations.length - i;
          if (citations[i] >= h) {
              answer = h;
              break;
          }
      }

      return answer;
  }
  ```
  - citations[i] >= h 조건을 최초로 만족할 때 h의 최댓값을 구할 수 있음
    - 이후로는 조건은 만족하지만 h가 점점 작아짐
### 오늘의 회고
    - 예전에 못 풀었던 기억이 나는데, 오늘의 나도 풀이를 떠올리지 못함 😂
    - 수학적(논리적) 머리가 필요해 😵‍💫 (연습하자!)

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``