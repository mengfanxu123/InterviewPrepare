# React

### React advantages

* Virtual DOM improves both the experience of the user and work of the developer — Virtual DOM helps to update any user’s changes without the other parts’ interference by applying isolated components. It greatly helps to smooth the experience of all participants in real time mode.
* Saving time while re-using React components — React deals with isolated components, that’s why you can reuse them anytime you need. System upgrades will not impact or change your system.
* The stable code is provided by one-direction data flow — Direct work with each component requires one-direction data flow and makes the code really stable. Another thing is that only downward data binding is possible in this JavaScript framework.
* An open-source library with a variety of tools — All updates are released to the community. React has had the open-source library and engineers can introduce the additional tools.

### Component Lifecycle

#### Mount:

* **Constructor:** call super props and set up state only call once when the component set up
* initial local state by this.state and binding event handler methods to an instance
* **Static getDerivedStateFromProps\(\):** keep the state synced with incoming props, this method is safe to replacement of componentwillRecevieProps
* **Render\(\)** prepare and structure you JSX
* **ComponentDidMount\(\)** cause side effect\(Http request\)：`componentDidMount()` is invoked immediately after a component is mounted \(inserted into the tree\). Initialization that requires DOM nodes should go here. If you need to load data from a remote endpoint, this is a good place to instantiate the network request.Update

### Update

* **Static getDerivedStateFromProps\(props, state\)** syn state to props
* **ShouldComponentUpdate\(nextProps, state\)** decide whether continuing or not, may cancel update process: not call for initial render and get network request and 

```javascript
componentDidUpdate(prevProps) {
  // Typical usage (don't forget to compare props):
  if (this.props.userID !== prevProps.userID) {
    this.fetchData(this.props.userID);
  }
}
```

* **Render\(\)** 
* getSnapshotBeforeUpdate\(\): replace componentwillUpdate: new component update in DOM. To keep the third party library UI in acy with every update
* **componentDidUpdate\(\)**: cause side effect

### Unmount:

* **componentwillUnmount\(\)** :  remove from DOM. DOM document object model the DOM represents the document as a node or object, programing language can connect to the page

### Error Handing

* [`static getDerivedStateFromError()`](https://reactjs.org/docs/react-component.html#static-getderivedstatefromerror)
*   * [`componentDidCatch()`](https://reactjs.org/docs/react-component.html#componentdidcatch)



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

example for english to CN

{% embed url="https://codesandbox.io/s/chinese-to-english-hoc-ifvvd" %}



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

Catch javaScript error anywhere and display a falback UI instead of the  component tree that crashed. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them.

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
    <button onclick={() => this.handleClick(e)}>Click</button>
    )
}
```

### Handling events



```text
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```

in the es6, a **common pattern** is for an event handler to be a method on the class.

in js, class methods are not bound by default, it is a part of how functions work in javascript 

This is not React-specific behavior; it is a part of [how functions work in JavaScript](https://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/). Generally, if you refer to a method without `()` after it, such as `onClick={this.handleClick}`, you should bind that method.lass Toggle extends React.Component {

```jsx
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

### two way no need binding



```jsx
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

### use arrow function callback



```javascript
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={(e) => this.handleClick(e)}>
        Click me
      </button>
    );
  }
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

### React Router 

```text

```

### 

1. **how do you import multiple functions from one module? give example \(让我白板上写几个case\) //用object**

\*\*\*\*

```text
export function foo() { console.log('foo') }
export function bar() { console.log('bar') }
export function baz() { foo(); bar() }

export default {foo, bar, baz}

// a.js, using default export

import util from './util'
util.foo()

// b.js, using named exports

import {bar} from './util'
bar()
```

### Principle for front end design

### S- single responsibility principle

### O-Open Close principle

### L - Liskov substitution principle

### I- interface segregation principle

### D-dependency inversion principle 

A class should have one and only one reason to change, meaning that a class should only have one job.

```text
const circle = (radius) => {
  const proto = { 
    type: 'Circle',
    //code 
  }
  return Object.assign(Object.create(proto), {radius})
}
const square = (length) => {
  const proto = { 
    type: 'Square',
    //code 
  }
  return Object.assign(Object.create(proto), {length})
}
```

### Diff between Class Component and Functional Component

```javascript
const welcom = (props) => {
return <h1>Hello, {props.name}</h1>
}
class welcome extends React.Component{
  render(){
  return<h1>Hello, {this.props.name}
  }
}
```

1.syntax : function component is plain component and  accept props and return react element class component required extend from react component and 

### forceUpdate 

Calling `forceUpdate()` will cause `render()` to be called on the component, skipping `shouldComponentUpdate()`. This will trigger the normal lifecycle methods for child components, including the `shouldComponentUpdate()` method of each child. React will still only update the DOM if the markup changes.

Normally you should try to avoid all uses of `forceUpdate()` and only read from `this.props` and `this.state` in `render()`.

### Forms

[ ](https://reactjs.org/docs/forms.html)form

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
```

### uncontrolled component/ control component

**controlled** : form data is handled by a React component, An input form element whose value is controlled by React in this way is called a “

**controlled component**”.controlled component : data is handled by dom itself 



```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

CORS is a security mechanism built into \(all\) modern web-browsers \(yes! into your web browser! That’s why your curl calls works fine\). It basically blocks all the http requests from your front end to any API that is not in the same “Origin” \(domain, protocol, and port—which is the case most of the time\).



{% embed url="https://reactjs.org/docs/state-and-lifecycle.html" %}



