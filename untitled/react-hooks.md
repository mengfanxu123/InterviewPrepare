# React Hooks

### What is Hooks

Hooks let you split one component into smaller functional  component based on what pieces are related, rather than base on split on lifecycle

```jsx
import React, { useState } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

const App = props => {
  const [personState, setPersonState] = useState({
    person: [{ name: "Mandy", age: 16 }]
  });
  const switchNameHandler = () => {
    setPersonState({
      person: [{ name: "Harry Lu", age: 17 }]
    });
  };
  return (
    <div>
      <button onClick={switchNameHandler}>Switch time</button>
      <div>name : {personState.person[0].name}</div>
      <div>age: {personState.person[0].age}</div>
    </div>
  );
};

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

### Counter Example

```jsx
import React,{useState} from "react";
import ReactDOM from "react-dom";

import "./styles.css";

const App = (props) => {
  const [counter, setCounter] = useState(0);
  return (
    <React.Fragment>
      <span>You CLicked {counter} times !</span>
      <button onClick={() =>setCounter(counter + 1)}>Increase</button>
      <button onClick={()=>setCounter(counter - 1)}>Decrease</button>
    </React.Fragment>
  )
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

### React Counter use Hooks

```jsx
function App() {
  const [num, setNum] = useState(Number(localStorage.getItem("num")) || 0);

  useEffect(() => {
    localStorage.setItem("num", num);
  }, [num]);

  return (
    <div>
      {num}
      <button onClick={() => setNum(num + 1)}>Add</button>
      <button onClick={() => setNum(num - 1)}>Subtract</button>
    </div>
  );
}
```

