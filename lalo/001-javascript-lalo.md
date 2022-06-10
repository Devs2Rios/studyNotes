# Java Script Notes

### JavaScript Fundamentals

<details>
<summary><b>Intro</b></summary>
<br/>

- Test with Console
    - Brave or Chrome - `⌘⌥J`
    - Safari - `⌘⌥C`
- JavaScript
    - High-Level - Not complex stuff (memory) worries
    - Object-Oriented - Data based on objects
    - Multi-Paradigm - Use different styles of programming
    - Programming language - Instruct computer to do things
- Web development basics
    - HTML(Nouns) | CSS(Adjectives) | JS(Verbs)
    - Separation of concerns - Every file separated, not in the HTML

</details>

<details>
<summary><b>JavaScript</b></summary>
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
        - Check what kind of value you have `typeof`
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

</details>

- Switch:
    - `switch(variable){case logic: exec;}`
    - `break;` if you want to break at that step
    - `case logic: case logic: exec;` several cases or
    - `default` like an else statement