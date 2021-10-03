# google

## BQ

Talk about the projects you worked on One time you went above and beyond to help others One time you have to change the design decisions midway

One time when you work with tight deadline



Front End 面筋

```javascript
implemnet customer setInerval clearInterval

function myInterval(fun, period){
    let timeMapid = {id : null};
    const wrapper = () => {
        timeMapid = setTimeout(()=>{
            fun();
            wrapper();
            
        }, period);
    }
    wrapper();
    return timeMapid;
}

const timerMapId = myInterval(()=>{
    console.log("callbacl");
    
}, 1000);

setTimeout(() => {
  clearTimeout(timerRef.id);
}, 5000);


```

```javascript
// Given functions
// fetchFruit(prefix, callback) // => callback called with array of fruit
// fetchAnimal(prefix, cb) // => callback called with array of animal
// fetchMiniral(prefix, cb) // => callback called with array of miniral
//  
// implement function mergeFetcher
//  
// const merged = mergeFetcher([fetchFruit, fetchAnimal, fetchMinirla]);
//  
// merged(‍‍‍‌‌‌‍‍‌‍‍‍‌‌‌‌‌‌‍'a', callback); //callback called with all result combined.
// Given functions
// fetchFruit(prefix, callback) // => callback called with array of fruit
// fetchAnimal(prefix, cb) // => callback called with array of animal
// fetchMiniral(pr‍‌‌‍‌‍‌‍‍‌‌‍‍‍‌‌‍‌‌‌efix, cb) // => callback called with array of miniral

// implement function mergeFetcher

// const merged = mergeFetcher([fetchFruit, fetchAnimal, fetchMinirla]);

// merged('a', callback); //callback called with all result combined.

 function mergeFetch(funcs) {
   // your code here
   return function (prefix, callback) {
     let res = [];
      let i = 0;
      funcs.map((func) => {
         func(prefix, (p, arr) => {
          let prefixRes = arr.filter((el) => el.startsWith(p));
          res = [...res, ...prefixRes];
           i++;
           if (i === funcs.length) {
            callback(res);
           }
         });
       });
     };
   }

// const fetchFruit = (prefix, callback) => {
//   callback(prefix, ["apple", "banaba"]);
// };

// const fetchAnimal = (prefix, callback) => {
//   callback(prefix, ["ale", "dog"]);
// };

// const fetchMiniral = (prefix, callback) => {
//   callback(prefix, ["aaaaaa", "ccccccc"]);
// };

// const merged = mergeFetch([fetchFruit, fetchAnimal, fetchMiniral]);
// merged("a", (data) => {
//   console.log(data); // [1, 2, 3]
// });
```

retry api many times

```javascript
retry(fn, times, dely){
  try{
    return await fn();  
  } catch (e) {
    if(!times){
      throw new error(e);
    }
    return await retry(fn, times--,dely);
  }
}
```

### promise all

```javascript
function all(promises){
    return promises.reduce((acc, cur) => {
        return acc.then((ress) => Promise.resolve(cur).then(r => [...ress, r]))
    }, Promise.resolve([])
}
```

## HTML CSS

### hover card

```markup
<html>
<body>
<div>
    <div class="tooltip">Hover me</div>
    <span class="tooltipText">name: Mandy</span>
</div>
</body>
<script>
let nameNode =document.getElementsByClassName("name");
let container =document.getElementsByClassName("container");
nameNode[0].onmouseover = function(){
  mouseover();
}
nameNode[0].onmouseout = function(){
  mouseout();
}
let hoverDiv = document.createElement("div");
hoverDiv.setAttribute("class", "hoverCard");
hoverDiv.innerText = "name: mandy, age:18";
const mouseover = () => {
  container[0].append(hoverDiv);
}
const mouseout = () => {
   container[0].removeChild(hoverDiv);
}
   
</script>
</html>
```

```css
// css change method
.tooltip {
    position: relative;
}

.tooltip .tooltipText {
   position: abosulte;
   visibility: hidden;
   width: 100px;
   backgroud: red;
   text-align: center;
   border-radius: 6px;
   padding: 5px 0;
   z-index: 1;
}

.tooltip:hover .tooltipText {
   visibility: visible;

}
```

### Circle

```markup
<div class="testclass">test 
 
</div>

 <div class="c">123</div>
 
 <script>
   let circleList = [{r: 200, text: "test1"}, {r: 200, text: "test2"}, {r: 300, text: "test3"}];
let sum = [];
circleList.forEach((el, index)=> {
  if(index != 0){
    sum.push(sum[index - 1] + el.r);
  } else {
    sum.push(el.r);
  }
});
   let divContainer = document.getElementsByClassName("testclass");
   circleList.forEach((el, index) => {
     let node = document.createElement("div");
     divContainer[0].appendChild(node);
     node.setAttribute("class",  "circle");
     node.style.width = `${el.r}px`;
     node.style.height = `${el.r}px`;
     node.style["border-radius"] = 50%;
     node.style.backgroud = "red";
     node.onmouseover = function(){
       mouseOver();
     };
     node.onmouseout = function(){
       mouseout();
     };
     node.addEventListener("click", mouseDown);
     function mouseOver() {
  node.style.width = `${el.r + 100}px`;
  node.style.height = `${el.r + 100}px`;
  node.innerText = el.text;
}
   function onmouseout() {
  node.style.width = `${el.r}px`;
  node.style.height = `${el.r}px`;
   node.innerText = "";
}
  function mouseDown(){
    node.innerText = sum[index];
  }
   })
   
 </script>
```

check out

```markup
<div class="checkboxConatiner">
  <input type="checkbox" id="a" checked>A </input>
  <input type="checkbox" id="b" >B </input>
  <input type="checkbox" id="c">C</input>
 <input type="checkbox" id="all">select all</input>
</div>
```

```javascript
let state = {};

Array.from(document.querySelectorAll("[id]")).forEach(el => {
  console.log(el.id, "el");
  state[el.id] = el.checked;
  console.log(state);
})

document.getElementsByClassName("checkboxConatiner")[0].addEventListener("input", event=> {
  const target = event.target;
  const checked = target.checked;
  console.log(event, target, checked);
  if(target.id === "all"){
    Object.keys(state).forEach(id =>{
      state[id] = checked;
    })
    console.log(state, "state");
  } else {
    state[target.id]= checked;
    const childCheck = Object.keys(state).filter(id => id !== "all").map(id => state[id]);
    state.all = childCheck.includes(false) ? false: true;
    console.log(state, childCheck);
  }
  render();
})


const render = () => {
  Array.from(document.querySelectorAll("[id]")).forEach(el => el.checked = state[el.id]);
}
```

