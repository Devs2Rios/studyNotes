# Node.js Event Loop

-   The event loop allows Node.js to perform non-blocking I/O operations - despite the fact that JavaScript is single-threaded (reads the code line by line) - by offloading operations to the system kernel (component that manages system resources, provides services to applications, enable communication between software and hardware) whenever possible

    -   Timeout example
        ```JS
        console.log('First');
        setTimeout(() => console.log('Second'), 0);
        console.log('Third');
        ```
        ```BASH
        First
        Third
        Second
        ```
    -   Async reading file example

        ```JS
        const { readFile } = require('fs');

        console.log('Started reading here:');
        readFile('./content/jokes/monkey.txt', 'utf-8', (err, result) => {
            if (err) {
                console.log(err);
                return;
            }
            console.log('--------------------------------------------');
            console.log(result);
            console.log('--------------------------------------------');
            console.log('Finished reading here during the event loop');
        });

        console.log('I was supposed to be at the end :(');
        ```

        ```BASH
        Started reading here:
        I was supposed to be at the end :(
        --------------------------------------------
        A monkey was drinking milk,
        a cat comes really angry and says
        "That's miau milk"
        The monkey responds
        "Was yihayihayihour milk"
        --------------------------------------------
        Finished reading here during the event loop
        ```

    -   Another interesting thing about the event loop is that it will run async functions like `setInterval()` until they are terminated

        ```JS
        // Prints 'Eat, Sleep, Rave, Repeat' every second
        setInterval(() => console.log('Eat, Sleep, Rave, Repeat'), 1000);
        ```

        ```BASH
        Eat, Sleep, Rave, Repeat
        Eat, Sleep, Rave, Repeat
        Eat, Sleep, Rave, Repeat
        ...
        ```

-   The event loop reads the code line by line but when an element is intended to be executed in the background, it just fires up the event, and eventually whent it's done the result comes back to our compiled code
-   Be aware of code that might be blocking your server like loops
    ```JS
    const http = require('http');
    const PORT = 3000;
    const server = http.createServer((req, res) => {
        if (req.url === '/') {
            res.end('Welcome home!');
        } else if (req.url === '/user') {
            res.end('Welcome user!');
            // This will block the whole server until it ends
            for (let i = 0; i < 1000000; i++) console.log(i);
        } else {
            res.end('404 error');
        }
    });
    server.listen(PORT, () => console.log(`Listening on port ${PORT}`));
    ```
-   A good way to manage this kind of situations is by convert these methods in promises

    ```JS
    const promiseLoop = range => {
        return new Promise((resolve, reject) => {
            try {
                const rangeArr = [];
                for (let i = 0; i < range; i++) rangeArr.push(i);
                resolve(rangeArr);
            } catch (err) {
                reject(err);
            }
        });
    };

    module.exports = { promiseLoop };
    ```

    ```JS
    const http = require('http');
    const { promiseLoop } = require('./loop-promise');
    const PORT = 3000;
    const server = http.createServer((req, res) => {
        if (req.url === '/') {
            res.end('Welcome home!');
        } else if (req.url === '/user') {
            res.end('Welcome user!');
            // Now our loop runs on the event loop and prints our numbers in an array
            promiseLoop(100000)
                .then(result => console.log(result))
                .catch(err => console.log(err));
        } else {
            res.end('404 error');
        }
    });
    server.listen(PORT, () => console.log(`Listening on port ${PORT}`));
    ```

-   We can also handle this logic with `async` and `await`

    ```JS
    const http = require('http');
    const { promiseLoop } = require('./loop-promise');
    const PORT = 3000;

    // Complex loop
    const multiLoop = async () => {
        try {
            const loop1 = await promiseLoop(1_000_000);
            const loop2 = await promiseLoop(500_000);
            console.log([...loop1, ...loop2]);
        } catch (err) {
            console.log(err);
        }
    };

    const server = http.createServer((req, res) => {
        if (req.url === '/') {
            res.end('Welcome home!');
        } else if (req.url === '/user') {
            res.end('Welcome user!');
            // Async
            multiLoop();
        } else {
            res.end('404 error');
        }
    });
    server.listen(PORT, () => console.log(`Listening on port ${PORT}`));
    ```

-   Node have also buit-in utilities to manage the promises with the async approach

    -   `util`

        ```JS
        const util = require('util');

        const loop = range => {
            const rangeArr = [];
            for (let i = 0; i < range; i++) rangeArr.push(i);
            console.log(rangeArr);
        };

        // Makes it a promise function
        const promiseLoop = util.promisify(loop);

        module.exports = { promiseLoop };
        ```

    -   Built-in promises

        ```JS
        // You can extract the methods promisified this way
        const { readFile, writeFile } = require('fs').promises;
        const path = require('path');

        const tips = './content/tips';
        const tip1 = path.join(tips, 'tip-one.txt');
        const twoTips = async tip2 => {
            try {
                const first = await readFile(tip1, 'utf-8');
                const second = `${first}\n${tip2}`;
                await writeFile(path.join(tips, 'tip-two.txt'), second);
            } catch (err) {
                console.log(err);
            }
        };

        module.exports = { twoTips };
        ```
