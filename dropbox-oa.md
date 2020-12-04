# dropbox oa

**getNodeByClass\(root, class a\){ //className // return all nodes that have class a \(string\) }**

```javascript
let res = [];
let pathRes = [];
function myfunction(name){
  const root = document.getElementsByClassName("root");
  for (let i = 0; i < root[0].childNodes.length; i++){
    curChild = root[0].childNodes[i];
    findNode(curChild, name);
    
  }
  console.log(res);
}

function findNode(node, name){
  if(node.className == name){
    res.push(node);
  }
  if(node.childNodes.length === 0){
    return;
  }
  for (let i = 0; i <node.childNodes.length; i++){
     curChild = node.childNodes[i];
    findNode(curChild, name, path);
  }
}
```

**getNodeByClassPath\(root, classpath a\){ //classNameHierarchy // return all nodes that match classpath a \(string\), only return the lowest child // a&gt;b&gt;c， return all nodes that have class c \(string\) and match this query**

```javascript
let res = [];
let pathRes = [];
function myfunction(name){
  const path = "test2>test1";
  pathList = path.split('>');
  const root = document.getElementsByClassName("root");
  for (let i = 0; i < root[0].childNodes.length; i++){
    curChild = root[0].childNodes[i];
    findNode(curChild, "test2", pathList);
    
  }
  // console.log(res);
  console.log(pathRes);
}

function findNode(node, name, path){
  if(node.className == name){
    findPath(node, path, 0);
  }
  if(node.childNodes.length === 0){
    return;
  }
  for (let i = 0; i <node.childNodes.length; i++){
     curChild = node.childNodes[i];
    findNode(curChild, name, path);
  }
}
function findPath(node, path, index){
  if(index === path.length - 1 && node.className === path[index]){
    pathRes.push(node);
    return;
  }
  if(node.className !== path[index]){
    return;
  }
  if(node.className === path[index]){
     for (let i = 0; i <node.childNodes.length; i++){
     curChild = node.childNodes[i];
   findPath(curChild, path, index + 1);
  }
  }
}
```



