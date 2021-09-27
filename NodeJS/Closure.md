# Closure

Take a look at this example:

```js
var x = 1;  
function foo(y) {  
  return function(z) {  
    return x + y + z;	  
  }  
}  
  
var f = foo(2);
```

If you run this command on the web console, you’ll see this:

console.dir(f);

![[closure.png]]