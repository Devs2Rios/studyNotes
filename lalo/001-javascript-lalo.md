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
    - Nested loop are sometimes usefull, like when you want all the 10 units square coordinates inside a 100\*100 square
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
      - Usefull console methods for debugging:
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

</details>
