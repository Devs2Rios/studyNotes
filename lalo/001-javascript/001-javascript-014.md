# Modern JavaScript Development: Modules, Tooling, and Functional

-   Modern JavaScript keep code in modules (npm [node package manager])
    -   The project is built into a JavaScript bundle ready to be deployed (usually with tools like webpack or parcel)
        -   Bundling: Join all bundles in one file
        -   Transpiling/Polyfilling: Converts modern JS into ES5

## Modules

-   Reusable encapsulated pieces of code

    ```JS
    // Gets the useState function from the react module/library
    import { useState } from 'react'; // Hoisting (moving all imports at the top of the file) is needed in JavaScript

    const App = () => {
        // We now can use the useState function in our code
        const [count, setCount] = useState(0);
        return <p onClick={() => setCount(prevCount => count++)}>{count}</p>
    }

    // We can export logic from this file and it can be used as a module in other files
    export default App;
    ```

    -   Great for complex applications
    -   We can isolate blocks of code (components)
    -   It's amazing for code abstraction
    -   Makes our apps more organized
    -   Allows us to easily reuse our code

-   Native in ES6

    -   Every file is a module

        -   Functions and variables scoped to the file
        -   Run in strict mode by default
        -   It doesn't have a top level `this` like `window` in scripts
        -   Allows imports and exports
            -   Imports are always synchronous
            -   This is what allows bundling and dead code elimination
        -   If using them with html we need to specify it's a module`<script type="module"></script>`
            -   It's always asynchronous, no optional `defer` or `async`
        -   When using modules in node we need to use the `.mjs` extension

            ```JS
            // utils.mjs
            export const add = (a, b) => a + b;
            ```

            ```JS
            // index.mjs
            import { add } from './utils.mjs';
            console.log(add(1, 2));
            ```

            ```SHELL
            node index.mjs
            3
            ```

        -   Exports and imports

            ```JS
            // a.mjs
            export const a = 1;
            ```

            ```JS
            // b.mjs
            const b1 = 2;
            const b2 = 3
            export {b1, b2}
            ```

            ```JS
            // c.mjs
            const c = 4;
            export default c; // common when we only want to import one thing
            ```

            ```JS
            // index.mjs
            // Deconstructs the module
            import { a } from './a.mjs';
            import { b1, b2 } from './b.mjs';
            // Exports an object and renames it
            import * as b from './b.mjs';
            // Default export (no parenthesis), can be renamed
            import c from './c.mjs';
            import d from './c.mjs';

            console.log(a); // 1
            console.log(b1, b2); // 2 3
            console.log(b); // [Module: null prototype] { b1: 2, b2: 3 }
            console.log(b.b1, b.b2); // 2 3
            console.log(c); // 4
            console.log(d); // 4
            ```

    -   Keep in mind that references keep their place in memory and are not cloned when they're exported
        ```JS
        // ref.mjs
        export const arr = [];
        export const addNum = num => arr.push(num);
        ```
        ```JS
        // index.mjs
        import { arr, addNum } from './ref.mjs';
        addNum(1);
        addNum(2);
        addNum(3);
        addNum(4);
        addNum(5);
        console.log(arr); // [ 1, 2, 3, 4, 5 ]
        ```

-   In ES2022 whe have a built-in `top-Level await`

    ```JS
    // index.js
    // No need of using an async function
    const res = await fetch('https://jsonplaceholder.typicode.com/todos/1');
    const data = await res.json();
    console.log(data);
    // { userId: 1, id: 1, title: 'delectus aut autem', completed: false }
    ```

    -   Be careful since the async calls block the whole script, especially when importing async resolved responses

        ```JS
        import { data } from './async.mjs';

        console.log('Execution started');
        const startTime = new Date();
        console.log(data);
        const endTime = new Date();
        console.log('Execution finished');
        const executionTime = endTime - startTime;
        console.log(`Execution time: ${executionTime} milliseconds`);
        ```

        ```SHELL
        node index.mjs
        Execution started
        { userId: 1, id: 1, title: 'delectus aut autem', completed: false }
        Execution finished
        Execution time: 1 milliseconds
        ```

-   The module pattern

    ```JS
    // index.mjs
    const myModule = (() => {
        // What we don't want to expose to the outside world
        const privateVariable = 'Hello World';
        const privateMethod = () => {
            console.log(privateVariable);
            return privateVariable;
        };
        // What we want to expose to the outside world
        return {
            publicVariable: privateMethod() + '!!!',
            publicMethod: () => {
                console.log(privateVariable);
                return privateVariable;
            },
        };
    })();

    console.log(myModule.publicVariable);
    /*
    Hello World
    Hello World!!!
    */
    console.log(myModule.publicMethod());
    /*
    Hello World
    Hello World
    */
    console.log(myModule.privateVariable); // undefined
    console.log(myModule.privateMethod); // undefined
    ```

-   CommonJS Modules

    ```JS
    // utils.js
    const add = (a, b) => a + b;
    module.exports = { add }; // There are several ways to export
    ```

    ```JS
    // index.js
    const { add } = require('./utils');
    console.log(add(4, 5));
    ```

    ```SHELL
    node index
    9
    ```

    -   This was the original approach intended for `node.js`

-   `NPM`
