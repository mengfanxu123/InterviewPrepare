# Merge Object Array

```javascript
obj1 = [
  { name: "Mandy", age: 26 },
  { name: "Peter", age: 21 },
  { name: "Tom" }
];
obj2 = [
  { name: "Mandy", company: "SIS" },
  { name: "Peter", company: "APPLE" },
  { name: "Tom", company: "Walmart" }
];

const merchageObj = (obj1, obj2) => {
  let res = [];
  for (let i = 0; i < obj1.length; i++) {
    res.push(Object.assign(obj2[i], obj1[i]));
  }
  return res;
};

console.log(JSON.stringify(merchageObj(obj1, obj2)));
```

