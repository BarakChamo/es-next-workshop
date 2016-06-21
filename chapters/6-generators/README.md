# Generators

[**MDN Documnetation on Generators**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/function*)



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

Attempt to mimic ES7 `async`/`await` functionality using ES6 generators.

For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/6-generators/solution2.md)
