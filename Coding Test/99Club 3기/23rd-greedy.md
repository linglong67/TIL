# 99클럽 코테 스터디 23일차 TIL + Greedy

### 학습 키워드
- Greedy

### 오늘의 문제
- 프로그래머스 → [마법의 엘리베이터](https://school.programmers.co.kr/learn/courses/30/lessons/148653)

### 풀이 접근 방식
- 현재 자릿수를 기준으로 올림, 내림 판단하는 방식
  ```java
  public int solution(int storey) {
      int answer = 0;

      while (storey != 0) {
          int current = storey % 10;
          int next = (storey / 10) % 10;

          if (current > 5 || (current == 5 && next >= 5)) {
              answer += 10 - current;
              storey = (storey / 10) + 1;
          } else {
              answer += current;
              storey /= 10;
          }
      }

      return answer;
  }
  ```
  - 방식에 대해서는 잘 떠올렸는데 실제 풀이로 옮기지 못했음 🥲
  - 현재 및 다음 자릿수를 가져오는 것과 if문 코드에 대한 이해를 잘 해야할 듯
### 오늘의 회고
    - 동전의 최소 개수 문제와 비슷한 유형이었음
    - 사고를 좀 더 유연하게 해보기! 👊

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``