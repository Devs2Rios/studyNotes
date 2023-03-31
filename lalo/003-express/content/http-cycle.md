# HTTP Request/Response Cycle

-   Client sends a HTTP request to the server that has the resources and the server send you back a HTTP response with the data you asked for

    -   In node you’ll always have them when starting a server

        ```JS
        const http = require('http');

        const PORT = 3000;
        const server = http.createServer((req, res) => {
            // Always needed, without end the page never loads
            res.end('Welcome!');
        });

        server.listen(PORT, () => console.log(`Listening on port ${PORT}...`));
        ```

-   Servers are computers that make sure that the resource is available
-   The cloud has a lot of these computers connected
-   Structure of the cycle
    -   Request
        -   Message
            -   `Method` - GET (read), POST (create), PUT (update), DELETE (delete)
                -   Get is the default request
            -   `URL` - The path where our request is going
            -   `status` - Code that indicates the output of our request
            -   `Referrer Policy` - Like cross origin setup
            -   `Remote Address` - IP address of the client making the request
            -   `HTTP version` - http/1.1 almost always
        -   `Headers` - Key pair values with information about our request
        -   `Body` - An object with data that is going to be used by the request
    -   Response
        -   Message
            -   `URL` - URL where the response comes from
            -   `Method` - GET (read), POST (create), PUT (update), DELETE (delete)
            -   `status` - Code that indicates the output of our response
            -   `Referrer Policy` - Like cross origin setup
            -   `Remote Address` - IP address of the client sending the response
            -   `HTTP version` - http/1.1 almost always
        -   `Headers` - Key pair values with information about our response
            -   `Content-Type` - Indicates the type of data delivered, like `application/json`
        -   `Body` - An object with data delivered by the response (also called payload)
-   HTTP server elements

    -   [PORT](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)
        -   Communication endpoint that allows the server listen incomming connections
        -   A number between 0 and 65535
        -   Some numbers are assigned to specific services or protocols like port 22 use for SSH
        -   The client specifies the IP and port number (remote address) to make the request
        -   The server sends the data requested
        -   3000, 5000, 8000 commonly use for local development
    -   [Status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
        1. Informational responses (100 – 199)
        2. Successful responses (200 – 299)
        3. Redirection messages (300 – 399)
        4. Client error responses (400 – 499)
        5. Server error responses (500 – 599)
    -   [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
        -   These specify what are you sending back
    -   Example

        ```JS
        const http = require('http');
        const { readFileSync } = require('fs');
        const homePage = readFileSync('./index.html', 'utf-8');
        const aboutPage = readFileSync('./about.html', 'utf-8');
        const notFoundPage = readFileSync('./not-found.html', 'utf-8');

        const PORT = 3000;
        const server = http.createServer((req, res) => {
            const url = req.url;
            // Sending status and headers depending on the URL
            if (url === '/') {
                res.writeHead(200, { 'content-type': 'text/html' });
                res.write(homePage);
            } else if (url === '/about') {
                res.writeHead(200, { 'content-type': 'text/html' });
                res.write(aboutPage);
            } else {
                res.writeHead(404, { 'content-type': 'text/html' });
                res.write(notFoundPage);
            }
            // Always needed, without end the page never loads
            res.end();
        });

        server.listen(PORT, () => console.log(`Listening on port ${PORT}...`));
        ```

-   Serving this files will become tedious fast with this approach, that’s why libraries with abstraction like express.js are more useful
