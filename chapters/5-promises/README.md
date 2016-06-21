# Promises

[**MDN Documnetation on Promises**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise)

Promises provide a better interface for asynchronous operations in JavaScript, avoiding the so-called *Callback Hell*.

Promises are executors that take a function and provide it with 2 function arguments, `resolve` and `reject` and returns a `promise` interface.

The executor function can do whatever acynchronous processing we need, calling `resolve` when it's done or `reject` if it encountered an error.

The returned `promise` interface has 2 methods, `.then()` and `.catch()` that are called when the executor function calls `resolve` or `reject` respectively.

Let's start by looking at the *old* way of doing async in JavaScript, with callbacks:
```javascript
  // set a timeout and resolve, async, after a second
  function asyncCallback(value, success, error){
    setTimeout(function(){
      return success(value)
    },1000)
  }

  // Again, set a timeout and resolve, async, after a second
  function asyncProcessing(value, success, error){
    setTimeout(function(){
      return success(value.data)
    },1000)
  }

  // Call asyncCallback, passing 2 callback
  asyncCallback({data: 'Hello'},
    function success(data){
      // Call asyncProcessing, passing another 2 callback
      asyncProcessing(data,
        
        // We are now 3 callback levels deep!
        function success(v){
          // Beginning of 'Callback Hell!'
          console.log(v)
        },
        function error(){

        })
    },
    function error(e){
      console.log(e)
    }
  )
```

Now let's look at implementing the same code using promises:

```javascript
 function asyncPromise(id){
   return new Promise((resolve, reject) => {
     console.log('fetching...')
     setTimeout(() => {
       if (!id) return reject('NO ID PROVIDED')
       resolve({value: 'Hello world!'})
     }, 1000)
   })
 }

 function processPromise(data){
   return new Promise((resolve, reject) => {
     console.log('processing...')
     setTimeout(() => resolve(data.value), 1000)
   })
 }

 asyncPromise()
   .then(data  => processPromise(data))
   .catch(err  => console.log(err))

```

#####Chaining promises

Promise handlers: `.then` and `.catch` can be chained by returning a another value or promise in their callback.

For Example with the previous function:
```javascript
 asyncPromise()
    // we return a promise from processPromise
   .then(data  => processPromise(data))
   // this call will be called when processPromise is resovled
   .then(value => console.log(value))
   // Any caught error will trigger the .catch()
   .catch(err  => console.log(err))
```


#####`async`/`await`
ES7 suggests a newer, more *"synchronous"* looking interface for performing asynchronous operations with `async` functions.

Functions marked as `async` are executed until they are told to `await` a promise, execution of the function will then be halted until the promise is resolved and the promised value returned.

While `async` functions still `await` on `Promise`s, these promises can be abstracted and we can write synchronous looking, single flow code that is easier to understand.

Let's explore this concept using an example similar to the ones above:
```javascript
  function asyncPromise(id){
    return new Promise((resolve, reject) => {
      console.log('fetching...')
      setTimeout(() => {
        if (!id) return reject('NO ID PROVIDED')
        resolve({value: 'Hello world!'})
      }, 1000)
    })
  }

  async function processPromise(dataPromise){
    let data = await dataPromise

    return data.value
  }

  (async function() {
    const p = asyncPromise(123)
    const value = await processPromise(p)
    console.log(value)
  }())
```

`asyncPromise` returns a promise that is resolved after a timeout. We then define an `async function` processPromise that accepts a promise as it's only argument.
`processPromise` then `await`s the promised value, similar to calling `.then()` on the promise, and assigns the resolved value to the `data` variable.

The final self executing async function initializes a promise `p`, passes it to `processPromise` and `await`s it further, finally logging the value to the console.

### Excercise

Look at the following snippet:
```javascript
 function evenOrBust(number, callback){
   if(number % 2) return callback(new Error('Bust!'), null)

   callback(null,  number)
 }

 evenOrBust(1, function(err, number){
   console.log(err.toString(), number)
 })

 evenOrBust(2, function(err, number){
   console.log(err, number)
 })
```

The function `evenOrBust` accepts a number and a callback. It returns the value if it is `even` or an error if the number is `odd`. This callback style where the error is passed or null as the first argument is called a `node style called`.

Now implement an asynchronous version of `evenOrBust`, `promiseEvenOrBust`. `promiseEvenOrBust` should accept a single argument, a number, and return a promise that is resolved with the number if it is `even` or rejected if it is `odd`.

Then, call `promiseEvenOrBust` with `even` and `odd` valued and handle the returned promise properly (Hint: using `then` and `catch`).

Complete this reference implementation
```javascript
 function evenOrBust(number, callback){
   if(number % 2) return callback(new Error('Bust!'), null)

   callback(null,  number)
 }
 
function promiseEventOrBust(value){
  //  return a promise
 }

 promiseEvenOrBust(1)
 promiseEvenOrBust(2)
```

###### Extra credit!
Try implementing the same functionality using `async`/`await` code.


 For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/5-promises/solution.md)
