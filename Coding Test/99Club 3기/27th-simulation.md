# 99클럽 코테 스터디 27일차 TIL + 시뮬레이션

### 학습 키워드
- 시뮬레이션

### 오늘의 문제
- 프로그래머스 → [할인 행사](https://school.programmers.co.kr/learn/courses/30/lessons/131127)

### 풀이 접근 방식
- 구간별 완전탐색 방식으로 접근
  ```java
  public int solution(String[] want, int[] number, String[] discount) {
      int answer = 0;

      for (int i = 0; i <= discount.length - 10; i++) {
          Map<String, Integer> map = new HashMap<>();

          for (int j = 0; j < want.length; j++) {
              map.put(want[j], number[j]);
          }

          for (int k = i; k < i + 10; k++) {
              String item = discount[k];
              if (map.containsKey(discount[k])) {
                  int count = map.get(item) - 1;
                  if (count > 0) {
                      map.put(item, count);
                  } else {
                      map.remove(item);
                  }
              }
          }
          if (map.isEmpty()) answer++;
      }

      return answer;
  }
  ```
  - 범위가 크지 않은 편이라, 위와 같은 접근으로도 통과되었던 것 같음
  - 채점 시에 나오는 실행 시간을 봤을 때 효율적인 방식은 아닐지도..?
- (그 외) 다른 사람 풀이 (슬라이딩 윈도우 기법 사용)
  ```java
  public int solution(String[] want, int[] number, String[] discount) {
      Map<String, Integer> wantMap = new HashMap<>();
      for (int i = 0; i < want.length; i++) {
          wantMap.put(want[i], number[i]);
      }

      int matchCount = 0;

      for (int i = 0; i <= discount.length - 10; i++) {
          Map<String, Integer> discountMap = new HashMap<>();
          for (int j = i; j < i + 10; j++) {
              discountMap.put(discount[j], discountMap.getOrDefault(discount[j], 0) + 1);
          }

          if (isMatching(wantMap, discountMap)) {
              matchCount++;
          }
      }

      return matchCount;
  }

  private boolean isMatching(Map<String, Integer> wantMap, Map<String, Integer> discountMap) {
      for (String key : wantMap.keySet()) {
          if (!discountMap.containsKey(key) || !discountMap.get(key).equals(wantMap.get(key))) {
              return false;
          }
      }
      return true;
  }
  ```
  - 처음에 만든 맵을 활용할 수 있는 구조라 좋은 듯
  - 하지만 막상 시간 효율적인 측면에서는 내 풀이와 거의 차이나지 않음
### 오늘의 회고
    - 내가 사용한 방식은 반쪽짜리 '슬라이딩 윈도우'였던 것 같지만, 이번 문제를 통해서 해당 개념을 알게 됨
    - 시뮬레이션 유형은 그래도 풀이를 생각할 수 있으면 어느 정도 구현이 가능한 듯! 😊

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``