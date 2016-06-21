# Classes

[**MDN Documnetation on Classes**](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)

Classes are finally introduced in JavaScript as of ES6, they provide a familiar syntax for managing object-oriented interfaces.

Classes are defined as follows:
```
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

The `class`'s constructor function is invoked on instantiation to, as the name suggests,construct the instance.


##### Class Methods

Other class methods and property getters can be defined on the class that will be available to all instances.

```javascript
class Animal {
  constructor(props) {
    this.name = props.name
    this.position = 0
  }

  static isAnimal(thing){
    return thing instanceof Animal
  }

  makeSound() {
    console.log(this.sound)
  }

  describe() {
    return `${ this.name } is a ${ this.constructor.name }`
  }

  get description() {
    return this.describe()
  }
}
```

##### Class Extensions

subclasses can also be declared that inherit from top-level classes
```javascript
class Animal { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Dog extends Animal {
  speak() {
    console.log(this.name + ' barks.');
  }
}
```


##### Class Mixins

Though not officially supported, we can create abstract classes that serve as mixins by creating dynamic classes that are extended on the fly.

For example:
```javascript
const WalkingMixin = BaseClass => class extends BaseClass {
  walk() {
    this.position ++
  }
}

class WalkingDog extends WalkingMixin(Dog) {
  // ... class extensions
}
```

In this example we apply the `WalkingMixin` to a `Dog` class at declaration time, thus creating a `WalkingDog` that can `walk()`


### Excercise

Define a class `Tourist` that extends a `Person` and conforms to the `TalkMixin` mixin.
`Tourist`s can travel to different locations while still preserving their `home` location, the initial construction location.
`Tourist` must expose a method `tour` that will set the tourist's current touring location.

Look at this code as reference for beginning the `Tourist` implementation
```javascript
class Person {
  constructor({ name, city }){
    this.name = name
    this.location = city
  }
}

const TalkMixin = BaseClass => class extends BaseClass {
  talk() {
    console.log(`
      Hello, my name is ${ this.name }.
      I'm in ${ this.location }
      I'm from ${ this.home ? this.home : this.location }
    `)
  }
}

class Tourist {
  /*...*/ 
}

let tourist = new Tourist({name: 'NAME', city: 'London'})
tourist.tour('New York')
tourist.talk()

// >> Hello, my name is NAME.
// >> I'm in New York
// >> I'm from London
```

For the complete reference solution, [click here](https://github.com/BarakChamo/es-next-workshop/edit/master/chapters/4-classes/solution.md)
