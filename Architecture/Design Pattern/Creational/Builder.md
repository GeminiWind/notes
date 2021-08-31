# Builder

## Definition

It construct complex objects from simple objects.

According to Wikipedia

> The builder pattern is a design pattern designed to provide a flexible solution to various object creation problems in object-oriented programming.

## Example

We will be using ab example of a person class which stores a Person's information

```js
class Person {
  constructor() {
    this.streetAddress = "";
	this.postCode = "";
	this.city = ""
    this.companyName = "";
	this.position = "";
    this.annualIncome = 0;
  }
  toString() {
    return (
      `Person lives at ${this.streetAddress}, ${this.city}, ${this.postcode}\n` +
      `and works at ${this.companyName} as a ${this.position} earning ${this.annualIncome}`
    );
  }
	
  withPostCode(postcode) {
    this.postCode = postCode;
	  
	return this;
  }
	
  build() {
	return this;
  }
}
```

then to use it

```js
const person = new Person().withPostCode('10000').build()
```

Tags: #builder, #designpattern