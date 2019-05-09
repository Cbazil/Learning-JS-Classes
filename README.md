### Learning About Classes

## Tools in use
    - VSCode
    - Chrome
    - Git
    - JavaScript

## What is Classes
 Basically a program-code-template for creating objects also assigning defualt values

## What are constructor functions
A good way of making simular objects eg. Multiple users, with there info.
- They are named with Capital letters first(This is how to identify)
- They should be executed only with "new" operator.
For instance: 

``` 
    function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User('Larry');

alert(user.name); // Larry;
alert(user.isAdmin); // false 
```

Constructor functions can contain methods

``` 
function User(name) {
    this.name = name;

    this.sayHi = function() {
        alert( "My name is: " + this.name );
    };
}
let john = new User('John');

join.sayHi(); // My name is John

/* john = {
    name: 'John';
    sayHi: function() { ... }
}
*/ 
```

## Class Expression
Classes can be defined inside another expression, passed around, return, assigned etc.

If a class has a name, it's visible inside the class only;
``` 
// "Named Class Expression"
    let User = class MyClass {
        sayHi(){
            alert(MyClass); // My class is visible only inside the class
        }
    };
    new User().sayHi(); // works, shows MyClass definition

    alert(MyClass); // error, MyClass not visible outside of the class 
```
We can even make classes dynamically "on-demand", like this
``` 
function makeClass(phrase) {
    // declare a class and return it
    return class {
        sayHi(){
            alert(phrase);
        };
    };
}
// Create a new class
let User = makeClass('Hello');
new User().sayHi(); // Hello
```
## Getters and Setters, and other shorthands
classes also include getters/setters, generators, computed property etc.
here's an example for user.name implemented using get/set: 
``` 
class User {
    constructor(name) {
        // invokes the setter
        this._name = name;
    }
    get name() {
        return this._name
    }
    set name(value) {
        if (value.length < 4) {
            alert("Name is too short.");
            return;
        }
        this._name = name;
    }
}
let user = new User('Johnny');
alert(user.name); // John

user = new User(""); // Name is too short.
```

## Summary
First, as per the general object-oriented terminology, a class is something that provides "Object templates", alllows to create same-structured objects

When we say "a class", that doesn't necessary means the class keyword.
This is a class: 
``` 
function User(name) {
    this.sayHi = function(){
        alert(name);
    }
} 
```

But in most cases class keyword is used, as it provides great syntax and many additional features.

The basic class syntax looks like this: 
``` 
class MyClass {
    prop = vulue; // field

    construtor(...) { // constructor
        // ...
    }
    method(...) {} // method

    get something(...) {} getter method
    set something(...) {} setter method

    [symbol.iterator]() {} // method with computed name/symbol name
    // ...
} 
```
MyClass is technically a function, while methods are written to MyClass.prototype

## Methods Children and Parent
// We don't want to replace the parent method Keywork "super"
- super.method(...) to call a parent method.
- super(...) to call a parent constructor (inside our constructor only).
For instance, let rabit auto hide when stopped
// CHECK cPrac2

Overriding  constructor

``` 
class Animal {
    constructor(name) {
        this.speed = 0;
        this.name = name;
    }
}
class Rabbit extends Animal {
    constructor(name, earLength) {
        super(name);
        this.earLength = earlength;
    }
}

let rabbit = new Rabbit("White Rabbit", 10);
alert(rabbit.name); // White Rabbit
alert(rabbit.earLength); // 10
```

## [[Prototype]]
[[Prototype]] and prototype have entirely different purposes. [[Prototype]] is used when resolving an object's properties. If an object doesn't have a property, its [[Prototype]] is checked, and then that object's [[Prototype]], and so on, until either a property is found or you hit the end of the prototype chain.

In contrast, prototype is the mechanism by which you assign [[Prototype]] properties to objects, since you can't access them directly other than with the non-standard __proto__ property.

Since functions are objects, they have both a [[Prototype]] internal property, used to resolve properties as with normal objects, and a prototype property, which is assigned as the [[Prototype]] of new objects constructed by the function.

Here, rabbit.eat() should call animal.eat() method of the parent object:

``` 
let animal = {
    name: "Animal",
    eat(){
        alert(`${this.name} eats.`)
    }
};

let rabbit = {
    __proto__: animal,
    name: "Rabbit",
    eat() {
        // that's  how super.eat() could presumably work
        this.__proto__.eat.call(this);
    }
};

rabbit.eat(); // Rabbit eats.
```

## [[HomeObject]]
When a function is specified as a class or object method, its [[HomeObject]] property becomes that object.
``` 
let animal = {
    name: "Animal",
    eat() {
        alert(`${this.name} eats.`);
    }
};

    let rabbit = {
    __proto__: animal,
    name: "Rabbit",
    eat() {
        super.eat();
    }
};

let longEar = {
    __proto__: rabbit,
    name: "Long Ear",
    eat() {
        super.eat();
    }
};

longEar.eat(); // Long Ear eats.
```

## Static properties and methods
we can also assign a method to the class function, not to its "prototype". such methods are called static.

An Example: 
``` 
class User {
    static staticMethod() {
        alert(this === User);
    }
}
User.staticMethod(); // true
```
### Static Properties
Static properties just like regular class properties

``` 
class Article {
    static publisher = "Ilya Kantor";
}
alert( Article.publisher ); // Ilya Kantor
```

### Static and inheritance
Statics are inhetited, we can  access Parent.method as Child.method
Check static file 

### Summary
Static methods are used for the functionality that doesn’t relate to a concrete class instance, doesn’t require an instance to exist, but rather belongs to the class as a whole, like Article.compare – a generic method to compare two articles.

Static properties are used when we’d like to store class-level data, also not bound to an instance.

### Private properties
Getter/Setter functions
Here we used getter/setter syntax.

But most of the time get.../set... functions are preferred, like this:

``` 
Class CoffeeMachine {
    _waterAmount = 0;

    setWaterAmount(value) {
        if (value < 0) throw new Error("Negative water");
        this._waterAmount = value;
    }
    getWaterAmount() {
        return this._waterAmount;
    }
}
new CoffeeMachine().setWaterAmount(100);
``` 
If we inherit class MegaMachine extends CoffeeMachine, then nothing prevents us from accessing this._waterAmount or this._power from the methods of the new class.

### Private
Privates should start with #. They are only accessible from inside the class.

For instance, here we add a private #waterLimit property and extract the water-checking logic into a separate method: 

``` 
class CoffeeMachine {
    #waterLimit = 200;
    
    #checkWater(value){
        if(value < 0) throw new Error("Negative water");
        if(value > this.#waterLimit) throw new Error("Too much water");
    }
    _waterAmount = 0;

    set waterAmount(value) {
        this.#checkWater(value);
        this._waterAmount = value;
    }

    get waterAmount() {
        return this.waterAmount;
    }
}
let coffeeMachine = new CoffeeMachine();

coffeeMachine.#checkWater(); // Error
coffeeMachine.#waterLimit = 1000; // Error

coffeeMachine.waterAmount = 100; // Works
```
We can have both private and public fields at the same time: 
``` 
class CoffeeMachine {
    #waterAmount = 0;

    get waterAmount(){
        return this.#waterAmount;
    }
    set waterAmount(value) {
        if (value < 0) throw new Error("Negative water");
        this.#waterAmount = value;
    }
}

let machine.waterAmount = 100;
alert(machine.#waterAmount); // Error
```
But if we inherit from CoffeeMachine, then we’ll have no direct access to #waterAmount.
Supportable
The situation in programming is more complex than with a real-life coffee machine, because we don’t just buy it once. The code constantly undergoes development and improvement.

If we strictly delimit the internal interface, then the developer of the class can freely change its internal properties and methods, even without informing the users…

It’s much easier to develop, if you know that certain methods can be renamed, their parameters can be changed, and even removed, because no external code depends on them.

For users, when a new version comes out, it may be a total overhaul, but still simple to upgrade if the external interface is the same.

To hide internal interface we use either protected or public properties:

Protected fields start with _. That’s a well-known convention, not enforced at the language level. Programmers should only access a field starting with _ from its class and classes inheriting from it.
Private fields start with #. JavaScript makes sure we only can access those from inside the class.