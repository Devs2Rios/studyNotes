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

    -   Node Package Manager manages dependencies (external libraries) in our project
    -   It handles the package and versions
    -   It comes with [node](https://nodejs.org/en) and you can check if you've installed it by using `npm -v`
    -   Starting a node project (creating the configuration file `package.json`)

        ```SHELL
        $ mkdir test
        $ cd test
        $ npm init
        It only covers the most common items, and tries to guess sensible defaults.

        See `npm help init` for definitive documentation on these fields
        and exactly what they do.

        Use `npm install <pkg>` afterwards to install a package and
        save it as a dependency in the package.json file.

        Press ^C at any time to quit.
        package name: (test)
        version: (1.0.0)
        description:
        entry point: (index.js)
        test command:
        git repository:
        keywords:
        author:
        license: (ISC)
        About to write to /Users/eat/Desktop/test/package.json:

        {
            "name": "test",
            "version": "1.0.0",
            "description": "",
            "main": "index.js",
            "scripts": {
                "test": "echo \"Error: no test specified\" && exit 1"
            },
            "author": "",
            "license": "ISC"
        }


        Is this OK? (yes)
        ```

        -   You'll need to fill the project fields, alternatively you can type `npm init -y` to get the default configuration:

            ```SHELL
            $ npm init -y
            Wrote to /Users/user/path/test/package.json:

            {
                "name": "test",
                "version": "1.0.0",
                "description": "",
                "main": "index.js",
                "scripts": {
                    "test": "echo \"Error: no test specified\" && exit 1"
                },
                "keywords": [],
                "author": "",
                "license": "ISC"
            }
            ```

    -   To install a package you'll now just need to write `npm install <package-name>` or `npm i <package-name>`

        -   This creates the `node_modules` directory that holds all the dependencies and the `package-lock.json` file which holds the exact dependency tree
            -   `node_modules` should never be included in version control software, instead we use `package.json` to install the dependencies in different computers by using `npm install`

    -   Bundling with [`Parcel`](https://parceljs.org/)

        -   Build tool installed also via `npm` with `npm install parcel --save-dev` (it's important to install it as dev dependency since it's not required on production)
        -   We can use it with `npx` (node package execute) or with a script specified in the `package.json` file

            -   Example

                ```JS
                // index.js
                import { cloneDeep } from 'lodash-es'; // package already installed via NPM

                const user = {
                    name: 'Tom',
                    age: 20,
                    friends: [
                        {
                            name: 'Bob',
                            age: 20,
                        },
                    ],
                };

                const user2 = cloneDeep(user);
                user2.name = 'Bob';

                console.log(user);
                console.log(user2);

                // Allows watching file changes and keeping our state
                if (module.hot) module.hot.accept();
                ```

                ```SHELL
                $ npx parcel index.js
                Server running at http://localhost:1234
                ✨ Built in 2.04s
                # This creates a folder with our build, in this case dist/index.js (a file that )
                # This file is now executable with node or our browser (no need to use <script type="module">)
                $ node dist/index.js
                { name: 'Tom', age: 20, friends: [ { name: 'Bob', age: 20 } ] }
                { name: 'Bob', age: 20, friends: [ { name: 'Bob', age: 20 } ] }
                ```

        -   Using `npm script`

            ```JS
            {
                "name": "test",
                "version": "1.0.0",
                "description": "",
                "scripts": {
                    "start": "parcel index.js",
                    "build": "parcel build index.js"
                },
                "keywords": [],
                "author": "",
                "license": "ISC",
                "dependencies": {
                    "lodash-es": "^4.17.21"
                },
                "devDependencies": {
                    "parcel": "^2.9.3"
                }
            }
            ```

            -   Now we can replicate the behavior from above by using `npm start` or build our distribution bundle with `npm run build`
