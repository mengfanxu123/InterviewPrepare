---
description: 面经 - f
---

# screening round

### implement Array.prototype.flat()

```javascript
// Some code
function flat(arr, depth = 1) {
  // your imeplementation here
  let res = [];
  arr.forEach(el => {
    if(Array.isArray(el) && depth){
      res.push(...flat(el, depth - 1));
    } else {
      res.push(el);
    }
  });
  return res;
}
// reduce 
const flat = (arr, depth = 1) =>
    arr.reduce((acc, cur) => [
      ...acc,
    ...(Array.isArray(cur) && depth ? flat(cur, depth - 1) : [cur])
  ], [])
// 
```

### create an Event Emitter

```javascript
// Some code
create an Event Emitter
const sub1  = emitter.subscribe('event1', callback1)
const sub2 = emitter.subscribe('event2', callback2)
const sub3 = emitter.subscribe('event1', callback1)
emitter.emit('event1', 1, 2);
// callback1 will be called twice
sub1.release()
sub3.release()
class EventEmitter {
  constructor(){
    this.map = new Map();
  }
  subscribe(eventName, callback) {
  	if(this.map.has(eventName)){
      this.map.get(eventName).push(callback);
    } else {
      this.map.set(eventName, [callback]);
    }
    return {
      release: () => {
        const t = this.map.get(eventName);
        if(t){
          t.splice(t.indexOf(callback), 1);
          if(t.length === 0){
            this.map.delete(t);
          }
        }
      }
    }
  }
  
  emit(eventName, ...args) {
  	if(this.map.has(eventName)){
      let targets = this.map.get(eventName);
      for (let callback of targets){
        callback(...args);
      }
    }
  }
}
```

### find corresponding node in two identical DOM tree

```javascript
// Some code
19. find corresponding node in two identical DOM tree


/**
 * @param {HTMLElement} rootA
 * @param {HTMLElement} rootB - rootA and rootB are clone of each other
 * @param {HTMLElement} nodeA
 */
const findCorrespondingNode = (rootA, rootB, target) => {
  // your code here
  if(rootA === target){
    return rootB;
  }
  let queueA = [rootA];
  let queueB = [rootB];
  while(queueA.length){
    const currElementA = queueA.shift();
    const currElementB = queueB.shift();
    if(currElementA === target){
      return currElementB;
    }
    queueA.push(...currElementA.children);
    queueB.push(...currElementB.children);
  }
  return null;
}
// recursion
const findCorrespondingNode = (rootA, rootB, target) => {
    
    if(rootA == target){
        return rootB;
    }
    
    for(let i = 0; i < rootA.children.length; i++){
        const res = findCorrespondingNode(rootA.children[i], rootB.children[i], target)
        if(res){
            return res;
        }
    }
}
// API
onst findCorrespondingNode = (rootA, rootB, target) => {
  // your code here
  const rootAWalker = document.createTreeWalker(rootA, NodeFilter.SHOW_ELEMENT);
  const rootBWalker = document.createTreeWalker(rootB, NodeFilter.SHOW_ELEMENT);
  let currentNodes = [rootAWalker.currentNode, rootBWalker.currentNode]
  while(currentNodes[0] !== target){
    currentNodes = [rootAWalker.nextNode(), rootBWalker.nextNode()];
  }
  return currentNodes[1];
}
```

### implement basic throttle()

```javascript
// Some code
implement basic throttle()
/**
 * @param {Function} func
 * @param {number} wait
 */
function throttle(func, wait) {
  // your code here
  let timer = 0;
  let delayedFunc;
  return (arg) => {
    if(timer === 0){
      func(arg);
      timer = setTimeout(()=> {
        timer = 0;
         if(delayedFunc) delayedFunc();
      }, wait)
    } else {
      delayedFunc = () => func(arg);
    }
  }
}
```

### implement basic debounce

```javascript
// Some code
function debounce(func, wait) {
  let cancel = null;
  return (args) => {
    clearTimeout(cancel)
    cancel = setTimeout(() => func(...args), wait)
  }
}
```

### Clear all timeout&#x20;

```javascript
// Some code
28. implement clearAllTimeout()

setTimeout(func1, 10000)
setTimeout(func2, 10000)
setTimeout(func3, 10000)

// all 3 functions are scheduled 10 seconds later
clearAllTimeout()

// all scheduled tasks are cancelled.


/**
 * cancel all timer from window.setTimeout
 */
let timers = [];
let originalClearTimeout = setTimeout;
window.setTimeout = (...args) => {
  var timerId = originalClearTimeout(...args);
  timers.push(timerId);
  return timerId;
}
function clearAllTimeout() {
  // your code here
  timers.forEach(t=>window.clearTimeout(t));
}

```

### Improve a function

```javascript
// Some code
let items = [
  {color: 'red', type: 'tv', age: 18}, 
  {color: 'silver', type: 'phone', age: 20},
  {color: 'blue', type: 'book', age: 17}
] 

// an exclude array made of key value pair
const excludes = [ 
  {k: 'color', v: 'silver'}, 
  {k: 'type', v: 'tv'}, 
  ...
] 

function excludeItems(items, excludes) { 
  excludes.forEach( pair => { 
    items = items.filter(item => item[pair.k] === item[pair.v])
  })
 
  return items
} 
/**
 * @param {object[]} items
 * @excludes { Array< {k: string, v: any} >} excludes
 */

/**
 * @param {object[]} items
 * @param { Array< {k: string, v: any} >} excludes
 * @return {object[]}
 */
function excludeItems(items, excludes) {
  let map = new Map();
  for (let {k, v} of excludes){
    if(!map.has(k)){
      map.set(k, new Set());
    }
      map.get(k).add(v);
  }
  return items.filter(el => {
    return !Object.keys(el).some(key => map.has(key) && map.get(key).has(el[key]));
  })
}
```

### Create a simple store for DOM element

```actionscript
// Some code
class NodeStore {
   /**
   * @param {Node} node
   * @param {any} value
   */
  constructor(){
    this.map = {};
  }
  set(node, value) {
   const symbol = Symbol();
   node.symbol = symbol;
   this.map[symbol] = value;
  }
  /**
   * @param {Node} node
   * @return {any}
   */
  get(node) {
   const symbol = node.symbol;
   return this.map[symbol];
  }
  
  /**
   * @param {Node} node
   * @return {Boolean}
   */
  has(node) {
    return this.map[node.symbol] !== undefined;
  }
}
```

### _give distance, time as parameter, wirte a function can do animation that move a box from left side to right side._

__

```javascript
// Some code
let e = document.getElementById("move");
const animationElement = function(element, duration, distance)
{
  const startTime = new Date().getTime();
  let endTime = null;
  const ani = setInterval(()=> {
    endTime = new Date().getTime();
    const p = (endTime - startTime)/duration;
    if(p >= 1){
      clearInterval(ani);
    }
      element.style["margin-left"] = p * distance + "px";
  }, 10)
}


animationElement(e, 3000, 200);
```

### 113. Virtual DOM I

```javascript
// Some code
/**
 * @param {HTMLElement} 
 * @return {object} object literal presentation
 */
function virtualize(element) {
  // your code here
  const result = {
    type: element.tagName.toLowerCase(),
    props: {}
  }
  // props without children
  for (let attr of element.attributes){
    const name = attr.name === "class" ? "className" : attr.name;
    result.props[name] = attr.value;
  }
  //children
  const children = [];
  for (let node of element.childNodes){
     if (node.nodeType === 3) { // text node
      children.push(node.textContent)
    } else {
      children.push(virtualize(node))
    }
  }
  result.props.children = children.length === 1 ? children[0] : children
  return result
}


/**
 * @param {object} valid object literal presentation
 * @return {HTMLElement} 
 */
function render(json) {
  // your code here
  if (typeof json === 'string') {
    return document.createTextNode(json)
  }
  
  // element
  const {type, props: {children, ...attrs}} = json
  const element = document.createElement(type)
  
  for (let [attr, value] of Object.entries(attrs)) {
    element[attr] = value
  }
  
  const childrenArr = Array.isArray(children) ? children : [children]
  
  for (let child of childrenArr) {
    element.append(render(child))
  }
  
  return element
}

```

### 118. Virtual DOM II - createElement

```javascript
// Some code
function createElement(type, props, ...children) {
  // your code here
  return {
    type,
    props: {
      ...props,
      children
    }
  }
}


/**
 * @param { MyElement }
 * @returns { HTMLElement } 
 */
function render(myElement) {
  // your code here
 if (typeof myElement === 'string') {
    return document.createTextNode(myElement);
  }
  const {type, props: { children, ...attrs}} = myElement;
  const currentNode = document.createElement(type);
  for(let [attr, value] of Object.entries(attrs)) {
    currentNode[attr] = value;
  }
  const childrenArr = Array.isArray(children) ? children : [children];
  for (let child of childrenArr) {
    currentNode.append(render(child));
  }
  return currentNode;
}
```

### 140. Virtual DOM III - Functional Component

```javascript
// Some code
140. Virtual DOM III - Functional Component
function createElement(type, props, ...children) {
  // your code here
  if(typeof type === 'function'){
    return type ({...props, children});
  }
  return {
    type,
    props: {
      ...props,
      children
    }
  }
}


/**
 * @param { MyElement }
 * @returns { HTMLElement } 
 */
function render(myElement) {
  // your code here
  if (typeof myElement === 'string'){
    return document.createTextNode(myElement);
  }
  const {type, props: {children, ...attrs}} = myElement;
  const node = document.createElement(type);
   for(let [attr, value] of Object.entries(attrs)) {
    node[attr] = value;
  }
  const childrenArr = Array.isArray(children) ? children : [children];
  for (let child of childrenArr) {
    node.append(render(child));
  }
  return node;
}
```
