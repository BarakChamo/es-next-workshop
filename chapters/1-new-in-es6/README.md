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


### Destructuring assignments
**MDN Documnetation on [destructuring assignments](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)**

Destructuring assignments allow us to extract value out of containing types such as Objects and Arrays.

##### Extracting values from arrays
```javascript
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```

<br/>
##### We can also extract values out of returned values
```javascript
function f() {
  return [1, 2];
}

var a, b; 
[a, b] = f(); 
console.log(a); // 1
console.log(b); // 2
```

<br/>
##### And we can also extract values by key from objects
```javascript
var o = {p: 42, q: true};
var {p, q} = o;

console.log(p); // 42
console.log(q); // true
```

<br/>
And also re-assign into new variable names.
```javascript
var o = {p: 42, q: true};
var {p: foo, q: bar} = o;
 
console.log(foo); // 42 
console.log(bar); // true  
```


### Computed property names
**MDN Documnetation on [ES6 Object Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#Computed_property_names)**

Another ES6 feature is computed key names in object declaration.

Assigning key programatically can now be part of the object literal's declaration

For examples:
```javascript
// Computed property names (ES6)
var i = 0;
var a = {
  ["foo" + ++i]: i,
  ["foo" + ++i]: i,
  ["foo" + ++i]: i
};

console.log(a.foo1); // 1
console.log(a.foo2); // 2
console.log(a.foo3); // 3

var param = 'size';
var config = {
  [param]: 12,
  ["mobile" + param.charAt(0).toUpperCase() + param.slice(1)]: 4
};

console.log(config); // { size: 12, mobileSize: 4 }
```

Combined with destructuring assignments we can have very powerful declarations and extractions:

```javascript
let key = "z";
let { [key]: foo } = { z: "bar" };

console.log(foo); // "bar"
```
