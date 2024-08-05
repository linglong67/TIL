# 99클럽 코테 스터디 14일차 TIL + 이분탐색

### 학습 키워드
- 이분탐색

### 오늘의 문제
- 백준 → [숫자 카드 2](https://www.acmicpc.net/problem/10816)

### 풀이 접근 방식
- Map에 N개의 숫자 카드별 개수를 저장 후 키를 정렬 → M개의 숫자에 대해 이분탐색 진행
  ```java
  public static void main(String[] args) throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      br.readLine();
      int[] nNums = Arrays.stream(br.readLine().split(" "))
                          .mapToInt(Integer::parseInt)
                          .toArray();

      br.readLine();
      int[] mNums = Arrays.stream(br.readLine().split(" "))
                          .mapToInt(Integer::parseInt)
                          .toArray();

      Map<Integer, Integer> map = new HashMap<>();
      for (int num : nNums) {
          map.put(num, map.getOrDefault(num, 0) + 1);
      }

      int[] sortedMapKey = map.keySet().stream().mapToInt(Integer::intValue).sorted().toArray();
      StringBuilder sb = new StringBuilder();

      for (int num : mNums) {
          int i = Arrays.binarySearch(sortedMapKey, num) >= 0 ? map.get(num) : 0;
          sb.append(i).append(" ");
      }

      System.out.println(sb.toString().trim());
  }
  ```
  - 전날 풀었던 문제와 거의 다르지 않아 문제 이해에 필요한 시간 절약
  - 이번엔 N개를 정렬하는 방식으로 접근해 더 간단히 해결
- (그 외) 다른 사람 풀이
  ```java
  public static void main(String[] args) {
      Scanner sc = new Scanner(System.in);
      StringBuilder sb = new StringBuilder();
      int[] arr = new int[20000001];
  
      int N = sc.nextInt();
      for (int i = 0; i < N; i++) {
          arr[sc.nextInt() + 10000000]++;
      }
  
      int M = sc.nextInt();
      for (int j = 0; j < M; j++) {
          sb.append(arr[sc.nextInt() + 10000000] + " ");
      }
  
      System.out.println(sb);
  }
  ```
  - 이분탐색이 아니더라도 쉽게 접근해서 해결했다고 생각함
  - 메모리는 많이 잡아먹지만 이런 풀이를 생각할 수 있다는 게 대단한 듯..!
### 오늘의 회고
    - 권장시간을 보고 오래 걸리지 않을까 했지만, 어제 풀었던 게 있어서 다행히 빠른 이해와 접근이 가능했음
    - 이분탐색도 개념적인 부분을 좀 더 알아두면 좋을 것 같음 🙂

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``