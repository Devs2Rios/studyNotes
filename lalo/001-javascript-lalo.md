# JavaScript from Zero to Expert

### Course notes

<details>
<summary><b>Intro</b></summary>
<br/>

- Web development basics
  - HTML(Nouns) | CSS(Adjectives) | JS(Verbs)
  - Separation of concerns - Every file separated, not in the HTML
- Test with Console
  - Brave or Chrome - `⌘⌥J`
  - Safari - `⌘⌥C`
- JavaScript
  - High-Level - Not complex stuff (memory) worries
  - Object-Oriented - Data based on objects
  - Multi-Paradigm - Use different styles of programming
  - Programming language - Instruct computer to do things
  - ES5, ES6+
    - 1995 - Mocha, first version of JavaScript created in just 10 days
      - A language to create interactive sites
    - 1996
      - It has nothing to do with Java
      - Changes to LiveScript and to JavaScript to attract Java divelopers
      - Microsoft launches IE and copies JavaScript into JScript
    - 1997 - ECMA releases ECMAScript 1 (ES1), the first standar for JavaScript
    - 2009 - ES5 (ECMAScript 5) was released with a lot of new features
    - 2015 - ES6 (ECMAScript 2015) was released (biggest update)
      - Changes to an annual release cycle
  - Don't break the web
    - Older code is still working
    - It's very buggy but still used
  - Development - Use the latest Chrome
  - Production - Transpile and polyfill the code to make it compatible with older browsers
  - ESNext - Future versions

</details>

<details>
<summary><b>JavaScript1</b></summary>
<br/>

- Value - Smallest unit of information
- Variable - Reusable value
  - `let` - Can be changed later
  - `const` - Won't be changed later, cannot be empty
  - `var` - Old way to define variables
  - Never declare a variablewithout really declaring it, it creates a global object and causes troubles
- Camel case is a convention
- Prevent `SyntaxError`
  - Never start a variable with a number
  - Just use letters, numbers, underscore or dollar
- Conventions
  - Don't use reserved words or `name`
  - Start with lowercase, upper is for classes
  - Check universal constants like `PI`
  - Be descriptive, `firstName` better than `name1`
- Primitives values
  - Primitives
    - Numbers `5, 5.9`
    - Strings `""`
    - Booleans `true, false`
    - Undefined `empty value`
    - Null `empty value`
    - Symbol `unique and cannot be changed`
    - BigInt `Larger numbers than Number can hold`
    - Dynamic type `you don't have to define the type of value`
  - Type conversion and coercion
    - Check what kind of value you have `typeof`
    - Change between types of values `Number('5')`
    - Some changes are automatic `'Love ' + 5 // 5 becomes a string`
    - Strings automatically transformed into numbers `'5' - '12' - 5`
  - Truthy and falsy values
    - `0, '', undefined, null, NaN` return a falsy value of `false`
    - All other values are truthy and return `true`
    - You can check by ransforming values to booleans:
      ```JavaScript
      Boolean(0) // false
      Boolean(1) // true
      ```
- Comments
  ```JavaScript
  // Single line
  /* Multiline */
  ```
- Math operators
  - `+` plus (sum of two numbers or concatenate strings)
  - `-` less
  - `/` divide
  - `*` multiply
  - `**` power of
- Assignment operators
  - `=` equal
  - `+=` add value to a variable
  - `-=` substract value to a variable
- Comparison operators
  - `<` less than
  - `>` plus than
  - `<=` less than equal
  - `>=` plus than equal
- Strings and template literals
  - Syntax `"String"` `'String'` `` `String` ``
  - Concatenate `'Hi ' + 'dear!'`
  - Template literals `` `I am ${jsValue} years old` ``
- Conditionals:
  - Positive `if (condition) {execution}`
  - Negative `if (!condition) {execution}`
  - Multiple `if (c) {e1} else if (c2) {e2} else {e3}`
- Expressions: poduce a value `true && false`
- Statements: sentences that translate our order `const str = 'Sentence'`
- Equality operators:
  - Strict operators, without type coercion:
    - `===` equal
    - `!==` not equal
    - `1 === '1' // false`
  - Strict operators, with type coercion:
    - `==` equal
    - `!=` not equal
    - `1 == '1' // true`
- Boolean logic:
  - `&&` and
  - `||` or
  - `!` not
- Switch: It's an statement so it can`t be inside a function or return
  ```JavaScript
  const variable = 1;
  switch(variable){
    case 1:
      console.log('It\'s one'); // If variable is equal to 1 it's executed
      break; //if you want to break at that step
    case 2:
      console.log('It\'s two'); // Multiple cases
    default:
      console.log('It\'s not a number');//like an else statement
  }
  ```
- Ternary operator: It's a expression so it can be inside a function or return
  ```JavaScript
  const isFive = 5 ? 'It\'s five' : 'It\'s not five';
  ```

</details>

<details>
<summary><b>JavaScript2</b></summary>
<br/>

- Strict mode - Use it always to create safer code
  - Start a file with `'use strict';`
- Functions - piece of code that can be used several times

  - Best way to implement the principle DRY (Don't Repeat Yourself)
  - Define functions
    - `function` reserved word can be used to define a function
      - `function funcName(parameters) {action};` this is a function declaration and it can be used before it's declarated
      - You can also use this reserved word to create an anonymous function (function expression): `const anonymous = function(params) {action}`
    - Arrow functions
      - They don't have the `this` keword
        ```JavaScript
        const myFunction = num1 => num1 + 1;
        ```
        - it returns explicitally without `return`
      - If it gets complex it needs more structure
        ```JavaScript
        const myFunction = (num1, num2) => num1 + num2; // Single line
        const myFunction = (num1, num2) => {
          return num1 + num2 // Multi-line needs return
        }
        ```
  - Call / run / invoke functions `myFunction(argument);`
    - The parameter is the name used to define the function variables and the argument the actual value used when calling the function
  - `return` returns a value at the end of the function
    - Just the first `return` achieved returns a value
    - Just works inside functions
    - If the function doesn't have a `return` it returns `undefined`
    - If you want to return a list use brackets `[]` if not it will return just the last value
      ```JavaScript
      return true, false //false
      return [true, false] //[true, false]
      ```
    - It needs parenthesis if you start the return value in the second line
      ```JavaScript
      return (
          5 + 10
      )
      ```
  - You can use functions inside other functions so you can write cleaner code
    ```JavaScript
    function func1() {return true};
    function func2() {
        const myTrue = func1();
        return [myTrue, false];
    }
    ```
  - Arrays
    - Declarate an array:
      - Literal: `const nums = [1,2,3,4];`
      - New object: `const nums = new Array(1,2,3,4);`
      - Zero indexed `nums[0] // first element, expression inside, not statement`
      - Length `nums.length // 4`
      - Change array values: `nums[0] = 10; //[10,2,3,4]`
      - This is not a primitive value so even though it's declared as const you can change the values inside the object.
      - If you put an array in another variable and modify it, the value will be modified in both becaus is the same object referenced in another variable, to change this behavior you'll need to copy it in the new variable.
    - Array methods:
      - `.push` add to the end
        ```JavaScript
        console.log(arr.push(5)) //5
        ```
      - `.unshift` add to the begining
        ```JavaScript
        console.log(arr.unshift(5)) //5
        ```
      - `.pop` remove the last element
        ```JavaScript
        console.log(arr.pop()) //Value popped
        ```
      - `.shift` removes the first element
        ```JavaScript
        console.log(arr.shift()) //Value shifted
        ```
      - `.indexOf` returns the index of the argument
        ```JavaScript
        arr.indexOf(value) // Returns a number
        ```
      - `.includes` returns whether or not an array includes certain value
        ```JavaScript
        arr.includes(value) // Returns a boolean
        ```
  - Objects

    - Non ordered data structure
    - Declarate an object:
      - Literal `const objName = {key: value, key2: value2};`
      - Acces to a key:
        - Dot notation, member access `objName.key`
        - Bracket notation, computed member access `objName['key']`
          - Useful when concatenation needed `objName['key'+'2']`
      - Add or modify an entry: `objName['key'+'2'] = 'new value 2';`
      - Add functions to objects
        ```JavaScript
        const objWithFunc = {
            firstName: 'John',
            johnIs: '',
            myFunc: function(msg) {
                this.johnIs = `${this.firstName} ${msg}`;
                return this.johnIs;
            }
        };
        console.log(objWithFunc.myFunc('is good!')); // Changes johnIs entry
        // console.log(objWithFunc['myFunc']('is good!')); // Another way to use the function
        console.log(objWithFunc.johnIs); // John is good!
        ```
        - Even though you are able to perform the function several times, that's a bad practice because it uses a lot of computing, the best way to do it is to use the function ones to define a value inside the object.

  - Iteration
    - For loop keeps running while condition is true
      ```JavaScript
      for (let i=0; i<10; i++) {console.log(i)};
      for (let i=0; i<10; i++) console.log(i); // This will also work
      ```
    - You can iterate through an array by using the index
      ```JavaScript
      const myArr = [0,1,2,3,4,5,6,7];
      const doubleArr = [];
      for (let i=0; i<myArr.length; i++) {
          doubleArr.push(i*2);
      };
      ```
    - Or by using an of loop
      ```JavaScript
      for (const i of myArr) {doubleArr.push(i*2);};
      ```
    - You can make jumps between the loop steps by using continue
      ```JavaScript
      for (const i of myArr) {
          if (i === 3) continue;
          doubleArr.push(i*2);
      };
      ```
    - Or you can break the loop if a condition is met
      ```JavaScript
      for (const i of myArr) {
          if (i === 5) break;
          doubleArr.push(i*2);
      };
      ```
    - This is a way to loop backwards
      ```JavaScript
      for (let i=myArr.length-1; i>=0; i--) {doubleArr.push(i*2);};
      ```
    - Nested loop are sometimes useful, like when you want all the 10 units square coordinates inside a 100\*100 square
      ```JavaScript
      const increment = 10;
      for (let x=0; x<100; x+=increment) {
          for (let y=0; y<100; y+=increment) {
              console.log('Coord:', [x,y]);
          }
      };
      ```
    - The while loop keeps runing until matches a condition
      ```JavaScript
      let ranNum = 0;
      while (ranNum!==100) {
          ranNum = Math.round(Math.random()*100);
          console.log(ranNum);
      };
      ```

</details>

<details>
<summary><b>Developer Skills & Editor Setup</b></summary>
<br/>

- Setup

  - Add Prettier extension to VS Code
  - default formatter `esbenp.prettier-vscode`
  - format on save `true`
  - toggle single quotes to `true` in the settings
  - select `avoid` in the Arrow Parens option
  - Add snippets
  - Go to `Code > Preferences > Configure User Snippets`
  - Write your snippets:
    ```JSON
    "Print to console": {
    "scope": "javascript,typescript",
    "prefix": "print",
    "body": ["console.log();"],
    "description": "Log output to console"
    }
    ```
  - Install [node.js](https://nodejs.org/en/)
  - Check which version of node you have `node -v`
  - NPM comes with node.js
  - Check which version of npm you have `npm -v`
  - Use a light server:
  - You can use a VS Extension
  - Or install it via NPM with the command `npm install live-server -g`
  - Run your server by using `live-server` on your working directory

- Developer mind
  - Goal
    - Realistic time based
    - Why are you learning? `Complement my career`
    - Imagine a project
    - Research technologies
  - Always understand the code by studying it and typing it
  - Reinforce knowledge
    - Use it
    - Take notes
    - Challenge yourself
      - [Codewars](https://www.codewars.com/)
    - Don't be in a hurry
  - Practice
    - Create your own challenges
    - Don't get stuck in "tutorial hell"
  - Write a lot and you'll be improving it
  - Refactor what you did
  - You'll never know everything so focus on your goal
  - Learn with other people and teach
  - Problem solver
    - Understand the problem
    - Divide and conquer
      - Break big problems into small steps
    - Do the necessary research
    - Write pseudocode before the actual code
  - Research tools, always ask the right questions
    - [MDN](https://developer.mozilla.org/en-US)
    - [StackOverflow](https://stackoverflow.com)
    - [Google](https://www.google.com)
  - Debugging
    - Bug: defect or problem in a computer program
      - Identify:
        - Discover the bug
        - Test software
        - Use reports
        - Check in contexts
      - Find:
        - Find the place where the bug is
      - Fix:
        - Correct the bug
      - Prevent:
        - Find it elsewhere
        - Write unit testing
    - Breakpoint:
      - useful console methods for debugging:
        ```JavaScript
        console.warn(); console.error(); console.table(object);
        ```
      - Chrome debugger:
        - `View > Developer > Inspect Element` or `⌘⌥C`
        - Go to sources and select the JavaScript file to debug
        - Add the desired breakpoints
        - Go step by step checking what's happening using `F9` or the step button
    - You can debug directly on VS Code by using `debugger;` before each breakpoint

</details>

<details>
<summary><b>HTML & CSS Crash Course</b></summary>
<br/>

- HTML
  - HyperText Markup Language
  - Semantic HTML is a way to give the more accurated tag to an element so it can be mor readable
  - Structure:
    ```HTML
    <html>
      <head>
        <title>Example</title>
      </head>
      <body>
        <h1>Heading example</h1>
        <p>Paragraph example</p>
        <!-- Comment example -->
      </body>
    </html>
    ```
  - Attributes: `<a href="https://www.some.link"></a>`
  - Inline and block elements work together:
    - Inline `<span></span>` displays inside anoder block
    - Block `<p></p>` displays as a block inside html
  - Classes
    - Attribute that defines the name of one or several elements in order to style them
      ```HTML
      <h1 class="inverted">This is an inverted color heading</h1>
      <p class="inverted">This is an inverted color paragraph</p>
      <!-- Classes can be used several times -->
      ```
  - IDs
    - Special attribute that gives an element an unique identifier
      ```HTML
      <p id="special-paragraph">Special</p>
      <!-- Unique element -->
      ```
- CSS

  - Cascading Style Sheets
  - It's the way to give style to HTML elements
  - Structure
    - Inside HTML (not recommended)
      ```HTML
      <style>
        body {
          background-color: white;
        }
      </style>
      ```
    - Or in a .css file linked to the html
      ```HTML
      <!-- index.html -->
      <head>
        <link href="style.css" rel="stylesheet">
      </head>
      ```
      ```CSS
      /* style.css */
      body {
        background-color: white;
      }
      ```
  - Inheritance
    - Child elements inherit some properties from their parents, for example if you add `font-family: Arial;` into `body {}` all body's children will have the same font-family
    - Some properties like border are not inherited
  - Syntax
    - Regular selector `p {color: black;}`
    - ID selector `#my-ID {font-size: 10px;}`
    - Class selector `.my-class {background-color: blue;}`
    - Child selector `#my-ID code {font-family: Menlo;}`
  - Box model:
    |Element|Description|
    |---|---|
    |**Content** |Text, images, etc.|
    |**Padding** |Transparent area around the content inside the box|
    |**Border** |Around the padding and the content|
    |**Margin** |Space between boxes|
    |**Fill Area**|Area that gets filled with background color or image|

    ```

       Margin
        --------------------------------
       |                                |
       |      Padding                   |
       |                                |
       |       W   i   d   t   h        |
       |       -----------------  H     |
       |      |                 | e     |
       |      |     CONTENT     | i     |
       |      |     *******     | g     |
       |      |                 | h     |
       |       -----------------  t     |
       |      Border:                   |
       |      Line around the box       |
       |      padding and content.      |
       |                                |
       |                                |
        --------------------------------

    ```

    - For better control of your box size you can use `* {box-sizing: border-box;}` which will allow you to define widths and heights considering the paddings and margins

  - For reset properties globaly you'll need to use the asterix which goes for all elements `* {margin: 0;}`

</details>

<details>
<summary><b>JavaScript in the Browser: DOM and Events Fundamentals</b></summary>
<br/>

- The DOM (Document Object Model)
  - Structured representation of HTML documents
  - Allows JS to access HTML elements and manipulate them
  - JS interaction with the DOM reference is in WEB APIs
- Acces to an HTML node
  - Access by query selector `document.querySelector('.my-class');`
    - Query selector only acces the first incidence, if you want to get all just use `.querySelectorAll()`
    - The `.` is only used when you are looking for a class selector, other methods like `myNode.classList.remove('my-class-1', 'my-class-2');`
  - Access by ID
    ```JavaScript
    document.getElementByID('my-ID'); // Faster
    document.querySelector('#my-ID'); // Easier
    ```
  - You can modify properties of the element
    ```JavaScript
    document.querySelector('.my-class').textContent = 'New content';
    document.querySelector('#my-ID').textContent = 'New content';
    ```
  - Events
    - An event is something that happends in te page like a mouse movement
    - Every node is able to hold an `addEventListener()` method
    - Click example
      ```JavaScript
      const myNode = document.querySelector('.my-class');
      const myFunction = () => return true;
      myNode.addEventListener('click', function() {return true});
      myNode.addEventListener('click', myFunction);
      ```

</details>

<details>
<summary><strong>How JavaScript Works Behind the Scenes</strong></summary>
<br/>

- ### A Hiigh-Level Overview of JavaScript

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

- ### The JavaScript Engine and Runtime

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

- ### Execution Contexts and The Call Stack:

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

- ### Scope and The Scope Chain
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
- ### Variable Environment: Hoisting and The TDZ

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

- ### The `this` Keyword

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

- ### Regular Functions vs. Arrow Functions

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

- ### Primitives vs. Objects (Primitive vs. Reference Types)

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

</details>

<details>
<summary><strong>Data Structures, Modern Operators and Strings</strong></summary>

- Destructuring Arrays

  ```JavaScript
  const arr = [2, 3, 4];
  // You can assingn an array values to different variables
  const a = arr[0];
  const b = arr[1];
  const c = arr[2];
  // Or destructure and do it in one line
  const [x, y, z] = arr;
  console.log(x, y, z); // 2, 3, 4

  // You can use destructure with arrays inside objects
  const sports = {
    name: 'Sports selection',
    trainingCentre: 'Two Rivers, MX, Mexico',
    categories: ['Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis'],
    warmUp: ['Jogging', 'Jumping', 'Sprinting'],
    coolDown: ['Walk', 'Stretch'],
    ranWorkout: function() {
      return [
        this.warmUp[Math.floor(Math.random() * this.warmUp.length)],
        this.categories[Math.floor(Math.random() * this.categories.length)],
        this.coolDown[Math.floor(Math.random() * this.coolDown.length)],
      ];
    },
  };
  // You can destructure an array by assin¡gning a name to the elements you want,
  // and leaving empty the ones you dont want
  let [favorite, , , , lessFavorite] = sports.categories;
  console.log(favorite, lessFavorite); // Rugby Tennis
  // Switch values
  [favorite, lessFavorite] = [lessFavorite, favorite];
  console.log(favorite, lessFavorite); // Tennis Rugby
  // Destructuring from a return value from a function
  let [myWarmUp, mySport, myCoolDown] = sports.ranWorkout();
  console.log(myWarmUp, mySport, myCoolDown); // Jumping Rugby Stretch

  // Destructuring nested arrays
  const nested = [0, [1, 11], [2, 3]];
  const [, [one], [two, three]] = nested;
  console.log(one, two, three); // 1 2 3

  // Destructuring with default values, if they are not assigned they're undefined
  const [ja, ha, kha = 'Russian'] = ['Español', 'Inglés'];
  console.log(ja, ha, kha); // Español Inglés Russian (undefined if not assigned)
  ```

- Destructuring Objects

  ```JavaScript
  const sports = {
    collectionName: 'Sports selection',
    trainingCentre: 'Two Rivers, MX, Mexico',
    categories: ['Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis'],
  };

  // For object destructure you need to match the key of the object
  let { collectionName, trainingCentre, categories } = sports;
  console.log(collectionName, trainingCentre, categories);
  // Sports selection Two Rivers, MX, Mexico [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ]

  // You can assign specific entries { entryName: yourVar }
  const {
    collectionName: myCollection,
    trainingCentre: myClub,
    categories: mySports,
  } = sports;
  console.log(myCollection, myClub, mySports);
  // Sports selection Two Rivers, MX, Mexico [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ]

  // You can set default values
  const { categories: normalSports, extreme = [] } = sports;
  console.log(normalSports, extreme);
  // [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ] []

  // Mutating variables
  let col1 = 'Red',
    col2 = 'Blue';
  const colors = { col1: 'Magenta', col2: 'Cyan' };
  ({ col1, col2 } = colors); // Wrapped into parenthesis
  console.log(col1, col2); // Magenta Cyan

  // Nested objects
  const square = {
    coord1: { x: 0, y: 0 },
    coord2: { x: 10, y: 0 },
    coord3: { x: 10, y: 10 },
    coord4: { x: 0, y: 10 },
  };
  const {
    coord1: { x, y, z = 0 }, // You can add defaults to prevent undefined values
  } = square;
  console.log(x, y, z); // 0 0 0

  // Destructuring an object inside a function
  function destructureObj({ name, surname }) {
    return `I am ${name} ${surname}`;
  }
  const jonasFierro = { name: 'Jonás', surname: 'Fierro' };
  console.log(destructureObj(jonasFierro));
  // I am Jonás Fierro
  ```

- The Spread Operator (...)

  ```JavaScript
  // SPREAD packs elements into an array
  // Is useful to unpack an array
  const arr1 = [0, 1, 2, 3, 4, 5];
  const arr2 = [...arr1, 6, 7, 8, 9];
  // arr2 is the same as [arr1[0], arr1[1], arr1[2], arr1[3], arr1[4], arr1[5], 6, 7, 8, 9]
  console.log(arr2); // [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

  // Yuo can unpack an array inside an object
  const arrInObj = { arr: [1, 2, 3, 4] };
  const arr3 = [...arrInObj.arr, 5];
  console.log(arr3); // [ 1, 2, 3, 4, 5 ]

  // Copy an array
  const arr4 = [...arr3];
  console.log(arr4); // [ 1, 2, 3, 4, 5 ]

  // Join 2 arrays
  const arr5 = [6, 7, 8, 9, 10];
  const arr6 = [...arr4, ...arr5];
  console.log(arr6); // [ 1, 2, 3, 4,  5, 6, 7, 8, 9, 10 ]

  // Iterables: arrays, strings, maps, sets, NOT objects
  const str = 'Iterate';
  const letters = [...str, '!'];
  console.log(letters); // [ 'I', 't', 'e', 'r', 'a', 't', 'e', '!' ]

  // Add it to a function
  function iterable(one, two, three) {
    let str = '';
    for (const count of [one, two, three]) {
      str += `Now the number is ${count}!\n`;
    }
    return str;
  }
  console.log(iterable(...[1, 2, 3]));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  */

  // You can use it with an object as well
  const oldObj = { old: "I'm old", age: 90 };
  const newObj = { ...oldObj, new: "I'm new", age: 1 };
  const copyOfNewObj = { ...newObj }; // Copy of newObj
  copyOfNewObj.old = "I'm not old";
  console.log(oldObj); // { old: "I'm old", age: 90 }
  console.log(newObj); // { old: "I'm old", age: 1, new: "I'm new" }
  console.log(copyOfNewObj); // { old: "I'm not old", age: 1, new: "I'm new" }
  ```

- Rest Pattern and Parameters

  ```JavaScript
  // REST packs elements into a variable
  const [a, b, ...others] = [1, 2, 3, 4, 5, 6, 7];
  console.log(a, b, others); // 1 2 [ 3, 4, 5, 6, 7 ]

  // REST is useful with destructuring
  const countries = {
    latam: ['México', 'Argentina', 'Brasil'],
    northam: ['United States', 'Canada'],
    oeurope: ['Netherlands', 'España', 'France', 'Italia'],
    eeurope: ['România', 'Hrvatska', 'Україна'],
  };
  const [mx, , brl, ...otherCountries] = [
    ...countries.latam,
    ...countries.eeurope,
  ];
  console.log(mx, brl, otherCountries);
  // México Brasil [ 'România', 'Hrvatska', 'Україна' ]

  const { oeurope: euroOr, eeurope: euroOcc, ...america } = countries;
  console.log(euroOr, euroOcc, america);
  // [ 'Netherlands', 'España', 'France', 'Italia' ]
  // [ 'România', 'Hrvatska', 'Україна' ]
  /*
  {
    latam: [ 'México', 'Argentina', 'Brasil' ],
    northam: [ 'United States', 'Canada' ]
  }
  */

  // Add it to a function
  function iterable(...counting) {
    let str = '';
    for (const count of counting) {
      str += `Now the number is ${count}!\n`;
    }
    return str;
  }
  console.log(iterable(1, 2, 3, 4, 5, 6, 7, 8));
  /*
    Now the number is 1!
    Now the number is 2!
    Now the number is 3!
    Now the number is 4!
    Now the number is 5!
    Now the number is 6!
    Now the number is 7!
    Now the number is 8!
    */
  const newArr = [1, 2, 3];
  console.log(iterable(...newArr));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  */
  console.log(iterable(...newArr, 4));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  Now the number is 4!
  */

  ```

- Short Circuiting (&& and ||)

  ```JavaScript
  // || (or) Returns the first value that is truthy
  console.log(1 || 'Dope'); // 1
  console.log(0 || 'Dope'); // Dope
  console.log(0 || ''); // null
  console.log(0 || '' || null || 'Truthty'); // Truthty
  const lights = { on: false };
  const lightsOn = lights.on || 'Turn on the lights';
  console.log(lightsOn); // Turn on the lights

  // && (and) returns the last value if everything is truthy
  // it stops when finds a falsy value
  console.log(0 && 'a'); // 0
  console.log(1 && 'a'); // a
  console.log(1 && 'a' && []); // []
  console.log(1 && 'a' && [1] && null); // null

  // Let's put them in conditionals
  const bool1 = true,
    bool2 = false,
    bool3 = true,
    bool4 = false;

  if (bool1 || bool2) console.log(`bool1: ${bool1} || bool2: ${bool2}`);
  // bool1: true || bool2: false
  if (bool2 || bool4) console.log(`bool2: ${bool2} || bool4: ${bool4}`);
  // nothing
  if (bool1 || bool3) console.log(`bool1: ${bool1} || bool3: ${bool3}`);
  // bool1: true || bool3: true
  if (bool1 && bool2) console.log(`bool1: ${bool1} && bool2: ${bool2}`);
  // nothing
  if (bool1 && bool3) console.log(`bool1: ${bool1} && bool3: ${bool3}`);
  // bool1: true && bool3: true
  if (bool2 && bool2) console.log(`bool2: ${bool2} && bool4: ${bool4}`);
  // nothing
  ```

- The Nullish Coalescing Operator (??)

  ```JavaScript
  // Nullish: Null and undefined
  const lights = { on: false };
  let lightsOn = lights.on ?? 'Turn on the lights';
  console.log(lightsOn); // false
  lights.on = undefined;
  lightsOn = lights.on ?? 'Turn on the lights';
  console.log(lightsOn); // 'Turn on the lights'
  ```

- Logical Assignment Operators

  ```JavaScript
  const p1 = {
    controller: 'P1',
    alias: 'Berta',
    hallOfFame: undefined,
  };
  const p2 = {
    controller: 'P2',
    alias: '',
    exp: 10,
    hallOfFame: undefined,
  };

  // The long way
  p1.exp = p1.exp || 1;
  console.log(p1);
  // {controller: 'P1', alias: 'Berta', hallOfFame: undefined, exp: 1}
  p2.exp = p2.exp && 1;
  console.log(p2);
  // {controller: 'P2', alias: '', exp: 1, hallOfFame: undefined}

  // The short way in JavaScript 2021
  p1.hallOfFame &&= 'Not yet!';
  console.log(p1);
  // {controller: 'P1', alias: 'Berta', hallOfFame: undefined, exp: 1}
  p2.alias ||= 'No-Alias';
  p2.hallOfFame ??= 'Not yet!';
  console.log(p2);
  // {controller: 'P2', alias: 'No-Alias', exp: 1, hallOfFame: 'Not yet!'}
  ```

- Looping Arrays: The for-of Loop

  ```JavaScript
  const bigArray = [];
  for (let i = 0; i < 5; i++) bigArray.push(Math.round(Math.random() * 1000));
  for (const ranNum of bigArray) console.log(`Te random number is ${ranNum}`);
  /*
  Te random number is 831
  Te random number is 769
  Te random number is 223
  Te random number is 188
  Te random number is 204
  */

  // for loop with index and destructure
  for (const [i, ranNum] of bigArray.entries())
    console.log(`Te random number ${i + 1} is ${ranNum}`);
  /*
  Te random number 1 is 831
  Te random number 2 is 769
  Te random number 3 is 223
  Te random number 4 is 188
  Te random number 5 is 204
  */
  ```

- Enhaced Object Literals

  ```JavaScript
  const thought = 'Thinking';
  const arrLength = 3;

  const objLiteral = {
    quote: "I'm literal",
    thoughts: ["I'm happy", "I'm sad", "I'm hungry"],
    // ES& enhaced object literals
    // Add an entry just by calling an outside variable
    thought,
    // Define an entry name by computing
    arrLength,
    [`arrWith${arrLength}els`]: new Array(arrLength),
    // Add a function just by declaring the name and adding the paranthesis
    newThougt() {
      this.thought = this.thoughts[
        Math.floor(Math.random() * this.thoughts.length)
      ];
      return this.thought;
    },
  };

  objLiteral.newThougt();
  console.log(objLiteral);
  /*
  {
    quote: "I'm literal",
    thoughts: [ "I'm happy", "I'm sad", "I'm hungry" ],
    thought: "I'm sad",
    arrLength: 3,
    arrWith3els: [ <3 empty items> ],
    newThougt: [Function: newThougt]
  }
  */
  ```

- Optional chaining (?.)

  ```JavaScript
  const pad = num => num.toString().padStart(5, '0');
  const tr = 'tr',
    bk = 'block';

  const chained = {
    [`${bk}${pad(1)}`]: {
      [`${tr}${pad(1)}`]: {
        hash: 'e193a01ecf8d30ad0affefd332ce934e32ffce72',
        time: new Date(2019, 1, 28, 18, 1, 10, 230),
      },
      [`${tr}${pad(2)}`]: {
        hash: '6fc978af728d43c59faa400d5f6e0471ac850d4c',
        time: new Date(2020, 6, 1, 14, 31, 3, 915),
      },
    },
    [`${bk}${pad(2)}`]: {
      [`${tr}${pad(3)}`]: {
        hash: '221407c03ae5c73109cce71d27e24637824f3333',
        time: new Date(2020, 10, 1, 17, 15, 50, 750),
      },
      [`${tr}${pad(4)}`]: {
        hash: 'c63528a52274a35d1c07bd9e55a83c6eb073de81',
        time: new Date(2021, 8, 30, 11, 11, 11, 111),
      },
    },
    [`${bk}${pad(3)}`]: {
      [`${tr}${pad(5)}`]: {
        hash: 'de1f53b6fbc3fecd35b0bbc963e21902a149e5e3',
        time: new Date(2021, 11, 3, 0, 3, 45, 104),
      },
      [`${tr}${pad(6)}`]: {
        hash: '20dd129da16a9afb802d8b595485f8d2719aea44',
        time: new Date(2022, 2, 16, 9, 21, 36, 426),
      },
    },
    [`${bk}${pad(4)}`]: {
      [`${tr}${pad(7)}`]: {
        hash: '',
      },
    },
  };

  console.log(chained?.block00001);
  /*
  {
    tr00001: {
      hash: 'e193a01ecf8d30ad0affefd332ce934e32ffce72',
      time: 2019-03-01T00:01:10.230Z
    },
    tr00002: {
      hash: '6fc978af728d43c59faa400d5f6e0471ac850d4c',
      time: 2020-07-01T19:31:03.915Z
    }
  }
  */
  console.log(chained?.block00001?.tr00003 ?? 'No such transaction in the block'); // No such transaction in the block
  console.log(chained?.block00004?.tr00007); // { hash: '' }
  console.log(
    chained?.block00004?.tr00007?.time ?? 'No timestamp in such transaction'
  ); // No timestamp in such transaction
  // It might be useful for a loop that checks transactions within a block
  const [...myBlocks] = Object.keys(chained);
  const myTransactions = [];
  for (let i = 0; i < 7; i++) myTransactions.push(`${tr}${pad(i + 1)}`);
  for (const myBlock of myBlocks) {
    for (const myTransaction of myTransactions) {
      const currentTransaction = chained[myBlock][myTransaction]?.hash;
      if (currentTransaction) {
        console.log(
          `Block ${myBlock}, transaction ${myTransaction}: ${currentTransaction}`
        );
      }
    }
  }
  /*
  Block block00001, transaction tr00001: e193a01ecf8d30ad0affefd332ce934e32ffce72
  Block block00001, transaction tr00002: 6fc978af728d43c59faa400d5f6e0471ac850d4c
  Block block00002, transaction tr00003: 221407c03ae5c73109cce71d27e24637824f3333
  Block block00002, transaction tr00004: c63528a52274a35d1c07bd9e55a83c6eb073de81
  Block block00003, transaction tr00005: de1f53b6fbc3fecd35b0bbc963e21902a149e5e3
  Block block00003, transaction tr00006: 20dd129da16a9afb802d8b595485f8d2719aea44
  */
  ```

- Looping Objects: Object Keys, Values, and Entries

  ```JavaScript
  const animals = {
  dog: {
      id: 'Dog',
      animalName: 'Frida',
      breed: 'Labrador',
      isPet: true,
    },
    cat: {
      id: 'Cat',
      animalName: 'Koshka',
      breed: 'Munchkin',
      isPet: true,
    },
    snake: {
      id: 'Snake',
      animalName: 'Piguay',
      breed: 'Python',
    },
  };

  const [...keys] = Object.keys(animals);
  console.log(keys); // [ 'dog', 'cat', 'snake' ]
  const [...values] = Object.values(animals);
  console.log(values);
  /*[
    { id: 'Dog', animalName: 'Frida', breed: 'Labrador', isPet: true },
    { id: 'Cat', animalName: 'Koshka', breed: 'Munchkin', isPet: true },
    { id: 'Snake', animalName: 'Piguay', breed: 'Python' }
  ]*/
  for (const [key, animal] of Object.entries(animals)) {
    console.log(
      `animals.${key}: I'm a ${animal.breed} ${animal.id}, my name is ${
        animal.animalName
      } and I'm ${(animal?.isPet && 'a pet') || 'not a pet'}`
    );
  }
  /*
  animals.dog: I'm a Labrador Dog, my name is Frida and I'm a pet
  animals.cat: I'm a Munchkin Cat, my name is Koshka and I'm a pet
  animals.snake: I'm a Python Snake, my name is Piguay and I'm not a pet
  */
  ```

- Sets

  ```JavaScript
  // A set is an unordered data (it has no indexes) structure that has unique elements inside of it
  const newSet = new Set([10, 11, 40, 50, 11, 66, 50]); // You can pass any iterable as argument
  console.log(newSet); // Set(5) { 10, 11, 40, 50, 66 }
  const newStringSet = new Set('Still Fozzy');
  console.log(newStringSet); // Set(9) { 'S', 't', 'i', 'l', ' ', 'F', 'o', 'z', 'y' }
  // set methods
  console.log(newSet.has(1)); // false
  console.log(newStringSet.has('z')); // true
  console.log(newStringSet.has(' ')); // true
  newStringSet.delete(' ');
  console.log(newStringSet.has(' ')); // false
  newStringSet.add('!');
  console.log(newStringSet.has('!')); // true
  console.log(newStringSet); // Set(9) { 'S', 't', 'i', 'l', 'F', 'o', 'z', 'y', '!' }
  for (const val of newStringSet) {
    if (val === 'F') {
      break;
    } else {
      console.log(val);
    }
  }
  /*
  S
  t
  i
  l
  */
  newStringSet.clear();
  console.log(newStringSet); // Set(0) {}
  const newArrFromSet = [...new Set('Parangaricutirimicuaro')];
  console.log(newArrFromSet); // [ 'P', 'a', 'r', 'n', 'g', 'i', 'c', 'u', 't', 'm', 'o' ]
  ```

- Maps: Fundamentals

  ```JavaScript
  // In maps the keys can have eny kind of value
  const coffee = new Map();
  // You can set values using the set method
  coffee.set('Roast', 'Dark');
  coffee.set('Origin', 'Chiapas');
  coffee.set(304029198, 'Batch serial number');
  // Set can be also used chained
  const arr = [10, 10, 9];
  coffee
    .set('Packed Date', 20220134)
    .set(1045, 'River One Store, HXQ')
    .set(arr, 'Quality Control')
    .set(true, 'Packed')
    .set(false, 'Not packed');
  console.log(coffee);
  /*
  Map(8) {
    'Roast' => 'Dark',
    'Origin' => 'Chiapas',
    304029198 => 'Batch serial number',
    'Packed Date' => 20220134,
    1045 => 'River One Store, HXQ',
    [ 10, 10, 9 ] => 'Quality Control',
    true => 'Packed',
    false => 'Not packed'
  }
  */
  const packedOn = coffee.get('Packed Date');
  console.log(coffee.get(packedOn < 1900) && coffee.get(packedOn >= 19000)); // Packed
  // Another useful methods
  console.log(coffee.has('Roast')); // true
  coffee.delete(arr); // Two arrays with the same values are not equal, it must be the same array
  console.log(coffee);
  /*
  Map(7) {
    'Roast' => 'Dark',
    'Origin' => 'Chiapas',
    304029198 => 'Batch serial number',
    'Packed Date' => 20220134,
    1045 => 'River One Store, HXQ',
    true => 'Packed',
    false => 'Not packed'
  }
  */
  console.log(coffee.size); // 7
  ```

- Maps: Iteration

  ```JavaScript
  // Prompt is a browser engine method, this is for the terminal
  const prompt = require('prompt-sync')();

  // Create a map using Arrays of two elements inside another array
  const programmingLangs = new Map([
    ['Question', "What's the best programming language"],
    [1, 'Python'],
    [2, 'JavaScript'],
    [true, 'Pythonist'],
    [false, 'Not pythonist'],
  ]);
  console.log(programmingLangs);
  /*
  Map(5) {
    'Question' => "What's the best programming language",
    1 => 'Python',
    2 => 'JavaScript',
    true => 'Pythonist',
    false => 'Not pythonist'
  }
  */
  // It could also be an object's entries
  const songs = { song1: 'GOD', song2: 'Unwind' };
  const songMap = new Map(Object.entries(songs));
  console.log(songMap); // Map(2) { 'song1' => 'GOD', 'song2' => 'Unwind' }

  // Iterations are easier destructuring
  console.log(programmingLangs.get('Question')); // What's the best programming language
  for (const [key, value] of programmingLangs) {
    if (typeof key === 'number') console.log(`Answer ${key}: ${value}`);
    /*
    Python
    JavaScript
    */
  }
  const answer = Number(prompt('Your answer (write the number): '));
  console.log(programmingLangs.get(answer === 1) || programmingLangs.get(false));
  // Depends on the answer it will return Python or Not pythonist

  // Convert map to array
  console.log([...songMap]); // [ [ 'song1', 'GOD' ], [ 'song2', 'Unwind' ] ]
  console.log([...songMap.keys()]); // [ 'song1', 'song2' ]
  console.log([...songMap.values()]); // [ 'GOD', 'Unwind' ]

  ```

- Which Data Structure to Use?

  - Sources of data: from the program, from the UI and from external sources (APIs)
  - Detect if it just needs values or key/value pairs
    - Just values
      - Arrays: if you need an order and you can have duplicated values
      - Sets: if you don't need an order and you don't want duplicated values, they're also faster
    - Keys and values
      - Objects: they're easier to use, you can use methods inside of them and are the best structure when using JSON
      - Maps: When you need keys that are not strings, they're easier to iterate, they perform better than objects

- Working With Strings

  ```JavaScript
  const myString = 'This is a string';
  // Access to certain letter by index
  console.log(myString[0]); // T
  // Return the length of a string
  console.log(myString.length); // 16
  // Find index of a letter inside a string
  console.log(myString.indexOf('a')); // 8
  console.log(myString.indexOf('x')); // -1 didn't find
  console.log(myString.lastIndexOf('i')); // 13
  // Cut a string
  console.log(myString.slice(4)); // is a string
  console.log(myString.slice(1, 10)); // his is a
  console.log(myString.slice(0, myString.indexOf(' a '))); // This is
  console.log(myString.slice(0, myString.lastIndexOf('i'))); // This is a str
  console.log(myString.slice(0, -5)); // This is a s
  // These methods create new string objects behind the scenes
  // Change case
  console.log(myString.toLowerCase()); // this is a string
  console.log(myString.toUpperCase()); // THIS IS A STRING
  let badName = 'MaLoLe';
  badName = badName[0].toUpperCase() + badName.slice(1).toLowerCase();
  console.log(badName); // Malole
  const email = 'prompt@devs2rios.io';
  let badEmail = ' promPt@devS2rIos.iO \n';
  badEmail = badEmail.toLowerCase().trim(); // Trim clears trailing whitespaces
  console.log(email === badEmail); // true
  const priceE = '3049,91€';
  const priceA = priceE.replace('€', '$').replace(',', '.');
  console.log(priceE, priceA); // 3049,91€ 3049.91$
  // Replacing all by using regex with the global flag
  const lol = 'ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha';
  const notSoLol = lol.replace(/ha\s/g, '');
  console.log(notSoLol); // ha
  // Methods that return booleans
  console.log(myString.includes('i')); // true
  console.log(myString.includes('x')); // false
  console.log(myString.startsWith('T')); // true
  console.log(myString.startsWith('t')); // false
  console.log(myString.endsWith('g')); // true
  console.log(myString.endsWith('G')); // false
  // If you look for a word regardless the case you can transform everything to lowercase befor searching

  // Transforming strings to arrays
  const myFood = 'Banana, Potato, Cucumber'.replace(/,/g, '').split(' ');
  console.log(myFood);
  // [ 'Banana', 'Potato', 'Cucumber' ]
  console.log(myFood.join(' * '));
  // Banana * Potato * Cucumber
  const [firstName, lastname] = 'Bob Alice'.split(' ');
  console.log(firstName, lastname); // Bob Alice

  // Capitalize first letter of every word
  const titleCase = str => {
    return str.replace(
      /([a-zA-Z]+)/g,
      word => word[0].toUpperCase() + word.slice(1).toLowerCase()
    );
  };
  console.log(titleCase('lksjdkd lajkdj kaks')); // Lksjdkd Lajkdj Kaks
  console.log('12'.padStart(4, '0')); // 0012
  console.log('12'.padEnd(4, '0')); // 1200
  console.log('12'.padStart(6, '0').padEnd(12, '0')); // 000012000000
  const maskPassword = str => str.slice(0, -4).replace(/./g, '*') + str.slice(-4);
  console.log(maskPassword('467')); // 467
  console.log(maskPassword('1234')); // 1234
  console.log(maskPassword('93u58')); // *3u58
  console.log(maskPassword('09032u4029039849nsdjk900'));
  // ********************k900
  console.log(maskPassword('pdncsojñxapkokpoawoijcnncdioe'));
  // *************************dioe
  console.log('Eat, Sleep, Rave, Repeat\n'.repeat(4).trim());
  /*
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  */
  ```

</details>

<details>
<summary><strong>A Closer Look at Functions</strong></summary>

- Default parameters

  ```JavaScript
  const myObjs = [];

  const muFunc = function (param1, param2 = 2, param3 = 3) {
    const myObj = { param1, param2, param3 };
    console.log(myObj);
    myObjs.push(myObj);
  };

  muFunc(1); // { param1: 1, param2: 2, param3: 3 }
  muFunc(1, 3); // { param1: 1, param2: 3, param3: 3 }
  muFunc(1, undefined, 1); // { param1: 1, param2: 2, param3: 1 }
  ```

- How Passing Arguments Works: Value vs. Reference

  - Objects: will be changed because they are referenced
  - Primitives: won't change because the arguments passes are copies of the values

  ```JavaScript
  const post = 'S0018';

  const don = {
    username: 'Dom',
    id: 1230487267,
  };

  const login = function (postNum, user) {
    postNum = 'F0384';
    user.username = `Mr. ${user.username}`;
    if (user.id === 1230487267) {
      console.log('Logged in!');
    } else {
      console.log('Wrong id');
    }
  };

  login(post, don); // Logged in!
  console.log(post); // S0018 didn't change
  console.log(don.username); // Mr. Dom changed

  // This is what's happening inside the function
  const postNum = post; // a copy of post in another variable
  const user = don; // this uses the same reference as don

  const newid = function (person) {
    person.id = Math.round(Math.random() * 9999999999);
  };

  newid(user); // using user instead dom because we want this id to change
  console.log(don); // { username: 'Mr. Dom', id: 7768518925 }
  console.log(user); // { username: 'Mr. Dom', id: 7768518925 }
  login(post, user); // Wrong id because don and user changed id because of the object reference
  ```

- First-Class and Higher-Order Functions

  - First-Class functions

    - Values are treated as values
    - They are another type of object
    - They can be saved as a variable value
    - We can use functions as arguments for other functions
    - They can be returned from other functions
    - They can call methods

  - High-Order functions (HOf)
    - They are functions that receive another function as argument or return another function
    - HOf are possible because of First-Class functions

- Functions Accepting Callback Functions

  - Callbacks allow to add abstraction

  ```JavaScript
  const oneWord = function (str) {
    return str.replace(/ /g, '').toLowerCase();
  };
  const upperFirstWord = function (str) {
    const [first, ...others] = str.split(' ');
    return [first.toUpperCase(), ...others].join(' ');
  };

  const transformer = function (str, fn) {
    console.log(`Original string: ${str}`);
    console.log(`Transformed string: ${fn(str)}`);
    console.log(`Transformed by: ${fn.name}`);
  };

  transformer('JavaScript is good!', upperFirstWord);
  /*
  Original string: JavaScript is good!
  Transformed string: JAVASCRIPT is good!
  Transformed by: upperFirstWord
  */
  transformer('JavaScript is good!', oneWord);
  /*
  Original string: JavaScript is good!
  Transformed string: javascriptisgood!
  Transformed by: oneWord
  */
  const happiness = function (repeats) {
    console.log('😬'.repeat(repeats));
  };

  [3, 4, 12, 1].forEach(happiness); // Happiness as callback
  /*
  😬😬😬
  😬😬😬😬
  😬😬😬😬😬😬😬😬😬😬😬😬
  😬
  */

  ```

- Function Returning Functions

  ```JavaScript
  const func = function (param1) {
    return function (param2) {
      console.log(`${param1} ${param2}`);
    };
  };
  const funcArrow = param1 => param2 => console.log(`${param1} ${param2}`);

  func('Hey')('you!'); // Hey you!
  funcArrow('Hey')('you!'); // Hey you!
  ```

- The call and apply Methods

  ```JavaScript
  const funcsObj = {
    range: 1000,
    ranNum(player) {
      return `${player}: ${Math.floor(Math.random() * this.range) + 1}`;
    },
  };

  console.log(funcsObj.ranNum('test')); // test: 22

  // If you want to use ranNum as a method for any object
  // you'll need to use .call() or .apply() so it won't point to undefined
  const ranNum = funcsObj.ranNum;
  const ran10 = { range: 10 };
  const ran100 = { range: 100 };
  console.log(ranNum.call(ran10, 'chuy')); // chuy: 8
  console.log(ranNum.call(ran100, 'glass')); // glass: 71
  // .apply needs an array as argument to do the same thing as call
  const dorothy = ['dorothy'];
  console.log(ranNum.apply(ran100, dorothy)); // dorothy: 69
  // Nevertheless it's easier with spread operator
  console.log(ranNum.call(ran100, ...dorothy)); // dorothy: 96
  ```

- The bind Method

  - Bind returns a new function where the keyword is bound

  ```JavaScript
  const funcsObj = {
    range: 1000,
    ranNum(player) {
      return `${player}: ${Math.floor(Math.random() * this.range) + 1}`;
    },
  };

  console.log(funcsObj.ranNum('test')); // test: 649

  // funcsObj.ranNum bound to { range: 5 } into ranNum5
  const ranNum5 = funcsObj.ranNum.bind({ range: 5 });
  // Calling ranNum5 with the player's name
  console.log(ranNum5('clark')); // clark: 3
  // Binding it to different ranNums
  const ranNum10 = funcsObj.ranNum.bind({ range: 10 });
  const ranNum20 = funcsObj.ranNum.bind({ range: 20 });
  const ranNum30 = funcsObj.ranNum.bind({ range: 30 });
  const ranNum40 = funcsObj.ranNum.bind({ range: 40 });
  // You can bound arguments to the .bind function
  const ranNum50 = funcsObj.ranNum.bind({ range: 50 }, 'fifty');
  console.log(ranNum50()); // fifty: 30
  // Let's create a lottery game
  const tickets = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; // Tickets to sold
  const letters = [...'ABCDEFGHIJKLMNOPQRSTUVWXYZ']; // Letters to create names
  const playerNames = []; // Players' array
  // Populate array
  for (let player = 0; player < tickets.length; player++) {
    let playerName = '';
    for (let i = 0; i < 3; i++) {
      playerName += letters[Math.floor(Math.random() * letters.length)];
    }
    playerNames.push(playerName);
  }
  // Lottery object
  const lottery = {
    playerNames,
    tickets,
    playersTickets: {},
    buyTickets() {
      for (const p of this.playerNames) {
        // Arrow function because we need to use this. inside
        const getNameNumIndex = entry => {
          const pName = entry.replace(/: \d+/, ''),
            pNum = Number(entry.replace(/[A-Z]{3}: /, '')),
            pIndex = this.tickets.indexOf(pNum);
          return [pName, pNum, pIndex];
        };
        // Preset variables before the game
        let ticketAvailable = false;
        let pName, pNum, pIndex;
        while (!ticketAvailable) {
          // Using the bound function
          [pName, pNum, pIndex] = getNameNumIndex(ranNum10(p));
          if (pIndex !== -1) {
            // If the ticket exists assign it to the current player (p)
            ticketAvailable = true;
          }
        }
        // Fill the entry in the playersTickets object
        this.playersTickets[pName] = pNum;
        // Delete the ticket from the tickets array
        this.tickets.splice(pIndex, 1);
      }
      // Change the tickets array for a sold out string
      this.tickets = 'Sold Out!';
    },
  };
  lottery.buyTickets();
  console.log(lottery);
  /*
  {
    playerNames: [
      'PNY', 'MOC', 'KJZ',
      'JHI', 'KYZ', 'CQV',
      'ROD', 'SLJ', 'BQM',
      'NGS'
    ],
    tickets: 'Sold Out!',
    playersTickets: {
      PNY: 8,
      MOC: 9,
      KJZ: 6,
      JHI: 1,
      KYZ: 3,
      CQV: 7,
      ROD: 5,
      SLJ: 4,
      BQM: 10,
      NGS: 2
    },
    buyTickets: [Function: buyTickets]
  }
  */

  // Partial binding
  const addTax = (rate, value) => value + value * rate;
  console.log(addTax(0.3, 100)); // 130
  // Bounding without one argument,
  // null goes for the this keyword and .16 for the first argument
  const mxVAT = addTax.bind(null, 0.16);
  // mxVAT = value => value + value + 0.16
  console.log(mxVAT(100)); // 116

  // Function returning function
  const mxVAT2 = value => rate => value + value * rate;
  console.log(mxVAT2(100)(0.25)); // 125
  ```

- Immediately Invoked Function Expressions (IIFE)

  - They're good for private outputs or variables that don't require to be mutated, nevertheless, they're like block scope so in modern JavaScript is not useful

  ```JavaScript
  (function () {
    console.log('Just once!'); // Just once!
    (() => console.log('Just once!'))(); // Just once!
  })();
  ```

- Closures

  - They're the closed-over variable environment of the execution in which a function was created, even after that execution context is gone
  - We can't create them manually, it happens automatically
  - We can't access to them because they're not a tangible Js object
  - The variables inside the closure have priority over the scope chain

  ```JavaScript
  const closureFunc = function () {
    let counter = 0;
    return function () {
      counter++;
      console.log(`Current Number: ${counter}`);
    };
  };

  // The function inside the variable creates an execution context
  // that remembers the variables inside the function
  const outsideCounter = closureFunc();
  outsideCounter(); // Current Number: 1
  outsideCounter(); // Current Number: 2
  outsideCounter(); // Current Number: 3
  console.dir(outsideCounter);
  /*
  [Function (anonymous)]
      [[Scopes]]: Scopes[3]
          0: Closure (closureFunc)
              counter: 3
  You cannot access to [[Scopes]] in your code
  */
  ```

- More Closure Examples

  ```JavaScript
  let f = 10;

  const g = function () {
    const a = 19;
    f = function () {
      console.log(a * f);
    };
  };
  const h = function () {
    const b = 30;
    f = function () {
      console.log(b * 4);
    };
  };

  g();
  f();
  console.dir(f);
  /*
  Closure created when g is used
  [[Scopes]]: Scopes[3]
      0: Closure (g)
          a: 19
  */

  // Re-assign f function
  h();
  f();
  console.dir(f);
  /*
  Closure replaced when h is used
  [[Scopes]]: Scopes[3]
      0: Closure (h)
          b: 30
  */
  const row = 250;
  const timedGrid = function (grid, newLineTime) {
    const row = grid / 5;
    setTimeout(function () {
      console.log(`Grid: ${grid}`);
      console.log(`Row: ${row}`);
    }, newLineTime * 1000);
    console.log(`New Line Time: ${newLineTime}`);
  };
  timedGrid(200, 2);
  /*
  New Line Time: 2
  Grid: 200
  Row: 40 -> From closure
  */
  const timedGrid2 = function (grid, newLineTime) {
    // This doesn't have const row
    setTimeout(function () {
      console.log(`Grid: ${grid}`);
      console.log(`Row: ${row}`);
    }, newLineTime * 1000);
    console.log(`New Line Time: ${newLineTime}`);
  };
  timedGrid2(200, 2);
  /*
  New Line Time: 2
  Grid: 200
  Row: 250 -> From global scope
  */
  ```

</details>
