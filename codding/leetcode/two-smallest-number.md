# Two smallest  number

```javascript
let arr = [-1, 2, 3, 2, 0];
const smallNumebr = arr => {
  s1 = Number.MAX_SAFE_INTEGER;
  s2 = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] < 0) continue;
    if (arr[i] < s1) {
      s2 = s1;
      s1 = arr[i];
    } else if (arr[i] < s2) {
      s2 = arr[i];
    }
  }
  return s2;
};

console.log(smallNumebr(arr));
```

