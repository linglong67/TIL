# 99클럽 코테 스터디 37일차 TIL + 완전탐색

### 학습 키워드
- 완전탐색

### 오늘의 문제
- 백준 → [부등호](https://www.acmicpc.net/problem/2529)

### 풀이 접근 방식
- 백트래킹 기법 사용
  ```java
  static int size;
  static String[] signs;
  static boolean[] used = new boolean[10];
  static List<String> results = new ArrayList<>();

  public static void main(String[] args) throws IOException {
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

      size = Integer.parseInt(br.readLine());
      signs = br.readLine().split(" ");

      backtrack("", 0);

      Collections.sort(results);

      System.out.println(results.get(results.size() - 1));
      System.out.println(results.get(0));
  }

  private static void backtrack(String num, int depth) {
      if (depth == size + 1) {
          results.add(num);
          return;
      }

      for (int i = 0; i < 10; i++) {
          if (!used[i] && (depth == 0 || isValid(num.charAt(depth - 1) - '0', i, signs[depth - 1]))) {
              used[i] = true;
              backtrack(num + i, depth + 1);
              used[i] = false;
          }
      }
  }

  private static boolean isValid(int a, int b, String sign) {
      return sign.equals("<") ? a < b : a > b;
  }
  ```
  - (어제처럼..) 직접 풀이하는 데에는 실패해서 다른 풀이를 참고했음 😂
  - 특정 문제를 해결하기 위해 가능한 모든 경로를 탐색하고 조건을 만족하지 않으면 선택을 취소하여 다른 경로를 시도하는 기법 (→ 백트래킹)
### 오늘의 회고 
    - 백트래킹이라는 용어는 오늘 처음 들어본 듯
    - 난이도가.. 쉽지 않다 😵‍💫

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``