# Prototype

## Definition

It creates new objects from the existing objects.

According to Wikipedia

> The prototype pattern is a creational design pattern in software development. It is used when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects.

## Example

We will be using example of car  

```js

class Car {

  constructor(name, model) {
    this.name = name;
    this.model = model;
  }

  SetName(name) {
   console.log(`${name}`)
  }

  clone() {
    return new Car(this.name, this.model);
  }
}

```

Thst's how we will use this,  

```js
let car = new Car();
car.SetName('Audi);

let car2 = car.clone()
car2.SetName('BMW')
```

Tags: #prototype, #designpattern