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

### Pure Function Component

A component that has no internal state of its own, and thus is often written as a function as opposed to an ES6 class. 

### React.memo

is a higher order component , similar to Pure component, but it is function components instead of class component

```jsx
const MyComponent = React.memo(function MyComponent(props){
    
})
```

### How to prevent rerender\(\) ? 

render\(\) many times 

1. use pureComponent : shouldComponentUpdate called and shallow compare the state and judge whether render change 

2. used shouldComponentUpdate

### Elements vs Component 

elements: elements are the smallest building blocks of react apps. React elements are plain object, and are cheap to create

to render a React element into a root DOM node, pass both to ReactDOM.render\(\). typical elements are not used directly, but get returned form component

React components are small, reusable pieces of code that return elements be render to the pages

code written with JSX will be covered to use React.createElement\(\), you will not typcially invoke React.createElement\(\)

```jsx
const element = <h1>hello word</h1>
ReactDOM.render(element, document.getElementbyId('root'))
```

### React Ref

React.creatRef creates a ref that can attached to react elements via react ref attributes, by using Refs, you can reused refs as much as you can

```jsx
class AutoFocusTextInput extends React,Componnet {
    constructor(props){
    super(props);
    this.textInput = React.createRef();
    }
    componentDidMount(){
    this.textInput.current.focusTextInput()
    }
    render(){
        return(
            <CustomTextInput ref={this.textInput}>
        )
    }
}
```

### Reacy.forwardRef

Ref forward is a technique for automatically passing a ref though a component to one of its children

```jsx
const FancyButton = React.forwardRef((props, ref) => {
    <button ref={ref} className="FancyButton">
    {props.children}
    </button>
});
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>
```

### React.lazy

React.lazy\(\) let you define a component that is loaded dynamically. This helps reduce the bundle size to delay loading components that aren't used during initial render

```jsx
const SomeComponent = React.lazy(()=>import("./SomeComponent"))
```

### Error Handling Method - Error Boundary

Catch javaScript error anywhere and display a fallback UI instead of the  component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

A class component becomes an error boundary if it defines ether of lifecycle  methods static getDerivedStateFormError\(\) or ComponentDidCatch\(\). Use static getDerivedStateFromError\(\) to render a fallback UI after erros has been throw. Use componentDidCatch\(\) to log error information

Error Boundary does not catch errors for:

* Event handlers
* Asynchronous code
* Server side rendering
* Errors thrown in the error boundary itself

```jsx
class ErrorBoundary extends Component{
    state = {
        hasError: false,
        errorMessage: ""
    }
    static getDerivedStateFromError(error){
        return{hasError: true}
    }
    componentDidCatch =(error,info)=>{
        this.setState({
            hasError: true,
            errorMassage: error
        })
    }
    render(){
        if(this.state.hasError){
            return <h1>{this.state.errorMassage</h1>
        }
        return this.props.children
    }
}
exprot default ErrorBoundary
```

### Controlled Component vs Uncontrolled Component



### Three way to handle events 

* Bind this in the constructor

```jsx
constructor(props){
    super(props);
    this.state ={};
    this.handleClick = this.handleClick.bind(this);
}
```

* Use arrow function

```jsx
handleClick =()=> {
// output
}
```

* use arrow function in the callback 

```jsx
render(){
    return(
    <button onclick={(e) => this.handleClick(e)}>Click</button>
    )
}
```

### PropTypes

you can use PropType to catch a lot of bugs with typechecking. You can use JavaScript extension like Flow or TypeSCript to typecheck you whole application

```jsx
class Greeting extends React.Component{
    render(){
        return (
        <h1>Hell, {this.props.name}</h1>
        );
    }
    Greeting.propTypes = {
    name: PropTypes.string
    }
}
```

 

