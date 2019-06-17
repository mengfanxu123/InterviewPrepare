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

