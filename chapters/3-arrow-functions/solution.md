####Arrow Functions Exercise Solution

````javascript
/*
  Date Formatting excercise - solution
*/

Date.prototype.getTimeNow = function(){
   return this
 }

 Date.prototype.getTimeInFuture = function(callback, ...futures){
   futures.forEach(future => {
     setTimeout(() => callback(
       new Date(this.getTime() + future)
     ), future)
   })
 }

 var d = new Date()

 d.getTimeInFuture(time => console.log(time), 1000, 2000, 3000, 4000)


````
