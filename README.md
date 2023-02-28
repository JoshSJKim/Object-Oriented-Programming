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

- cardinal will have the following properties
-

```js
cardinal.name;
cardinal.color;
cardinal.numLegs;
```

## Verify an Object's Constructor with instanceof

- When a constructor function creates an object, the object is called an 'instance' of the constructor.
- Use the ```instanceof``` operator to verify whether an object was created with constructor.
- It will return true or false based on the comparison result.

```js
let Bird = function (name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // true
```

- If an object is created without using a constructor, ```instanceof``` will return false.

```js
let canary = {
    name: "Mildred",
    color: "Yellow",
    numLegs: 2
};

canary instanceof Bird; // false
```

## Understand Own Properties

- Properties such as 'name' and 'color' specified in an object are called 'own properties'.
- Own Properties are defined directly on the instance object.
- All instance objects each have its own copies of 'own properties'.
- You can extract all 'own properties' of an object and return it in an array.

```js
function Bird(name) {
    this.name = name;
    this.numLegs = 2;
}

let canary = new Bird("Tweety");
let ownProps = [];
for (let property in canary) {
    if (canary.hasOwnProperty(property)) {
        ownProps.push(property);
    }
}

console.log(ownProps);  // ['name', 'numLegs']
```

## Use Prototype Properties to Reduce Duplicate Code

- If there is a static property throughout instance objects created using the constructor function, (ex. numLegs = 2 for bird constructor)
  - it's not efficient to have numerous duplicate properties.
- You can create ```prototype``` of ```bird``` that can be shared among ALL instances of ```Bird```.

```js
Bird.prototype.numLegs = 2;
```

- Now, 'numLegs' property will be assigned to all instances of 'Bird'.
- This applies to all instances of 'Bird' only.

## Iterate over all properties

- There are two kinds of properties
  - own property - defined directly on the object instance itself
  - prototype property - defined on the prototype

```js
function Dog(name) {    // constructor function
    this.name = name;   // own property
}

Dog.prototype.numLegs = 4;  // prototype property

let beagle = new Dog("Snoopy"); // create a new instance object 'beagle'

let ownProps = [];              // initialize new variables with empty arrays
let prototypeProps = [];

for (let property in beagle) {  // iterate through the beagle object and look for properties
    if (beagle.hasOwnProperty(property)) {  // if object 'beagle' has its own property 'property',
        ownProps.push(property);            // push that property to new array 'ownProps'
    } else {
        prototypeProps.push(property);      // any properties other than 'own property' (i.e. prototype property)
    }                                       // push those properties to new array 'prototypeProps'
}

console.log(ownProps);          // ["name"]
console.log(prototypeProps);    // ["numLegs"]
```

## Understand the Constructor Property

- The ```constructor``` property is a reference to the constructor function that created the instance.
- The advantage of the ```constructor``` property is that it's possible to check for this property to find out what kind of object it is.

```js
function Dog(name) {
    this.name = name;
}

function joinDogFraternity(candidate) {
    if (candidate.constructor === Dog) {    // If object 'candidate' was created using the 'Dog' constructor function
        return true;    
    } else {
        return false;
    }
}
```

- Note that the ```constructor``` property can be overwritten
- It's generally better to use the ```instanceof``` method to check the type of an object.

## Change the Prototype to a New Object

- It can also become inefficient to add properties to ```prototype``` individually.

```js
Bird.prototype.numLegs = 2;

Bird.prototype.eat = function() {
    console.log("nom nom nom");
}

Bird.prototype.describe = function() {
    console.log("My name is " + this.name);
}
```

- There is a more efficient way to set the ```prototype``` to a new object that already contains the properties.

```js
Bird.prototype = {
    numLegs: 2,
    eat: function() {
        console.log("nom nom nom");
    },
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```

## Remember to Set the Constructor Property when Changing the Prototype

- If the prototype is manually set to a new object, it erases the constructor property.
- Remember to define the   ```constructor``` property when manually setting the prototype to a new object.

```js
function Dog(name) {
    this.name = name;
}

Bird.prototype = {
    constructor: Bird,  // define the constructor property
    numLegs: 2,
    eat: function() {
        console.log("nom nom nom");
    },
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```

## Understand Where an Object's Prototype Comes From

- An object inherits its ```prototype``` directly from its constructor function that created the object (just like genes are inherited to children)
  
```js
function Bird(name) {
    this.name = name;
}

let duck = new Bird("Donald");
```

- 'duck' inherits its ```prototype``` from the 'bird' constructor function.
- This relationship can be checked with the ```isPrototypeOf``` method

```js
Bird.prototype.isPrototypeOf(duck); // This would return 'true'
```

## Understand the Prototype Chain

- In JavaScript, every object has an internal property called [[Prototype]] that points to another object, called its prototype.
- The prototype is a blueprint that defines properties and methods that the object can access and use.
- When you access a property or method on an object, JavaScript first looks at the object itself to see if it has the property or method.
- If it does not find it, it looks at the object's prototype, and so on up the prototype chain, until it reaches the root object Object.prototype.

- The prototype chain is established when you create an object using a constructor function or using Object.create().
- The prototype of an object created using a constructor function is set to the constructor function's prototype property.
- The prototype of an object created using Object.create() is set to the object passed as an argument to Object.create().

```js
function Animal() {
}

Animal.prototype.speak = function() {
  console.log('The animal speaks.');
};

function Dog() {
}

Dog.prototype = Object.create(Animal.prototype);

Dog.prototype.bark = function() {
  console.log('The dog barks.');
};

const myDog = new Dog();
myDog.bark(); // "The dog barks."
myDog.speak(); // "The animal speaks."
```

- In this example, we create two constructor functions, Animal and Dog.
- We define a method called ```speak``` on the Animal prototype and a method called ```bark``` on the Dog prototype.
- We use Object.create() to set the Dog prototype to an instance of the Animal prototype, so that myDog inherits from Animal.prototype.
- We create a new instance of Dog called myDog and call its bark and speak methods.

- When we call myDog.bark(), JavaScript first looks for the bark method on myDog and finds it on Dog.prototype.
- When we call myDog.speak(), JavaScript first looks for the speak method on myDog and does not find it.
- It then looks for speak on Dog.prototype, does not find it, and looks on Animal.prototype, where it finds it and executes it.

Here's another prototype chain

```js
function Dog(name) {
    this.name = name;
}

let beagle = new Dog("Snoopy"); // new instance object 'beagle' is created using the constructor function 'Dog'

Dog.prototype.isPrototypeOf(beagle); // true. 'beagle' is a subtype of Dog.prototype

Object.prototype.isPrototypeOf(Dog.prototype); // true Object.prototype is the supertype of both Dog.prototype and object 'beagle'
```

## Use Inheritance So You Don't Repeat Yourself

- There's a principle in programming known as DRY (Don't Repeat Yourself).
- Repeated codes can be problematic because any change requires fixing code in multiple places.
- This means more work and more room for errors.

```js
Bird.prototype = {
    constructor: Bird,
    describe: function() {
        console.log("My name is " + this.name);
    }
};

Dog.prototype = {
    constructor: Dog,
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```

- In the example above, the ```describe``` method is repeated in two places.
- The code can be edited to eliminate redundancy by creating a supertype (parent) called 'Animal'.

```js
function Animal() { };

Animal.prototype = {
    constructor: Animal,
    describe: function() {
        console.log("My name is " + this.name);
    }
};
```

- Since 'Animal' includes the ```describe``` method, it can be removed from 'Bird' and 'Dog'.

## Inherit Behaviors from a Supertype

- Technique called 'inheritance' is used to reuse methods defined in a supertype inside its subtypes without having to define them again individually.
- The first step is to make an instance of the 'supertype'.

```js
let animal = new Animal();
```

- This is the method that's been covered so far in terms of creating an object using the 'new' operator.
- There are disadvantages of using this syntax for inheritance.

Below is an alternative approach without the disadvantages.

```js
let animal = Object.create(Animal.prototype);
```

- ```Object.create(obj)``` creates a new object and sets ```obj``` as the new object's prototype.
- By setting ```Animal.prototype``` as the 'prototype' of 'animal', it is assigning all of the attributes of ```Animal.prototype``` to all instances of 'animal' (whether already created, or to be created).

```js
function Animal() { }

Animal.prototype = {
    constructor: Animal,
    eat: function() {
        console.log("nom nom nom");
    }
};

let duck = Object.create(Animal.prototype);
let beagle = Object.create(Animal.prototype);

duck.eat()                              // nom nom nom
console.log(duck instanceof Animal);    // true
```

## Set the Child's Prototype to an Instance of the Parent

- Previously, the first step for inheriting behavior from the supertype (parent) was discussed.
- Now to set the prototype of the subtype (child).

```js
Bird.prototype = Object.create(Animal.prototype); // The subtype 'Bird' is now a 'child' of the supertype 'Animal' (parent)
```

- 'Bird' now includes all of the attributes of its parent 'Animal'.

```js
let duck = new Bird("Donald");

duck.eat(); // nom nom nom
console.log(duck instanceof Animal); // true
```

## Reset an Inherited Constructor Property

- when an object inherits its ```prototype``` from another object, it also inherits the constructor property

```js
function Bird() { }

let duck = new Bird();
console.log(duck.constructor); // [Function: Bird]
```

- The example above shows an instance of the 'Bird' constructor function, which created a 'duck' object.
- Calling duck.constructor will display that the object was created using the 'Bird' constructor function.

```js
function Bird() { }

Bird.prototype = Object.create(Animal.prototype); // This will make Bird.prototype inherit the attributes of Animal.prototype

let duck = new Bird();
console.log(duck.constructor); // [Function: Animal]
```

- After the 'Bird.prototype' inherits 'Animal.prototype', it also inherits its constructor property.
- Now, when you call 'duck.constructor', it will display that the constructor is 'Animal', when it fact it was created using the 'Bird' constructor.
- To fix this, you can manually set the constructor property of 'Bird' to the 'Bird' object.

```js
function Bird() { }

Bird.prototype = Object.create(Animal.prototype);

Bird.prototype.constructor = Bird; // This will reset the constructor of Bird.prototype to 'Bird'

let duck = new Bird();
console.log(duck.constructor); // [Function: Bird]
```

## Add Methods After Inheritance

- A constructor function that inherits prototype object from a supertype constructor function can still have its own methods in addition to the inherited methods.

```js
function Animal() { }               // create an Animal object
Animal.prototype.eat = function() { // Define a method 'eat' for Animal.prototype
    console.log("nom nom nom");
};

function Dog() { }                  // create a Dog object
Dog.prototype = Object.create(Animal.prototype); // Have Dog object inherit the attributes of Animal.prototype  
Dog.prototype.constructor = Dog;                 // Reset the constructor to Dog for Dog object.
```

- In the example shown above, Dog object inherited the constructor and 'eat' method from the Animal object.
- You can add different behaviors that are unique to the Dog object.

```js
Dog.prototype.bark = function() {
    console.log("Woof!");
};

let beagle = new Dog();
beagle.eat();   // nom nom nom - inherited from Animal.prototype
beagle.bark();  // Woof! - Added unique to Dog.prototype
```

## Override Inherited Methods

- You can override an inherited method, simply by adding the inherited method directly to the child prototype.

```js
function Bird() { }                 // create a 'Bird' object
Bird.prototype.fly = function() {   // this 'Bird' object has a method 'fly', which returns a string
    return "I am flying!";
};

function Penguin() { }              // create a 'Penguin' object
Penguin.prototype = Object.create(Bird.prototype);  // Have the 'Penguin' object inherit the method defined in 'Bird' prototype
Penguin.prototype.constructor = Penguin;            // reset the 'Penguin' constructor to 'Penguin'

Penguin.prototype.fly = function() {                // Override the method 'fly' by re-defining it in 'Penguin' prototype
    return "Alas, this is a flightless bird.";      // the return string is unique to Penguin.prototype
}

let penguin = new Penguin();  // create a new instance of a Penguin object
console.log(penguin.fly());   
// When method 'fly' is called in the new instance of Penguin object, it will display "Alas, this is a flightless bird."
// If the override method is not defined, it will return " I am flying!"                         
```

## Use a Mixin to Add Common Behavior Between Unrelated Objects

- Up to now, behavior was shared through inheritance.
- But there are cases where inheritance is not the best approach.
- It does not work well for unrelated objects, such as 'Bird' and 'Airplane'.
- They both fly, but they are not the same type.

- Use ```mixin``` to use collection of functions between unrelated objects.

```js
let flyMixin = function(obj) {
    obj.fly = function() {
        console.log("Flying, wooosh!");
    }
};
```

- Once setup, 'flyMixin' will take any object and give it the 'fly' method

```js
let bird = {
    name: "Donald",
    numLegs: 2
};

let plane = {
    model: "777",
    numPassengers: 524,
};

flyMixin(bird);     // flyMixin() is now passed to both 'bird' and 'plane'
flyMixin(plane);    // it then assigns the function 'fly' to both objects.

bird.fly();    // both 'bird' and 'plane' will display "Flying, wooosh!"
plane.fly();
```

## Use Closure to Protect Properties Within an Object from Being Modified Externally

- In the previous challenge, the 'name' property of the 'bird' object was public.
- It is considered public because it can be accessed and modified outside of bird's definition.
  
```js
let bird = {
    name: "Donald",
    numLegs: 2
};

bird.name = "Duffy"; // change name of bird to "Duffy"
```

- This means that nay part of the code can easily modify the name of bird to any other value.
- This can cause numerous problems if handling passwords and bank accounts, etc.
  
- The simplest way to convert public property to private is by creating a variable within the constructor function.
- This changes the scope of that variable to be within the construction function, instead of leaving it available on a global scope.
- Doing so will allow the variable to be accessed and modified by methods that are also defined in the constructor function.

```js
function Bird() { 
  let hatchedEgg = 10;

  this.getHatchedEggCount = function() { // Here, getHatchedEggCount is a privileged method. Meaning it has access to the private variable hatchedEgg.
    return hatchedEgg;                   // This is possible because hatchedEgg is declared in the same context as getHatchedEggCount.
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount();
```

- In JS, a function always has access to the context in which it was created. This is called ```closure```.
