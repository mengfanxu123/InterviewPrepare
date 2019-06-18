# leetcode

### 560 Subarray Sum Equals K

{% embed url="https://leetcode.com/problems/subarray-sum-equals-k/" %}



Given an array of integers and an integer **k**, you need to find the total number of continuous subarrays whose sum equals to **k**.

**Example 1:**  


```text
Input: nums = [1,1,1], k = 2
Output: 2
```

```javascript
// method 1: prefixSum O(n^2)

```

```javascript
var subarraySum = function(nums, k) {
    if (nums === null || nums.length === 0) return 0;
    let map = {};
    map[0] = 1;
    let count = 0
    prefixSum = 0
    nums.forEach(ele => {
        prefixSum += ele;
        count += (map[prefixSum - k] || 0) 
        map[prefixSum] = (map[prefixSum] || 0) + 1;
    });
    return count;
    
};
```



### 509 Fibonacci Number

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

```text
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
```

Given `N`, calculate `F(N)`.

{% embed url="https://leetcode.com/problems/fibonacci-number/" %}

1. recursive
2. DP

```javascript
const fib = (N) => {
    if(N === 0) return 0;
    if(N === 1) return 1
    return fib(N - 1) + fib(N - 2)
}
// Time complexity O(2^n)
// Space O(n) call stack
const fib = N => {
    if(N === 0)return 0;
    if(N ==== 1) return 1;
    let dp = new Array(N + 1);
    dp[0] =0;
    dp[1] = 1;
    for(let i = 2; i <= N; i++){
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[N]
}
// time complexity o(n)
// space O(n)

```

### 1. 2SUM

```javascript
var twoSum = function(nums, target) {
    let map = {};
    let res = []
    for (let i = 0; i < nums.length; i++){
        if(map[target - nums[i]] != null && map[target - nums[i]] !== i ){
            res.push(i, map[target - nums[i]]);
            return res;
        }
        map[nums[i]] = i;
    }
};
```

