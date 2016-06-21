#### Generators Exercise 2 Solution

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

const login = async(function* (id) {
   const user = yield getUser(id)
   if (!user) throw new Error('User not found')
   return user
})

 const userOne = login(1)

 userOne
   .then(user => console.log(user))
   .catch(error => console.log(error.toString()))


 const userTwo = login(2)

 userTwo
   .then(user => console.log(user))
   .catch(error => console.log(error.toString()))

```
