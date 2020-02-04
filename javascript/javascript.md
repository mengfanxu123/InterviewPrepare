# JavaScript

### Common HTML Events



| onchange | An HTML element has been changed |
| :--- | :--- |
| onclick | The user clicks an HTML element |
| onmouseover | The user moves the mouse over an HTML element |
| onmouseout | The user moves the mouse away from an HTML element |
| onkeydown | The user pushes a keyboard key |
| onload | The browser has finished loading the page |

## String

### String method

1.  **indexof\(\)**var str = "Please locate where 'locate' occurs!"; var pos = str.indexOf\("locate"\); ans: 7
2. The **`lastIndexOf()`** method returns the index of the **last** occurrence of a specified text in a string:
3. The `search()` method searches a string for a specified value and returns the position of the match:

```javascript
var str = "Please locate where 'locate' occurs!";
var pos = str.search("locate");
document.getElementById("demo").innerHTML = pos;
```

### Extracting String Parts



* `slice(`_`start`_`,` _`end`_`)`
* `substring(`_`start`_`,` _`end`_`)`
* `substr(`_`start`_`,` _`length`_`)`

### Replacing String Content 

```text
str = "Please visit Microsoft!";
var n = str.replace("MICROSOFT", "W3Schools");
```

### Extracting String Characters



* `charAt(`_`position`_`)`
* `charCodeAt(`_`position`_`)`
* Property access \[ \]

### Converting a String to an Array

A string can be converted to an array with the `split()` method:

```text
var txt = "a,b,c,d,e";   // String
txt.split(",");          // Split on commas
txt.split(" ");          // Split on spaces
txt.split("|");  
```

## Number

### Numeric Strings

JavaScript will try to convert strings to numbers in all numeric operations:

This will work:

```javascript
var x = "100";
var y = "10";
var z = x / y;       // z will be 10

but x + y = 10010
// x means concat
```

### NaN - Not a Number

`NaN` is a JavaScript reserved word indicating that a number is not a legal number.

Trying to do arithmetic with a non-numeric string will result in `NaN` \(Not a Number\):

### Converting Variables to Numbers

There are 3 JavaScript methods that can be used to convert variables to numbers:

* The `Number()` method
* The `parseInt()` method
* The `parseFloat()` method

These methods are not **number** methods, but **global** JavaScript methods.



| Number\(\) | Returns a number, converted from its argument. |
| :--- | :--- |
| parseFloat\(\) | Parses its argument and returns a floating point number |
| parseInt\(\) | Parses its argument and returns an integer |

## Array

### Arrays are Objects

Arrays are a special type of objects. The `typeof` operator in JavaScript returns "object" for arrays.

But, JavaScript arrays are best described as arrays.

Arrays use **numbers** to access its "elements". In this example, `person[0]` returns John:

### Converting Arrays to Strings

The `join()` method also joins all array elements into a string.

It behaves just like `toString()`, but in addition you can specify the separator:  


```text
var fruits = ["Banana", "Orange", "Apple", "Mango"];
document.getElementById("demo").innerHTML = fruits.join(" * ");
```

### Pop Shift push unshift

pop remove last element 

shift remove first element

push add in last 

unshift add in first

### Deleting Elements

```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
delete fruits[0];           // Changes the first element in fruits to undefined

```

### Splicing an Array

The first parameter \(2\) defines the position **where** new elements should be **added** \(spliced in\).

The second parameter \(0\) defines **how many** elements should be **removed**.

The rest of the parameters \("Lemon" , "Kiwi"\) define the new elements to be **added**.

The `splice()` method returns an array with the deleted items:

```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(2, 2, "Lemon", "Kiwi");
```

### Using splice\(\) to Remove Elements

```javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.splice(0, 1);        // Removes the first element of fruits
```



### Merging \(Concatenating\) Arrays

The **`concat()`** method is used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.

```javascript
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]

```

### Slicing an Array

he `slice()` method slices out a piece of an array into a new array.

This example slices out a part of an array starting from array element 1 \("Orange"\):

```javascript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1);
```

The `slice()` method can take two arguments like `slice(1, 3)`.

The method then selects elements from the start argument, and up to \(but not including\) the end argument.

### JavaScript Array Iteration Methods

### Array.forEach\(\)

cannot break



### Array.map\(\)

The `map()` method creates a new array by performing a function on each array element.

The `map()` method does not execute the function for array elements without values.

The `map()` method does not change the original array.

This example multiplies each array value by 2:

### Array.filter\(\)

### Array.reduce\(\)

```text
var numbers1 = [45, 4, 9, 16, 25];
var sum = numbers1.reduce(myFunction);

function myFunction(total, value, index, array) {
  return total + value;
}
```

Note that the function takes 4 arguments:

* The total \(the initial value / previously returned value\)
* The item value
* The item index
* The array itself

The example above does not use the index and array parameters. It can be rewritten to:

### Array sort

Array sort is sort by aphbbate , not num order so use customer array

```javascript
num.sort((a, b)=>a-b)
```

### Array.every\(\)

The `every()` method check if all array values pass a test.

This example check if all array values are larger than 18:

### Array.some\(\)

### Array.indexOf\(\)

### Array.find\(\)

```javascript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12

```

### Array.findIndex\(\)

### Array.prototype.flat\(\)

```text

```

## Map

```javascript
let map1 = new Map();
map1.set('bar', 'foo');

console.log(map1.get('bar'));
// expected output: "foo"

console.log(map1.get('baz'));
```

