# instacart

```javascript
// const timeMap = function () {
//   this.map = new Map();
//   this.recentMap = new Map();
// };

// timeMap.prototype.set = function (key, value, timestamp) {
//   if (!this.map.has(key)) this.map.set(key, []);
//   this.map.get(key).push({ value, timestamp });
//   this.recentMap.set(key, value);
// };

// timeMap.prototype.get = function (key, timestamp) {
//   if (!this.map.has(key)) return "";
//   if (timestamp === undefined) {
//     return this.recentMap.get(key);
//   }
//   return this.binarySearch(this.map.get(key), timestamp);
// };

// timeMap.prototype.binarySearch = function (arr, timestamp) {
//   console.log(this.map);
//   let l = 0,
//     r = arr.length - 1;
//   while (l < r - 1) {
//     const mid = Math.floor((l + r) / 2);
//     console.log(mid, "mid", arr[mid].timestamp);
//     if (arr[mid].timestamp === timestamp) return arr[mid].value;
//     if (arr[mid].timestamp < timestamp) {
//       l = mid;
//     } else {
//       r = mid;
//     }
//   }
//   console.log(l, r, "l, r");
//   if (arr[r] && arr[r].timestamp <= timestamp) return arr[r].value;
//   if (arr[l] && arr[l].timestamp <= timestamp) return arr[l].value;
//   return "";
// };

// let m = new timeMap();
// m.set("a", "a1", 1);
// m.set("b", "b1", 1);
// m.set("a", "a2", 2);
// m.set("a", "a3", 4);
// console.log(m.get("a", 3));


const map = function () {
  this.map = new Map();
  this.recentMap = new Map();
};

map.prototype.set = function (key, value, timestamp) {
  this.map.set(`${key}-${timestamp}`, value);
  this.recentMap.set(key, value);
};

map.prototype.get = function (key, timestamp) {
  if (timestamp !== null) {
    return this.map.get(`${key}-${timestamp}`);
  } else {
    return this.recentMap.get(key);
  }
};
```

