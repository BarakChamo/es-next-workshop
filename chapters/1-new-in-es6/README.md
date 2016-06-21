# New in ES6

### `const` and `let`
**MDN Documnetation on [`let`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/let) and [`const`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/const)**

`let` and `const` replace `var` from older versions of JavaScript.

`let` assignments can be re-assigned and `const` is used for read-only, single-assignment values.

There are a few subtle differences between `let` and `var`.

##### 1. `let` is not hoisted

##### 1. `let` cannot be re-declared in the same scope

##### 2. `let` has block scope
```javascript
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // same variable!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // different variable
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```


### *speard*, *rest* and *default*
**MDN Documnetation on [rest](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/rest_parameters), [spread](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) and [default arguments](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Default_parameters)**

##### speard arguments

Speard arguments can span over multiple "single" arguments. 

For example
```javascript
// Instead of using arguments
function myFunction(x, y, z) { }
let args = [0, 1, 2];
myFunction.apply(null, args);

// We can group all of the function's arguments
function myFunction(x, y, z) { }
let args = [0, 1, 2];
myFunction(...args);

// And we can also spread arrays items
let parts = ['shoulders', 'knees'];
let lyrics = ['head', ...parts, 'and', 'toes']; // ["head", "shoulders", "knees", "and", "toes"]
```

##### rest arguments

Rest is the opposite of spread, allowing us to represent multiple arguments as a single one.
```javascript
// Before rest parameters, the following could be found:
function f(a, b){
  let args = Array.prototype.slice.call(arguments, f.length);
  console.log(args)
  // …
}

// to be equivalent of
function f(a, b, ...args) {
  console.log(args)
}
```


##### default arguments

We can also specify function's default argument values as part of the function's declaration.

```javascript
function hello(name='world'){
  console.log('Hello ' + name + '!')
}

hello()
```
