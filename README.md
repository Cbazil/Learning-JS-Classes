### Learning About Classes

## Tools in use
    - VSCode
    - Chrome
    - Git
    - JavaScript

## What is Classes
 Basically a program-code-template for creating objects also assigning defualt values

## What are constructor functions
A good way of making simlar objects eg. Multiple users, with there info.
- They are named with Capital letters first(This is how to identify)
- They should be executed only with "new" operator.
For instance: 

``` function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User('Larry');

alert(user.name); // Larry;
alert(user.isAdmin); // false 
```

Constructor functions can contain methods

``` function User(name) {
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
*/ ```

## Class Expression
Classes can be defined inside another expression, passed around, return, assigned etc.

If a class has a name, it's visible inside the class only;
``` // "Named Class Expression"
    let User = class MyClass {
        sayHi(){
            alert(MyClass); // My class is visible only inside the class
        }
    };
    new User().sayHi(); // works, shows MyClass definition

    alert(MyClass); // error, MyClass not visible outside of the class 
```
We can even make classes dynamically "on-demand", like this
``` function makeClass(phrase) {
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
``` class User {
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
``` function User(name) {
    this.sayHi = function(){
        alert(name);
    }
} ```

But in most cases class keyword is used, as it provides great syntax and many additional features.

The basic class syntax looks like this: 
``` class MyClass {
    prop = vulue; // field

    construtor(...) { // constructor
        // ...
    }
    method(...) {} // method

    get something(...) {} getter method
    set something(...) {} setter method

    [symbol.iterator]() {} // method with computed name/symbol name
    // ...
} ```
MyClass is technically a function, while methods are written to MyClass.prototype