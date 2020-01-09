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

