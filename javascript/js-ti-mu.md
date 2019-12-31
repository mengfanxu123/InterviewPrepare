# JS 题目

## 对于object 处理

**Given: a=1 b=2 c=3 d=4 e=5 f=6 ... z=2**

**abc -&gt; 1 + 2 + 3 = 6**

**bdc -&gt; 2 + 4 + 3 = 9**

**fc -&gt; 6 + 3 = 9**  


**Input: "abc cde adb dfb def ee abcd cc"**  


**output: {**

  **"6": \["abc", "cc"\],**

  **"12": \["cde", "dfb"\],**

  **"7": \["adb"\],**

  **"15": \[ "def"\],**

  **"10": \["ee", "abcd"\]**

**}**  


```javascript
const conver = str => {
  let map = {};
  let arr = str.split(" ");
  arr.forEach(element => {
    let num = 0;
    for (let i = 0; i < element.length; i++) {
      num += element.charCodeAt(i) - 96;
    }
    if (map[num] !== undefined) {
      map[num].push(element);
    } else {
      map[num] = [element];
    }
  });
  return map;
};

console.log(JSON.stringify(conver("abc cde adb dfb def ee abcd cc")));

```



