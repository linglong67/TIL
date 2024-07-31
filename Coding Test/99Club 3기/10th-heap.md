# 99클럽 코테 스터디 10일차 TIL + 힙

### 학습 키워드
- 힙

### 오늘의 문제
- 프로그래머스 → [이중우선순위큐](https://school.programmers.co.kr/learn/courses/30/lessons/42628)

### 풀이 접근 방식
- 최소힙, 최대힙 동시 사용
  ```java
  public int[] solution(String[] operations) {
      PriorityQueue<Integer> minHeap = new PriorityQueue<>();
      PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);

      for (String op : operations) {
          String[] s = op.split(" ");

          if (s[0].equals("I")) {
              int num = Integer.parseInt(s[1]);
              minHeap.offer(num);
              maxHeap.offer(num);
              continue;
          }

          if (minHeap.isEmpty()) {
              continue;
          }

          if (s[1].equals("1")) {
              minHeap.remove(maxHeap.poll());
          } else {
              maxHeap.remove(minHeap.poll());
          }
      }

      return minHeap.isEmpty() ? new int[]{0, 0}
              : new int[]{maxHeap.peek(), minHeap.peek()};
  }
  ```
  - 제목에 힌트가 들어있던 문제
  - 최대힙을 함께 사용하면 쉽게 해결 가능
    - 최대힙 구현 → PriorityQueue 생성자에 Collections.reverseOrder() 또는 (a, b) -> b - a와 같은 방식으로 넣어줄 수 있음

### 오늘의 회고
    - 제목에 힌트가 들어있다고 했지만 사실 난.. 혹시 다른 방법이나 클래스를 사용하는 건가 싶어서 살짝 뻘짓(고민)함 🤣
    - 온전히 스스로 풀었다고 하긴 조금 애매하지만 그래도 PriorityQueue를 아니까 비교적 쉬운 접근이 가능했음
    - 힙 자료구조에 대해서는 조금 더 공부를 해보는 게 좋을 것 같다~!

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``