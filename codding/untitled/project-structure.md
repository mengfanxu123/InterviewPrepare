# project structure

{% embed url="https://codesandbox.io/s/search-box-fdfo6" %}

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

```javascript
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

```

```javascript
const express = require("express");
const router = express.Router();
const User = require("./models/User");
var bodyParser = require("body-parser");
var multer = require("multer");
var fs = require("fs");
router.use(bodyParser.json());

var storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, "./public/images");
  },
  filename: (req, file, cb) => {
    console.log(file);
    var fileType = "";
    if (file.mimetype === "image/gif") {
      filetype = "gif";
    }
    if (file.mimetype === "image/png") {
      filetype = "png";
    }
    if (file.mimetype === "image/jpeg") {
      filetype = "jpg";
    }
    cb(null, "image-" + Date.now() + "." + filetype);
  }
});
var upload = multer({ storage: storage });

router.get("/allEmployees", (req, res) => {
  console.log("all");
  const orderBy = req.query.orderBy || "name";
  const order = req.query.order || "asc";
  const page = parseInt(req.query.page) || 0;
  const limit = parseInt(req.query.limit) || 5;

  const query =
    req.query.managerId === undefined ? {} : { manager: req.query.managerId };
  console.log(query);
  // const q = req.query.managerId || null;
  // // console.log(q, "q");
  // if (req.query.managerId !== null) {
  //   const query = { manager: req.query.managerId };
  // } else {
  //   const query = {};
  // }
  // const query = {};
  console.log(query, "ManagerID");

  const options = {
    page: page + 1,
    limit,
    sort: { [orderBy]: order },
    populate: {
      path: "manager",
      select: "name",
      sort: { [orderBy]: order }
    }
  };
  User.paginate(query, options).then(result => {
    console.log("sending result: ", result);
    res.json(result);
  });
});

router.get("/employeeList", (req, res) => {
  User.find({ name: { $ne: "None" } }, "id name", function(err, docs) {
    if (err) res.send(err);
    res.status(200).json(docs);
  });
});

router.get("/editEmployeeList", (req, res) => {
  User.find({ _id: { $ne: req.query.id } }, "id name", function(err, docs) {
    if (err) res.send(err);
    res.status(200).json(docs);
  });
});

router.get("/drReports", (req, res) => {
  User.find({ manager: req.body.id }, function(err, docs) {
    if (err) res.status(400).send("drReports err" + err);
    res.status(500).json(docs);
  });
});

router.post("/addUser", upload.single("avatar"), (req, res) => {
  // console.log(req.file.path);

  console.log(req.body);
  const user = new User({
    name: req.body.name,
    title: req.body.title,
    startDate: req.body.startDate,
    officePhone: req.body.officePhone,
    cellPhone: req.body.cellPhone,
    sms: req.body.sms,
    email: req.body.email,
    // manager: req.body.manager === "None" ? "" : req.body.manager,
    numberOfDr: 0,
    manager:
      req.body.manager === "" || req.body.manager === "undefined"
        ? null
        : req.body.manager,
    avatar: req.file
      ? {
          data: req.file.path,
          contentType: req.file.mimetype
        }
      : null
  });
  // });
  user.save(function(err) {
    if (err) res.status(500).send(err);
  });
  if (req.body.manager !== "") {
    var query = { _id: req.body.manager };
    User.findOneAndUpdate(query, { $inc: { numberOfDr: 1 } }, function(
      err,
      user
    ) {
      if (err) res.send(err);
      console.log(req.body.manager);
      res.send(user);
    });
  } else {
    res.send(user);
  }
});

router.delete("/delete", (req, res) => {
  let employeeId = req.query.id;
  User.findById(employeeId, "manager", function(err, employee) {
    if (err || !employee)
      return res.status(400).send("delete user fail: " + err);
    // Find employee's manager.
    console.log(employee.manager, "test");
    // Find employee's DRs.
    // Set DRs' manager to the employee's manager, if any.
    User.updateMany(
      { manager: employeeId },
      { $set: { manager: employee.manager } },
      function(err, docs) {
        if (err) return res.status(500).send("delete user fail: " + err);

        // If has manager, decrement employee's manager's DR count.
        if (employee.manager) {
          User.findOneAndUpdate(
            { _id: employee.manager },
            { $inc: { numberOfDr: docs.nModified - 1 } },
            function(err, user) {
              if (err) return res.status(500).send("delete user fail: " + err);
            }
          );
        }
        // Finally delete this employee and return.
        User.findByIdAndDelete(employeeId, function(err) {
          if (err) {
            return res.status(500).send("delete user fail: " + err);
          }
          return res.status(200).send("delete user success");
        });
      }
    );
  });
});

router.put("/updateEmployee", upload.single("avatar"), (req, res) => {
  let id = req.query.id;
  let oldManager = req.body.oldManger;
  let newManager = req.body.newManager;
  console.log("oldManager", oldManager);
  console.log("newManager", newManager);
  // if Manager changed 1. None - new Manager 2. oldManger to newManger 3. oldMange to None
  // find oldManager and decrease 1 to the old ManagerReport
  // Manager change ?
  if (oldManager !== newManager) {
    if (oldManager) {
      User.findOneAndUpdate(
        { id: oldManager },
        { $inc: { numberOfDr: -1 } },
        function(err, user) {
          if (err) res.status(500).send(err);
          // res.send(user);
        }
      );
    }
    if (newManager) {
      User.findOneAndUpdate(
        { id: req.body.manager },
        { $inc: { numberOfDr: 1 } },
        function(err, user) {
          if (err) res.status(500).send(err);
          // res.send(user);
        }
      );
    }
  }
  console.log("id", req.body.id);
  User.findOneAndUpdate(
    { _id: id },
    {
      name: req.body.name,
      title: req.body.title,
      startDate: req.body.startDate,
      officePhone: req.body.officePhone,
      cellPhone: req.body.cellPhone,
      sms: req.body.sms,
      email: req.body.email,
      manager:
        req.body.newManager === "" || req.body.newManager === "undefined"
          ? null
          : req.body.newManager,
      numberOfDr: req.body.numberOfDr,
      avatar: req.file
        ? {
            data: req.file.path,
            contentType: req.file.mimetype
          }
        : null
    },
    function(err, user) {
      if (err) res.status(500).send(err);
      else res.status(200).send(user);
    }
  );
});

module.exports = router;
```

