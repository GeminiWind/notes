# Singleton

## Definition

It ensure that there's only for object created for a particular class.

According to Wikipedia

> In software engineering, the singleton pattern is a software design pattern that restricts the instantiation of a class to one "single" instance. This is useful when exactly one object is needed to coordinate actions across the system.

## Example

We will be using example of car  

Creating a Singleton class 

```js
class DatabaseConnection {
  private connection

  getConnection() {
    if (!connection) {
	  connection = doConnect();
	}
	
	return connection
  }
}

```

Thst's how we will use this,  

```js
const connection = DatabaseConnection.getConnection();
```

Tags: #singleton, #designpattern