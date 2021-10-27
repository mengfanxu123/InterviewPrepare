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
