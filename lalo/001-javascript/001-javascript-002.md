# JavaScript2

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
