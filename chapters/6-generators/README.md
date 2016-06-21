# Generators

[**MDN Documnetation on Generators**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/function*)

Generators are special JavaScript functions that maintain internal state and make it easy to custom iterators.

They only compute value, or iterate, on demand and are a good way of implementing highly-efficient and lazily evaluted iterables.

Generators are created from generator functions (`function*()`). These are functions that `yield` a value instead of `return`ing it, halting execution instead of terminating it and waiting for the next iteration.

To iterate a generator, we call `next()` on it, and execution is resumed until the function `yield`s or `return`s.

A generator provides a wrapper interface for the iterator, whenever a value is `yield`ed it is contained in a `IteratorResult`. An object with a `value` and a `done`, marking the iterator as completed or not.

Let's look at a basic example:
```javascript
function* idMaker(){
  var index = 0;
  while(index < 3)
    yield index++;
}

var gen = idMaker();

console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().done); // true
```

### Excercise 1

Implement an infinite generator function that yields a fibonacci series.

Complete the following reference implementation:

```javascript
 function* fibonacci () {
   yield
 }

 let f = fibonacci()

 console.log(f.next().value) // 1
 console.log(f.next().value) // 1
 console.log(f.next().value) // 2
 console.log(f.next().value) // 3
 console.log(f.next().value) // 5
 console.log(f.next().value) // 8
```

 For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/6-generators/solution1.md)

<br/>
### Excercise 2

Let's attempt to mimic ES7 `async`/`await` functionality using ES6 generators.

```javascript
function async(generate){
  return function () {
    var generator = generate.apply(this, arguments);

    function handle(result){
      if (result.done) return Promise.resolve(result.value);

      return Promise.resolve(result.value).then(function (res){
        return handle(generator.next(res));
      }, function (err){
        return handle(generator.throw(err));
      });
    }

    try {
      return handle(generator.next());
    } catch (error) {
      return Promise.reject(error);
    }
  }
 }

 const users = {
   1: {first_name: 'John', last_name: 'Doe'}
 }

 const getUser = id => new Promise(
   (res, rej) => {
     if (Math.random() <= 0.66) return rej(new Error(404))

     return setTimeout(
       () => res(users[id]),
       0
     )
   }
 )

const login = async(/* figure it out! */)

const userOne = login(1)

userOne
  .then(user => console.log(user))
  .catch(error => console.log(error.toString()))


const userTwo = login(2)

userTwo
  .then(user => console.log(user))
  .catch(error => console.log(error.toString()))
```

For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/6-generators/solution2.md)
