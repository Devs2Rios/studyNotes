# Node.js intro

## [Node](https://nodejs.org/en)

-   Engine that compiles our code
-   Compile programs:

    -   You can run them with the command line `node index` (you can either use `.js` or not)
    -   Or start a Repl with `node`

        -   Which will run an environmet to compile instruction directly in the CLI

            ```BASH
            $ ~ > node
            Welcome to Node.js v16.17.0.
            Type ".help" for more information.
            ```

-   Global objects

    -   `__dirname` - Current working directory
    -   `__filename` - File name
    -   `require` - function to use modules
    -   `module` - info about current module (file)
    -   `process` - info about env where the program is executed
    -   [Many others](https://nodejs.org/api/globals.html)

-   Modules

    -   Every file in node is a module

        ```JS
        // ./utils
        const isEven = num => num % 2 === 0;
        module.exports = { isEven };
        ```

        ```JS
        // Import ./utils to ./index.js
        const { isEven } = require('./utils');
        console.log(isEven(2)); // true
        console.log(isEven(1)); // false
        ```

    -   There are several other ways to export modules

        ```JS
        module.exports.isEven = num => num % 2 === 0;
        ```

        ```JS
        const isEven = num => num % 2 === 0;
        module.exports.evenFunction = isEven;
        ```

    -   If a function is invoked in a file it can be called with `require`

        ```JS
        // ./count-to-three.js
        const countToThree = () => Array.from(
            { length: 3 },
            (_, i) => i + 1).forEach(n => console.log(n)
        );
        countToThree();
        ```

        ```JS
        // ./index.js
        require('./count-to-three');
        /*
        1
        2
        3
        */
        ```

    -   Built-in Modules

        -   Don't require relative path `'./'`
        -   Important modules
            -   `OS`
            -   `PATH`
            -   `FS`
            -   `HTTP`
            -   [Many more](https://www.w3schools.com/nodejs/ref_modules.asp)
        -   OS module

            ```JS
            const os = require('os');
            // Get user info
            console.log(os.homedir());
            console.log(os.userInfo());
            // OS Data
            console.log('OS type', os.type());
            console.log('Total memory', os.totalmem());
            console.log('Free memory', os.freemem());
            ```

        -   PATH module

            ```JS
            const path = require('path');
            console.log(path.sep); // /
            const logo = path.join('/content', 'images', 'logo.svg');
            console.log(logo); // /content/images/logo.svg
            console.log(path.basename(logo)); // logo.svg
            console.log(path.resolve(__dirname)); // Absolute path to the current directory
            ```

        -   FS module
            ```JS
            // Reading a poem from
            const { readFileSync } = require('fs');
            const path = require('path');
            const poem = path.join('./content/poems', 'poem.txt');
            const poemcontent = readFileSync(poem, 'utf-8');
            console.log(poemcontent);
            /*
            I love flowers
            and if I require
            I'll read their leaves
            with node.js
            */
            // Create a new file
            const newPoem = path.join('./content/poems', 'new-poem.txt');
            writeFileSync(newPoem, "No idea\nno heart\nI believe\nI'm a fullstack\n", {
                flag: 'a', // append if exists
            });
            ```
