# Untitled

**Singleton, Rest api \(blog post\)**  
**Maximum sum sub array**

\*\*\*\*

**distributed system, load balancing, session, CDN**

\*\*\*\*

### Hover:

```css
.element {
  width: 50px;
  height: 30px;
  background-color: pink;
  transition: width 2s;
}

.element:hover {
  width: 100px;
  height: 30px;
  background-color: pink;
}
```

```markup
<div class="element">
</div>
```

**1.Write a form component with redux, thunk && back-end server\(app.put\(...\)\)**

**2.Write a component which can fetch data and show the data from the backend server with redux, thunk, back-end server**

**3.Write a shrink div, hover with an animation to expend**

[**https://codepen.io/ShiweiCao/pen/Zjgwmw**](https://codepen.io/ShiweiCao/pen/Zjgwmw)  
****

**4.Write the class “Calc” to make below codes work:**

 **Let a = new Calc\(2\)**

 **a.add\(2\).multiple\(3\).value\(\) = 12**  


```javascript
class Calc {
   constructor(value) {
       this.value = value;
   }
   add(value) {
       this.value += value;
       return this;
   }
   multiple(value) {
       this.value *= value;
       return this;
   }
   getValue() {
       return this.value;
   }
}


let a = new Calc(2);
let b = a.add(2).multiple(3).getValue();
console.log(b);

```

**.两个大小数组找交集，分析时间空间复杂度**

**1\) Initialize intersection I as empty.**

**2\) Find smaller of m and n and sort the smaller array.**

**3\) For every element x of larger array, do following**

**…….b\) Binary Search x in smaller array. If x is present, then copy it to I.**

**4\) Return I.**

**2.解释mergeSort**  


