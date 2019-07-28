# word search II && I

word search I

```javascript
// use Deep Frist Search to search board and use boolen 2 d array to check visited characters 
// time O(mn*4^k) where k is the length of the string; mn for for loop and for the dfs method its 4^k.
//Since the dfs method goes only as deep as the word length we have T(k)=4(T(k-1))=4*4T(k-2)=....=.. which will be 4^k. 
//space O(4mn) if the function call stack is taken into account. In each cell, we recursively call its 4four neighbors and there are mn cells in total.
class Solution {
    int[][] dirs = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public boolean exist(char[][] board, String word) {
        char start = word.charAt(0);
        for (int i = 0; i < board.length; i++){
            for (int j = 0; j < board[0].length; j++){
                if(board[i][j] == start){
                    boolean[][] path = new boolean[board.length][board[0].length];
                   if( helper(board, word, i, j,path, 0)) return true;
                }
            }
        }
        return false;
    }
    public boolean helper(char[][] board, String word, int i, int j,boolean[][] path, int index){
         if(index == word.length()) return true;
        if(i < 0 || j < 0 || i >= board.length ||j >= board[i].length|| index > word.length()){
            return false;
        } 
     if(board[i][j] != word.charAt(index) || path[i][j] == true) return false;
        path[i][j] = true;
        for (int[] dir : dirs){
            int x = i + dir[0];
            int y = j + dir[1];
               if( helper(board, word, x, y, path, index + 1)){
                   return true;
               } 
        }
        path[i][j] = false;
        return false;
    }
}
```

word search II

```java
// use DFS and Trie
// words build a trie and at leaf node add a word 
// use dfs check and backtrack it
// remeber use a boolean[][] to avoid deuplicate 

class TrieNode{
        TrieNode[] children = new TrieNode[26];
        String word;
        TrieNode(){}
    }

class Solution {
   
    private int[][] directions = {{1, 0},{-1, 0},{0, 1},{0, -1}};
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<>();
        if(board == null || board.length == 0 || board[0].length == 0) return res;
        int m = board.length, n = board[0].length;
        TrieNode root = buildTree(words);
         for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                int index = board[i][j] - 'a';
                if(root.children[index] == null){
                    continue;
                }
               TrieNode p = root;
                boolean[][] visited = new boolean[m][n];
                dfs(p, i, j, res, board, visited); 
            }
         }
        return res;
     }
    private TrieNode buildTree(String[] words){
        TrieNode root = new TrieNode();
        for(String word : words){
            TrieNode p = root;
            for(char c : word.toCharArray()){
                int index = c - 'a';
                if(p.children[index] == null){
                    p.children[index] = new TrieNode();
                }
                p = p.children[index];
            }
            p.word = word;
        }
        return root;
    } private void dfs(TrieNode p, int i, int j, List<String> res, char[][] board, boolean[][] visited){
        if(i >= board.length || i < 0 || j >= board[0].length || j < 0 || visited[i][j]){
            return;
        }
        if(p.children[board[i][j] - 'a'] == null){
            return;
        }
        if(p.children[board[i][j] - 'a'].word != null){
            res.add(p.children[board[i][j] - 'a'].word);
            p.children[board[i][j] - 'a'].word = null;  
           //since we have visited this leaf node, then set "word" null , make sure we do not visit it once again.
        }
        visited[i][j] = true;
        for(int[] dir : directions){
            int newX = i + dir[0];
            int newY = j + dir[1];
            dfs(p.children[board[i][j] - 'a'], newX, newY, res, board, visited);
        }
        visited[i][j] = false;  //very important backtracking!
    } 
}
```

