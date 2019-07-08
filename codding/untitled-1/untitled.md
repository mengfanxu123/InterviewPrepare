# add\(a, b\) add\(a\)\(b\) add\(a\)\(b\)\(\)

```javascript
const add = function(a, b) {
  if (b) {
    return a + b;
  } else {
    return function(b) {
      return a + b;
    };
  }
};

console.log(add(1)(2));

const sum = function(x) {
  if (arguments.length === 2) {
    return arguments[0] + arguments[1];
  } else {
    return function(y) {
      return x + y;
    };
  }
};

console.log(sum(1, 2));

const add1 = (a, b) => (b || b === 0 ? a + b : b => a + b);
console.log(add1(2)(3));

function add(x) {
  let sum = x;
  return function resultFn(y) {
    if (arguments.length) {
      //not relying on falsy value
      sum += y;
      return resultFn;
    }
    return sum;
  };
}
console.log(add(1)(2)(2)());

```

