####Template String Exercise Solution

```javascript
  function* fibonacci () {
    var current = 0, next = 1, swap
    while (true) {
      swap = current
      current = next
      next = swap + next
      yield current;
    }
  }

  let f = fibonacci()

  console.log(f.next().value)
  console.log(f.next().value)
  console.log(f.next().value)
  console.log(f.next().value)
  console.log(f.next().value)
  console.log(f.next().value)
```
