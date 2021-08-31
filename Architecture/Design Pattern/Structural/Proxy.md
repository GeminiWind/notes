# Decorator

## Definition

By using Proxy, a class can represent functionality of another class.

According to Wikipedia

> The proxy pattern is a software design pattern. A proxy, in its most general form, is a class functioning as an interface to something else.


## Exampple 
Let's take an example of value proxy  

```js
class Percentage {
  constructor(percent) {
    this.percent = percent;
  }

  toString() {
    return `${this.percent}&`;
  }

  valueOf() {
    return this.percent / 100;
  }
}

```

That's how we can use that,  

```js
let fivePercent = new Percentage(5);
console.log(fivePercent.toString());
console.log(`5% of 50 is ${50 * fivePercent}`);
```

Tags: #proxy, #designpattern