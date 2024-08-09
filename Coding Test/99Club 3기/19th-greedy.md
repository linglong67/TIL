# 99클럽 코테 스터디 19일차 TIL + Greedy

### 학습 키워드
- Greedy

### 오늘의 문제
- 프로그래머스 → [구명보트](https://school.programmers.co.kr/learn/courses/30/lessons/42885)

### 풀이 접근 방식
- 투 포인터 사용
  ```java
  public int solution(int[] people, int limit) {
      Arrays.sort(people);
      int left = 0;
      int right = people.length - 1;
      int boats = 0;

      while (left <= right) {
          if (people[left] + people[right] <= limit) {
              left++;
          }

          right--;
          boats++;
      }

      return boats;
  }
  ```
  - 적절한 풀이법을 시간 내에 생각하지 못했음..
  - 구명보트에 최대 2명이라는 제약 조건을 제대로 확인하지 못함 🥲 
### 오늘의 회고
    - 스스로 해결한 풀이가 아니라 아쉽지만, 생각보다 쉽게 접근할 수 있는 풀이여서 이해는 잘 되었던 것 같다.
    - 비슷한 유형이 또 나온다면 그래도 오늘보단 금방 떠올릴 수 있을 듯! 🙂

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``