# Java Script Notes

### JavaScript Fundamentals

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
- Values are objects or primitives
    - Objects
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
            - `Boolean(0) // false`
            - `Boolean(1) // true`
- Comments
    - `// Single line`
    - `/* Multiline */`
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
    - `"String"` `'String'` `` `String` ``
    - Concatenate `'Hi ' + 'dear!'`
    - Template literals `` `I am ${jsValue} years old` ``
- Conditionals:
    - Positive `if (condition) {execution}`
    - Negative `if (!condition) {execution}`
    - Multiple `if (c) {e1} else if (c2) {e2} else {e3}`
- Expressions: poduce a value
    -  `true && false`
- Statements: sentences that translate our order
    - `const str = 'Sentence'`
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
- Switch:
    - It's an statement so it can`t be inside a function or return
    - `switch(variable){case logic: exec;}`
    - `break;` if you want to break at that step
    - `case logic: case logic: exec;` several cases or
    - `default` like an else statement
- Ternary:
    - It's a expression so it can be inside a function or return
    - `5 ? It's five : 'It's not five'`

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
            - You can also use this reserved word to create an anonymous function (function expression):
                - `const anonymous = function(params) {action}`
        - Arrow functions
            - It doesn't have the `this` keword
            - `parameter => action`
                - it returns explicitally without `return`
            - If it gets complex it needs more structure
                - `const myFunction = (multiple, params) => {multipleLineAction needs return}`
    - Call / run / invoke functions
        - `myFunction(argument);`
        - The parameter is the name used to define the function variables and the argument the actual value used when calling the function
    - `return` returns a value at the end of the function
        - Just the first `return` achieved returns a value
        - Just works inside functions
        - If the function doesn't have a `return` it returns `undefined`
        - If you want to return a list use brackets `[]` if not it will return just the last value
            - `return true, false //false`
            - `return [true, false] //[true, false]`
    - You can use functions inside other functions so you can write cleaner code
        ``` JavaScript
        function func1() {return true};
        function func2() {
            const myTrue = func1();
            return [myTrue, false];
        }
        ```

</details>