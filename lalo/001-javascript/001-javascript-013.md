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

        -   `Protocol` + `IPAddress` + `Port number (https=443 / http=80)`

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

-   The event loop on asynchronous operations

    -   JavasScript runtime: container that executes JavaScript

        -   Engine: Heart of the runtime (heap, call stack)
        -   Web APIs: Included functionality (DOM, fetch API, etc)
        -   Event loop:
            -   Micro-tasks queue: special queue made for promises
                -   Take precedence over callbacks
                -   They're added to the call stack when the promise is done
            -   Callback queue:
                -   Here's where asynchronous (`setTimeout`, `load`, etc) operations are prepared to be send to the call stack
                -   When they're ready to be executed (event loop tick)
                -   If micro-tasks queue takes a lot of time everything here will be delayed
        -   Here's an example of execution

            ```JS
            console.log('Test start');
            setTimeout(() => {
                console.log('Callback');
            }, 0);
            Promise.resolve().then(() => {
                console.log('Promise');
            });
            console.log('Test end');
            /*
            Test start -> Sync
            Test end -> Sync
            Promise -> Micro-tasks queue
            Callback -> Callback queue
            */
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

-   `fetch()` API

    -   A placeholder from a future result of an operation
    -   Lifecycle

        -   Pending -> Settled -> (fulfilled | rejected)
        -   Only settled once
        -   The result of a promise is consumed by our code

            ```JS
            const getCountryAndNeighborData = country => {
                    fetch(`${endpoint}name/${country}`)
                    .then(response => response.json())
                    .then(data => {
                    renderCountry(data[0]);
                    const [neighbor] = data[0].borders;
                    if (!neighbor) return null;
                    return fetch(`${endpoint}alpha/${neighbor}`); // Never nest a then inside another then
                })
                .then(response => response.json())
                .then(data2 => renderCountry(data2[0], true));
            };
            getCountryAndNeighborData('usa');
            ```

        -   Handling errors and adding helpers

            ```JS
            // Request logic added into this helper function
            const getJSON = function (url, errorMsg = 'Something went wrong') {
              return fetch(url).then(response => {
                if (!response.ok) throw new Error(`${errorMsg} (${response.status})`);
                return response.json();
              });
            };
            // Handy error message helper
            const countryErrorMessage = c => `Country ${c} not found.`;
            // Request
            const getCountryAndNeighborData = country => {
              getJSON(`${endpoint}name/${country}`, countryErrorMessage(country))
                .then(data => {
                  const neighbors = data[0].borders;
                  if (!neighbors) throw new Error('No neighbor found!');
                  // Returns the helper function to continue the chain
                  return getJSON(
                    `${endpoint}alpha/${neighbors[0]}`,
                    countryErrorMessage(neighbors[0])
                  );
                })
                .then(data2 => data2[0]) // Chained request response
                .catch(err => console.error(err)) // Catches errors
                .finally(() => console.log('Finishes')); // It's always executed
            };
            getCountryAndNeighborData('australia');
            ```

-   Promises

    ```JS
    const lotteryPromise = new Promise((resolve, reject) => {
        console.log('Lottery draw is happening...');
        setTimeout(() => {
            const randomNumber = Math.floor(Math.random() * 10);
            if (randomNumber > 5) {
                resolve(randomNumber); // fulfill state
            } else {
                reject(new Error('Number is too low')); // reject state
            }
        }, 2000);
    });
    // Consume the promise
    lotteryPromise.then(res => console.log(res)).catch(err => console.error(err));

    // Promisifying setTimeout
    const wait = seconds => {
        return new Promise(resolve => {
            setTimeout(resolve, seconds * 1000);
        });
    };
    wait(2)
        .then(() => {
            console.log('I waited for 2 second');
            return wait(1);
        })
        .then(() => console.log('I waited for 1 second'));

    // Immediately executing promises
    Promise.resolve('abc').then(x => console.log(x));
    Promise.reject(new Error('Problem!')).catch(x => console.error(x));
    ```

-   `async/await` promises

    ```JS
    const getCat = async () => {
        // in this approach we use try/catch to handle errors
        try {
            const response = await fetch(
                'https://api.thecatapi.com/v1/images/search'
            );
            if (!response.ok) throw new Error('Something went wrong');
            const data = await response.json();
            console.log(data[0]); // Result of the request
            return data[0];
        } catch (error) {
            console.error(error);
            return error; // Needed to avoid an undefined return from the fulfilled promise
        }
    };

    getCat();
    /*
    {
        id: '4km',
        url: 'https://cdn2.thecatapi.com/images/4km.gif',
        width: 500,
        height: 200
    }
    */
    ```

    -   We can get multiple responses at the same time with combinator functions

        ```JS
        const get2Cats = async () => {
            // Promise.all returns an array of resolved promises
            const res = await Promise.all([getCat(), getCat()]);
            console.log(res.map(cat => cat.url));
            return res;
        };

        const get2CatsRace = async () => {
            // Promise.race returns the first promise to resolve (no matter if it's fulfilled or rejected)
            const res = await Promise.race([getCat(), getCat()]);
            console.log(res);
            return res;
        };

        const get2CatsSettled = async () => {
            // Promise.allSettled returns an array of promises with their status
            const res = await Promise.allSettled([getCat(), getCat()]);
            console.log(res);
            return res;
        };

        const get2CatsAny = async () => {
            // Promise.any returns the first fulfilled promise
            const res = await Promise.any([getCat(), getCat()]);
            console.log(res);
            return res;
        };

        get2Cats();
        /*
        [
            'https://cdn2.thecatapi.com/images/bte.jpg',
            'https://cdn2.thecatapi.com/images/ap9.gif'
        ]
        */

        get2CatsRace();
        /*
        {
            id: '4b2',
            url: 'https://cdn2.thecatapi.com/images/4b2.gif',
            width: 400,
            height: 300
        }
        */

        get2CatsSettled();
        /*
        [
            {
            status: 'fulfilled',
            value: {
                id: '28f',
                url: 'https://cdn2.thecatapi.com/images/28f.jpg',
                width: 400,
                height: 598
            }
            },
            {
            status: 'fulfilled',
            value: {
                id: 'MTcwNTI3NA',
                url: 'https://cdn2.thecatapi.com/images/MTcwNTI3NA.jpg',
                width: 1024,
                height: 682
            }
            }
        ]
        */
        get2CatsAny();
        /*
        {
            id: 'ci7',
            url: 'https://cdn2.thecatapi.com/images/ci7.jpg',
            width: 425,
            height: 270
        }
        */
        ```
