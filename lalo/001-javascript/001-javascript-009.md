# Working With Arrays

- Methods are functions attached to Arrays which are objects

- Simple Array Methods

  ```JavaScript
  let arr = ['a', 'b', 'c', 'd', 'e'];

  // .slice() doesn't mutate the original array
  console.log(arr.slice(2)); // [ 'c', 'd', 'e' ]
  console.log(arr); // [ 'c', 'd', 'e' ]
  console.log(arr.slice(1, 3)); // [ 'b', 'c' ]
  console.log(arr.slice(-1)); // [ 'e' ]
  console.log(arr.slice()); // [ 'a', 'b', 'c', 'd', 'e' ] a copy
  console.log([...arr]); // [ 'a', 'b', 'c', 'd', 'e' ] another copy

  // .splice() mutates the original array
  arr.splice(1, 3);
  console.log(arr); // [ 'a', 'e' ]
  arr.splice(1, 2);
  console.log(arr); // [ 'a' ]

  // .reverse() mutates the original array
  arr = ['a', 'b', 'c', 'd', 'e'];
  arr.reverse();
  console.log(arr); // [ 'e', 'd', 'c', 'b', 'a' ]

  // .concat() doesn't mutate the original array
  const arr2 = arr.concat([...arr].reverse());
  console.log(arr);
  // [ 'e', 'd', 'c', 'b', 'a' ]
  console.log(arr2);
  // [ 'e', 'd', 'c', 'b', 'a', 'a', 'b', 'c', 'd', 'e' ]
  console.log([...arr, ...[...arr].reverse()]);
  // [ 'e', 'd', 'c', 'b', 'a', 'a', 'b', 'c', 'd', 'e' ]

  // .join() doesn't mutate the original array
  console.log(arr.join('-')); // e-d-c-b-a
  ```

- The new at Method

  ```JavaScript
  const arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  console.log(arr[0]); // 0
  console.log(arr.at(0)); // 0
  // Last element
  console.log(arr[arr.length - 1]); // 10
  console.log(arr.slice(-1)); // 10
  console.log(arr.at(-1)); // 10
  console.log('Dope'.at(-1)); // e
  ```

- Looping Arrays: forEach

  ```JavaScript
  const arr = [10, -15, 3, 5, -9, 12];
  // With an of loop
  console.log('---Loop---');
  for (const num of arr)
    console.log(`${num > 0 ? `In: ${num}` : `Out: ${Math.abs(num)}`}`);
  /*
  ---Loop---
  In: 10
  Out: 15
  In: 3
  In: 5
  Out: 9
  In: 12
  */
  // With the forEach method
  console.log('---forEach()---');
  arr.forEach(num =>
    console.log(`${num > 0 ? `In: ${num}` : `Out: ${Math.abs(num)}`}`)
  );
  /*
  ---forEach()---
  In: 10
  Out: 15
  In: 3
  In: 5
  Out: 9
  In: 12
  */
  console.log('---forEach()---');
  // instead using for (const [i, num] of arr.entries())
  arr.forEach((num, i) => {
    console.log(
      `(${String(i).padStart(2, '0')}) ${
        num > 0 ? `In: ${num}` : `Out: ${Math.abs(num)}`
      }`
    );
  });
  /*
  ---forEach()---
  (00) In: 10
  (01) Out: 15
  (02) In: 3
  (03) In: 5
  (04) Out: 9
  (05) In: 12
  */
  ```

- forEach With Maps and Sets

  ```JavaScript
  const cities = new Map([
    ['CDMX', 'Mexico City'],
    ['NYC', 'New York City'],
    ['TKY', 'Tokyo'],
  ]);
  // forEach used on the map
  cities.forEach((k, v, m) => {
    // m is the map object
    console.log(`'${k}': '${v}'`);
  });
  /*
  'Mexico City': 'CDMX'
  'New York City': 'NYC'
  'Tokyo': 'TKY'
  */
  new Set([2, 2, 12, 34, 10, 4]).forEach((v, _, s) => {
    // s is the set onject, as sets doesn't have indexes the key and value are the same
    console.log(`${v}: ${v}`);
  });
  /*
  2: 2
  12: 12
  34: 34
  10: 10
  4: 4
  */
  ```

- Creating DOM Elements

  ```JavaScript
  container.innerHTML = ''; // Cleans the content of the HTML element
  // Create your HTML element(s) in a string template literal
  const html = `
      <div>
        <p>New element!</p>
      </div>
    `;
  // Inserts the HTML after the begining of the container
  container.insertAdjacentHTML('afterbegin', html);
  ```

- Data Transformations: map, filter, reduce

  ```JavaScript
  const arr1 = [1, 2, 3, 4];

  // .map()
  const arr2 = arr1.map(num => num * 2);
  console.log(arr2); // [ 2, 4, 6, 8 ]

  // .filter()
  const arr3 = arr1.filter(num => num % 2 === 0);
  console.log(arr3); // [ 2, 4 ]

  // .reduce()
  const arr4 = arr1.reduce((accumulator, current) => accumulator + current);
  console.log(arr4); // 10
  ```

- The map Method

  ```JavaScript
  const pricesUSD = [10.2, 5.25, 100, 25.2];

  // Returns a brand new array
  const dollarPrice = 20.54,
    pricesMXN = pricesUSD.map(price => price * dollarPrice);

  /*
  With regular functions
  pricesMXN = pricesUSD.map(function(price) {
      return price * dollarPrice;
  };
  */

  for (const [i, price] of pricesUSD.entries())
    console.log(`${price.toFixed(2)} USD = ${pricesMXN[i].toFixed(2)} MXN`);
  /*
  10.20 USD = 209.51 MXN
  5.25 USD = 107.83 MXN
  100.00 USD = 2054.00 MXN
  25.20 USD = 517.61 MXN
  */
  ```

- The filter Method

  ```JavaScript
  const pricesUSD = [10.2, 5.25, 100, 25.2, 234.12];

  // Returns a brand new array
  const expensive = pricesUSD.filter(price => price > 80);
  console.log(expensive); // [ 100, 234.12 ]
  ```

- The reduce Method

  ```JavaScript
  const pricesUSD = [10.2, 5.25, 100, 25.2, 234.12, 5];

  // Returns a primitive value
  const total = pricesUSD.reduce(function (acumulator, current) {
    console.log(`acumulator: ${acumulator} | current: ${current}`);
    return acumulator + current;
  });
  /*
  acumulator: 10.2 | current: 5.25
  acumulator: 15.45 | current: 100
  acumulator: 115.45 | current: 25.2
  acumulator: 140.65 | current: 234.12
  acumulator: 374.77 | current: 5
  */

  const lol = [...'abcdefghijk'].reduce(
    (acumulator, current) => acumulator + `${current}ha`
  );
  console.log(lol); // abhachadhaehafhaghahhaihajhakha

  // Get max value
  console.log(pricesUSD.reduce((a, b) => (a > b ? a : b))); // 234.12
  ```

- The Magic of Chaining Methods

  - Don't overchain, it can lead to performance issues
  - Don't chain methods that mutate the original array like the splice or reverse method

  ```JavaScript
  const movements = [200, 450, -400, 3000, -650, -130, 70, 1300];
  const eurToUSD = 1.1;
  const totalInUSD = movements
    .filter(mov => mov > 0)
    .map((mov, i, arr) => {
      console.log(arr) // Check the array for debugging
      mov * eurToUSD
    })
    .reduce((a, b) => a + b, 0);
  console.log(totalInUSD);
  ```

- The find Method

  ```JavaScript
  const wallet = {
    crypto1: { symbol: 'ETH', balance: 1232, inUSD: 1933.25 },
    crypto2: { symbol: 'BTC', balance: 243, inUSD: 24125.24 },
    crypto3: { symbol: 'APE', balance: 122, inUSD: 7.01 },
    crypto4: { symbol: 'AVAX', balance: 4459, inUSD: 27.23 },
    crypto5: { symbol: 'MATIC', balance: 9832812, inUSD: 1.01 },
    crypto6: { symbol: 'SOL', balance: 2094, inUSD: 42.4 },
  };
  // Retrieves the first element found
  const myEth = Object.values(wallet).find(crypto => crypto.symbol === 'ETH');
  console.log(myEth); // { symbol: 'ETH', balance: 1232, inUSD: 1933.25 }
  console.log(myEth.balance); // 1232
  console.log(Object.values(wallet).find(crypto => crypto.symbol === 'XRP')); // undefined
  ```

- The findIndex Method

  ```JavaScript
  const arr = [...'abcdefghijklmnñopqrstuvwxyz'];
  // Returns the index of the value you are searchig for
  console.log(arr.findIndex(letter => letter === 'ñ')); // 14
  console.log(arr[14]); // ñ
  ```

- some and every

  ```JavaScript
  const arr = [90, 2043, 1000, 345, 5690];
  // Returns a boolean if the condition is achieved or not in at least one element
  console.log(arr.some(num => num > 100)); // true
  console.log(arr.some(num => num > 10000)); // false
  // Returns a boolean if the condition is achieved or not in all elements
  console.log(arr.every(num => num > 80)); // true
  console.log(arr.every(num => num > 10000)); // false
  // With callback
  const myCallback = num => num > 100;
  console.log(arr.some(myCallback)); // true, DRY
  ```

- flat and flatMap

  ```JavaScript
  // Nested Array
  const arr = [
    [90, 2043, 1000],
    [[345], [5690]],
  ];
  // .flat() unnests a nested array at the level indicated
  console.log(arr.flat()); // [ 90, 2043, 1000, [ 345 ], [ 5690 ] ]
  console.log(arr.flat(2)); // [ 90, 2043, 1000, 345, 5690 ]
  // .flatMap() makes a map and flat at the same time
  console.log(arr.flatMap(narr => narr)); // [ 90, 2043, 1000, [ 345 ], [ 5690 ] ]
  ```

- Sorting Arrays

  ```JavaScript
  // String array
  const books = ['Creep', 'Chunk', 'Yangling', 'Deogus'];
  console.log(books.sort()); // [ 'Chunk', 'Creep', 'Deogus', 'Yangling' ]
  // It modifies the original array
  console.log(books); // [ 'Chunk', 'Creep', 'Deogus', 'Yangling' ]

  // Numbers array
  const prices = [12.5, 5.5, 8.3, 9.1];
  console.log(prices.sort()); // [ 12.5, 5.5, 8.3, 9.1 ]
  /*
  The function is based on strings, that's why 12.5 is the first one.
  To make a succesful number sort use a and b parameters where:
      a - The first element for comparison.
      b - The second element for comparison.
      < 0, sort a before b (a - b returns a negative number)
      > 0, sort a after b (a + b returns a positive number)
      === 0, keep original order of a and b
  */
  // Ascending
  console.log(prices.sort((a, b) => (a > b ? 1 : -1))); // [ 5.5, 8.3, 9.1, 12.5 ]
  console.log(prices.sort((a, b) => a - b)); // [ 5.5, 8.3, 9.1, 12.5 ]
  // Descending
  console.log(prices.sort((a, b) => (a < b ? 1 : -1))); // [ 12.5, 9.1, 8.3, 5.5 ]
  console.log(prices.sort((a, b) => a + b)); // [ 12.5, 9.1, 8.3, 5.5 ]
  // The loop keeps runing until the numbers are ordered accordingly to the function
  ```

- More Ways of Creating and Filling Arrays

  ```JavaScript
  // Literal
  let arr = ['Creep', 'Chunk', 'Yangling', 'Deogus'];
  const arr2 = new Array('Creep', 'Chunk', 'Yangling', 'Deogus');

  // New empty plus .fill()
  arr = new Array(4); // [ <4 empty items> ]
  // arr.fill(1); // [ 1, 1, 1, 1 ]
  arr.fill(1, 3); // [ <3 empty items>, 1 ]
  arr2.fill(1, 2, 3); // [ 'Creep', 'Chunk', 1, 'Deogus' ]

  // New array with .from()
  const arr3 = Array.from({ length: 4 }, () => 1); // [ 1, 1, 1, 1 ]
  const arr4 = Array.from({ length: 4 }, (_, i) => i + 1);
  // [ 1, 2, 3, 4 ] _ not used variables
  ```
