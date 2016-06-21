####Template String Exercise Solution

````javascript
/*
  Date Formatting excercise - solution
*/

const name = 'Barak'

function dateFormat(strings, ...keys){
  var result = [strings[0]]

  for (var i = 0; i < keys.length; i++) {
    result.push(
      keys[i] instanceof Date ? keys[i].toLocaleDateString() : keys[i],
      strings[i + 1]
    )
  }

  return result.join('')
}

console.log(dateFormat`Hello ${ name }, Today's date is ${ new Date() }`)

````
