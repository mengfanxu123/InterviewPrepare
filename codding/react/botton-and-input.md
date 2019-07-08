# Botton and Input

{% embed url="https://codesandbox.io/s/botton-and-input-o4rtb" %}

```jsx
// click botton to get output in input text 
import React, { Component } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      input: "",
      bottonJson: [
        { botton1: "botton1input" },
        { botton2: "botton2input" },
        { botton3: "botton3input" }
      ]
    };
  }
  handleChangeInput = e => {
    console.log(e);
    this.setState({
      input: e
    });
  };

  render() {
    const { bottonJson } = this.state;
    console.log(this.state);
    return (
      <div>
        <input type="text" value={this.state.input} />
        <div>
          {bottonJson.map((ele, index) => {
            return (
              <div>
                <botton
                  onClick={() =>
                    this.handleChangeInput(Object.entries(ele)[0][1])
                  }
                >
                  {Object.entries(ele)[0][0]}
                </botton>
              </div>
            );
          })}
        </div>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

