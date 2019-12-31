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

### Design Class Emitter

```javascript
class Emitter {
  constructor(){
    this.subscribedEvents = new Map();
  }

  subscribe(eventName, callback) {
    this.subscribedEvents.set(eventName, callback);
  }

  unsubscribe(eventName) {
    this.subscribedEvents.delete(eventName);
  }

  emit(eventName){
      const callback = this.subscribedEvents.get(eventName);
      if(callback){
        const args = Array.from(arguments);
        args.splice(0, 1);
        callback.apply(this, args);
      }
  }
}

const emmiter = new Emitter();
emmiter.subscribe("event1", (name, surname)=&gt;{alert[name + " " + surname)});
emmiter.emit("event1", "Hello", "World");
emmiter.unsubscribe("event1");
emmiter.emit("event1", "Hello", "World");
```



