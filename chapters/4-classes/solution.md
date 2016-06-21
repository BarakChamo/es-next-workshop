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

class Tourist extends TalkMixin(Person) {
  constructor({ name , city }){
      super({name, city})
      this.home = city
  }

  tour(city){
    this.location = city
  }
}

let tourist = new Tourist({name: 'Barak', city: 'London'})
tourist.tour('New York')
tourist.talk()
