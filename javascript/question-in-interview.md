# question in interview

### How to validate a from

* Client-side validation :  

  * javaScript validation is coded using JavaScript: validation API and use Regular Expression with required pattern
  * Built-in form validation : use HTML5 form validation feature : HTML5 validation attribute 

* server side validation

{% code title="build-in validation" %}
```markup
<form>
<input type="text" id="choose" name="ilike" required/>
<button>submit</button>
</form>
```
{% endcode %}

```css
input : invalid {
    border : 2px dashed red
}
input: valid {
    border: 2px solid black
```

```markup
<form>  
 <label for="choose">Would you prefer a banana or a cherry?</label> 
 <input id="choose" name="i_like" required pattern="banana|cherry"> 
 <button>Submit</button>
</form>    
```

### Debounce

```javascript
// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      func.apply(this, args)
    }, wait)
  }
}
// 不难看出如果用户调用该函数的间隔小于wait的情况下，上一次的时间还未到就被清除了，并不会执行函数

```

How to hide element \(visually hide\) CSS grid v.s. Flexbox v.s. Float 

Accessibility 

SEO optimization

Implement\(HTML, CSS, Javascript\): 

### **Autocomplete Modal** 

{% embed url="https://codesandbox.io/s/autoinput-sl2l4" %}

```jsx
import React from "react";
import ReactDOM from "react-dom";

import "./styles.css";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.items = ["David", "Damien", "Sara", "James", "Jane", "Sapiens"];
    this.state = {
      suggestions: [],
      input: ""
    };
  }
  handleInput = e => {
    const value = e.target.value;
    let suggestions = [];
    if (value.length > 0) {
      const regex = new RegExp(`^${value}`, "i");
      suggestions = this.items.sort().filter(v => regex.test(v));
    }
    this.setState(() => ({ suggestions, text: value }));
  };
  suggestionSelected(value) {
    this.setState(() => ({
      text: value,
      suggestions: []
    }));
  }
  renderSuggeust() {
    const { suggestions } = this.state;
    return (
      suggestions.length !== 0 && (
        <div className="srchList">
          <ol>
            {suggestions.map(item => (
              <li onClick={() => this.suggestionSelected(item)}>{item}</li>
            ))}
          </ol>
        </div>
      )
    );
  }
  render() {
    return (
      <div>
        <div>
          <input value={this.state.value} onChange={this.handleInput} />
          <div>{this.renderSuggeust()}</div>
        </div>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

{% embed url="https://codepen.io/postleonardo/pen/PwdQmv" %}

\*\*\*\*

### **Progress bar**

{% embed url="https://codesandbox.io/s/progress-bar-hhon2" %}

```jsx
import React from "react";
import ReactDOM from "react-dom";

import "./styles.css";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      status: "start",
      width: 0,
      interval: ""
    };
  }
  handleClick = async () => {
    if (this.state.status === "start") {
      this.setState({ status: "stop" });
      let intervalId = setInterval(() => {
        if (this.state.width === 100) {
          return;
        }
        this.setState({ width: this.state.width + 1 });
      }, 200);
      this.setState({ interval: intervalId });
    } else if (this.state.status === "stop") {
      await clearInterval(this.state.interval);
      this.setState({ status: "start" });
    }
  };

  render() {
    return (
      <div>
        <div className="progress">
          <div className="filter" style={{ width: `${this.state.width}%` }} />
        </div>
        <button onClick={this.handleClick}>{this.state.status}</button>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

 ****

**Star widget** 

### **Timer** 

{% embed url="https://codesandbox.io/s/timer-8gd0c" %}

\*\*\*\*

Carousel 

Masonry 

Input Validator

Implement \(Javascript\): 

Promise 

Promise with limit 

Promise.all 

querySelector 

**EvenEmitter Observable**

 **Flat array** 

### Given two identical DOM tree structures, A and B, and a node from A, find the corresponding node in B.



Implement \(Util function\) 

Debounce 

Throttle 

Memoize Retry



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

function deepCopy(obj){
    //判断是否是简单数据类型，
    if(typeof obj == "object"){
        //复杂数据类型
        var result = obj.constructor == Array ? [] : {};
        for(let i in obj){
            result[i] = typeof obj[i] == "object" ? deepCopy(obj[i]) : obj[i];
        }
    }else {
        //简单数据类型 直接 == 赋值
        var result = obj;
    }
    return result;
}

```

