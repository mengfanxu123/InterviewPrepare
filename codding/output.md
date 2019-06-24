# Output

### Kroger closure

```javascript
//1.
function m(mul) {
  var myf = function(x) {
    return mul * x;
  };
  return myf;
}
var operation = m(10);
console.log(operation(10));
// output 100

//2. 
var x = 10;
if ((null) || (console.log("Hello")) || x > 5) {
 console.log("Hello");
}
// the "Hello" will be printed 2 times.
*/
//3.
// funcObject - object instantiation & this tests
let Circle = function (radius) {
 this.radius = radius;
 this.getArea = function() {
     return Math.PI*Math.pow(this.radius, 2);
 }
}
// Note: new in call
let myCircleNew = new Circle(5);  // area - 78.5 for radius 5
console.log("myCircleNew...  logs");
console.log(myCircleNew.getArea());
// Note:  no new in call
let myCircleDirectCall = Circle(10); // area 314.16
console.log("myCircleDirectCall...  logs");
console.log(myCircleDirectCall.getArea());
// myCircleNew.getArea() returns 78.5;  myCircleDirectCall.getArea() fails with error

// 4. 
var counter = 0;
var myArray = ["Yaakov", 2, {handle: "yaakovchaikin"}];
for (var i = 0; i < myArray.length; i++) {
 console.log(counter++);
}
console.log(counter); // 3

// 5.
let myLiteralObj = {
    age: 20,
    setAge: (newAge) => {
        this.age = newAge; //this指的是window，57
    },
    getAge: () => this.age, //this指的是window，57
    getSeniorStatusThroDirectAccess:  function() {
        if (this.age>55)    // Note direct attribute access，this指的是myLiteralObj，20
            return "Senior";
        else
            return("Not Senior")
    },
    getSeniorStatusThroGettor:  function() {
        if (this.getAge()>55)      // Note access via Gettor，57
            return "Senior";
        else
            return("Not Senior")
    },
}
myLiteralObj.setAge(57);
console.log("DirectAccess: " +
        myLiteralObj.getSeniorStatusThroDirectAccess());
console.log("Through gettor: " +
        myLiteralObj.getSeniorStatusThroGettor());
//   Output is “DirectAccess: Not Senior”  followed by “Through gettor: Senior”
// 6.

 (function(window) {

3  var obj = {};
4
5  obj.dreamOn = function () {
6   console.log("I want to see the global scope! Let me out!");
7  };
8
9  window.doer = obj;
10
11 });
12
13 doer.dreamOn();

// D.     The attempted Immediately Invoked Function Execution (IIFE) is not being invoked and passed in the window object. It's missing '(window)' Line 11 right before the semicolon.

```

**7. DOM manipulation: Given this HTML and the 2 code snippets**

| **&lt;input id="name" type="text" value="Hi"&gt;** |
| :--- |


**Snippet 1**

| **console.log\(document.getElementById\("name"\).value + " Hello world!"\);** |
| :--- |


**Snippet 2**

| **console.log\(document.querySelector\("\#name"\).value + " Hello world!"\);** |
| :--- |


**What will be the difference in the output between the 2 Javascript code snippets?**

**A.     No difference**

**B.     First one will not display the word 'Hi'**

**C.     Second one will throw a Javascript error.**

**D.     First one will throw a Javascript error.**

**Answer: A**  


**8.  Events:  What will the code snippet below do?**

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><b>...</b>
        </p>
        <p><b>&lt;head&gt;</b>
        </p>
        <p><b>&lt;script&gt;</b>
        </p>
        <p><b>document.addEventListener(&quot;DOMContentLoaded&quot;, function(event) {</b>
        </p>
        <p><b>  console.log(&quot;Yey!&quot;);</b>
        </p>
        <p><b>});</b>
        </p>
        <p><b>&lt;/script&gt;</b>
        </p>
        <p><b>&lt;/head&gt;</b>
        </p>
        <p><b>&lt;body&gt;</b>
        </p>
        <p><b>...</b>
        </p>
        <p><b>&lt;h1&gt;Hello!&lt;/h1&gt;</b>
        </p>
        <p><b>&lt;/body&gt;</b>
        </p>
        <p><b>&lt;/html&gt;</b>
        </p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>**A.     It will output Yey! when the web page is loaded, but before external resources like images are downloaded to ≠ user's machine.**

**B.     It will output Yey! when the user hits the Reload browser button.**

**C.     It will never output Yey!**

**D.     It will output Yey! concurrently as the browser displays the 'h1' tag.Answer: A**

