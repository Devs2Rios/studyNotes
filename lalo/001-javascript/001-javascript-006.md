# How JavaScript Works Behind the Scenes

## A High-Level Overview of JavaScript

- High-Level: You don't manage hardware resources
- Garbage-collected: Clears the memory time to time
- Interpreted or just-in-time compiled: We write human readable code and is interpreted by the computer as machine code
- Multi-paradigm:
  - Procedural programming - Organize code with some functions in betweem
  - Object-oriented programming (OOP) -
  - Functional programming
- Prototype-based object-oriented
  - Almost everything is an object (has methods inside)
    ```JavaScript
    // Array object
    // --------------------------------
    const myArr = new Array(1);
    // [ <1 empty item> ]
    myArr.push('Index 1');
    // [ <1 empty item>, 'Index 1' ]
    myArr[0] = 'Index 0';
    // [ 'Index 0', 'Index 1' ]
    myArr.length
    // 2
    // --------------------------------
    ```
  - First-class functions
    - Functions treated as variables, we can pass them into other functions and return them from functions
      - `document.querySelector('.some-class').addEventListener('click', firstClassFunction);`
  - Dynamically-typed language
    - No data type definitions (identified at runtime)
    - Data type is automatically changed
      ```JavaScript
      let myVar = 3;
      myVar = 'Changed to string';
      ```
  - Non-blocking event loop
    - _Concurrency model_ is how JavaScript handles multiple tasks happening at the same time
    - Runs in a single thread, so it can only do one thing at a time
    - By using an _event loop_ JavaScript takes long running tasks, executes them in background and puts them back in the main thread when they're finished

## The JavaScript Engine and Runtime

- Computer Science side note:
  - Compilation: The code is converted into machine code so the computer can execute it
    - `Source Code` -Compilation-> `Portable file: Machine code` -Execution-> `Program running`
  - Interpretation: An interpreter runs through the source code and executes it line by line
    - `Source Code` -Execution line by line-> `Program running`
  - Just-in-time (JIT) compilation: the code is converted into machine code at once, then it's executed immediately
    - `Source Code` -Compilation-> `Machine code` -Execution-> `Program running`
- An engine is a program that executes JavaScript code
  - Some of the most popular are:
    - Node JS, Google's V8, Firefox, Safari
  - How does an engine work?
    - Call Stack: Where the code is executed
    - Heap: Where the objects are stored
  - Engine step by step
    - Parsing: Checks for errors in the code and generates the Abstract Syntax Tree (AST)
    - Compilation: Takes the AST and converts it into machine code (Just-in-time compilation)
    - Execution: Executes the machine code in the Call Stack
    - Optimization: Modern JavaScript executes code faster by bringing a not optimized machine code to execution and then re-compilate it until it's optimized
- Runtime
  - The heart of the runtime is an engine.
  - In the browser the engine has extra-functionalities provided by the WEB APIs and the callback queue (events, data, etc.)
    - The callback queue puts callback functions ready to use in the call stack

## Execution Contexts and The Call Stack:

> **Execution context (EC):** Environment in which a piece of JavaScript is executed, stores the necessary information for a code to be executed
>
> - Structure:
>   - Variable environment
>     - let, const and var decalrations, functions, arguments object (not arrow functions)
>   - Scope chain
>   - `this` keyword (not arrow functions)

- Execution:
  - Global execution context for top level code (it's always one) -> Code outside our functions
  - Execution of the top-level code inside the global EC
  - Execution of functions and waiting for callbacks (one per function call)

> **The Call Stack:** Is where all the execution contexts are stacked for execution and it gives the instructions to execute

### Scope and The Scope Chain

- Scoping: How oure variables are organized and accessed
- Lexical Scoping: Scoping is controlled by placement of functions and blocks in the code
- Scope: Space or environment in which certain variable is declared
  - Global scope: Top level code accesible everywhere
  - Function scope: Variables accesible inside the function (local scope)
  - Block scope (ES6 only): `let` and `const` variables are accesible only inside a block, functions are block scope just in strict mode
- Scope of a variable: Region of our code where a certain variable can be accessed
  ```JavaScript
  const myGlobalVar = 'Global scope';
  let mutable = 'I will change';
  function first() {
    const myFunctionScope = 'Local scope';
    mutable = 'I changed';
    // Local scopes can access global scopes
    return `${myGlobalVar} ${myFunctionScope}`;
  }
  first(); // 'Global scope Local scope' and changes mutable
  console.log(mutable); // 'I changed'
  // Block scopes only live within a block
  if (myGlobalVar) {
    // You can use global scopes in functions
    const blockScope = myGlobalVar.replace('Global', 'Block');
    var varVariable = myGlobalVar.replace('Global', 'Var');
    console.log(blockScope); // 'Block scope'
  }
  // Printing the scopes, local and block scopes cannot be accessed in the global scope
  console.log(myGlobalVar); // 'Global scope'
  console.log(varVariable); // 'Var scope' var is not block scope because is not ES6
  console.log(myFunctionScope); // Uncaught ReferenceError: myFunctionScope is not defined
  console.log(blockScope); // Uncaught ReferenceError: blockScope is not defined
  ```

## Variable Environment: Hoisting and The TDZ

- Hoisting: Makes some types of variables accesible/usable in the code before they are actually declared

  - Before execute the code, variable declarations are scanned and a new property is declared in the variable environment object for each variable.
    ||Hoisted|Initial Value|Scope
    |---|---|---|---|
    |**`function()` declarations** |✅ Yes|Actual function|Block|
    |**`var` variables** |✅ Yes|`undefined`|Function|
    |**`let` and `const` variables** |🚫 No|`<uninitialized>`, Temporal Dead Zone (TDZ)|Block|
    |**`function` expressions and arrows `= () => {}`** |Depends if using `var` or `let/const`|Depends if using `var` or `let/const`|Depends if using `var` or `let/const`|

- Why hoisting?
  - Using functions before the actual declaration
  - `var` hoisting is just a byproduct
- Why TDZ?

  - Easier to avoid cache errors: accessing variables before declare is a bad practice
  - Makes const variables actually work

- In Practice:

  ```JavaScript
  // Hoisting and Temporal Dead Zone (TDZ)
  'use strict';

  // Variables

  console.log(varVar);
  // Returns undefined also if var is used in functions so you cannot call them
  // var keyword adds a variable into the DOM window object, so be careful
  console.log(letVar);
  // ReferenceError: Cannot access 'letVar' before initialization
  console.log(constVar);
  // ReferenceError: Cannot access 'constVar' before initialization
  var varVar = 'var variable';
  let letVar = 'let variable';
  const constVar = 'const variable';

  // Functions

  console.log(funcDec());
  // Function declaration
  console.log(funcExp());
  // ReferenceError: Cannot access 'funcExp' before initialization
  console.log(funcArr());
  // ReferenceError: Cannot access 'funcArr' before initialization

  function funcDec() {
    return 'Function declaration';
  }
  const funcExp = function() {
    return 'Function expression';
  };
  const funcArr = () => 'Arrow function';
  ```

  - The conclusion is never to use `var` because it an lead to hoisting problems
  - Declare functions before calling them

  ## The `this` Keyword

  - Special variable created for every execution context
    - Points to the owner of the object
    - It's not static and depends on how the function is called (its value is asigned when it's called)
      - Method `this` -> Object that is calling the method
        ```JavaScript
        const owner = {name: 'Mr. Owner', whoIsTheOwner: function() {return this.name + ' is the owner'}}
        // The owner is the object referenced in the variable const owner
        owner.whoIsTheOwner(); // Mr. Owner is the owner
        ```
      - Simple function call `this` -> undefined
      - Arrow functions `this` -> Don't have it because it doesn't uses the lexical this keyword, it points to window
      - Event listener `this` -> DOM element attached to the event
      - `new` `call` `apply` `bind`

  ```JavaScript
  console.log(this);
  // Strict mode: {}
  // No strict mode: {} -> Window in browser

  const thisFunction = function(thisNumber) {
    console.log(thisNumber);
    console.log(this);
  };
  thisFunction(1);
  // Strict mode: 1, undefined
  // No strict mode: 1, <ref *1> Object [global] -> Undefined in browser

  const thisArrowFunction = function(thisNumber) {
    console.log(thisNumber);
    console.log(this);
  };
  thisArrowFunction(2);
  // Strict mode: 2, undefined
  // No strict mode: 2, <ref *1> Object [global] -> Window in browser

  const thisObject = {
    number: 3,
    objectFunction: function() {
      console.log(this.number);
      console.log(this);
    },
  };
  thisObject.objectFunction();
  // Strict mode: 3, { number: 3, objectFunction: [Function: objectFunction] }
  // No strict mode: 3, { number: 3, objectFunction: [Function: objectFunction] }

  const thisOtherObject = { number: 4 };
  thisOtherObject.objectFunction = thisObject.objectFunction;
  thisOtherObject.objectFunction();
  // Strict mode: 4, { number: 4, objectFunction: [Function: objectFunction] }
  // No strict mode: 4, { number: 4, objectFunction: [Function: objectFunction] }

  const objectFunctionOutside = thisObject.objectFunction;
  console.log(objectFunctionOutside());
  // Strict mode: undefined, TypeError: Cannot read property 'number' of undefined
  // No strict mode: undefined, <ref *1> Object [global] -> Window in browser - undefined
  ```

  ## Regular Functions vs. Arrow Functions

  - Arrow functions inside objects will return undefined for this

    ```JavaScript
    const thisObject = {
      number: 1,
      objectFunction: function() {
        console.log(this.number);
        console.log(this);
      },
      objectArrowFunction: () => {
        console.log(this.number);
        console.log(this);
      },
    };

    thisObject.objectFunction();
    // Strict and no strict mode:
    /*
    1
    {
      number: 1,
      objectFunction: [Function: objectFunction],
      objectArrowFunction: [Function: objectArrowFunction]
    }
    */

    thisObject.objectArrowFunction();
    // Strict and no strict mode: undefined, {}
    // It's because an arrow this is a reference to the global scope, window in the browser
    // B
    ```

  - Var adds values to global scope and those can be accessed by using this inside arrow functions

    ```JavaScript
    var number = 2;
    const thisObject = {
      number: 1,
      objectArrowFunction: () => {
        console.log(this.number);
        console.log(this);
      },
    };

    thisObject.objectArrowFunction();
    // On browser: 2, Window{... number: 2 ...}
    ```

  - You can also have trouble calling the `this` keword inside a function that is inside another function in an object

    ```JavaScript
    const thisObject = {
      number: 1,
      objectFunction: function() {
        console.log(this.number);
        console.log(this);
        const isOne = function() {
          console.log(this.number === 1);
        };
        isOne();
      },
    };

    thisObject.objectFunction();
    // Strict mode: 1, TypeError: Cannot read property 'number' of undefined
    // No strict mode: 1, { number: 1, objectFunction: [Function: objectFunction] }, false
    ```

    - A smart solution for this is to use another variable inide the first method, usually `self` or `that`

    ```JavaScript
    const thisObject = {
      number: 1,
      objectFunction: function() {
        console.log(this.number);
        console.log(this);
        const self = this;
        const isOne = function() {
          console.log(self.number === 1);
        };
        isOne();
      },
    };

    thisObject.objectFunction();
    // Strict and no strict mode:
    /*
    1
    { number: 1, objectFunction: [Function: objectFunction] }
    true
    */
    ```

    - Or you can use an arrow function because it doesn't have a this keyword and inside the other method it'll use the `this` keword of the parent object

    ```JavaScript
    const thisObject = {
      number: 1,
      objectFunction: function() {
        console.log(this.number);
        console.log(this);
        const isOne = () => {
          console.log(this.number === 1);
        };
        isOne();
      },
    };

    thisObject.objectFunction();
    // Strict and no strict mode:
    /*
    1
    { number: 1, objectFunction: [Function: objectFunction] }
    true
    */
    ```

    - The `arguments` keyword returns the arguments of the function but onlu in function expressions

      ```JavaScript
      const funcExpr = function(a, b) {
        console.log(arguments);
        return a + b;
      };
      funcExpr(1, 2);
      // [Arguments] { '0': 1, '1': 2 }
      funcExpr(1, 2, 3, 4, 5);
      // [Arguments] { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5 }

      const funcArrow = (a, b) => {
        console.log(arguments);
        return a + b;
      };
      funcArrow(1, 2);
      // ReferenceError: arguments is not defined
      funcArrow(1, 2, 3, 4, 5);
      // ReferenceError: arguments is not defined
      ```

  ## Primitives vs. Objects (Primitive vs. Reference Types)

  - Primitives:

    - _Number, String, Boolean, Undefined, Null, Symbol, BigInt_
    - Stored in the Call Stack

      ```JavaScript
      let someVariable = 30;
      let oldVariable = someVariable;
      someVariable = 31 // Value saved on 0002 not in 0001 because it's used on oldVariable
      const myObj = {someEntry: 'Some entry value'} // referenced to an object saved on Heap
      ```

      | Identifier   | Address | Value |
      | ------------ | ------- | ----- |
      | someVariable | 0001    | 30    |
      | oldVariable  | 0002    | 31    |
      | myObj        | 0003    | D30F  |

    - Can be modified after asigned
      ```JavaScript
      let someNum = 1;
      console.log(someNum); // 1
      let newNum = someNum;
      someNum = 2;
      console.log(newNum); // 1
      console.log(someNum); // 2
      ```

  - Objects

    - _Object literal, Arrays, Functions, Many more…_
    - Stored in the Heap

      | Address | Value                           |
      | ------- | ------------------------------- |
      | D30F    | {someEntry: 'Some entry value'} |

    - There are referenced inside variables and if you change them inside one variable it will be changed inside other variables that share the reference
      ```JavaScript
      const me = { name: 'Jonas', age: 30 };
      const friend = me;
      friend.age = 27;
      console.log(me); // { name: 'Jonas', age: 27 }
      console.log(friend); // { name: 'Jonas', age: 27 }
      ```
    - If you want to create a new object using a previous one you can use the following method
      ```JavaScript
      const newFriend = Object.assign({}, friend);
      newFriend.name = 'Douglas';
      newFriend.age = 30;
      console.log(friend); // { name: 'Jonas', age: 27 }
      console.log(newFriend) // { name: 'Douglas', age: 30 }
      ```
      - This is good for a first level copy but it doesn't works with objects inside objects (deep cloning)
