# Template Strings

[**MDN Documnetation on Arrow Functions**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Arrow functions are a shorter form of JavaScript functions. 

They are always bound to the lexical context (the `this` where they are written).

#####For example

```javascript
var a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryl­lium"
];

var a2 = a.map(function(s){ return s.length });

console.log(a2)

var a3 = a.map( s => s.length );

console.log(a3)
```


##### Lexical `this`

Arrow functions are bound to their lexical context, not their own.

For example:
```javascript
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the person object
  }, 1000);
}

var p = new Person();
```

When the constructor is called, the timed-out function will still be bound to the Person instance's context and will be able to increment the person's age.


##### Lexical arguments

Arrow functions do not support the `arguments` keyword and as such, accessing the `arguments` keyword will refer to the arguments of the enclosing `function()`

For example:

```javascript
var arguments = 42;
var arr = () => arguments;

arr(); // 42

function foo() {
  var f = (i) => arguments[0]+i; // foo's implicit arguments binding
  return f(2);
}

foo(1); // 3
```

### Excercise

Look at the additional function of the `Date` type, `getTimeNow` that returns the current time.

Now, you must implement a function called `getTimeInFuture` that accept one callback and a series of durations.

```javascript
Date.prototype.getTimeInFuture = function(callback, t1, t1, t1, ... , tn){ }
```

Implement `getTimeInFuture` as part of the `Date` prototype so that it will call the callback with the time in the future for every `t` duration provided.

Use this template to get started:
```javascript
 Date.prototype.getTimeNow = function(){
  return this
}

const d = new Date()

console.log(d.getTimeNow())

  Date.prototype.getTimeInFuture = function(){ /**/ }

var d = new Date()

d.getTimeInFuture(time => console.log(time), 1000, 2000, 3000, 4000 /* 5000, 6000 */)
```

Hints:
- 1. Try using arrow functions to bind to the `Date`'s context
- 2. Try using `rest` arguments

For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/3-arrow-functions/solution.md)
