# 99클럽 코테 스터디 5일차 TIL + 해시

### 학습 키워드
- 해시

### 오늘의 문제
- 프로그래머스 → [전화번호 목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)

### 풀이 접근 방식
- 1차 시도 (이중 for문 사용)
  ```java
  public boolean solution(String[] phone_book) {
      Arrays.sort(phone_book);
      boolean answer = true;
  
      for (int i = 0; i < phone_book.length; i++) {
          if (i != 0 && phone_book[i - 1].length() < phone_book[i].length()) {
              for (int j = 0; j < i; j++) {
                  if (phone_book[i].startsWith(phone_book[j])) {
                      answer = false;
                  }
              }
          }
      }
  
      return answer;
  }
  ```
  - 이중 for문 영향으로 효율성 테스트 시 시간 초과 발생
- 2차 시도 (이중 for문 걷어내고, Map 사용)
  ```java
  public boolean solution(String[] phone_book) {
      Arrays.sort(phone_book);
  
      Map<String, Integer> map = new LinkedHashMap<>();
      for (String s : phone_book) {
          map.put(s, s.length());
      }
  
      boolean isPrefix = false;
      String prevKey = null;
  
      for (String key : map.keySet()) {
          if (prevKey != null && prevKey.length() < key.length()) {
              isPrefix = key.startsWith(prevKey);
          }
          if(isPrefix) break;
          prevKey = key;
      }
  
      return !isPrefix;
  }
  ```
  - 2번쨰 for문에서 정렬한 순으로 비교하기 위해 LinkedHashMap을 사용
- (그 외) 1차 코드 보완
  ```java
  public boolean solution(String[] phone_book) {
    Arrays.sort(phone_book);
    boolean answer = true;

    for (int i = 0; i < phone_book.length; i++) {
        if (i != 0 && phone_book[i - 1].length() < phone_book[i].length()) {
            if (phone_book[i].startsWith(phone_book[i - 1])) {
                answer = false;
                break;
            }
        }
    }

    return answer;
  }
  ```
  - 사실 1차 시도 때 사용한 이중 for문은 크게 의미가 없었음
    - 바로 앞 전화번호만 비교하면 되기 때문 (그럼 굳이 해시 방식도 필요없을지도..)
    - 이 문제 한정일 수도 있지만 정확성 테스트, 효율성 테스트에서도 이 방식이 시간 더 적게 걸림

### 오늘의 회고
    - 이중 for문은 꼭 필요한 경우가 아니라면 지양하기 (오늘처럼 필요없는데.. 작성하면 더더욱 안됨!)
    - 효율적으로(혹은 유용하게) 해시 활용하는 방법 알아두면 좋을 것 같음 

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``