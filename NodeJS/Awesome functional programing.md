1. curry
	- Split argument of function into many chunks
	- Example:
	```js
	const mutiple = (a) => (b) => a*b;

	const tripple = multiple(3);

	const result = tripple(3); //9
	```

2. compose

	- The output of the previous function must be the input of next function. The order of execution run from **right to left**
	- Implementation can be done as the following
	```js
	const compose = (...fns) => (...args) => 
         fns.reduceRight((acc, fn) => acc = fn(acc), args);
	```
	
	or

	```js
	const compose = (...fns) => (...args) => 
         fns.reserver()((acc, fn) => acc = fn(acc), args);
	```

3. pipe

	- The output of the previous function must be the input of next function. The order of execution run from **left to right**
	- Implementation can be done as the following:

	```js
	const compose = (...fns) => (...args) => 
       fns.reduce((acc, fn) => acc = fn(acc), args);
	```

4.  partial application
	- Mean that fixed value for specified parameters of function
	- Purpose: to reuse function in the most effective way
	- Example:

	```js
	const mutiplyThreeNumber = (a, b, c) => a * b * c

	const double = (a) => mutiplyThreeNumber(a,2,1);

	const multiplyWithThreeAndFive = (a) =>  mutiplyThreeNumber(a,3,5);
	```
	
5.  monad
    - Like wrapper, wrap the variable into container to use safe method like `Maybe`, `Just`, `Nothing`
6.  point free style
- Function without =>