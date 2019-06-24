# JavaScript

### JavaScript

JavaScript is a high-level, interpreted programming language

### ES6 New Feature

* Let Const
* Class
* Arrow Function
* Spread and Destructing
* Modules
* Promise
* Symbol

### Hoisting

Hoisting is a term used to explain the behavior of 'var ' declaration. When declared or initialized with the var keyword. var will move up to the top of the current scope

However, only the variable declarations and function declarations are hoisted. Variable assignments and function expressions are not hoisted. 

```javascript
console.log(myName);
var myName = "Mandy";
// out put undefined

var myName;
console.log(myName);
myName = "Mandy"

```

### Closure

A closure is inner function that has access to the variables in the outer function



### Callback Function

The callback function is a function passed into another function as argument, which is then invoked inside the outer function to complete an outer function

```javascript
function printString(string, callback){
    setTimeOut(
     () => {
      console.log(string)
      callback()
     }, 
     Math.floor(Math.random() * 100) + 1
    )
}
// print A B and C callback hell
function printAll(){
  printString("A", ()=>{
   printString("B", ()=>{
    printString("C", ()=>{})
   })
  })
}
```

### Callback Hell

Callback Hell is a problem caused by asynchronous AJAX call, Which means where are mutliple nested callback hell

### Promise

Promise is a function to solve the async issues.

it is must be one of these states

* Pending: initial state, not fulfilled or rejected
* fulfilled: operation completed successfully
* rejected: meaning that operation failed

a promise object will either successes or fail

promised all : return a single promise that resolves when all of the promise in argument have solved or when the outterable argument contains no promises

{% code-tabs %}
{% code-tabs-item title="Promise" %}
```javascript
function printString(string){
    return new Promise((resolve, reject)=>{
        setTimeout(
            () =>{
                console.log(string)
                resolve
            }, Math.floor(Math.random() * 100) + 1
        )
    })
}
function printAll(){
    printString("A")
    .then(() => printString("B"))
    .them(() => printString("C"))
}
printAll()

function asyncDouble(n){
    return new Promise((resolve, reject)=>{
        if (typeof n === "number"){
            resolve(n*2)
        } else {
            reject(new Error(n + "is not a number"))
        }
    })
}
asyncDouble(3)
.then(
    date =>console.log(data);
    error =>console.log(error);
    )
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### How to use promise chain

```javascript
doSometing()
.then(result => doSomethingElse(result))
.then(newResult => doThirdThing(newResult))
.then(finalResult => {
    console.log(`Got the final result: ${finalResult}`)
})
.catch(failureCallback)
```

### Composition

Promise.resolve\(\) and Promise.rejcet\(\) are shortcut to manually create an already resolved or rejected promise respectively

We can start operations in parallel and wait for them to finished 

```javascript
Promise.all([func1(), func2(), func3()])
.then(([result1, result2, result3]) => {/*use result1, res2, res3*/})
```

```javascript
[func1, func2, func3].reduce((p, f) => p.then(f), Promise.resolve())
.then(result3 => { /* use result3 */ });
// sequential composition can be done mor simply with await
let result;
for (const f of [func1, func2, func3]) {
  result = await f(result);
}
```

### Splice\(\)

Syntax: 

```text
var arrDeletedItems = array.splice(start[, deleteCount[, item1[, item
2[, ...]]]])
```

char.splice\(startIndex, removeItemsNums, insert items1, intert items2\)

### Ways to improve the website loading time

* improve your hosting plan
* understand http request and reduce the http request
* make images internet-friendly. compress your image, lazy loading content
* take advantage of caching: download to you hard drive once into cache, or temporary storage space. Those files are now store locally. 
* Uitilize CDNS and Remove Unused Script 

### Event Loop

JS is a single thread language and allow js to use promise and callback during the event loop, first function will be added to a call stack, when this function is settime out or this is a promise, it will be added to event queue, we will check the call stack whether empty or not, if it is empty, it will then add the event queue function to stack, and execute 

### Prototypal inheritance VS Classical inheritance

classical inheritance: a description of the object to be created. Classes inherit from classes and create subclass relationships.

prototypal inheritance: a prototype is a working object instance. Objects inherit directly from other objects. 

### Assign



```javascript
var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```



