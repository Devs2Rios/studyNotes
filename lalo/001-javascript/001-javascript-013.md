# Asynchronous JavaScript: Promises, Async/Await, and AJAX

## Intro

-   Synchronous code is executed line by line in sequence and asynchronous code is executed in the background while the rest of the code runs normally, like `setTimeout()` and some events like `load`
-   `AJAX` is asynchronous `JavaScript` and `XML` that allows us to communicate with web servers
    -   Most APIs don't use `XML` now a day but the name is still being used the same
    -   The most common API format is now `JSON`
-   `API` is an Application Programming Interface (software that can be used by other software)
    -   `Online APIs` - Apps running on a server and sending responses to other apps
    -   `Web API` - Our own APIs handled on backend code
-   How the internet works:

    -   You send a request to the server and the server sends back a response (client server architecture)
    -   It's all made by a dns (domain name service) which converts a domain into it's IP address

        -   `Protocol` + `IPAddres` + `Port number (https=443 / http=80)`

            ```SHELL
            http://104.27.142.889:443
            ```

        -   If the domain is valid it creates a TCP/IP socket connection with the server

            -   Transition Control Protocol and Internet Protocol
            -   These protocols define how he data travels across the web
            -   The request usually has a start line and the headers

                ```SHELL
                # Method + request target + HTTP Version
                GET /rest/v1/students/1 HTTP/1.1
                # Request headers are different depending on the request
                Host: www.test.xyz
                ...
                # Body if required
                ```

            -   If the request is accepted the server sends a response
                ```SHELL
                # Start line: HTTP version + Status Code + Status Message
                HTTP/1.1 200 OK
                # Response headers are different depending on the request
                Date: Thurs, 14 Sep 2021
                # Body (commonly a JSON)
                ```

-   Callback hell

    -   Tons of nested callbacks to get one request
    -   We can handle this with recursion

        ```JS
        const getCountryRequest = function (url, callback = null) {
        const request = new XMLHttpRequest();
        request.open('GET', url);
        request.send();
        request.addEventListener('load', function () {
            const [data] = JSON.parse(this.responseText);
            if (callback) return callback(data);
            return data;
        });
        };

        const getCountryAndNeighborData = function (country) {
        getCountryRequest(`${endpoint}name/${country}`, function (data) {
            const [neighbor] = data.borders;
            if (!neighbor) return;
            return getCountryRequest(
            `${endpoint}alpha/${neighbor.toLowerCase()}`
            );
        });
        };

        getCountryAndNeighborData('usa'); // USA and Canada
        ```

## Code Examples

-   `AJAX`

    ```JS
    const getCountryData = function (country) {
        const request = new XMLHttpRequest();
        const endpoint = 'https://restcountries.com/v3.1/name/';
        // open(Method, Endpoint)
        request.open('GET', endpoint + country);
        request.send();
        request.addEventListener('load', function () {
            const [data] = JSON.parse(this.responseText);
            console.log(data);
        });
    };
    getCountryData('portugal');
    // {name: {…}, tld: Array(1), cca2: 'PT', ccn3: '620', cca3: 'PRT', …}
    ```
