# Factory

## Definition

It creates families or groups of common objects without specifying their concrete classes.

According to Wikipedia:

> The abstract factory pattern provides a way to encapsulate a group of individual factories that have a common theme without specifying their concrete classes.

## Example

We will be using the example of Drink and Drink making machine.  

```js
class Drink
{
  consume() {}
}

class Tea extends Drink
{
  consume() {
    console.log('This is Tea');
  }
}

class Coffee extends Drink
{
  consume()
  {
    console.log(`This is Coffee`);
  }
}
```

Making Drink Factory  

```js
class DrinkFactory
{
  prepare(amount)
}

class TeaFactory extends DrinkFactory
{
  makeTea() 
  {
   console.log(`Tea Created`);
   return new Tea();
  }
}

class CoffeeFactory extends DrinkFactory
{
   makeCoffee() 
  {
   console.log(`Coffee Created`);
   return new Coffee();
  }
}

```

We will use our factory now  

```js
let teaDrinkFactory = new TeaFactory();
let tea = teaDrinkFactory.makeTea()
tea.consume() 
```

Tags: #abstractfactory, #designpattern