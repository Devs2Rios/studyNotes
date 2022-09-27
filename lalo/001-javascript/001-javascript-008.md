# A Closer Look at Functions

- Default parameters

  ```JavaScript
  const myObjs = [];

  const muFunc = function (param1, param2 = 2, param3 = 3) {
    const myObj = { param1, param2, param3 };
    console.log(myObj);
    myObjs.push(myObj);
  };

  muFunc(1); // { param1: 1, param2: 2, param3: 3 }
  muFunc(1, 3); // { param1: 1, param2: 3, param3: 3 }
  muFunc(1, undefined, 1); // { param1: 1, param2: 2, param3: 1 }
  ```

- How Passing Arguments Works: Value vs. Reference

  - Objects: will be changed because they are referenced
  - Primitives: won't change because the arguments passes are copies of the values

  ```JavaScript
  const post = 'S0018';

  const don = {
    username: 'Dom',
    id: 1230487267,
  };

  const login = function (postNum, user) {
    postNum = 'F0384';
    user.username = `Mr. ${user.username}`;
    if (user.id === 1230487267) {
      console.log('Logged in!');
    } else {
      console.log('Wrong id');
    }
  };

  login(post, don); // Logged in!
  console.log(post); // S0018 didn't change
  console.log(don.username); // Mr. Dom changed

  // This is what's happening inside the function
  const postNum = post; // a copy of post in another variable
  const user = don; // this uses the same reference as don

  const newid = function (person) {
    person.id = Math.round(Math.random() * 9999999999);
  };

  newid(user); // using user instead dom because we want this id to change
  console.log(don); // { username: 'Mr. Dom', id: 7768518925 }
  console.log(user); // { username: 'Mr. Dom', id: 7768518925 }
  login(post, user); // Wrong id because don and user changed id because of the object reference
  ```

- First-Class and Higher-Order Functions

  - First-Class functions

    - Values are treated as values
    - They are another type of object
    - They can be saved as a variable value
    - We can use functions as arguments for other functions
    - They can be returned from other functions
    - They can call methods

  - High-Order functions (HOf)
    - They are functions that receive another function as argument or return another function
    - HOf are possible because of First-Class functions

- Functions Accepting Callback Functions

  - Callbacks allow to add abstraction

  ```JavaScript
  const oneWord = function (str) {
    return str.replace(/ /g, '').toLowerCase();
  };
  const upperFirstWord = function (str) {
    const [first, ...others] = str.split(' ');
    return [first.toUpperCase(), ...others].join(' ');
  };

  const transformer = function (str, fn) {
    console.log(`Original string: ${str}`);
    console.log(`Transformed string: ${fn(str)}`);
    console.log(`Transformed by: ${fn.name}`);
  };

  transformer('JavaScript is good!', upperFirstWord);
  /*
  Original string: JavaScript is good!
  Transformed string: JAVASCRIPT is good!
  Transformed by: upperFirstWord
  */
  transformer('JavaScript is good!', oneWord);
  /*
  Original string: JavaScript is good!
  Transformed string: javascriptisgood!
  Transformed by: oneWord
  */
  const happiness = function (repeats) {
    console.log('😬'.repeat(repeats));
  };

  [3, 4, 12, 1].forEach(happiness); // Happiness as callback
  /*
  😬😬😬
  😬😬😬😬
  😬😬😬😬😬😬😬😬😬😬😬😬
  😬
  */

  ```

- Function Returning Functions

  ```JavaScript
  const func = function (param1) {
    return function (param2) {
      console.log(`${param1} ${param2}`);
    };
  };
  const funcArrow = param1 => param2 => console.log(`${param1} ${param2}`);

  func('Hey')('you!'); // Hey you!
  funcArrow('Hey')('you!'); // Hey you!
  ```

- The call and apply Methods

  ```JavaScript
  const funcsObj = {
    range: 1000,
    ranNum(player) {
      return `${player}: ${Math.floor(Math.random() * this.range) + 1}`;
    },
  };

  console.log(funcsObj.ranNum('test')); // test: 22

  // If you want to use ranNum as a method for any object
  // you'll need to use .call() or .apply() so it won't point to undefined
  const ranNum = funcsObj.ranNum;
  const ran10 = { range: 10 };
  const ran100 = { range: 100 };
  console.log(ranNum.call(ran10, 'chuy')); // chuy: 8
  console.log(ranNum.call(ran100, 'glass')); // glass: 71
  // .apply needs an array as argument to do the same thing as call
  const dorothy = ['dorothy'];
  console.log(ranNum.apply(ran100, dorothy)); // dorothy: 69
  // Nevertheless it's easier with spread operator
  console.log(ranNum.call(ran100, ...dorothy)); // dorothy: 96
  ```

- The bind Method

  - Bind returns a new function where the keyword is bound

  ```JavaScript
  const funcsObj = {
    range: 1000,
    ranNum(player) {
      return `${player}: ${Math.floor(Math.random() * this.range) + 1}`;
    },
  };

  console.log(funcsObj.ranNum('test')); // test: 649

  // funcsObj.ranNum bound to { range: 5 } into ranNum5
  const ranNum5 = funcsObj.ranNum.bind({ range: 5 });
  // Calling ranNum5 with the player's name
  console.log(ranNum5('clark')); // clark: 3
  // Binding it to different ranNums
  const ranNum10 = funcsObj.ranNum.bind({ range: 10 });
  const ranNum20 = funcsObj.ranNum.bind({ range: 20 });
  const ranNum30 = funcsObj.ranNum.bind({ range: 30 });
  const ranNum40 = funcsObj.ranNum.bind({ range: 40 });
  // You can bound arguments to the .bind function
  const ranNum50 = funcsObj.ranNum.bind({ range: 50 }, 'fifty');
  console.log(ranNum50()); // fifty: 30
  // Let's create a lottery game
  const tickets = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; // Tickets to sold
  const letters = [...'ABCDEFGHIJKLMNOPQRSTUVWXYZ']; // Letters to create names
  const playerNames = []; // Players' array
  // Populate array
  for (let player = 0; player < tickets.length; player++) {
    let playerName = '';
    for (let i = 0; i < 3; i++) {
      playerName += letters[Math.floor(Math.random() * letters.length)];
    }
    playerNames.push(playerName);
  }
  // Lottery object
  const lottery = {
    playerNames,
    tickets,
    playersTickets: {},
    buyTickets() {
      for (const p of this.playerNames) {
        // Arrow function because we need to use this. inside
        const getNameNumIndex = entry => {
          const pName = entry.replace(/: \d+/, ''),
            pNum = Number(entry.replace(/[A-Z]{3}: /, '')),
            pIndex = this.tickets.indexOf(pNum);
          return [pName, pNum, pIndex];
        };
        // Preset variables before the game
        let ticketAvailable = false;
        let pName, pNum, pIndex;
        while (!ticketAvailable) {
          // Using the bound function
          [pName, pNum, pIndex] = getNameNumIndex(ranNum10(p));
          if (pIndex !== -1) {
            // If the ticket exists assign it to the current player (p)
            ticketAvailable = true;
          }
        }
        // Fill the entry in the playersTickets object
        this.playersTickets[pName] = pNum;
        // Delete the ticket from the tickets array
        this.tickets.splice(pIndex, 1);
      }
      // Change the tickets array for a sold out string
      this.tickets = 'Sold Out!';
    },
  };
  lottery.buyTickets();
  console.log(lottery);
  /*
  {
    playerNames: [
      'PNY', 'MOC', 'KJZ',
      'JHI', 'KYZ', 'CQV',
      'ROD', 'SLJ', 'BQM',
      'NGS'
    ],
    tickets: 'Sold Out!',
    playersTickets: {
      PNY: 8,
      MOC: 9,
      KJZ: 6,
      JHI: 1,
      KYZ: 3,
      CQV: 7,
      ROD: 5,
      SLJ: 4,
      BQM: 10,
      NGS: 2
    },
    buyTickets: [Function: buyTickets]
  }
  */

  // Partial binding
  const addTax = (rate, value) => value + value * rate;
  console.log(addTax(0.3, 100)); // 130
  // Bounding without one argument,
  // null goes for the this keyword and .16 for the first argument
  const mxVAT = addTax.bind(null, 0.16);
  // mxVAT = value => value + value + 0.16
  console.log(mxVAT(100)); // 116

  // Function returning function
  const mxVAT2 = value => rate => value + value * rate;
  console.log(mxVAT2(100)(0.25)); // 125
  ```

- Immediately Invoked Function Expressions (IIFE)

  - They're good for private outputs or variables that don't require to be mutated, nevertheless, they're like block scope so in modern JavaScript is not useful

  ```JavaScript
  (function () {
    console.log('Just once!'); // Just once!
    (() => console.log('Just once!'))(); // Just once!
  })();
  ```

- Closures

  - They're the closed-over variable environment of the execution in which a function was created, even after that execution context is gone
  - We can't create them manually, it happens automatically
  - We can't access to them because they're not a tangible Js object
  - The variables inside the closure have priority over the scope chain

  ```JavaScript
  const closureFunc = function () {
    let counter = 0;
    return function () {
      counter++;
      console.log(`Current Number: ${counter}`);
    };
  };

  // The function inside the variable creates an execution context
  // that remembers the variables inside the function
  const outsideCounter = closureFunc();
  outsideCounter(); // Current Number: 1
  outsideCounter(); // Current Number: 2
  outsideCounter(); // Current Number: 3
  console.dir(outsideCounter);
  /*
  [Function (anonymous)]
      [[Scopes]]: Scopes[3]
          0: Closure (closureFunc)
              counter: 3
  You cannot access to [[Scopes]] in your code
  */
  ```

- More Closure Examples

  ```JavaScript
  let f = 10;

  const g = function () {
    const a = 19;
    f = function () {
      console.log(a * f);
    };
  };
  const h = function () {
    const b = 30;
    f = function () {
      console.log(b * 4);
    };
  };

  g();
  f();
  console.dir(f);
  /*
  Closure created when g is used
  [[Scopes]]: Scopes[3]
      0: Closure (g)
          a: 19
  */

  // Re-assign f function
  h();
  f();
  console.dir(f);
  /*
  Closure replaced when h is used
  [[Scopes]]: Scopes[3]
      0: Closure (h)
          b: 30
  */
  const row = 250;
  const timedGrid = function (grid, newLineTime) {
    const row = grid / 5;
    setTimeout(function () {
      console.log(`Grid: ${grid}`);
      console.log(`Row: ${row}`);
    }, newLineTime * 1000);
    console.log(`New Line Time: ${newLineTime}`);
  };
  timedGrid(200, 2);
  /*
  New Line Time: 2
  Grid: 200
  Row: 40 -> From closure
  */
  const timedGrid2 = function (grid, newLineTime) {
    // This doesn't have const row
    setTimeout(function () {
      console.log(`Grid: ${grid}`);
      console.log(`Row: ${row}`);
    }, newLineTime * 1000);
    console.log(`New Line Time: ${newLineTime}`);
  };
  timedGrid2(200, 2);
  /*
  New Line Time: 2
  Grid: 200
  Row: 250 -> From global scope
  */
  ```
