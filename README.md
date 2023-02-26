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