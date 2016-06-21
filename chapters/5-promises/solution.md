#### Asynchronous Exercise Solution


#### Using `Promise`s:
````javascript
function promiseEvenOrBust(number){
   return new Promise(function(resolve, reject){
     evenOrBust(number, function(err, number){
       if (err) return reject(err)

       resolve(number)
     })
   })
 }

 promiseEvenOrBust(1).catch(e => console.log(e.toString()))
 promiseEvenOrBust(2).then(n => console.log(n))
````

#### Using `async`/`await`:

```javascript
 function evenOrBust(number, callback){
   if(number % 2) return callback(new Error('Bust!'), null)

   callback(null,  number)
 }
 
function promiseEvenOrBust(number){
   return new Promise(function(resolve, reject){
     evenOrBust(number, function(err, number){
       if (err) return reject(err)
       resolve(number)
     })
   })
 }
 
 async function asyncEvenOrBust(number){
   let n
   
   try {
     n = await promiseEvenOrBust(number)
     console.log(n)
   } 
   catch(e) {
     console.log(e.toString())
   }
 }
```
