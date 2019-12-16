# Jump\[DP\]

思路： 从后往前scan 因为最后一个left elemnet is true we will as default value and we have 2 situations

1. this position jumps will reach the last ele, we will just need one step and we can set this position as true
2. if we cannot directly reach the end, we should jump for nums\[i\] to 0 to jump to other postion at i + j, if i + j can reach last end this position can also reach last end this min step also is min\[i + j\] + 1

45Jump Game II

```javascript
// timeo(n)
// space o(n)
class Solution {
    public int jump(int[] nums) {
        int dp[] = new int[nums.length];
        
        dp[nums.length - 1] = 0;
        for (int i = nums.length - 2; i >= 0; i--){
            if(nums[i] + i >= nums.length - 1) dp[i] = 1;
            else{
                int min = Integer.MAX_VALUE;
                for(int j = nums[i]; j > 0; j--){
                    if(dp[i + j] == 0) continue;
                    min = Math.min(dp[i + j], min);
                }
                if(nums[i] == 0 || nums[i] != 0 && min == Integer.MAX_VALUE){
                    dp[i] = 0;
                } else {
                    dp[i] = min + 1;
                }
            }
        }
        return dp[0];
    }
}
```

55Jump Game

```java
class Solution {
    public boolean canJump(int[] nums) {
        boolean[] dp = new boolean[nums.length];
        dp[nums.length - 1] = true;
        for (int i = nums.length - 2; i >= 0; i--){
            if(i + nums[i] > nums.length - 1){
                dp[i] = true;
            }else {
                for (int j = 1; j <= nums[i]; j++){
                    if(dp[i + j] == true) {
                        dp[i] = true;
                    break;
                }
            }
            
        }
       
    }
         return dp[0];
}
}

```

