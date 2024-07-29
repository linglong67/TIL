# 99클럽 코테 스터디 8일차 TIL + 스택/큐

### 학습 키워드
- 스택/큐

### 오늘의 문제
- 프로그래머스 → [기능개발](https://school.programmers.co.kr/learn/courses/30/lessons/42586)

### 풀이 접근 방식
- 큐 사용
  ```java
  public int[] solution(int[] progresses, int[] speeds) {
      Queue<Integer> queue = new LinkedList<>();
      for (int i = 0; i < progresses.length; i++) {
          int mod = (100 - progresses[i]) % speeds[i];
          int divide = (100 - progresses[i]) / speeds[i];
          queue.add(mod == 0 ? divide : divide + 1);
      }

      List<Integer> list = new ArrayList<>();
      int peek = queue.poll();
      int count = 1;
      while (!queue.isEmpty()) {
          int polled = queue.poll();
          if (polled <= peek) {
              count++;
              continue;
          }

          list.add(count);
          count = 1;
          peek = polled;
      }
      list.add(count);

      return list.stream().mapToInt(Integer::intValue).toArray();
  }
  ```
  - 남은 작업일수를 큐에 저장하고, 큐에서 순차적으로 데이터를 빼내면서 배포 시 반영되는 기능 수 계산
  - 다른 풀이를 참고하니 굳이 while문을 또 돌리지 않아도 해결 가능한 듯 (큐 → size(), clear() 활용)
- (그 외) 다른 사람 풀이
  ```java
  public int[] solution(int[] progresses, int[] speeds) {
      int[] dayOfEnd = new int[100];
      int day = -1;
      for (int i = 0; i < progresses.length; i++) {
          while (progresses[i] + (day * speeds[i]) < 100) {
              day++;
          }
          dayOfEnd[day]++;
      }
      return Arrays.stream(dayOfEnd).filter(i -> i != 0).toArray();
  }
  ```
  - 순차적으로 배포 일수를 계산하고 앞 기능 배포 시 반영 가능하다면(작업완료 상태라면) +1
  - 큐를 사용하지 않았지만 짧고 직관적인 느낌이라 인상 깊었음

### 오늘의 회고
    - 큐라는 힌트가 있어서 비교적 쉽게 해결할 수 있었던 편
    - 어떻게 코드를 조금 더 깔끔하게 짤 수 있을지도 고려해보면 좋을 것 같다.

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``