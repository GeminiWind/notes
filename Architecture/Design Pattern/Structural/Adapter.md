# Adapter

## Definition

This pattern allows classes with incompatible interfaces to work together by wrapping its own interface around existing class

According to Wikipedia

> In software engineering, the adapter pattern is a software design pattern that allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

## Exampple 
We are using an example of calculator. OutdatedCalculator is an old interface and ModernCalculator is new interfcae. We will bw building an adapter that will wraps up new interface and will give us results using it's new methods,  

```js
class OutdatedCalculator {
  constructor() {
    this.operations = function(value1, value2, operation) {
      switch (operation) {
        case 'add':
          return value1 + value2;
        case 'sub':
          return value1 - value2;

      }
    };
  }
}


class ModernCalculator {
  constructor() {
    this.add = function(value1, value2) {
      return value1 + value2;
    };
    this.sub = function(value1, value2) {
      return value1 - value2;
    };
  }
}

```

Creating Adapter class,  

```js
class ModernCalculatorAdapter {
  constructor() {
    const cal = new OutdatedCalculator();

    this.add = function (value1, value2) {
	  return cal.operations(value1, value2, 'add')
	}
	  
	this.sub = function (value1, value2) {
	  return cal.operations(value1, value2, 'sub')
	}
}
```

Thst's how we will use this,  

```js

const adaptedCalc = new ModernCalculatorAdapter();
console.log(adaptedCalc.add(10, 55));
```

Tags: #adapter, #designpattern