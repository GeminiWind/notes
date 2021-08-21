# Curry

- Take the argument until enough number of parameter. If number of paramter is not enough, it returns function to take missing argument
- Purpose: reused, like we have `discount` fn, then you can get `discount10Percent` and `discount30Percent`
- Example:

	```js
	const mutiple = (a) => (b) => a*b;

	const tripple = multiple(3);

	const result = tripple(3); 
	```
	
Tags: #fp
