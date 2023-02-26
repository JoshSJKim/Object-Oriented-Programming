# Object-Oriented-Programming

Basic principles of OOP

## Use of 'this' Keyword

- You can use dot notation to access properties in an object.

```js
let duck = {
    name: "Aflac",
    numLegs: 2
};

console.log(duck.name); // "Aflac"
```

- Objects can have a special type of property called 'method'
- Methods are properties with a function assigned.
- Calling this method using the dot notation will return the function result

```js
let duck = {
    name: "Aflac",
    numLegs: 2,
    sayLegs: function () {return "This duck has " + duck.numLegs + " legs.";}
};

console.log(duck.sayLegs()); // "This duck has 2 legs."
```

- While using the dot notation is valid, it poses a risk of errors down the line.
- For example, if the variable name changes from 'duck' to 'dog', you'll have to search through the entire code to change all 'duck' to 'dog'.
- It may be a simple task for an example like shown above, but if the code becomes complex, it may not be so simple.

- For such circumstances, use the 'this' keyword instead.

```js
let duck = {
    name: "Aflac",
    numLegs: 2,
    sayLegs: function () {return "This duck has " + this.numLegs + " legs.";}
};
```

- Because the above code uses the 'this' keyword, you won't have to worry about changing everything if the variable name changes.
- 'this' refers to the object that the method is associated with, which in this case is 'duck'.
- This is only a single example of how 'this' can be used.

## Define a Constructor Function

- Constructors are functions that create new objects.
- It defines properties and behaviors that will belong to the newly created object.

For example

```js
function bird() {
    this.name = "Albert";
    this.color = "blue";
    this.numLegs = 2; 
}
```

- the above constructor defines a Bird object with properties name, color, and number of legs, which are set to Albert, blue, and 2

- Some general rules when defining a constructor
  - Constructors are defined with a capitalized name to differentiate from other functions.
  - Constructors use 'this' keyword to set properties of the object.
    - 'this' refers to the object it will create
  - Constructors define properties and behaviors instead of returning a value as other functions might

## Use a Constructor to Create Objects

```js
function bird() {
    this.name = "Albert";
    this.color = "blue";
    this.numLegs = 2; 
}

let blueBird = new Bird();
```

- Note: 'this' inside the constructor function always refers to the object being created.
  - In the case above, 'this' is referring to 'blueBird'.

- When calling a constructor function, you need to use the ```new``` operator.
- This tells JS to create a new instance of 'Bird' called 'blueBird'.
- Omitting the ```new``` operator will lead to unexpected results.

- The new object 'blueBird' now has all the properties defined inside the Bird constructor.

```js
blueBird.name;
blueBird.color;
blueBird.numLegs;
```

- And just like any other object, its properties can be accessed and modified.

```js
blueBird.color = "blue";
```

## Extend Constructors to Receive Arguments

- Using a constructor to create objects is useful.
- But it becomes inefficient if you have to create an object and define each property value manually.
- You can pass parameters to the constructor function at the time of creating the object to increase efficiency and manageability.

```js
function Bird(name, color) {    // This is the constructor with two parameters
    this.name = name;           // first parameter will define the value of name  
    this.color = color;         // second parameter will define the value of color
    this.numLegs = 2;           // numLegs are the same for all birds
}
```

- Now, create a new bird object

```js
let cardinal = new Bird("Cardi", "red");
```

It will create the following

```js
var cardinal = {
    name: "Bruce",
    color: "red",
    numLegs: 2
};
```