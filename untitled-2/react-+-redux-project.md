# React + Redux project

## component

```jsx
import React, { Component } from "react";
import "./styles.css";
import { connect } from "react-redux";
import * as actions from "./Actions-creater";
import Reusebutton from "../src/reusebutton.js";
class App extends Component {
  componentDidMount() {
    this.props.list();
  }
  handleRemoveMovieFromMyList = id => {
    this.props.removeMovieFromMyList(id);
  };
  handleAddMovietoMyList = id => {
    this.props.addMovieToMyList(id);
  };
  render() {
    const { myLists, recommendation } = this.props;
    // console.log(myList, recommendations);
    return (
      <div className="App">
        <img
          className="logo"
          src="https://store-images.s-microsoft.com/image/apps.51445.9007199266246365.c6dce6b1-5edd-4e64-a117-0e45b8165403.c7938026-2c39-48b0-b8f8-067273b77187"
        />

        <h2>My List</h2>
        <div className="myList">
          {myLists.map((element, index) => {
            // console.log(element);
            return (
              <div className="movie">
                <div className="postShow">
                  <div className="overlay" />
                  {/*this is reusedable component both from my list and recommedation */}
                  <Reusebutton
                    element={element}
                    handle={this.handleRemoveMovieFromMyList}
                    index={index}
                    text="remove"
                  />
                </div>
              </div>
            );
          })}
        </div>
        <h2>Recommendations</h2>
        <div className="recommendations">
          {recommendation.map((element, index) => {
            return (
              <div className="movie">
                <div className="postShow">
                  <div className="overlay" />
                  {/*this is reusedable component both from my list and recommedation, when you click it, will happend */}
                  <Reusebutton
                    element={element}
                    handle={this.handleAddMovietoMyList}
                    index={index}
                    text="add"
                  />
                </div>
              </div>
            );
          })}
        </div>
      </div>
    );
  }
}

const mapStateToProps = state => {
  return {
    myLists: state.myList,
    recommendation: state.recommendations
  };
};

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


import React from "react";
import "./styles.css";
const listElement = props => {
  return (
    <div>
      <h3>{props.element.title}</h3>
      <img src={props.element.img} alt={props.element.id} />
    </div>
  );
};

export default listElement;


```

## Reducer

```jsx
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

## action

```jsx
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
export const removeMovieFromMyList = payload => {
  return {
    type : "ROMVE",
    payload
  }
}
export function addMovieToMyList(id) {
  return {
    type: "ADD_TO_MYLIST",
    id: id
  };
}

```

