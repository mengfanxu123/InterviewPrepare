# React

### Component Lifecycle

#### Mount:

* Constructor: call super props and set up state only call once when the component set up
* Static getDerivedStateFromProps\(\): keep the state synced with incoming props, this method is safe to replacement of componentwillRecevieProps
* Render\(\) prepare and structure you JSX
* ComponentDidMount\(\) cause side effect\(Http request\)

### Update

* Static getDerivedStateFromProps\(props, state\) syn state to props
* ShouldComponentUpdate\(nextProps, state\) decide whether continuing or not, may cancel update process
* Render\(\) 
* getSnapshotBeforeUpdate\(\): replace componentwillUpdate: new component update in DOM. To keep the third party library UI in acy with every update

### Unmount:

* componentwillUnmount\(\) :  remove from DOM. DOM document object model the DOM represents the document as a node or object, programing language can connect to the page

### HOC

high order component is the function that pass old component and return a new component. It is used for reused code

### Why use HOC

HOC is best way to show behavior between React component

```jsx
const withSecretTolift = (WrappComponent) => {
    class HOC extends React.Component{
        render(){
            return (
                <WrappComponent {this.props} secretTolife = {42} />
                
            );
        }
    }
    return HOC;
}
```

![lifecycle](../.gitbook/assets/1_u8htumgapqmyzivfgqmfpa.jpeg)

### state vs props

State: State is used for store and manage data within a component,  use setState to update date from Virtual DOM.  State is not  visible with other component 

Props: Props is used pass value from parents components to children component

only changes in props and or state trigger react to re-render the components and potentially update the DOM in the browser 

### React VS Angular

| React | Angular |
| :--- | :--- |
| library | framework |
| JSX\(pure javascript\) | typescript\(if you use java, very similar with JAVA, has same principals and pattern\) |
| Very fast\(great performance, better than Angular\) | Easy to learn  |
| Great for complex application with manage state used redux or react context API |  |
| one direction data-flow | bi-direction data flow |
| one way data binding | two ways data binding |
| component based  |  |

### axios

Axios is a promise based HTTP client from browser and node.js and also one of most common used library to send HTTP request in React

```jsx
// get method
axios
    .get("/user")
    .then(response=> {
        console.log(response)
    })
    .catch(err => {
        console.log(err)
    })
axios
    .post("/user", {name : "name", password: "password"})
    .then(response=>{
        console.log(response)
    })
    .catch(err=>{
    console.log(err)
    })
```

#### example : axios used in component \(componentDidUpdate\)

```jsx
import React from "react";
import ReactDOM from "react-dom";
import axios from "axios";

import "./styles.css";

class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: []
    };
  }
  componentDidMount() {
    // right place to do axios request in lifecycle
    axios
      .get("https://api.github.com/users")
      .then(response => {
        this.setState({
          data: response.data
        });
      })
      .catch(err => {
        console.log(err);
      });
  }
  render() {
    const { data } = this.state;
    const imageStyle = { width: 100, height: 100 };
    return (
      <div>
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>userName</th>
              <th>image</th>
            </tr>
          </thead>
          <tbody>
            {data.map((ele, item) => {
              return (
                <tr>
                  <td>{ele.id}</td>
                  <td>{ele.login}</td>
                  <td>
                    <img
                      style={imageStyle}
                      src={ele.avatar_url}
                      alt={ele.avatar_url}
                    />
                  </td>
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

### Pure Component

same as Component except it handle the shouldComponentUpdate method for you. When props or state changes, pureComponent will do shallow comparison on both props and state

Component wont compare current props and state to next out of box,. the component will re-render by default whenever shoudComponentUpdate is called 

### How to prevent rerender\(\) ? 

render\(\) many times 

1. use pureComponent : shouldComponentUpdate called and shallow compare the state and judge whether render change 

2. used shouldComponentUpdate

