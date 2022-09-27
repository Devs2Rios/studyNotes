# Data Structures, Modern Operators and Strings

- Destructuring Arrays

  ```JavaScript
  const arr = [2, 3, 4];
  // You can assingn an array values to different variables
  const a = arr[0];
  const b = arr[1];
  const c = arr[2];
  // Or destructure and do it in one line
  const [x, y, z] = arr;
  console.log(x, y, z); // 2, 3, 4

  // You can use destructure with arrays inside objects
  const sports = {
    name: 'Sports selection',
    trainingCentre: 'Two Rivers, MX, Mexico',
    categories: ['Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis'],
    warmUp: ['Jogging', 'Jumping', 'Sprinting'],
    coolDown: ['Walk', 'Stretch'],
    ranWorkout: function() {
      return [
        this.warmUp[Math.floor(Math.random() * this.warmUp.length)],
        this.categories[Math.floor(Math.random() * this.categories.length)],
        this.coolDown[Math.floor(Math.random() * this.coolDown.length)],
      ];
    },
  };
  // You can destructure an array by assin¡gning a name to the elements you want,
  // and leaving empty the ones you dont want
  let [favorite, , , , lessFavorite] = sports.categories;
  console.log(favorite, lessFavorite); // Rugby Tennis
  // Switch values
  [favorite, lessFavorite] = [lessFavorite, favorite];
  console.log(favorite, lessFavorite); // Tennis Rugby
  // Destructuring from a return value from a function
  let [myWarmUp, mySport, myCoolDown] = sports.ranWorkout();
  console.log(myWarmUp, mySport, myCoolDown); // Jumping Rugby Stretch

  // Destructuring nested arrays
  const nested = [0, [1, 11], [2, 3]];
  const [, [one], [two, three]] = nested;
  console.log(one, two, three); // 1 2 3

  // Destructuring with default values, if they are not assigned they're undefined
  const [ja, ha, kha = 'Russian'] = ['Español', 'Inglés'];
  console.log(ja, ha, kha); // Español Inglés Russian (undefined if not assigned)
  ```

- Destructuring Objects

  ```JavaScript
  const sports = {
    collectionName: 'Sports selection',
    trainingCentre: 'Two Rivers, MX, Mexico',
    categories: ['Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis'],
  };

  // For object destructure you need to match the key of the object
  let { collectionName, trainingCentre, categories } = sports;
  console.log(collectionName, trainingCentre, categories);
  // Sports selection Two Rivers, MX, Mexico [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ]

  // You can assign specific entries { entryName: yourVar }
  const {
    collectionName: myCollection,
    trainingCentre: myClub,
    categories: mySports,
  } = sports;
  console.log(myCollection, myClub, mySports);
  // Sports selection Two Rivers, MX, Mexico [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ]

  // You can set default values
  const { categories: normalSports, extreme = [] } = sports;
  console.log(normalSports, extreme);
  // [ 'Rugby', 'Skateboard', 'Soccer', 'Swimming', 'Tennis' ] []

  // Mutating variables
  let col1 = 'Red',
    col2 = 'Blue';
  const colors = { col1: 'Magenta', col2: 'Cyan' };
  ({ col1, col2 } = colors); // Wrapped into parenthesis
  console.log(col1, col2); // Magenta Cyan

  // Nested objects
  const square = {
    coord1: { x: 0, y: 0 },
    coord2: { x: 10, y: 0 },
    coord3: { x: 10, y: 10 },
    coord4: { x: 0, y: 10 },
  };
  const {
    coord1: { x, y, z = 0 }, // You can add defaults to prevent undefined values
  } = square;
  console.log(x, y, z); // 0 0 0

  // Destructuring an object inside a function
  function destructureObj({ name, surname }) {
    return `I am ${name} ${surname}`;
  }
  const jonasFierro = { name: 'Jonás', surname: 'Fierro' };
  console.log(destructureObj(jonasFierro));
  // I am Jonás Fierro
  ```

- The Spread Operator (...)

  ```JavaScript
  // SPREAD packs elements into an array
  // Is useful to unpack an array
  const arr1 = [0, 1, 2, 3, 4, 5];
  const arr2 = [...arr1, 6, 7, 8, 9];
  // arr2 is the same as [arr1[0], arr1[1], arr1[2], arr1[3], arr1[4], arr1[5], 6, 7, 8, 9]
  console.log(arr2); // [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

  // Yuo can unpack an array inside an object
  const arrInObj = { arr: [1, 2, 3, 4] };
  const arr3 = [...arrInObj.arr, 5];
  console.log(arr3); // [ 1, 2, 3, 4, 5 ]

  // Copy an array
  const arr4 = [...arr3];
  console.log(arr4); // [ 1, 2, 3, 4, 5 ]

  // Join 2 arrays
  const arr5 = [6, 7, 8, 9, 10];
  const arr6 = [...arr4, ...arr5];
  console.log(arr6); // [ 1, 2, 3, 4,  5, 6, 7, 8, 9, 10 ]

  // Iterables: arrays, strings, maps, sets, NOT objects
  const str = 'Iterate';
  const letters = [...str, '!'];
  console.log(letters); // [ 'I', 't', 'e', 'r', 'a', 't', 'e', '!' ]

  // Add it to a function
  function iterable(one, two, three) {
    let str = '';
    for (const count of [one, two, three]) {
      str += `Now the number is ${count}!\n`;
    }
    return str;
  }
  console.log(iterable(...[1, 2, 3]));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  */

  // You can use it with an object as well
  const oldObj = { old: "I'm old", age: 90 };
  const newObj = { ...oldObj, new: "I'm new", age: 1 };
  const copyOfNewObj = { ...newObj }; // Copy of newObj
  copyOfNewObj.old = "I'm not old";
  console.log(oldObj); // { old: "I'm old", age: 90 }
  console.log(newObj); // { old: "I'm old", age: 1, new: "I'm new" }
  console.log(copyOfNewObj); // { old: "I'm not old", age: 1, new: "I'm new" }
  ```

- Rest Pattern and Parameters

  ```JavaScript
  // REST packs elements into a variable
  const [a, b, ...others] = [1, 2, 3, 4, 5, 6, 7];
  console.log(a, b, others); // 1 2 [ 3, 4, 5, 6, 7 ]

  // REST is useful with destructuring
  const countries = {
    latam: ['México', 'Argentina', 'Brasil'],
    northam: ['United States', 'Canada'],
    oeurope: ['Netherlands', 'España', 'France', 'Italia'],
    eeurope: ['România', 'Hrvatska', 'Україна'],
  };
  const [mx, , brl, ...otherCountries] = [
    ...countries.latam,
    ...countries.eeurope,
  ];
  console.log(mx, brl, otherCountries);
  // México Brasil [ 'România', 'Hrvatska', 'Україна' ]

  const { oeurope: euroOr, eeurope: euroOcc, ...america } = countries;
  console.log(euroOr, euroOcc, america);
  // [ 'Netherlands', 'España', 'France', 'Italia' ]
  // [ 'România', 'Hrvatska', 'Україна' ]
  /*
  {
    latam: [ 'México', 'Argentina', 'Brasil' ],
    northam: [ 'United States', 'Canada' ]
  }
  */

  // Add it to a function
  function iterable(...counting) {
    let str = '';
    for (const count of counting) {
      str += `Now the number is ${count}!\n`;
    }
    return str;
  }
  console.log(iterable(1, 2, 3, 4, 5, 6, 7, 8));
  /*
    Now the number is 1!
    Now the number is 2!
    Now the number is 3!
    Now the number is 4!
    Now the number is 5!
    Now the number is 6!
    Now the number is 7!
    Now the number is 8!
    */
  const newArr = [1, 2, 3];
  console.log(iterable(...newArr));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  */
  console.log(iterable(...newArr, 4));
  /*
  Now the number is 1!
  Now the number is 2!
  Now the number is 3!
  Now the number is 4!
  */

  ```

- Short Circuiting (&& and ||)

  ```JavaScript
  // || (or) Returns the first value that is truthy
  console.log(1 || 'Dope'); // 1
  console.log(0 || 'Dope'); // Dope
  console.log(0 || ''); // null
  console.log(0 || '' || null || 'Truthty'); // Truthty
  const lights = { on: false };
  const lightsOn = lights.on || 'Turn on the lights';
  console.log(lightsOn); // Turn on the lights

  // && (and) returns the last value if everything is truthy
  // it stops when finds a falsy value
  console.log(0 && 'a'); // 0
  console.log(1 && 'a'); // a
  console.log(1 && 'a' && []); // []
  console.log(1 && 'a' && [1] && null); // null

  // Let's put them in conditionals
  const bool1 = true,
    bool2 = false,
    bool3 = true,
    bool4 = false;

  if (bool1 || bool2) console.log(`bool1: ${bool1} || bool2: ${bool2}`);
  // bool1: true || bool2: false
  if (bool2 || bool4) console.log(`bool2: ${bool2} || bool4: ${bool4}`);
  // nothing
  if (bool1 || bool3) console.log(`bool1: ${bool1} || bool3: ${bool3}`);
  // bool1: true || bool3: true
  if (bool1 && bool2) console.log(`bool1: ${bool1} && bool2: ${bool2}`);
  // nothing
  if (bool1 && bool3) console.log(`bool1: ${bool1} && bool3: ${bool3}`);
  // bool1: true && bool3: true
  if (bool2 && bool2) console.log(`bool2: ${bool2} && bool4: ${bool4}`);
  // nothing
  ```

- The Nullish Coalescing Operator (??)

  ```JavaScript
  // Nullish: Null and undefined
  const lights = { on: false };
  let lightsOn = lights.on ?? 'Turn on the lights';
  console.log(lightsOn); // false
  lights.on = undefined;
  lightsOn = lights.on ?? 'Turn on the lights';
  console.log(lightsOn); // 'Turn on the lights'
  ```

- Logical Assignment Operators

  ```JavaScript
  const p1 = {
    controller: 'P1',
    alias: 'Berta',
    hallOfFame: undefined,
  };
  const p2 = {
    controller: 'P2',
    alias: '',
    exp: 10,
    hallOfFame: undefined,
  };

  // The long way
  p1.exp = p1.exp || 1;
  console.log(p1);
  // {controller: 'P1', alias: 'Berta', hallOfFame: undefined, exp: 1}
  p2.exp = p2.exp && 1;
  console.log(p2);
  // {controller: 'P2', alias: '', exp: 1, hallOfFame: undefined}

  // The short way in JavaScript 2021
  p1.hallOfFame &&= 'Not yet!';
  console.log(p1);
  // {controller: 'P1', alias: 'Berta', hallOfFame: undefined, exp: 1}
  p2.alias ||= 'No-Alias';
  p2.hallOfFame ??= 'Not yet!';
  console.log(p2);
  // {controller: 'P2', alias: 'No-Alias', exp: 1, hallOfFame: 'Not yet!'}
  ```

- Looping Arrays: The for-of Loop

  ```JavaScript
  const bigArray = [];
  for (let i = 0; i < 5; i++) bigArray.push(Math.round(Math.random() * 1000));
  for (const ranNum of bigArray) console.log(`Te random number is ${ranNum}`);
  /*
  Te random number is 831
  Te random number is 769
  Te random number is 223
  Te random number is 188
  Te random number is 204
  */

  // for loop with index and destructure
  for (const [i, ranNum] of bigArray.entries())
    console.log(`Te random number ${i + 1} is ${ranNum}`);
  /*
  Te random number 1 is 831
  Te random number 2 is 769
  Te random number 3 is 223
  Te random number 4 is 188
  Te random number 5 is 204
  */
  ```

- Enhaced Object Literals

  ```JavaScript
  const thought = 'Thinking';
  const arrLength = 3;

  const objLiteral = {
    quote: "I'm literal",
    thoughts: ["I'm happy", "I'm sad", "I'm hungry"],
    // ES& enhaced object literals
    // Add an entry just by calling an outside variable
    thought,
    // Define an entry name by computing
    arrLength,
    [`arrWith${arrLength}els`]: new Array(arrLength),
    // Add a function just by declaring the name and adding the paranthesis
    newThougt() {
      this.thought = this.thoughts[
        Math.floor(Math.random() * this.thoughts.length)
      ];
      return this.thought;
    },
  };

  objLiteral.newThougt();
  console.log(objLiteral);
  /*
  {
    quote: "I'm literal",
    thoughts: [ "I'm happy", "I'm sad", "I'm hungry" ],
    thought: "I'm sad",
    arrLength: 3,
    arrWith3els: [ <3 empty items> ],
    newThougt: [Function: newThougt]
  }
  */
  ```

- Optional chaining (?.)

  ```JavaScript
  const pad = num => num.toString().padStart(5, '0');
  const tr = 'tr',
    bk = 'block';

  const chained = {
    [`${bk}${pad(1)}`]: {
      [`${tr}${pad(1)}`]: {
        hash: 'e193a01ecf8d30ad0affefd332ce934e32ffce72',
        time: new Date(2019, 1, 28, 18, 1, 10, 230),
      },
      [`${tr}${pad(2)}`]: {
        hash: '6fc978af728d43c59faa400d5f6e0471ac850d4c',
        time: new Date(2020, 6, 1, 14, 31, 3, 915),
      },
    },
    [`${bk}${pad(2)}`]: {
      [`${tr}${pad(3)}`]: {
        hash: '221407c03ae5c73109cce71d27e24637824f3333',
        time: new Date(2020, 10, 1, 17, 15, 50, 750),
      },
      [`${tr}${pad(4)}`]: {
        hash: 'c63528a52274a35d1c07bd9e55a83c6eb073de81',
        time: new Date(2021, 8, 30, 11, 11, 11, 111),
      },
    },
    [`${bk}${pad(3)}`]: {
      [`${tr}${pad(5)}`]: {
        hash: 'de1f53b6fbc3fecd35b0bbc963e21902a149e5e3',
        time: new Date(2021, 11, 3, 0, 3, 45, 104),
      },
      [`${tr}${pad(6)}`]: {
        hash: '20dd129da16a9afb802d8b595485f8d2719aea44',
        time: new Date(2022, 2, 16, 9, 21, 36, 426),
      },
    },
    [`${bk}${pad(4)}`]: {
      [`${tr}${pad(7)}`]: {
        hash: '',
      },
    },
  };

  console.log(chained?.block00001);
  /*
  {
    tr00001: {
      hash: 'e193a01ecf8d30ad0affefd332ce934e32ffce72',
      time: 2019-03-01T00:01:10.230Z
    },
    tr00002: {
      hash: '6fc978af728d43c59faa400d5f6e0471ac850d4c',
      time: 2020-07-01T19:31:03.915Z
    }
  }
  */
  console.log(chained?.block00001?.tr00003 ?? 'No such transaction in the block'); // No such transaction in the block
  console.log(chained?.block00004?.tr00007); // { hash: '' }
  console.log(
    chained?.block00004?.tr00007?.time ?? 'No timestamp in such transaction'
  ); // No timestamp in such transaction
  // It might be useful for a loop that checks transactions within a block
  const [...myBlocks] = Object.keys(chained);
  const myTransactions = [];
  for (let i = 0; i < 7; i++) myTransactions.push(`${tr}${pad(i + 1)}`);
  for (const myBlock of myBlocks) {
    for (const myTransaction of myTransactions) {
      const currentTransaction = chained[myBlock][myTransaction]?.hash;
      if (currentTransaction) {
        console.log(
          `Block ${myBlock}, transaction ${myTransaction}: ${currentTransaction}`
        );
      }
    }
  }
  /*
  Block block00001, transaction tr00001: e193a01ecf8d30ad0affefd332ce934e32ffce72
  Block block00001, transaction tr00002: 6fc978af728d43c59faa400d5f6e0471ac850d4c
  Block block00002, transaction tr00003: 221407c03ae5c73109cce71d27e24637824f3333
  Block block00002, transaction tr00004: c63528a52274a35d1c07bd9e55a83c6eb073de81
  Block block00003, transaction tr00005: de1f53b6fbc3fecd35b0bbc963e21902a149e5e3
  Block block00003, transaction tr00006: 20dd129da16a9afb802d8b595485f8d2719aea44
  */
  ```

- Looping Objects: Object Keys, Values, and Entries

  ```JavaScript
  const animals = {
  dog: {
      id: 'Dog',
      animalName: 'Frida',
      breed: 'Labrador',
      isPet: true,
    },
    cat: {
      id: 'Cat',
      animalName: 'Koshka',
      breed: 'Munchkin',
      isPet: true,
    },
    snake: {
      id: 'Snake',
      animalName: 'Piguay',
      breed: 'Python',
    },
  };

  const [...keys] = Object.keys(animals);
  console.log(keys); // [ 'dog', 'cat', 'snake' ]
  const [...values] = Object.values(animals);
  console.log(values);
  /*[
    { id: 'Dog', animalName: 'Frida', breed: 'Labrador', isPet: true },
    { id: 'Cat', animalName: 'Koshka', breed: 'Munchkin', isPet: true },
    { id: 'Snake', animalName: 'Piguay', breed: 'Python' }
  ]*/
  for (const [key, animal] of Object.entries(animals)) {
    console.log(
      `animals.${key}: I'm a ${animal.breed} ${animal.id}, my name is ${
        animal.animalName
      } and I'm ${(animal?.isPet && 'a pet') || 'not a pet'}`
    );
  }
  /*
  animals.dog: I'm a Labrador Dog, my name is Frida and I'm a pet
  animals.cat: I'm a Munchkin Cat, my name is Koshka and I'm a pet
  animals.snake: I'm a Python Snake, my name is Piguay and I'm not a pet
  */
  ```

- Sets

  ```JavaScript
  // A set is an unordered data (it has no indexes) structure that has unique elements inside of it
  const newSet = new Set([10, 11, 40, 50, 11, 66, 50]); // You can pass any iterable as argument
  console.log(newSet); // Set(5) { 10, 11, 40, 50, 66 }
  const newStringSet = new Set('Still Fozzy');
  console.log(newStringSet); // Set(9) { 'S', 't', 'i', 'l', ' ', 'F', 'o', 'z', 'y' }
  // set methods
  console.log(newSet.has(1)); // false
  console.log(newStringSet.has('z')); // true
  console.log(newStringSet.has(' ')); // true
  newStringSet.delete(' ');
  console.log(newStringSet.has(' ')); // false
  newStringSet.add('!');
  console.log(newStringSet.has('!')); // true
  console.log(newStringSet); // Set(9) { 'S', 't', 'i', 'l', 'F', 'o', 'z', 'y', '!' }
  for (const val of newStringSet) {
    if (val === 'F') {
      break;
    } else {
      console.log(val);
    }
  }
  /*
  S
  t
  i
  l
  */
  newStringSet.clear();
  console.log(newStringSet); // Set(0) {}
  const newArrFromSet = [...new Set('Parangaricutirimicuaro')];
  console.log(newArrFromSet); // [ 'P', 'a', 'r', 'n', 'g', 'i', 'c', 'u', 't', 'm', 'o' ]
  ```

- Maps: Fundamentals

  ```JavaScript
  // In maps the keys can have eny kind of value
  const coffee = new Map();
  // You can set values using the set method
  coffee.set('Roast', 'Dark');
  coffee.set('Origin', 'Chiapas');
  coffee.set(304029198, 'Batch serial number');
  // Set can be also used chained
  const arr = [10, 10, 9];
  coffee
    .set('Packed Date', 20220134)
    .set(1045, 'River One Store, HXQ')
    .set(arr, 'Quality Control')
    .set(true, 'Packed')
    .set(false, 'Not packed');
  console.log(coffee);
  /*
  Map(8) {
    'Roast' => 'Dark',
    'Origin' => 'Chiapas',
    304029198 => 'Batch serial number',
    'Packed Date' => 20220134,
    1045 => 'River One Store, HXQ',
    [ 10, 10, 9 ] => 'Quality Control',
    true => 'Packed',
    false => 'Not packed'
  }
  */
  const packedOn = coffee.get('Packed Date');
  console.log(coffee.get(packedOn < 1900) && coffee.get(packedOn >= 19000)); // Packed
  // Another useful methods
  console.log(coffee.has('Roast')); // true
  coffee.delete(arr); // Two arrays with the same values are not equal, it must be the same array
  console.log(coffee);
  /*
  Map(7) {
    'Roast' => 'Dark',
    'Origin' => 'Chiapas',
    304029198 => 'Batch serial number',
    'Packed Date' => 20220134,
    1045 => 'River One Store, HXQ',
    true => 'Packed',
    false => 'Not packed'
  }
  */
  console.log(coffee.size); // 7
  ```

- Maps: Iteration

  ```JavaScript
  // Prompt is a browser engine method, this is for the terminal
  const prompt = require('prompt-sync')();

  // Create a map using Arrays of two elements inside another array
  const programmingLangs = new Map([
    ['Question', "What's the best programming language"],
    [1, 'Python'],
    [2, 'JavaScript'],
    [true, 'Pythonist'],
    [false, 'Not pythonist'],
  ]);
  console.log(programmingLangs);
  /*
  Map(5) {
    'Question' => "What's the best programming language",
    1 => 'Python',
    2 => 'JavaScript',
    true => 'Pythonist',
    false => 'Not pythonist'
  }
  */
  // It could also be an object's entries
  const songs = { song1: 'GOD', song2: 'Unwind' };
  const songMap = new Map(Object.entries(songs));
  console.log(songMap); // Map(2) { 'song1' => 'GOD', 'song2' => 'Unwind' }

  // Iterations are easier destructuring
  console.log(programmingLangs.get('Question')); // What's the best programming language
  for (const [key, value] of programmingLangs) {
    if (typeof key === 'number') console.log(`Answer ${key}: ${value}`);
    /*
    Python
    JavaScript
    */
  }
  const answer = Number(prompt('Your answer (write the number): '));
  console.log(programmingLangs.get(answer === 1) || programmingLangs.get(false));
  // Depends on the answer it will return Python or Not pythonist

  // Convert map to array
  console.log([...songMap]); // [ [ 'song1', 'GOD' ], [ 'song2', 'Unwind' ] ]
  console.log([...songMap.keys()]); // [ 'song1', 'song2' ]
  console.log([...songMap.values()]); // [ 'GOD', 'Unwind' ]

  ```

- Which Data Structure to Use?

  - Sources of data: from the program, from the UI and from external sources (APIs)
  - Detect if it just needs values or key/value pairs
    - Just values
      - Arrays: if you need an order and you can have duplicated values
      - Sets: if you don't need an order and you don't want duplicated values, they're also faster
    - Keys and values
      - Objects: they're easier to use, you can use methods inside of them and are the best structure when using JSON
      - Maps: When you need keys that are not strings, they're easier to iterate, they perform better than objects

- Working With Strings

  ```JavaScript
  const myString = 'This is a string';
  // Access to certain letter by index
  console.log(myString[0]); // T
  // Return the length of a string
  console.log(myString.length); // 16
  // Find index of a letter inside a string
  console.log(myString.indexOf('a')); // 8
  console.log(myString.indexOf('x')); // -1 didn't find
  console.log(myString.lastIndexOf('i')); // 13
  // Cut a string
  console.log(myString.slice(4)); // is a string
  console.log(myString.slice(1, 10)); // his is a
  console.log(myString.slice(0, myString.indexOf(' a '))); // This is
  console.log(myString.slice(0, myString.lastIndexOf('i'))); // This is a str
  console.log(myString.slice(0, -5)); // This is a s
  // These methods create new string objects behind the scenes
  // Change case
  console.log(myString.toLowerCase()); // this is a string
  console.log(myString.toUpperCase()); // THIS IS A STRING
  let badName = 'MaLoLe';
  badName = badName[0].toUpperCase() + badName.slice(1).toLowerCase();
  console.log(badName); // Malole
  const email = 'prompt@devs2rios.io';
  let badEmail = ' promPt@devS2rIos.iO \n';
  badEmail = badEmail.toLowerCase().trim(); // Trim clears trailing whitespaces
  console.log(email === badEmail); // true
  const priceE = '3049,91€';
  const priceA = priceE.replace('€', '$').replace(',', '.');
  console.log(priceE, priceA); // 3049,91€ 3049.91$
  // Replacing all by using regex with the global flag
  const lol = 'ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha ha';
  const notSoLol = lol.replace(/ha\s/g, '');
  console.log(notSoLol); // ha
  // Methods that return booleans
  console.log(myString.includes('i')); // true
  console.log(myString.includes('x')); // false
  console.log(myString.startsWith('T')); // true
  console.log(myString.startsWith('t')); // false
  console.log(myString.endsWith('g')); // true
  console.log(myString.endsWith('G')); // false
  // If you look for a word regardless the case you can transform everything to lowercase befor searching

  // Transforming strings to arrays
  const myFood = 'Banana, Potato, Cucumber'.replace(/,/g, '').split(' ');
  console.log(myFood);
  // [ 'Banana', 'Potato', 'Cucumber' ]
  console.log(myFood.join(' * '));
  // Banana * Potato * Cucumber
  const [firstName, lastname] = 'Bob Alice'.split(' ');
  console.log(firstName, lastname); // Bob Alice

  // Capitalize first letter of every word
  const titleCase = str => {
    return str.replace(
      /([a-zA-Z]+)/g,
      word => word[0].toUpperCase() + word.slice(1).toLowerCase()
    );
  };
  console.log(titleCase('lksjdkd lajkdj kaks')); // Lksjdkd Lajkdj Kaks
  console.log('12'.padStart(4, '0')); // 0012
  console.log('12'.padEnd(4, '0')); // 1200
  console.log('12'.padStart(6, '0').padEnd(12, '0')); // 000012000000
  const maskPassword = str => str.slice(0, -4).replace(/./g, '*') + str.slice(-4);
  console.log(maskPassword('467')); // 467
  console.log(maskPassword('1234')); // 1234
  console.log(maskPassword('93u58')); // *3u58
  console.log(maskPassword('09032u4029039849nsdjk900'));
  // ********************k900
  console.log(maskPassword('pdncsojñxapkokpoawoijcnncdioe'));
  // *************************dioe
  console.log('Eat, Sleep, Rave, Repeat\n'.repeat(4).trim());
  /*
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  Eat, Sleep, Rave, Repeat
  */
  ```
