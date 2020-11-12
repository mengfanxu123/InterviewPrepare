# React Code Sample

### TO DO LIST USED REACT

{% embed url="https://codesandbox.io/s/to-do-list-wlpl2" %}

```javascript
import React from "react";
import ReactDOM from "react-dom";

import "./styles.css";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: "",
      list: [],
      remain: 0
    };
  }
  inputChangeHandle = e => {
    this.setState({
      input: e.target.value
    });
  };
  handleClick = () => {
    if (this.state.input) {
      let curlist = [this.state.input, true];
      this.setState({
        list: [...this.state.list, curlist],
        remain: this.state.remain + 1
      });
    }
  };
  handleToggle = index => {
    if (this.state.list[index][1]) {
      let curList = [this.state.list[index][0], false];
      const newlist = [
        ...this.state.list.slice(0, index),
        curList,
        ...this.state.list.slice(index + 1)
      ];
      this.setState({
        list: newlist,
        remain: this.state.remain - 1
      });
    } else {
      let curList = [this.state.list[index][0], true];
      const newlist = [
        ...this.state.list.slice(0, index),
        curList,
        ...this.state.list.slice(index + 1)
      ];
      this.setState({
        list: newlist,
        remain: this.state.remain + 1
      });
    }
  };
  render() {
    const { input, list } = this.state;
    console.log(input, list, this.state);
    return (
      <div>
        <input tpye="text" value={input} onChange={this.inputChangeHandle} />
        <button onClick={this.handleClick}>add</button>
        <br />
        {this.state.remain} remain out of {list.length} task
        <ul>
          {list.map((item, index) => {
            return (
              <li
                onClick={() => this.handleToggle(index)}
                style={{
                  textDecoration: list[index][1] ? "none" : "line-through"
                }}
              >
                {item}
              </li>
            );
          })}
        </ul>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);
```

{% embed url="https://codesandbox.io/s/todolist2-i3fdr" %}

## 

## sorted table + filter \(React\)

{% embed url="https://codesandbox.io/s/sorted-table-and-filter-et3uf" %}

## filter 

{% embed url="https://codesandbox.io/s/autoinput-sl2l4?from-embed" %}

## Progress Bar

{% embed url="https://codesandbox.io/s/progress-bar-hhon2?from-embed=&file=/src/index.js:857-887" %}

```jsx
import React, { useState } from "react";
import "./styles.css";

const App = () => {
  const [list, setList] = useState([]);
  const [input, setInput] = useState("");
  console.log(input, list);
  handeClick = () => {
    const item = { value: input, checked: false };
    setList([...list, item]);
  };

  handleCheck = (index) => {
    const item = {
      value: list[index].value,
      checked: !list[index].checked
    };
    setList([...list.slice(0, index), item, ...list.slice(index + 1)]);
  };

  handleRemove = (index) => {
    setList([...list.slice(0, index), ...list.slice(index + 1)]);
  };
  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={handeClick}>{"add list"}</button>
      {list.map((item, index) => {
        return (
          <div>
            <input
              type={"checkbox"}
              value={item.checked}
              onChange={() => handleCheck(index)}
            />{" "}
            <span>{item.value}</span>{" "}
            <button onClick={() => handleRemove(index)}>{"remove"}</button>
          </div>
        );
      })}
    </div>
  );
};

export default App;

```

