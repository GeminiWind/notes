# Composite

## Definition

omposes objects so that they can be manipulated as single object.

According to Wikipedia

> The composite pattern describes a group of objects that are treated the same way as a single instance of the same type of object.

## Exampple 
We will be creating Renderer classes for rendering multiple shapes,  

```js
class Employer{
  constructor(name, role){
    this.name=name;
    this.role=role;

  }
  print(){
    console.log("name:" +this.name + " relaxTime: " );
  }
}
```

Creating GroupEmployer,  

```js
class EmployerGroup{
  constructor(employers=[]){
    console.log(name)
    this.employers=employers;
  }
  size(){
    return this.employers.length
  }
}
```

Thst's how we will use this,  

```js
let zee= new Employer("zee","developer")
let shan= new Employer("shan","developer")

let groupDevelopers = new EmployerGroup([zee,shan]);
console.log(groupDevelopers.size())
```

Tags: #composite, #designpattern