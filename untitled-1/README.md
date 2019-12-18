# CSS

### What is CSS

CSS is a language that describes the style of an HTML language 

### Specificity Herarchy

Inline style &gt; id &gt; class , attribute &gt; element

###  Id VS class

Id specificity hierarchy is higher than class.  id is unque used in a specific element, and class can use in my different places 

### New Feature in CSS3

* Media Query
* Selector
* Flex box
* Transform
* Multicolumn Layout

### Box Model

margin border padding context and box model is essentially a box that wraps around every html element

### ​display

* inline
* block: start in new line example: &lt;div&gt; &lt;h1&gt;
* inline-Block: allow set width and height on the element

### Display: none VS Visibility: hidden

* visibility: hides the element, but still takes up space in layout
* display: remove the element from the doc, it does not take up any space

### flex box

set parent element display: flex 

#### perfect centering

{% code title="center div" %}
```css
.outer {
    display: flex;
    height: 300px;
    width:300
    justify-content: center;
    align-items: center;
    background:red;
}
.inner {
    height: 100px;
    width: 100px;
    background: blue
}

```
{% endcode %}

```css
.outer {
    position: relative;
    width: 300px;
    height: 300px;
    background:red;
}
.inner {
    position: absolute;
    top: 50%;
    left:50%;
    transform: translate(-50%, -50%);
}
```

```markup
<div class="outer">
    <div class="inner">
    </div>
</div>
```

{% embed url="https://codepen.io/mengfanxu123/pen/qGGZZO" %}

### How to layout 1:2:1 3 div

{% embed url="https://codepen.io/mengfanxu123/pen/qeEBGx" %}

```css
.outer{
  display : flex;
  flex-wrap: wrap;
}

.div1{
  background: red;
  height: 100px;
  flex-grow: 1
}

.div2{
  background: blue;
  height: 100px;
/*   width:25% */
  flex-grow: 2
}

.div3{
  background: pink;
  height: 100px;
  flex-grow:1;
  
}

.out{
  display: flex;
  height: 200px;
  width: 200px;
  background: grey;
  justify-content: center;
  align-items:center;
}

.in{
  height: 100px;
  width: 100px;
  background: black
}
```

### 

### Flex Vs Grid 

* grid is two dimensions and flex is one dimension
* grid is more useful in large part and flex is more useful in small part 

### [P](https://codepen.io/mengfanxu123/pen/qGGZZO)osition

* static : default position
* relative: is positioned relative to its normal position, adjust away from its normal position 
* fixed: positioned relative to the view point, always stay in same place even if the page is scrolled
* absolute: is positioned relative to the nearest positioned ancestor 
* sticky: is positioned based on the user's scroll position. Between relative and fixed

### Responsive Design

* Meidia query
  * define different style rules for different media types and handle different devices' viewport



* Flexbox

  * need a container with attributes display: display : flex flex-wrap

{% embed url="https://codepen.io/mengfanxu123/pen/BXyzoP" %}

{% embed url="https://codepen.io/estelle/pen/brDpB" %}

## z-index

The `z-index` property specifies the stack order of an element.

An element with greater stack order is always in front of an element with a lower stack order.

**Note:** `z-index` only works on positioned elements \(position: absolute, position: relative, position: fixed, or position: sticky\).



