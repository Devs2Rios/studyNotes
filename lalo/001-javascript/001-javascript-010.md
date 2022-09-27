# Numbers, Dates, Intl and Timers

- Converting and Checking Numbers

  ```JavaScript
  // All numbers are floats
  console.log(10 === 10.0); // true
  // Some floating operations result different as expected
  console.log(0.1 + 0.2); // 0.30000000000000004
  // This decimal error is something we have to deal with
  // Strings to numbers
  console.log('2', Number('2')); // 2 2
  console.log(+'2'); // 2
  // Parsing
  // .parseInt(value, number type) -> 10 is decimal
  console.log(Number.parseInt('10pt', 10)); // 10
  console.log(Number.parseInt('0x0', 10)); // 0
  console.log(Number.parseInt(' 50.2cm ')); // 50
  // .parseFloat()
  console.log(Number.parseFloat(' 50.2cm ')); // 50.2
  // .isNaN() check if value is not a number
  console.log(Number.isNaN(' 10 ')); // false -> is a number
  console.log(Number.isNaN(+'10A')); // true -> is not a number
  console.log(Number.isNaN(10 / 0)); // Infinity -> on browser
  // .isFinite() best way to check is the value is a number
  console.log(Number.isFinite(10)); // true
  console.log(Number.isFinite('10')); // false
  console.log(Number.isFinite(10 / 0)); // false
  // .isInteger()
  console.log(Number.isInteger(10)); // true
  console.log(Number.isInteger(10.0)); // true
  console.log(Number.isInteger(10.01)); // false
  console.log(Number.isInteger('10')); // false
  console.log(Number.isInteger(10 / 0)); // false
  ```

- Math and Rounding

  ```JavaScript
  // Square root
  console.log(Math.sqrt(9)); // 3
  console.log(9 ** (1 / 2)); // 3
  // Cubic root
  console.log(8 ** (1 / 3)); // 2
  // Max value does type cohersion but no parsing
  console.log(Math.max(10, 5, 2, 300, 450, 12)); // 450
  console.log(Math.max(10, 5, 2, 300, '450', 12)); // 450
  console.log(Math.max(10, 5, 2, 300, '450cm', 12)); // NaN
  // Min value does type cohersion but no parsing
  console.log(Math.min(10, 5, 2, 300, 450, 12)); // 2
  // PI
  console.log(Math.PI); // 3.141592653589793
  const radius = 12;
  console.log(Math.PI * radius ** 2); // 452.3893421169302
  console.log(Math.PI * Number.parseFloat('10mm') ** 2); // 314.1592653589793
  // Random
  Math.random(); // Random float between 0-1
  console.log(Math.round(Math.random() * 100)); // Random integer between 0 and 100
  const randint = (v1, v2) => v1 + Math.round(Math.random() * Math.abs(v1 - v2));
  console.log(randint(-10, 10));
  // Math.trunc() removes the decimal part
  console.log(Math.trunc(0.5)); // 0
  // Math.round() rounds the decimal part >=.5 up | < .5 down
  console.log(Math.round(1.5)); // 2
  // Math.ceil() rounds the decimal always up
  console.log(Math.ceil(1.2)); // 2
  // Math.floor() rounds the decimal always down
  console.log(Math.floor(1.9)); // 1
  // The previous round methods do type coercion
  console.log(Math.trunc('0.5')); // 0
  console.log(Math.round('1.5')); // 2
  console.log(Math.ceil('1.2')); // 2
  console.log(Math.floor('1.9')); // 1
  // Be careful with negative numbers
  console.log(Math.trunc(-12.5)); // -12
  console.log(Math.round(-12.6)); // -13
  console.log(Math.round(-12.5)); // -12
  console.log(Math.ceil(-12.1)); // -12
  console.log(Math.floor(-12.9)); // -13
  // Managing decimals
  // .toFixed() returns a string with the decimals indicated as arguments
  console.log((5.5).toFixed(2)); // 5.50
  console.log((5.5398492).toFixed(2)); // 5.54 -> string
  console.log(+(5.5398492).toFixed(2)); // 5.54 -> integer
  ```

- The Remainder Operator

  ```JavaScript
  // Returns the reminder of a division
  console.log(5 % 2); // 1
  console.log(5 % 3); // 2
  console.log(5 % 4); // 1
  console.log(5 % 5); // 0
  // Check even or odd
  const evenOrOdd = n => (n % 2 == 0 ? 'Even' : 'Odd');
  console.log(evenOrOdd(2)); // Even
  console.log(evenOrOdd(3)); // Odd
  console.log(evenOrOdd(250)); // Even
  console.log(evenOrOdd(233)); // Odd
  ```

- Numeric Separators

  ```JavaScript
  // Underscore can help you read numbers
  const tierrasol = 150_000_000_000;
  console.log(tierrasol); //150000000000
  console.log(10_00); // 1000
  console.log(1_000); // 1000
  // Just use it between numbers
  console.log(10.0_0); // 10.00
  console.log(10._00);
  // SyntaxError: Invalid or unexpected token
  // Just use number separators on numbers, not strings
  console.log(Number('1_1_00000')); // NaN
  ```

- Working with BigInt

  ```JavaScript
  // Numbers are 64 bits so there's a limit of how big numbers can be
  console.log(2 ** 53 - 1); // 9007199254740991 -> largest safe integer on JS
  console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
  // If you go up sometimes it'll work and sometimes it won't
  console.log(2 ** 53); // 9007199254740992
  console.log(2 ** 53 + 1); // 9007199254740992
  console.log(2 ** 53 + 2); // 9007199254740994
  console.log(2 ** 53 + 3); // 9007199254740996
  // If you want to use bigger numbers you can use BigInt
  const myBigInt = 84233678210128747891290932872478890904n;
  // You can just make operations with big ints with another big ints
  console.log(myBigInt + 1n); // 84233678210128747891290932872478890905n
  console.log(myBigInt + BigInt(2)); // 84233678210128747891290932872478890906n
  // Be careful with types, bigint is different that a number
  console.log(typeof myBigInt); // bigint
  console.log(20n == 20); // true
  console.log(20n == '20'); // true
  console.log(20n === 20); // false
  // Some math operations won't work or will change their behavior
  console.log(12n / 3n); // 4n -> the result is always rounded
  console.log(Math.sqrt(9n)); // TypeError: Cannot convert a BigInt value to a number
  ```

- Creating Dates

  ```JavaScript
  // Current date
  const now = new Date();
  console.log(now); // Current date in this format -> 2022-08-24T20:07:45.740Z
  // From strings
  console.log(new Date('2022-08-24T20:07:45.740Z')); // 2022-08-24T20:07:45.740Z
  console.log(new Date('24 December, 2020')); // 2020-12-24T06:00:00.000Z
  // From numbers
  console.log(new Date(2022, 7, 22, 2, 30, 0)); // 2022-08-22T07:30:00.000Z
  console.log(new Date(1992, 8, 4)); // 1992-09-04T06:00:00.000Z
  // Based on Unix time
  console.log(new Date(0)); // 1970-01-01T00:00:00.000Z
  // Days to miliseconds
  const daysToMs = days => days * 24 * 60 * 60 * 1000;
  console.log(daysToMs(3)); // 259200000
  // Useful date scenarios
  const future = new Date(2050, 0, 1, 12, 0, 10);
  console.log(future); // 2050-01-01T18:00:10.000Z
  console.log(future.getFullYear()); // 2050
  console.log(future.getMonth()); // 0
  console.log(future.getDate()); // 1
  console.log(future.getDay()); // 6
  console.log(future.getHours()); // 12
  console.log(future.getMinutes()); // 0
  console.log(future.getSeconds()); // 10
  console.log(future.toISOString()); // 2050-01-01T18:00:10.000Z
  console.log(future.toLocaleString()); // 1/1/2050, 12:00:10 PM
  console.log(future.getTime()); // 2524672810000 -> Unix time
  console.log(Date.now()); // Current date in unix time
  // New Date from Unix time
  console.log(new Date(1661373658381)); // 2022-08-24T20:40:58.381Z
  // Setters
  future.setFullYear(2100);
  console.log(future); // 2100-01-01T18:00:10.000Z
  ```

- Operations With Dates

  ```JavaScript
  // You can perform calculations with miliseconds
  const now = new Date();
  const birthDay = new Date(1992, 8, 4, 6, 21, 12);
  console.log(now);
  // 2022-08-25T01:26:01.895Z
  console.log(birthDay);
  // 1992-09-04T12:21:12.000Z
  // To miliseconds
  console.log(+now);
  // 1661390843089
  console.log(+birthDay);
  // 715609272000
  // Calc days between two dates
  const calcDays = (d1, d2) => Math.floor((d2 - d1) / (24 * 60 * 60 * 1000));
  console.log(calcDays(birthDay, now)); // 10946.572760081019
  console.log(calcDays(new Date(2022, 7, 1), now)); // 10946.572760081019
  ```

- Internationalizing Dates (Intl)

  ```JavaScript
  const now = new Date();
  // You can get an International date output from a date object
  console.log(new Intl.DateTimeFormat('en-US').format(now)); // 8/24/2022
  console.log(new Intl.DateTimeFormat('en-AU').format(now)); // 24/08/2022
  console.log(new Intl.DateTimeFormat('es-MX').format(now)); // 24/8/2022
  console.log(new Intl.DateTimeFormat('ru-RU').format(now)); // 24.08.2022
  ```

- Internationalizing Numbers (Intl)

  ```JavaScript
  const num = 12324241223.12;
  // You can get an International number output from a number object
  console.log(new Intl.NumberFormat('en-US').format(num)); // 12,324,241,223.12
  console.log(new Intl.NumberFormat('it-IT').format(num)); // 12.324.241.223,12
  console.log(new Intl.NumberFormat('es-MX').format(num)); // 12,324,241,223.12
  console.log(new Intl.NumberFormat('es-ES').format(num)); // 12.324.241.223,12
  // You can add options to the formatting
  const options1 = { style: 'unit', unit: 'celsius' },
    options2 = { style: 'currency', currency: 'MXN' },
    options3 = { style: 'percent' };
  console.log(new Intl.NumberFormat('en-US', options1).format(num)); // 12,324,241,223.12°C
  console.log(new Intl.NumberFormat('en-US', options2).format(num)); // MX$12,324,241,223.12
  console.log(new Intl.NumberFormat('en-US', options3).format(num)); // 1,232,424,122,312%
  ```

- Timers: setTimeout and setInterval

  ```JavaScript
  // Keeps working on the background until the timeout is reached
  const count = Array.from({ length: 3 }, (_, i) => i * 10);
  const timer = setTimeout(
    arr => {
      for (const n of arr) console.log(n);
    },
    1000,
    count // Argument
  );
  console.log('Counting…');
  /*
  Counting…
  0
  10
  20
  */
  // Deleting the timeout before executing
  if (count.includes(20)) clearTimeout(timer);
  // Intervals runs every certain time
  let second = 0;
  // Second counter
  let currentSecond;
  clearInterval(currentSecond); // clears counter before
  currentSecond = setInterval(() => console.log(++second), 1000);
  ```
