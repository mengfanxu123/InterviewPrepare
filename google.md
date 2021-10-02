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

