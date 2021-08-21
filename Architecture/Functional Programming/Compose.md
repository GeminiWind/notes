# Compose
- take multiple function as argument. Then run each function from bottom to top, outout of the previous function will be input for next function
- Implementation in Javascript
	```js
	const compose = (...fns) => (...args) => 
         fns.reduceRight((acc, fn) => acc = fn(acc), args);
	```
	
- Example 

	```js
	const greeting = (name) => `Welcome ${name}`;
	const upperFirst = (str) => str.charAt(0).toUpperCase() + str.slice(1);

	const generateWelcomeMsg = compose(greeting, upperFirst);

	generateWelcomeMsg('haidv') // return Welcome Haidv

	```

- When to use: React

Tags: #fp