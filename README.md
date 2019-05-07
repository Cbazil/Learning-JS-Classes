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
alert(user.isAdmin); // false ```

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

