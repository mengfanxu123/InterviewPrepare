# React Router

React is a popular library for creating single-page applications \(SPAs\) that are rendered on the client side

### Basic Router

```javascript
import {BrowserRouter, Route} from 'react-router-dom';

/* Home component */
const Home = () => (
  <div>
    <h2>Home</h2>
  </div>
);

/* About component */
const About = () => (
  <div>
    <h2>About</h2>
  </div>
);

/* Users component */
const Users = () => (
  <div>
    <h2>Users</h2>
  </div>
);

class App extends React.Component {
  render() {
    return (
      <BrowserRouter>
        <div>
          <Route path="/" component={Home} />
          <Route path="/about" component={About} />
          <Route path="/users" component={Users} />
        </div>
      </BrowserRouter>
    );
  }
}
```

### Link

naviget between the pages 

