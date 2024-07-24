# 99클럽 코테 스터디 2일차 TIL + 배열

### 학습 키워드
- 배열

### 오늘의 문제
- 프로그래머스 → [x만큼 간격이 있는 n개의 숫자](https://school.programmers.co.kr/learn/courses/30/lessons/12954)

### 풀이 접근 방식
- 반복문
  ```java
  public long[] solution(int x, int n) {
      long[] answer = new long[n];
  
      for (int i = 0; i < n; i++) {
          answer[i] = (long) i * x + x;
      }
  
      return answer;
  }
  ```

### 오늘의 회고
    - 오늘 문제는 꽤 단순한 편이었다. 어제 문제를 보고 나서 푸니 더 그렇게 느껴지는 것 같다.
    - 이런 날은 시간 내서 챌린저 문제를 풀어봤어도 좋았을 듯

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``