# Amazon

## freq  &gt; 10



### Merge Two Sorted Lists\(12\)



Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```text
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                cur.next = l1;
                l1 = l1.next;
            } else{
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        if(l1 != null){
            cur.next = l1;
        }else{
            cur.next = l2;
        }
        return dummy.next;
    }
}
```



### 132 Pattern\(12\)

{% embed url="https://leetcode.com/problems/132-pattern/" %}

```java
class Solution {
    public boolean find132pattern(int[] nums) {
         if(nums == null || nums.length < 3) {
            return false;
        }
        for(int i = 0; i < nums.length - 2; i++) {
            int bigger = nums[i];    
            for(int j = i + 1; j < nums.length; j++) {
                // 1. We don't care about numbers
                // less than a[i]
                if(nums[j] <= nums[i]) continue;
                
                // 2. If num is greater than bigger
                // then update bigger
                if(nums[j] >= bigger) {
                    bigger = nums[j];
                } else {
                    // Now this number is greater than nums[i]
                    // see 1. and less than bigger, see 2.
                    return true;
                }  
            }
        }
        return false;
    }
}
```

### Meeting Rooms II\(19\)

{% embed url="https://leetcode.com/problems/meeting-rooms-ii/" %}



```java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        int[] start = new int[intervals.length];
        int[] end = new int[intervals.length];
        for (int i = 0; i < intervals.length; i++){
            start[i] = intervals[i][0];
            end[i] = intervals[i][1];
        }
        Arrays.sort(start);
        Arrays.sort(end);
        int room = 0;
        int endindex = 0;
        for (int i = 0; i < intervals.length; i++){
            if(start[i] < end[endindex]){
                room++;
            }else {
                endindex++;
            }
        }
        return room;
    }
}
```



