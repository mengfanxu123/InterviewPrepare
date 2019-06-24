# Remove Duplicate Number

```javascript
arr = [1, 2, 3, 5, 5, 4, 10, 12];
uniqueArray = arr.filter((ele, index) => {
  return arr.indexOf(ele) === index;
});

uniqueArray = [...new Set(arr)];
```



