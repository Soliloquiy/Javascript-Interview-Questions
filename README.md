# Javascript Interview Questions

### Question 1
![Question 1](https://user-images.githubusercontent.com/80487497/135481847-68d8f06d-48d0-4668-b874-9c93ee687a1e.png)

Solution:
* There are two pitfalls to be aware of.
  * The first is that null, although a primitive, is actually an object type. This can be taken care of by checking if bar is equal to null.
  ```javascript
   console.log((bar !== null) && (typeof bar === "object"));  // logs false
  ```
  * The second is if you want to include functions and arrays as part of the object type. This can be taken care of by creating OR conditionals for functions and arrays.
  
  ```javascript
   console.log((bar !== null) && ((typeof bar === "object") || (typeof bar === "function") || (Array.isArray(bar));
  ```
##

### Question 2
![Question 2](https://user-images.githubusercontent.com/80487497/135489089-19f880f9-0d29-45ff-a968-9bbb9a6b04e6.png)

Solution:
* The result will be:
  ```javascript
   a defined? false
   b defined? true
  ```
* Details to take note of:
  * Looking at the parantheses of the function, we can ascertain that it is an Immediately Invoked Function.
  * a and b are local variables, and so should not normally be defined in the global scope, so why is b true?
* The key to this problem is recognizing the shorthand for
 ```javascript
   var a = b = 3;
  ```
  
is actually
 
 ```javascript
   b = 3;
   var a = b;
  ```
  
 NOT
 
 ```javascript
   var a = 3;
   var b = 3;
  ```
* First, this means that we are using what is called 'implicit global declaration'. When a variable is assigned a value inside a function without using var, let, or const, it becomes a global variable. This is why strict mode is useful in preventing 'sloppy' mistakes like this from occuring.
* b is undefined in the local scope, hence why a is undefined, since it is a copy of the local variable b.
##

### Question 3
![Question 3](https://user-images.githubusercontent.com/80487497/135494955-ea782c2d-08f3-4e2f-847e-f43794d121a6.png)

Solution:
* The result will be
 ```javascript
   outer func:  this.foo = bar
   outer func:  self.foo = bar
   inner func:  this.foo = undefined
   inner func:  self.foo = bar
 ``` 
 * Outer function: `this` and `self` are referencing `myObject`, because the function `func` they are being called from is a property of myObject
 * Inner function: `this` is now referencing the outer function, which does not contain the variable `foo`. 
    * `self`, however, is referencing the `this` that was declared directly inside the function `func`.
##

### Question 4
![Question 4](https://user-images.githubusercontent.com/80487497/135498439-f1ab3943-f76b-402e-8cf7-30a0008bfd72.png)

* Strict mode is used to enforce more secure and error free code. Code that does not have strict enforcement is at times referred to as `sloppy mode`
* This is accomplished by:
  * Throwing errors when the delete operator is used
  * Disallowing variables to be declared without var,let, or const
  * Throwing errors for assignments to non-writable properites
##

### Question 
![Question 5](https://user-images.githubusercontent.com/80487497/135499984-9805e954-be52-4355-aa63-95a7043452df.png)

* When console logged, the result will be:
 ```javascript
   foo1 returns:
   Object {bar: "hello"}
   foo2 returns:
   undefined 
 ``` 
 * `foo1` returns the expected result, however `foo2` returns undefined.
   * This is one of the few cases where the position of the curly brace (whether on the same line, or the one below it) is of vital importance.
   * When using a return statement, if a curly brace is not placed on the same line, javascript will implicitly add a semicolon during runtime. This executes the return statement without any subsequent code, which results in undefined.
   * It is important to note that this effect does not occur when using if, while, or for statements, as the curly brace can be placed on the next line without the implicit addition of the semicolon during runtime.
##
