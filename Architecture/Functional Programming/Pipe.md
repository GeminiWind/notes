# Pipe

- Like `compose` but reserve order of execution

- Implementation (in Javascript)

	```js
	const compose = (...fns) => (...args) => 
       fns.reduce((acc, fn) => acc = fn(acc), args);
	```
	
- Example:

```js
const greeting = (name) => `Welcome ${name}`;
const upperFirst = (str) => str.charAt(0).toUpperCase() + str.slice(1);

const generateWelcomeMsg = compose(upperFirst, greeting);

generateWelcomeMsg('haidv') // return Welcome Haidv

```

Tags: #fp