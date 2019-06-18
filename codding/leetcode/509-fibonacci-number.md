# 509 Fibonacci Number



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

