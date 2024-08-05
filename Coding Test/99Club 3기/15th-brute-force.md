# 99클럽 코테 스터디 15일차 TIL + 완전탐색

### 학습 키워드
- 완전탐색

### 오늘의 문제
- 리트코드 → [Prefix and Suffix Search](https://leetcode.com/problems/prefix-and-suffix-search/description/)

### 풀이 접근 방식
- 1차 시도 (가장 간단한 방법으로!)
  ```java
  class WordFilter {
      private String [] words;
  
      public WordFilter(String[] words) {
          this.words = words;
      }
  
      public int f(String pref, String suff) {
          int index = -1;
          for (int i = words.length - 1; i >= 0; i--) {
              if(words[i].charAt(0) != pref.charAt(0)) continue;
  
              if (words[i].startsWith(pref) && words[i].endsWith(suff)) {
                  index = i;
                  break;
              }
          }
  
          return index;
      }
  }
  ```
  - 최초로 시도 시, 시간 초과 발생 → continue 사용, 높은 인덱스부터 시작하는 전략으로 수정해 통과
  - 이건.. 사실 다른 사람 코드를 참고해 시간 초과 이슈 해결
  - 하지만 여전히 성능은 좋지 않았음
- 2차 시도 (Map 자료구조 활용)
  ```java
  class WordFilter {
  private Map<String, Integer> prefSuffMap = new HashMap<>();
  
      public WordFilter(String[] words) {
          for (int i = 0; i < words.length; i++) {
              String word = words[i];
              int wordLen = word.length();
  
              for (int j = 0; j <= wordLen; j++) {
                  String prefix = word.substring(0, j);
                  
                  for (int k = 0; k <= wordLen; k++) {
                      String suffix = word.substring(k, wordLen);
                      prefSuffMap.put(String.join("_", prefix, suffix), i);
                  }
              }
          }
      }
  
      public int f(String pref, String suff) {
          return prefSuffMap.getOrDefault(String.join("_", pref, suff), -1);
      }
  }
  ```
  - 이 문제에서 내가 할 수 있는 최선의 풀이일 것 같음 (근데 이것도 다른 풀이를 통해 깨달았음..)
  - 알맞게 substring을 하기 위해 반복문 조건은 word.length 값을 포함해야 함
  - 이 방식의 성능도 Trie 활용에 비하면 많은 떨어짐
- (그 외) 다른 사람(클럽장님) 풀이
  ```java
  public class WordFilter {
      // TrieNode 클래스: 트라이의 각 노드를 표현
      private class TrieNode {
          private final TrieNode[] children = new TrieNode[26]; // 자식 노드 배열
          private final List<Integer> wordIndices = new ArrayList<>(); // 해당 노드를 통과하는 단어 인덱스
      }
  
      private final TrieNode prefixRoot = new TrieNode(); // 접두사 트라이의 루트
      private final TrieNode suffixRoot = new TrieNode(); // 접미사 트라이의 루트
      
      // 단어의 특정 부분을 트라이에 삽입하는 메서드
      private void insert(final String word, final int start, final int end, final int step, TrieNode root, final int index) {
          for (int i = start; i != end; i += step) {
              int charIndex = word.charAt(i) - 'a'; // 현재 문자에 대한 인덱스 계산
  
              // 현재 문자에 대한 자식 노드가 없으면 생성
              if (root.children[charIndex] == null) {
                  root.children[charIndex] = new TrieNode();
              }
  
              root = root.children[charIndex]; // 현재 노드를 자식 노드로 갱신
              root.wordIndices.add(index); // 노드에 단어 인덱스 추가
          }
      }
  
      // 트라이에서 특정 부분 문자열에 해당하는 인덱스를 검색하는 메서드
      private List<Integer> getIndices(final String str, final int start, final int end, final int step, TrieNode root) {
          for (int i = start; i != end; i += step) {
              root = root.children[str.charAt(i) - 'a']; // 현재 문자에 대한 자식 노드로 이동
              if (root == null) return Collections.emptyList(); // 자식 노드가 없으면 빈 리스트 반환
          }
          return root.wordIndices; // 현재 노드의 인덱스 리스트 반환
      }
      
      // 생성자: 단어 배열을 이용해 트라이를 초기화
      public WordFilter(final String[] words) {
          final Set<String> processedWords = new HashSet<>(); // 중복 단어를 방지하기 위한 Set
  
          // 각 단어를 트라이에 삽입
          for (int i = words.length - 1; i >= 0; i--) {
              String word = words[i];
              if (processedWords.contains(word)) continue; // 이미 처리된 단어는 건너뜀
  
              processedWords.add(word); // 단어 추가
  
              // 접두사와 접미사 트라이에 단어 삽입
              insert(word, 0, word.length(), 1, prefixRoot, i);
              insert(word, word.length() - 1, -1, -1, suffixRoot, i);
          }
      }
  
      
      // 주어진 접두사와 접미사로 단어를 찾고 가장 큰 인덱스를 반환하는 메서드
      public int f(final String prefix, final String suffix) {
          List<Integer> prefixIndices = getIndices(prefix, 0, prefix.length(), 1, prefixRoot);
          List<Integer> suffixIndices = getIndices(suffix, suffix.length() - 1, -1, -1, suffixRoot);
  
          // 두 리스트를 비교하여 가장 큰 공통 인덱스 찾기
          int prefixIndex = 0, suffixIndex = 0;
          while (prefixIndex < prefixIndices.size() && suffixIndex < suffixIndices.size()) {
              int prefixValue = prefixIndices.get(prefixIndex);
              int suffixValue = suffixIndices.get(suffixIndex);
  
              if (prefixValue == suffixValue) return suffixValue; // 동일한 인덱스 발견 시 반환
  
              // 두 인덱스 비교 후 더 큰 인덱스를 가진 리스트를 진행
              if (suffixValue > prefixValue) {
                  suffixIndex++;
              } else {
                  prefixIndex++;
              }
          }
  
          return -1; // 공통 인덱스가 없을 경우 -1 반환
      }
  }
  ```
  - 사실 아직 Trie 자료구조에 대한 개념이 잘 잡히지 않아 100% 이해하진 못한 상태 🥲
  - 하지만 이 코드를 실행하면 성능이 매우 많이 개선됨
### 오늘의 회고
    - 문제 자체를 이해하는 데는 어려움이 없었으나, 성능을 고려한 풀이가 쉽지 않음
    - Trie 자료구조 및 구현방식을 알아두면 좋을 듯..! 🤔

``#99클럽 #코딩테스트준비 #개발자취업 #항해99 #TIL``