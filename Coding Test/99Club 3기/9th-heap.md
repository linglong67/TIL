# 99클럽 코테 스터디 9일차 TIL + 힙

### 학습 키워드
- 힙

### 오늘의 문제
- 프로그래머스 → [더 맵게](https://school.programmers.co.kr/learn/courses/30/lessons/42626)

### 풀이 접근 방식
- 힙 사용
  ```java
  public int solution(int[] scoville, int K) {
      PriorityQueue<Integer> heap = new PriorityQueue<>();
      Arrays.stream(scoville).forEach(heap::offer);

      int count = 0;
      while (true) {
          if (heap.size() == 1 && heap.peek() < K)
              return -1;

          if (heap.peek() >= K)
              break;

          heap.offer(heap.poll() + heap.poll() * 2);
          count++;
      }

      return count;
  }
  ```
  - PriorityQueue를 사용한 최소힙으로 해결

### 오늘의 회고
    - Java에서 힙 자료구조를 구현한 PriorityQueue에 대해 먼저 간단히 공부한 후, 문제를 풀어서 비교적 쉽게 접근할 수 있었다.
    - 그날의 키워드를 좀 더 알아보고 문제를 푸는 건 처음인데 나에겐 도움이 되는 방식인 것 같다! 👍 

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``