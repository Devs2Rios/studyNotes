# Events

-   Node relies heavily in events, they actually happened all the time and the order in which they are executed matter, like when an user makes a request to a certain URL

    ```JS
    const EventEmitter = require('events');

    const customEmitter = new EventEmitter();

    // The order in which events are emitted matters

    customEmitter.on('response', data => {
        console.log(`Data received: ${data.name}`);
    });
    customEmitter.emit('response', { name: 'Korn' });
    // Data received: Korn

    customEmitter.on('response', data => {
        console.log(`Data received again: ${data.name}`);
    });
    customEmitter.emit('response', { name: 'The Doors' });
    /*
    Data received: The Doors
    Data received again: The Doors
    */
    ```

## Streams

-   Streams are very useful for instances when an operation will take a lot of time

    -   Like reading a big file

        ```JS
        const { createReadStream } = require('fs');

        const stream = createReadStream('./content/obsessed/eat-sleep-rave-repeat.txt');

        stream.on('data', result => console.log(result));
        ```

    -   Or sending a big response

        ```JS
        const http = require('http');
        const { createReadStream } = require('fs');
        const PORT = 3000;

        const server = http.createServer((req, res) => {
            if (req.url === '/') {
                const fileStream = createReadStream(
                    './content/obsessed/eat-sleep-rave-repeat.txt',
                    'utf-8'
                );
                // Pipe transfers data from one stream to another
                // in this case from the fileStream to the response
                fileStream.on('open', () => fileStream.pipe(res));
                fileStream.on('error', err => res.end(err));
            }
        }
        server.listen(PORT, () => console.log(`Listening on port ${PORT}`));
        ```
