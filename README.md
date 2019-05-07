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
