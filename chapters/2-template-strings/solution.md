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

[Run this solution in Babel.io](https://babeljs.io/repl/#?evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-0%2Cstage-1%2Cstage-2%2Cstage-3&code=function%20dateFormat(strings%2C%20...keys)%7B%0A%20%20var%20result%20%3D%20%5Bstrings%5B0%5D%5D%0A%0A%20%20for%20(var%20i%20%3D%200%3B%20i%20%3C%20keys.length%3B%20i%2B%2B)%20%7B%0A%20%20%20%20result.push(%0A%20%20%20%20%20%20keys%5Bi%5D%20instanceof%20Date%20%3F%20keys%5Bi%5D.toLocaleDateString()%20%3A%20keys%5Bi%5D%2C%0A%20%20%20%20%20%20strings%5Bi%20%2B%201%5D%0A%20%20%20%20)%0A%20%20%7D%0A%0A%20%20return%20result.join('')%0A%7D%0A%0Aconsole.log(dateFormat%60Hello%20%24%7B%20name%20%7D%2C%20Today's%20date%20is%20%24%7B%20new%20Date()%20%7D%60))
