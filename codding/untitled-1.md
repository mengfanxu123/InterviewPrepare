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

