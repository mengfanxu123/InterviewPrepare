# Flatten

### Flatten nested array

* reduce

```javascript
function flatten(data) {
  return data.reduce(function(flat, toFlatten) {
    return flat.concat(Array.isArray(toFlatten) ? flatten(toFlatten) : toFlatten);
  }, []);
}
```

* forEach

```javascript
const flatten = data => {
  let res = [];
  data.forEach(ele => {
    if (Array.isArray(ele)) {
      res.push(...flatten(ele));
    } else {
      res.push(ele);
    }
  });
  return res;
};
```

