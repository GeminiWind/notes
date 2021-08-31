# Factory

## Definition

It defines an interface for creating a single object and let childclasses to decide which class to instantiate.

According to Wikipedia:

> In class-based programming, the factory method pattern is a creational pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of the object that will be created. This is done by creating objects by calling a factory method—either specified in an interface and implemented by child classes, or implemented in a base class and optionally overridden by derived classes—rather than by calling a constructor.

## Example

```js
class BallFactory {
  constructor() {
    this.createBall = function(type) {
      let ball;
      if (type === 'football' || type === 'soccer') ball = new Football();
      else if (type === 'basketball') ball = new Basketball();
      ball.roll = function() {
        return `The ${this._type} is rolling.`;
      };
 
      return ball;
    };
  }
}
 
class Football {
  constructor() {
    this._type = 'football';
    this.kick = function() {
      return 'You kicked the football.';
    };
  }
}
 
class Basketball {
  constructor() {
    this._type = 'basketball';
    this.bounce = function() {
      return 'You bounced the basketball.';
    };
  }
}
```

then to use it

```js
const myBasketball = factory.createBall('basketball');

const myFootball = factory.createBall('football');
const myBasketball = factory.createBall('basketball');
```

Tags: #factory, #designpattern