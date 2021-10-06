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

Solution:
* Strict mode is used to enforce more secure and error free code. Code that does not have strict enforcement is at times referred to as `sloppy mode`
* This is accomplished by:
  * Throwing errors when the delete operator is used
  * Disallowing variables to be declared without var,let, or const
  * Throwing errors for assignments to non-writable properites
##

### Question 5
![Question 5](https://user-images.githubusercontent.com/80487497/135499984-9805e954-be52-4355-aa63-95a7043452df.png)

Solution:
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

### Question 6
![Question 6](https://user-images.githubusercontent.com/80487497/135873695-1fa5d390-abb3-40b5-a6ea-24e4938789aa.png)

Solution:
* When console logged, the result will be:
 ```javascript
   0.30000000000000004
   false
 ``` 
* In JavaScript, numbers are all stored as floating point numbers. This means that when dealing with decimals, there is a possibility of the resulting places after the decimal point to total up to 17 points.
* This makes floating point arithmatic not 100% accurate.
* The problem can be solved however, by using a method such as `toFixed()` which allows you control of the precision of floating point numbers

##


### Question 7
![Question 7](https://user-images.githubusercontent.com/80487497/135875931-f6a7e06f-410b-49da-99bd-c5d1b397ad11.png)

Solution:
* When console logged, the result will be:
 ```javascript
   1
   4
   3
   2
 ``` 
* The key to this problem is understanding the asychronicity and corresponding event queues that exists within Javascript.
* When the `setTimeout` codes are ran, Javascript appends the events to an event queue. This event queue keeps track of all the events that have been ran. They are then handled by putting them in the order that they were seen while simultaneously delaying their execution until the previous event has been executed.
* This means that any code that is not asynchronous, such as console logging numbers `1` and `4`, are executed first. `3` and `2` will be placed on the event queue as they utilize an asychronous function `setTimeout()`. `3` will then be executed next as the given time in `setTimeout` is 0 ms, and `2` will be executed last as it has a time of 1000 ms

##

### Question 8
![Question 8](https://user-images.githubusercontent.com/80487497/135879003-44710f61-0212-4764-83e6-2cbd833ad9fc.png)


Solution:
* The function will be:
 ```javascript
    function isPalindrome(str) {
    str = str.replace(/\W/g, '').toLowerCase();
    return (str == str.split('').reverse().join(''));
}
 ``` 
* The most important part of this problem is recognizing the code `replace(/\W/g, '')`.
   * The metacharacter `\W` (notice it is upper, not lower case) searches a string for non-word characters (a word character is a character from a-z, A-Z, 0-9, underscore)
   * The `g` tells the function to replace the character globally, meaning if it appears more than once (multiple spaces or commas).
   * The `''` tells the function to replace the non-word characters with nothing, thus effectively deleting it. 
* The rest of the problem is simply converting the characters to a standard form for comparison `toLowerCase()`, and then comparing its reverse by splitting the string into an array, reversing it, then joining it.

##

### Question 9
![Question 9](https://user-images.githubusercontent.com/80487497/135888577-7c8e053b-3cea-4af0-99e5-ead06ec7d193.png)

Solution:
* The function will be:
 ```javascript
    function sum(x) {
     if (arguments.length == 2) {
      return arguments[0] + arguments[1];
    } else {
      return function(y) { return x + y; };
    }
   }
 ``` 
* The arguments object exists within a function and takes the form of an array. This allows us to check the length of the arguments (number of arguments pased), and access the arguments individually.
  * In the case where two arguments are passed, both can be referenced by `arguments[]` and summed. 
* If an anonymous function is declared within a function, the function will pass the element next to the function `sum(2)(3)`, which is `3` in this case, to the anonymous function which can then be used.
* Returning `function(y) {x + y}` means to pass the original argument `2` to `x`, then pass `3` to `y`, and finally sum them.
* Another method, instead of using the arguments object, is to pass both `x` and `y` as arguments to the function.
* The reasoning behind it is: 
  * When a function is invoked, JavaScript does not require the number of arguments to match the number of arguments in the function definition. If the number of arguments passed exceeds the number of arguments in the function definition, the excess arguments will simply be ignored. On the other hand, if the number of arguments passed is less than the number of arguments in the function definition, the missing arguments will have a value of undefined when referenced within the function. So, in the above example, by simply checking if the 2nd argument is undefined, we can determine which way the function was invoked and proceed accordingly. 

##

### Question 10
![Question 10](https://user-images.githubusercontent.com/80487497/135916643-c9aa67d3-f799-4299-a2e9-1178b7c11537.png)


Solution:
* The number `5` will always be logged to the console
* The reason behind this has to do with the scope that is established (through closure) when functions are declared, in addition to the use of `var` as a method of variable declaration.
* "In JavaScript, functions close over the scope they are declared in and retain access to that scope even as variable values inside of that scope change."
  * Each button in this example contains an anonymous function that logs an index value to the console.
  * In this case, the scope of the anonymous function is global, and contains every `i` that was looped through. This means that when the function is called by the `onClick` event handler, the last `i` that was declared will be what is logged to the console.
* This is the reason the `let` variable declaration was created. Instead of having access to the entire global scope, `let` creates a new scope each time the for loop is ran, ultimately creating a separated scope for each function to close over.
* It is important to know that `let` has block closure, which is the mechanism that allows it to create a new scope each time the for loop is ran.
* The code to overcome the problem is to change the `var` declaration to a `let` declaration in the for loop:
 ```javascript
    for (let i = 0; i < 5; i++) {
    var btn = document.createElement('button');
    btn.appendChild(document.createTextNode('Button ' + i));
    btn.addEventListener('click', function(){ console.log(i); });
    document.body.appendChild(btn);
}
 ``` 

##


### Question 11
![Question 11](https://user-images.githubusercontent.com/80487497/135919831-ef1e3b26-c0e9-4c10-a768-f2c83a9ce585.png)

Solution:
* It will add the two elements of the array into the object d as properties, with the values of undefined 

##

### Question 12
![Question 12](https://user-images.githubusercontent.com/80487497/135920977-d4e674f5-41f2-4879-83c1-56fff3bfabd8.png)


Solution:
* When console logged, the result will be:
 ```javascript
"array 1: length=5 last=j,o,n,e,s"
"array 2: length=5 last=j,o,n,e,s"

 ``` 
* The key to this problem is understanding which methods directly mutate the arrays they are called on, copying by reference vs value, and how the `push()` method actually works
  * `reverse()` mutates the array it is called on
  * `split()` does not mutate array that it is called on
  * Because `arr1` is an array, which is a non primitive, it is copied by reference, not by value. This means that when `arr2` is equated to `arr1.reverse()` the reference to the address of `arr1` is copied, thus any changes made to `arr2` will be reflected on `arr1` as well.
  * `push()` adds an entire array as a single element onto the array that is is called on. This is not to be confused with concatenation where the elements are still split when combined.
   * `arr1` and `arr2` will contain `['n','h','o','j', ['j','o','n','e','s'] ]`, NOT `['n','h','o','j','j','o','n','e','s' ]`
  * `slice()` will return the element at the index that is referenced and onwards until the end of an array. Since `-1` references the last element in the array, `j,o,n,e,s` is returned

##

### Question 13
![Question 13](https://user-images.githubusercontent.com/80487497/135926655-da3bc9ff-0343-45e4-ac38-8a0fbe5a2b37.png)



Solution:
* When console logged, the result will be:
 ```javascript
    "122"
    "32"
    "02"
    "112"
    "NaN2"
    NaN
 ``` 
* The first one uses type coercion when summing `1` + `"2"`. `1` will be converted to a string type and concatenated with `"2"` which results in `"12"`. `"12"` is then concatenated with `"2"` to produce `"112"`.
* This problem uses a unary operator (`+`) to convert the second value (`"2"`) into a number type. `1` will be added to `2` to result in `3`, and then converted back to a string type for concatenation with the final `"2"`.
* This problem uses a unary operator (`-`) to convert the second value (`1`) into a number type. `1` will be subtracted from `1` to result in `0`, and then converted back to a string type for concatenation with the final `"2"`.
* This problem uses a unary operator (`+`) to convert the first value (`"1"`) into a number type, **however**, it is immediately converted back into a string type for concatenation with the second value `"1"`, resulting in `"112"`, and then concatenated with the final `"2"`.
* When a subtraction operand (`-`) is used with a string type, it will result in `NaN`. This means that `"A" - "B"` will result in `NaN`, and then through type coercion is converted to a string and concatenated with the final `"2"`.
* Similar to the previous problem, `"A" - "B"` wil result in `NaN`, **however**, any number that has an operation with `NaN` will result in `NaN`. Because `2` is a number, the result will be `NaN`. 

##


### Question 14
![Question 14](https://user-images.githubusercontent.com/80487497/135927533-5da92f24-478a-43f9-aa87-460001e77f4f.png)


Solution:
* The function can be modified as follows:
 ```javascript
    let list = readHugeList();

    let nextListItem = function() {
        let item = list.pop();

        if (item) {
            // process the list item...
            setTimeout( nextListItem, 0);
        }
};

 ``` 
* Stack overflow is caused when the **call stack** allocates more memory than it is able to the call stack. 
* It is important to know that the call stack uses a Last In First Out (LIFO) method. This means that in the case of recursive functions, the call stack will keep "stacking" calls until the final function is called and/or it runs out of memory
* To resolve this issue, `setTimeout` is used to utilize the **event queue** and the **event loop**.
  * The event loop monitors both the event queue and the call stack. Once the call stack is clear (meaning the function is finished processing the list item and has executed in this case), the event queue will push the next recursive function call onto the call stack, and so on. 

##

### Question 15
![Question 15](https://user-images.githubusercontent.com/80487497/136264157-32a60e91-37ad-4ed0-a9ca-2203e5aeed8e.png)



Solution:
* An example of closures is:
 ```javascript
const globalVar = "xyz";

(function outerFunc(outerArg) {
    const outerVar = 'a';
    
    (function innerFunc(innerArg) {
    const innerVar = 'b';
    
    console.log(
        "outerArg = " + outerArg + "\n" +
        "innerArg = " + innerArg + "\n" +
        "outerVar = " + outerVar + "\n" +
        "innerVar = " + innerVar + "\n" +
        "globalVar = " + globalVar);
    
    })(456);
})(123);
 ``` 
 * Console log output:
 ```javascript
outerArg = 123
innerArg = 456
outerVar = a
innerVar = b
globalVar = xyz
 ``` 
* A closure is the ability of a function to maintain access to variables in its own scope, in the scope of the function it is enclosed by, and the global scope
* In the example above, `123` is used as the argument for the IIFE `outerFunc`, `456` is used as the argument for the IIFE `innerFunc`.
* As can be seen, the `innerFunc` has access to all the arguments and variables defined in itself, the `outerFunc`, and the global scope.

##

### Question 16


Solution:
* :
 ```javascript

 ``` 

* 

##
