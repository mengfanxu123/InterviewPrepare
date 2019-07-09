# Test:

## Test used enzyme and jest



#### About Testing in `create-react-app` <a id="about-testing-in-create-react-app"></a>

To run test in `create-react-app` just run `npm test`. `create-react-app` will run test on files which end with `.test.js` in any place inside `src` directory.

```jsx
function sum(a, b) {
  return a + b;
}

function multiply(a, b) {
  return a * b;
}

describe('test for sum function', () => {
  it('should return 3 when pass 1 and 2', () => {
    expect(sum(1, 2)).toEqual(3);
  });
  it('should return 10 when pass 5 and 5', () => {
    expect(sum(5, 5)).toEqual(10);
  });
});

describe('test for multiply function', () => {
  it('should return 4 when pass 1 and 4', () => {
    expect(multiply(1, 4)).toEqual(4);
  });
  it('should return 10 when pass 2 and 5', () => {
    expect(multiply(2, 5)).toEqual(10);
  });
});
```

* A test suite is a block of unit tests that are all closely related; they test the same function or similar parts of our code base.
* We introduce a test suite in Jest using `describe()`
* Each individual unit test is called a “spec”.
* Jest makes it natural to write specs by containing them in a function called `it()`

