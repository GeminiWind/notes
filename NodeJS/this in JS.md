---
date updated: '2021-09-27T20:50:43+07:00'

---

# *this* in JS

- No specified block: *this* point to **window**/**global** depend on the running env. If the js execution is browser, *this* points to **window**. If it run on BE side, *this* point to **global**'
- In object

```js
const person = {
	name: 'haidv',
	age: 25,
	greeting: function() {
		return `Hello ${this.name}`
	}
}

console.log(person.greeting()) // will be output to Hello haidv7

  

let c = person.greeting

console.log(c()); // will be output to `Hello undefined`. Now this point to global/window
```

- In class
```js
class Animal {
	constructor(name) {
		this.name = name
	}

	greeting () {
		return `Hello ${this.name}`
	}
}

const dog = new Animal('dog');

console.log(dog.greeting()) // will be output to Hello dog

let d = dog.greeting;

console.log(d()); // throw error Can not read property 'name' of undefined
```
