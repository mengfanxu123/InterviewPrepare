# project detail and Design

### 1.front end

component connect with reduce 

```javascript
const mapStateToProps = state => {
  return {
    myList: state.myList,
    recommendation: state.recommendations
  };
};
//action connect part
const mapDispatchToProps = dispatch => {
  return {
    removeMovieFromMyList: id => {
      dispatch(actions.removeMovieFromMyList(id));
    },
    addMovieToMyList: id => {
      dispatch(actions.addMovieToMyList(id));
    },
    list: () => {
      dispatch(actions.getList());
    }
  };
};

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(App);
```

{% embed url="https://action.js" %}

```javascript
export function requestStart() {
  return {
    type: "DATA_FETCH_START"
  };
}
export function requestSuccess(response) {
  return {
    type: "DATA_FETCH_SUCCESS",
    data: response.data
  };
}
export function requestFail(error) {
  return {
    type: "DATA_FETCH_FAIL",
    error
  };
}

export function getList() {
  return (dispatch, store) => {
    dispatch(requestStart());
    axios
      .get("https://5d11c0f984e9060014576512.mockapi.io/NetflixData")
      .then(response => {
        console.log(response.data);
        dispatch(requestSuccess(response));
      })
      .catch(err => {
        dispatch(requestFail(err));
      });
  };
}

export function removeMovieFromMyList(id) {
  return {
    type: "REMOVE_MOVIE_FROM_MYLIST",
    id: id
  };
}

export function addMovieToMyList(id) {
  return {
    type: "ADD_TO_MYLIST",
    id: id
  };
}

```

### Action.js\(dispatch action to reducer and also handle http request\)

```javascript
import axios from "axios";

export function requestStart() {
  return {
    type: "DATA_FETCH_START"
  };
}
export function requestSuccess(response) {
  return {
    type: "DATA_FETCH_SUCCESS",
    data: response.data
  };
}
export function requestFail(error) {
  return {
    type: "DATA_FETCH_FAIL",
    error
  };
}

export function getList() {
  return (dispatch, store) => {
    dispatch(requestStart());
    axios
      .get("https://5d11c0f984e9060014576512.mockapi.io/NetflixData")
      .then(response => {
        console.log(response.data);
        dispatch(requestSuccess(response));
      })
      .catch(err => {
        dispatch(requestFail(err));
      });
  };
}

export function removeMovieFromMyList(id) {
  return {
    type: "REMOVE_MOVIE_FROM_MYLIST",
    id: id
  };
}

export function addMovieToMyList(id) {
  return {
    type: "ADD_TO_MYLIST",
    id: id
  };
}
```

### Reducer.js is used for get statee and do some action and return new state

```javascript
const initState = {
  isFetching: false,
  myList: [],
  recommendations: [],
  err: null
};
const myList = (state = initState, action) => {
  switch (action.type) {
    case "DATA_FETCH_START":
      return {
        ...state,
        isFetching: true
      };
    case "DATA_FETCH_FAIL":
      return {
        ...state,
        error: action.error,
        isFetching: false
      };
    case "DATA_FETCH_SUCCESS":
      return {
        ...state,
        isFetching: false,
        err: null,
        myList: action.data[0].mylist,
        recommendations: action.data[0].recommendations
      };
    case "REMOVE_MOVIE_FROM_MYLIST":
      return {
        myList: [
          ...state.myList.slice(0, action.id),
          ...state.myList.slice(action.id + 1)
        ],
        recommendations: [...state.recommendations, state.myList[action.id]]
      };
    case "ADD_TO_MYLIST":
      return {
        myList: [...state.myList, state.recommendations[action.id]],
        recommendations: [
          ...state.recommendations.slice(0, action.id),
          ...state.recommendations.slice(action.id + 1)
        ]
      };
    default:
      return state;
  }
};

export default myList;




```

### How to use Router in React

```javascript
class App extends Component {
  render() {
    return (
      <div>
        <Router history={history}>
          <div>
            <Button variant="contained">
              <Link component={RouterLink} to="/addEmployee">
                Add Employee
              </Link>
            </Button>
            <Button variant="contained">
              <Link component={RouterLink} to="/">
                Home
              </Link>
            </Button>
            <Button variant="contained" />
            <Switch>
              <Route exact={true} path="/" component={Home} />
              <Route path="/addEmployee" component={addEmployee} />
            </Switch>
          </div>
        </Router>
      </div>
    );
  }
}
```

```javascript
export function editManagerList(id) {
  return (dispatch, getState) => {
    dispatch(getManagerListStart());
    axios
      .get("/users/editEmployeeList", {
        params: {
          id
        }
      })
      .then(reponse => {
        console.log(reponse.data);
        dispatch(getManagerListSuccess(reponse.data));
      })
      .catch(err => {
        dispatch(getManagerListFail(err));
      });
  };
}
```

