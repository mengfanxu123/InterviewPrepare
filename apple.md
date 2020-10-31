# Apple



## Longest Valid Parentheses

```java
class Solution {
    public int longestValidParentheses(String s) {
       Stack<Integer> stack = new Stack<>();
       stack.push(-1);
       int max = 0;
       for (int i = 0; i < s.length(); i++){
         if(s.charAt(i) == ')' && stack.size() > 1 && s.charAt(stack.peek()) == '('){
             stack.pop();
             max = Math.max(max, i - stack.peek());
         } else {
            stack.add(i);
         }
       }
      return max;
    }
}
```

## Merge k Sorted Lists

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
      if(lists == null || lists.length == 0) return null;
      PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b)-> a.val - b.val);
      for (ListNode node : lists){
        if(node != null) pq.add(node);
      }
      ListNode dummy = new ListNode(-1);
      ListNode cur = dummy;
      while(!pq.isEmpty()){
        ListNode node = pq.remove();
        cur.next = node;
        if(node.next != null){
          pq.add(node.next);
        }
        cur = node;
      }
      return dummy.next;
    }
}
```

## Decode String

```java
class Solution {
    public String decodeString(String s) {
         Deque<Character> queue = new LinkedList<>();
        for (char c : s.toCharArray()) {
            queue.offer(c);
        }
        return helper(queue);
    }
    
    public String helper(Deque<Character> queue) {
        StringBuilder sb = new StringBuilder();
        int num = 0;
        while (!queue.isEmpty()) {
            char c= queue.poll();
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            } else if (c == '[') {
                String sub = helper(queue);
                for (int i = 0; i < num; i++) {
                    sb.append(sub);    
                }
                num = 0;
            } else if (c == ']') {
                break;
            } else {
                sb.append(c);
            }
        }
        return sb.toString();
    }
  }

```

## Word Break

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
       if (wordDict.contains(s)) return true;
    Queue<Integer> queue = new LinkedList<Integer>();
    List<String> res = new ArrayList<>();
    queue.offer(0);
    // use a set to record checked index to avoid repeated work.
    // This is the key to reduce the running time to O(N^2).
    Set<Integer> visited = new HashSet<Integer>();
    visited.add(0);
    while (!queue.isEmpty()) {
        int curIdx = queue.poll();
        for (int i = curIdx+1; i <= s.length(); i++) {
            if (visited.contains(i)) continue;
            if (wordDict.contains(s.substring(curIdx, i))) {
               res.add(s.substring(curIdx, i));
                if (i == s.length()) {
                  System.out.println(res + "test");
                  return true;
                }
                queue.offer(i);
                visited.add(i);
            }
        }
    }
    return false;
    }
}
```

