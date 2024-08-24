# 99클럽 코테 스터디 34일차 TIL + DFS/BFS

### 학습 키워드
- DFS/BFS

### 오늘의 문제
- 프로그래머스 → [타겟 넘버](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

### 풀이 접근 방식
- DFS로 접근
  ```java
  int[] numbers;
  int target;
  int answer;

  public int solution(int[] numbers, int target) {
      this.numbers = numbers;
      this.target = target;
      answer = 0;

      dfs(0, 0);

      return answer;
  }

  private void dfs(int index, int sum) {
      if (index == numbers.length) {
          if (sum == target) answer++;
          return;
      }

      dfs(index + 1, sum + numbers[index]);
      dfs(index + 1, sum - numbers[index]);
  }
  ```
  - dfs에 넣을 변수들을 고민하는데 시간이 좀 걸렸던 편이었음 🤔 
  - DFS/BFS에 익숙해지면 풀이도 간단하고 쉽게 해결할 수 있는 문제인 듯
- (그 외) 다른 사람 풀이 → DFS (ChatGPT)
  ```java
  public int solution(int[] numbers, int target) {
      return dfs(numbers, target, 0, 0);
  }

  private int dfs(int[] numbers, int target, int index, int sum) {
      // 기본 조건: 모든 숫자를 사용했을 때
      if (index == numbers.length) {
          // 현재 합계가 타겟과 같은지 확인
          return sum == target ? 1 : 0;
      }
      
      // 재귀 호출: 현재 숫자를 더하거나 빼는 두 가지 경우를 모두 탐색
      return dfs(numbers, target, index + 1, sum + numbers[index])
           + dfs(numbers, target, index + 1, sum - numbers[index]);
  }
  ```
  - 개인적으로는 전역변수를 두지 않고 이런 식으로 풀이하는 게 더 깔끔하고 좋아보임
  - int 리턴으로 하니 코드 구현이 훨씬 간단해지는 것 같아 다음에는 이런 방식을 고려해야겠음! 👍
### 오늘의 회고 
    - 예전에 풀어봤던 문제인데 생각보다 풀이가 바로 생각나지 않아 조금 당황스러웠음
    - 최근 몇일 연속해서 DFS/BFS 유형을 푸니 버벅이긴 해도 전보다 익숙해진 느낌이 들었음 😁

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``