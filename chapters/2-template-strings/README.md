# Template Strings

[**MDN Documnetation on Template Strings**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals)

Template literlas, or template strings, are new JavaScript string literals that enable inline embedding of expressions.
These expressions are evaluated in the context of the literal's declaration and provide a much more elegant form of string manipulation than the concatentaion way we're used to with ES5.

#####For example

### Excercise

Implement a string templating tag function that will format JavaScript `Date` instanctes in a template literal.

Here's an example code template, fill in the function and log the templated string
```javascript
 /*
  Date Formatting excercise
 */
 
 const name = 'YOUR_NAME'
 const date = new Date()

 function dateFormat(strings, ...keys){
   // format the dates
   // and return the new string
 }
 
 console.log(/*...*/)
 
 //>> Should print Hello {NAME}, Today's date is 6/22/2016
 ```
 
 For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/2-template-strings/solution.md)
