# JavaScript1

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
