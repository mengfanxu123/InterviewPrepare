# JavaScript

### concat

The **`concat()`** method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]

```

### Array sort

Array sort is sort by aphbbate , not num order so use customer array

```javascript
num.sort((a, b)=>a-b)
```

### DeepCopy and shallowCopy

how to deepCopy and not change original data

* JOSN.parse\(JSON.stringify\(a\)\);
* Lodash

```javascript
var objects = [{ 'a': 1 }, { 'b': 2 }];
 
var deep = _.cloneDeep(objects);
console.log(deep[0] === objects[0]);
```

```javascript
function isObj(obj) {
    return (typeof obj === 'object' || typeof obj === 'function') && obj !== null
}

function deepCopy(obj, hash = new WeakMap()) {
    if(hash.has(obj)) return hash.get(obj)
    let cloneObj = Array.isArray(obj) ? [] : {}
    hash.set(obj, cloneObj)
    for (let key in obj) {
        cloneObj[key] = isObj(obj[key]) ? deepCopy(obj[key], hash) : obj[key];
    }
    return cloneObj
}

```

