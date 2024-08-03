# 99클럽 코테 스터디 13일차 TIL + 이분탐색

### 학습 키워드
- 이분탐색

### 오늘의 문제
- 프로그래머스 → [숫자 카드](https://www.acmicpc.net/problem/10815)

### 풀이 접근 방식
- M개의 숫자카드를 정렬한 후, Map과 Arrays.binarySearch 이용 
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
      for (int num : mNums) {
          map.put(num, 0);
      }

      int[] copyForSort = Arrays.copyOf(mNums, mNums.length);
      Arrays.sort(copyForSort);

      for (int num : nNums) {
          int i = Arrays.binarySearch(copyForSort, num);
          if (i >= 0) {
              map.put(num, 1);
          }
      }

      StringBuilder sb = new StringBuilder();
      for (int num : mNums) {
          sb.append(map.get(num)).append(" ");
      }

      System.out.println(sb.toString().trim());
  }
  ```
  - 필요 이상으로 복잡하게 푼 것 같음 (코드 리팩토링해볼 생각...)
  - 다른 풀이를 보니 M개를 정렬하는 게 아니라 N개를 정렬하는 게 맞는 듯
- (그 외) 다른 사람 풀이
  ```java
  public static void main(String[] args) {
      Scanner sc = new Scanner(System.in);
      int N = sc.nextInt(), arr[] = new int[N];
      
      for(int i=0; i<N; i++)
          arr[i] = sc.nextInt();
      
      Arrays.sort(arr);
      int M = sc.nextInt();
      while(M-- > 0)
          System.out.print((Arrays.binarySearch(arr, sc.nextInt()) < 0 ? 0 : 1) + " ");
  }
  ```
  - 훨씬 간결, 깔끔
  - 다만 시간은 좀 더 오래 걸리는 데, 이 부분은 Scanner 때문일 수 있을 듯
### 오늘의 회고
    - 문제가 어렵지는 않았는데 불필요한 코드/연산을 많이 넣은 것 같다. 리팩토링하면서 좀 더 깔끔하게 바꿔볼 생각!
    - 오랜만에 백준 문제 풀려고 하니까 어색하더라.. 데이터 읽어오는 것도 그렇고 😅

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``