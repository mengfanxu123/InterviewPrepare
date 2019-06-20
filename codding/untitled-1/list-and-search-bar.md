# List and Search bar

use map and filter 

{% embed url="https://codesandbox.io/s/mutable-pond-1ncj6" %}

```javascript
import React from "react";
import ReactDOM from "react-dom";
import "./styles.css";

const data = [
  {
    name: "Mandy",
    age: 19
  },
  {
    name: "Ryan",
    age: 20
  },
  {
    name: "Bob",
    age: 21
  }
];

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: "",
      data: data
    };
  }

  handleSearch = e => {
    this.setState({
      input: e.target.value
    });
  };

  render() {
    const { data, input } = this.state;
    const filteredPeople = data.filter(person =>
      Object.values(person).some(value =>
        value
          .toString()
          .toLowerCase()
          .includes(input.toLowerCase())
      )
    );
    return (
      <div>
        <input type="text" onChange={e => this.handleSearch(e)} value={input} />
        <table>
          <thead>
            <tr>
              <th>Name</th>
              <th>Age</th>
            </tr>
          </thead>
          <tbody>
            {filteredPeople.map((ele, index) => {
              return (
                <tr key={index}>
                  <td>{ele.name}</td>
                  <td>{ele.age}</td>
                </tr>
              );
            })}
          </tbody>
        </table>
      </div>
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<App />, rootElement);

```

