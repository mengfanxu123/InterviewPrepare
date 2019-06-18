# Coding during interview

### Ref example

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }
  render() {
    return <div ref={this.myRef} />;
  }
}
```

​Write a component and click button -&gt; div display, use two ways

```jsx
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      buttonShow: true
    };
  }

  handleButton = e => {
    this.setState({
      buttonShow: false
    });
  };

  render() {
    const { buttonShow } = this.state;
    console.log(this.state);
    return (
      <div>
        <div style={{ display: buttonShow ? "" : "none" }}>
          <h1>h1</h1>
        </div>
        <button onClick={this.handleButton}>click</button>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

### use pure JavaScript

```markup
<div id = "click">
  <h1>Hello</h1>
  <button onclick= "clickFunction()">click</button>
</div>
```

```javascript
function clickFunction(){
  document.getElementById("click").style.display="none"; 
}
```

### Find List used dictionary

give a string list and a string, according to this string, to give an list order by this string

input " String  s = "word" Stirng list = \["wait". "rain", "dead", "oh'\] output : \["wait", "oh", "rain", "dead"\]

```javascript
let str = "word";
let arr = ["oao", "rain", "dead", "ocr"];

const alienSort = (str, arr) => {
  const map = {};
  str.split("").forEach((element, index) => {
    if (!map[element]) {
      map[element] = index;
    }
  });
  console.log(map);
  arr.sort((a, b) => {
    const min = a.length < b.length ? a.length : b.length;
    for (let i = 0; i < min; i++) {
      if (a[i] !== a[i]) return map[a[i]] - map[b[i]];
      else continue;
    }
    return 0;
  });
  return arr;
};

console.log(JSON.stringify(alienSort(str, arr)));
```

