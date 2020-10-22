# Karat - Compass

find box length

```javascript
// 第一问
const findRectange = (arr) => {
  let res = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr[0].length; j++) {
      if (arr[i][j] === 0) {
        return helper(i, j, arr);
          }
        }
        console.log(JSON.stringify(arr));
      }
    }
  }
};

const helper = (i, j, arr) => {
  let res = [i, j];
  let width = 0;
  let height = 0;
  while (j + width < arr[0].length && arr[i][j + width] === 0) {
    width++;
  }
  while (i + height < arr.length && arr[i + height][j] === 0) {
    height++;
  }
  return [...res, width, height];
};
// dierwen
// // 第二问：matrix里面有多个矩形，没有联通。输出所有矩形
const findRectange = (arr) => {
  let res = [];
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr[0].length; j++) {
      if (
        arr[i][j] === 0 &&
        (i === 0 || arr[i - 1][j] === 1) &&
        (j === 0 || arr[i][j - 1] === 1)
      ) {
        const cur = helper(i, j, arr);
        res.push(cur);
        console.log(JSON.stringify(arr));
      }
    }
  }
  return res;
};
// 3

let dirs = [
  [1, 0],
  [-1, 0],
  [0, 1],
  [0, -1],
];
const helper = (i, j, arr, curRes) => {
  if (
    i < 0 ||
    i >= arr.length ||
    j < 0 ||
    j >= arr[0].length ||
    arr[i][j] === 1
  ) {
    return;
  }
  curRes.push(i + " " + j);
  arr[i][j] = 1;
  dirs.forEach((el) => {
    let x = el[0] + i;
    let y = el[1] + j;
    helper(x, y, arr, curRes);
  });
};
```

## Parent and Children

```java
 /*
     * 输入是int[][] input, input[0]是input[1] 的parent，比如 {{1,4}, {1,5}, {2,5}, {3,6},
     * {6,7}}会形成上面的图 第一问是只有0个parents和只有1个parent的节点 第二问是 两个指定的点有没有公共祖先
     * 第三问是就一个点的最远祖先，如果有好几个就只需要输出一个就好，举个栗子，这里5的最远祖先可以是1或者2，输出任意一个就可以
     */
    public static void main(String[] args) {
        int[][] edges = { { 1, 4 }, { 1, 5 }, { 2, 5 }, { 3, 6 }, { 7, 2 } };
        System.out.println(findparent(edges, 7));
    }

    // 第一问：就假设输出有一个parent的吧
    public static List<Integer> findparent(int[][] edges, int n) {
        int[] indegree = new int[n];
        for (int[] edge : edges) {
            int child = edge[1];
            indegree[child]++;
        }
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 1)
                res.add(i);
        }
        return res;
    }
}

public static void main(String[] args) {
        int[][] edges = { { 1, 4 }, { 1, 5 }, { 2, 5 }, { 3, 6 }, { 7, 2 } };
        System.out.println(commParent(edges, 4, 5));
    }

    // 第二问：两个指定的点有没有公共祖先
    // 思路：找出a,b的所有ancestors,这时候就要用map来存所有点的parent了
    // 思考，如果a就是b的parent。。。
    public static boolean commParent(int[][] edges, int a, int b) {
        Map<Integer, List<Integer>> map = new HashMap<>();
        for (int[] edge : edges) {
            int parent = edge[0];
            int child = edge[1];
            map.putIfAbsent(child, new ArrayList<>());
            map.get(child).add(parent);
        }
        Set<Integer> aParent = findAllAnc(map, a);
        Set<Integer> bParent = findAllAnc(map, b);
        for (int x : bParent) {
            if (aParent.contains(x))
                return true;
        }
        return false;
    }

    public static Set<Integer> findAllAnc(Map<Integer, List<Integer>> map, int a) {
        Set<Integer> set = new HashSet<>();
        Queue<Integer> q = new LinkedList<>();
        q.add(a);
        while (!q.isEmpty()) {
            int cur = q.remove();
            set.add(cur);
            List<Integer> parents = map.get(cur);
            if (parents == null)
                continue;
            for (int p : parents) {
                q.add(p);
            }
        }
        return set;
    }
    // 第三问：一个点的最远祖先，感觉就是用DFS做
    // int[] res来作为helper int[]， res[0] = 当前level, res[1]就是当前level的ancestor。用来打擂台
    
    public static void dfs(Map<Integer, List<Integer>> map, int a, int[] res, int level){
        if(level > res[0]){
            // find a higher ancestor
            // update highest level and hightes ancestor
            res[0] = level;
            res[1] = a;
        }
        List<Integer> parents = map.get(a);
        if(parents != null && parents.size()!=0){
            for(int parent:parents){
                dfs(map, parent, res, level+1);
            }
        }
    }
}
```

### Dictionary and map

```java
public class testjava {
    public static void main(String[] args) {
        String dic = "abbycdddjt";
        String[] list = new String[] { "cat", "baby" };
        System.out.println("test");
        List<String> res = findList(dic, list);
        for (String s : res) {
            System.out.println(s);
        }
    }

    public static List<String> findList(String dic, String[] list) {
        System.out.println(dic);
        List<String> res = new ArrayList<>();
        Map<Character, Integer> map = new HashMap<>();
        for (char c : dic.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }
        System.out.println(map);
        for (String s : list) {
            if (checkStr(map, s)) {
                res.add(s);
            }
        }
        return res;
    }

    public static boolean checkStr(Map<Character, Integer> map, String str) {
        Map<Character, Integer> curMap = new HashMap<>(map);
        for (char c : str.toCharArray()) {
            if (curMap.get(c) == null)
                return false;
            else {
                int num = map.get(c) - 1;
                if (num == 0) {
                    curMap.remove(c);
                } else {
                    curMap.put(c, num);
                }
            }
        }
        return true;
    }
}
```

### Calculator

```java
public static void main(String[] args){
        String s = "1 + 2 - 4 ";
        System.out.println(calculate(s));
        int[] index = {0};
        String s1 = "1 + (2 - 4) ";
        System.out.println(calculateII(s1, index));
    }
/* 只有 +, -, , (, )
   我的思路是，把括号里面的当做sub problem
   对于最基本的subproblem: 只有 +，-，' '
* */
// 这是最基本的那个，不带上括号
    public static int calculate(String s){
        int res = 0;
        int sign = 1;
        int cur = 0;
        for(int i = 0; i < s.length(); i++){
            char c = s.charAt(i);
            if(Character.isDigit(c)){
                cur = cur*10 + c-'0';
            }else if(c == '+'){
                res += sign * cur;
                sign = 1;
                cur = 0;
            }else if(c == '-'){
                res += sign * cur;
                sign = -1;
                cur = 0;
            }
        }
        // 别忘了最后一个数
        res += sign * cur;
        return res;
    }
    // 带上括号，复杂了一点，避免重复遍历，把index设置成一个全局变量
    public static int calculateII(String s, int[] index){
        int res = 0;
        int sign = 1;
        int cur = 0;
        for(; index[0] < s.length(); index[0]++){
            char c = s.charAt(index[0]);
            if(Character.isDigit(c)){
                cur = cur * 10 + (c-'0');
            }else if(c == '+'){
                res += sign * cur;
                sign = 1;
                cur = 0;
            }else if(c == '-'){
                res += sign * cur;
                sign = -1;
                cur = 0;
            }else if(c == '('){
                index[0] ++;
                int sub = calculateII(s, index);
                System.out.println(sub);
                res += sign * sub;
            }else if(c == ')'){
                // 注意最后一步
                res += sign * cur;
                return res;
            }
        }
        // 注意最后一步
        res += sign * cur;
        return res;
    }
```

### Domain and LCS

```java
import java.util.*;
public class Domain {
    public static void main(String[] args){
        String[][] domains = {
                {"google.com", "60"},
                {"yahoo.com", "50"},
                {"sports.yahoo.com", "80"}};
        System.out.println(sub_domain_total(domains));
        String[] user1 = {"/nine.html", "/four.html", "/six.html", "/seven.html", "/one.html" };
        String[] user2 = {"/nine.html", "/two.html", "/three.html", "/four.html", "/six.html", "/seven.html"};
        System.out.println(LCH(user1,user2));
    }
    /*
    第一题：求广告的每个sub domain被click的总次数
    input: {
                {"google.com", "60"},
                {"yahoo.com", "50"},
                {"sports.yahoo.com", "80"}};
    output : "com",90 "google.com",60 "yahoo.com",130 "sports.yahoo.com","80
    * */
    public static List<List<String>> sub_domain_total(String[][] domains){
        List<List<String>> res = new ArrayList<>();
        Map<String, Integer> map = new HashMap<>();
        for(String[] domain:domains){
            String name = domain[0];
            int click = Integer.parseInt(domain[1]);
            // helper function: find all sub domains of current domain name
            for(String sub : subs(name)){
                map.putIfAbsent(sub,0);
                map.put(sub, map.get(sub)+click);
            }
        }
        for(Map.Entry<String, Integer> entry : map.entrySet()){
            res.add(Arrays.asList(entry.getKey(), String.valueOf(entry.getValue())));
        }
        return res;
    }

    private static List<String> subs(String domain){
        List<String> res = new ArrayList<>();
        String[] parts = domain.split("\\.");
        String s = "";
        for(int i = parts.length-1; i >= 0; i--){
            s = "." + parts[i] + s;
            res.add(s.substring(1));
        }
        return res;
    }
    /*
    第二题：给每个user访问历史记录，找出两个user之间longest continuous common history
    就是longest common substring问题：
    如果 s.at(i) == s.at(j)
         dp[i][j] = dp[i-1][j-1] + 1;
         else: dp[i][j] = 0
    * */

    public static List<String> LCH(String[] user1, String[] user2){
        // maintain[0] = max length, maintain[1] index of end
        List<String> res = new ArrayList<>();
        int[] maintain = new int[2];
        int[][] dp = new int[user1.length+1][user2.length+1];
        for(int i = 1; i <= user1.length; i++){
            for(int j = 1; j <= user2.length; j++){
                if(user1[i-1] == user2[j-1]){
                    dp[i][j] = dp[i-1][j-1] + 1;
                    // find a longer one
                    if(dp[i][j] > maintain[0]){
                        maintain[0] = dp[i][j];
                        maintain[1] = i;
                    }
                }else{
                    dp[i][j] = 0;
                }
            }
        }
        for(int i = maintain[1]-maintain[0]; i < maintain[1]; i++){
            res.add(user1[i]);
        }
        return res;
    }
}
```

## 79 word search

```java
class Solution {
    int[][] dirs = new int[][]{{-1, 0}, {1, 0}, {0, 1}, {0, -1}};
    List<int[]> path = new ArrayList<>();
    public boolean exist(char[][] board, String word) {
      if(board == null || board.length == 0) return false;
      boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i = 0; i < board.length; i++){
          for (int j = 0; j < board[0].length; j++){
            if(word.charAt(0) == board[i][j] && visited[i][j] == false){
              List<int[]> list = new ArrayList<>();
               if(helper(board, visited, 0, word, i, j, list)) {
                 for (int[] arr: path){
                   System.out.println(arr[0] + " " + arr[1]);
                 }
                 return true;
                 }
            }
          }
        }
      return false;
    }
  public boolean helper(char[][] board, boolean[][] visited, int index, String word, int i, int j, List<int[]> list){
    if(index == word.length()) {
      path = new ArrayList<>(list); 
      return true;
      };
    if(i < 0 || i >= board.length || j < 0 || j >= board[0].length || visited[i][j] == true || board[i][j] != word.charAt(index) ) return false;
    visited[i][j] = true;
   list.add(new int[]{i, j});
    for (int[] dir : dirs){
      int x = dir[0] + i;
      int y = dir[1] + j;
      if(helper(board, visited, index + 1, word, x, y, list)) return true;
    }
    visited[i][j] = false;
    return false;
  }
}
```





