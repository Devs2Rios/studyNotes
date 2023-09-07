# Object-Oriented Programming (OOP) With JavaScript

-   Object Oriented programming is a paradigm based on the concept of objects
-   The object or model describe real-world abstract features
-   Objects contain data and logic
-   Every object is a block of code that interacts with other objects
-   Objects can be accessed by interfaces
-   Makes code easier to maintain
-   In traditional OOP we use classes (blueprint)

    ```
    Pet {
        name
        species
        walk(steps) {}
    }
    ```

-   An instance is an object based on a class

    ```
    koshka = Pet(
        name: 'Koshka'
        species: 'Cat'
    )
    koska.walk(10)
    ```

## OOP principles

-   Abstraction: Makes the object easier to implement by hiding the details (logic behind the object, like `.addEventListener()`)
-   Encapsulation: Keep some properties and methods private in the class (not accessible outside the context of the object)
-   Inheritance: Classes that inherit another classes, like a `Dog` class inheriting `Pet` and adding specific properties or methods for `Dog` like `bark(){}`
-   Polymorphism: A child can overwrite the method from the parent, for example if we create an elephant class based on `Pet` and make the `walk` method to advance 2 steps per step because it's a huge animal

## OPP in JavaScript

-   In JS an object is always linked to a prototype object (prototypal inheritance)

    -   The behavior of the object is delegated to the linked prototype
    -   We use the `new` keyword which creates a new object and uses the `this` keyword to refer to that object
        -   Creates the `__proto__` property on every object
    -   The prototype chain
        -   Prototypes are linked to other prototypes until they get the native JavaScript prototype
            ```JS
            function Animal(species) { this.species = species; }
            const turtle = new Animal('Turtle');
            console.log(turtle instanceof Animal); // true
            console.log(turtle instanceof Object); // true
            console.log(Animal instanceof Object); // true
            console.log(turtle.__proto__.__proto__); // [Object: null prototype] {} - null is the top of the chain
            ```
    -   Prototype creation techniques

        -   Constructor functions

            ```JavaScript
            function Animal(species) {
                this.species = species;
                // Don't add methods since is a bad practice and leads to bad performance
            }
            // Instance
            const turtle = new Animal('Turtle');
            // Animal { species: 'Turtle' }
            console.log(turtle instanceof Animal); // true
            console.log(turtle instanceof Object); // true
            ```

            -   The function is linked to a prototype
            -   It automatically returns an object

        -   `ES6` Classes

            ```JavaScript
            // Class expression
            // const PersonCl = class {};

            // Class declaration
            class PersonCl {
                constructor(firstName, lastName, age) {
                    this.firstName = firstName; // String.prototype with properties and methods inherits the behavior of the object
                    this.lastName = lastName;
                    this.age = age;
                    // Don't add methods to the constructor since is a bad practice and leads to bad performance
                }
                // methods
                fullName() {
                    return `${this.firstName} ${this.lastName}`;
                }
                greeting() {
                    return `Hey there! ${this.fullName()}`;
                }
            }
            // Instances of the class
            const jessica = new PersonCl('Jessica', 'Williams', 27);
            console.log(jessica); // PersonCl { firstName: 'Jessica', lastName: 'Williams', age: 27 }
            console.log(jessica.fullName()); // Jessica Williams
            console.log(jessica.__proto__ === PersonCl.prototype); // true
            console.log(jessica instanceof PersonCl); // true
            console.log(jessica.greeting()); // Hey there! Jessica Williams

            // Classes are not hoisted
            // Classes are first-class citizens
            // Classes are executed in strict mode
            ```

            -   Classes are a good approach, but it's better to use them if we understand prototypal inheritance
            -   It allows to make objects in a more readable and maintainable way
            -   Setters and getters are assistant functions that allow to retrieve and modify properties

                ```JS
                class Car {
                    constructor(brand, speed) {
                        this.brand = brand;
                        this.speed = speed;
                    }
                    get brand() {
                        return this._brand;
                    }
                    set brand(brandName) {
                        // We can add logic into the setter to validate our properties
                        try {
                            if (brandName && brandName.length > 2) this._brand = brandName;
                            else throw new Error('Brand name must be at least 3 characters');
                        } catch (error) {
                            console.error(error);
                        }
                    }
                    get speedUS() {
                        return this.speed / 1.6;
                    }
                    set speedUS(speed) {
                        this.speed = speed * 1.6;
                    }
                }
                const ford = new Car('Ford', 120);
                console.log(ford.speedUS); // 75
                ford.speedUS = 50; // Since speedUS is a getter, we can use it as a setter and is treated like a property, not a method
                console.log(ford.speed); // 80
                console.log(ford); // Car { make: 'Ford', speed: 80 }
                console.log(ford.brand); // Ford
                const errorCar = new Car('K', 100); // Error: Brand name must be at least 3 characters
                console.log(errorCar); // Car { speed: 100 }
                ```

            -   Static methods are added to the class object and cannot be accessed on instances, like `Array.from()`

                ```JS
                class Math {
                    // Static methods are not executed on the instances of the class
                    static add(x, y) {
                        return x + y;
                    }
                }
                console.log(Math.add(1, 2)); // 3
                const myMath = new Math();
                console.log(myMath.add(1, 2)); // TypeError: myMath.add is not a function
                ```

        -   `Object.create()`

            ```JavaScript
            const Pet = {
                name: '',
                species: '',
                // Method to initialize the instance
                init(name, species) {
                    this.name = name;
                    this.species = species;
                },
            };
            // Instance
            const barky = Object.create(Pet); // Object linked to Pet
            barky.name = 'Barky';
            barky.species = 'Dog';
            // { name: 'Barky', species: 'Dog' }
            console.log(barky instanceof Object); // true
            const koshka = Object.create(Pet); // Object linked to Pet
            koshka.init('Koshka', 'Cat');
            console.log(koshka); // { name: 'Koshka', species: 'Cat' }
            ```

-   Using the `prototype` structure we can add elements to our objects

    ```JS
    // Let's add a walk function to the Animal prototype
    Animal.prototype.walk = function () {
        console.log(`${this.species} Walking...`); // It has access to the object properties
    }; // All Animal Objects will now have this method
    Animal.prototype.inDanger = false;
    console.log(Animal.prototype); // { walk: [Function (anonymous)] } Not the prototype of animal but the prototype that will be used in every instance
    console.log(Animal.prototype.isPrototypeOf(Animal)); // false;
    console.log(turtle.__proto__); // { walk: [Function (anonymous)] } Same as above, we use __proto__ to display an instance prototype
    console.log(Animal.prototype.isPrototypeOf(turtle)); // true;
    turtle.walk(); // Turtle Walking...
    // Even though we can add properties to the object they're not added in the constructor but in the __proto__
    console.log(turtle); // Animal { species: 'Turtle' }
    console.log(turtle.hasOwnProperty('species')); // true;
    Animal.prototype.inDanger = false;
    console.log(Animal.prototype); // { walk: [Function (anonymous)], inDanger: false };
    console.log(turtle.hasOwnProperty('inDanger')); // false;
    ```

    -   It is not recommended to modify the prototype of native JavaScript objects like Array
        ```JS
        const arr = [2, 0, 3, 9, 4, 9, 3, 9];
        Array.prototype.unique = function () {
            return [...new Set(this)];
        };
        console.log(arr.unique()); // [ 2, 0, 3, 9, 4 ]
        ```

-   Inheritance between objects

    -   Construction functions

        ```JS
        const Podcast = function (name, episodes) {
            this.name = name;
            this.episodes = episodes;
        };

        Podcast.prototype.averageEpisodeDuration = function () {
            let totalDuration = 0;
            for (let i = 0; i < this.episodes.length; i++) {
                totalDuration += this.episodes[i].duration;
            }
            return totalDuration / this.episodes.length;
        };

        // PatreonPodcast inherits from Podcast
        const PatreonPodcast = function (name, episodes, monthlyDonation) {
            Podcast.call(this, name, episodes); // call the parent constructor
            this.monthlyDonation = monthlyDonation;
        };

        // Linking prototypes
        PatreonPodcast.prototype = Object.create(Podcast.prototype); // links the prototype
        PatreonPodcast.prototype.constructor = PatreonPodcast; // set the constructor

        PatreonPodcast.prototype.annualEarnings = function () {
            return this.monthlyDonation * 12;
        };

        const herejes = new PatreonPodcast(
            'Herejes',
            [
                {
                    title: 'Hereje 1',
                    duration: 60,
                },
            ],
            100
        );

        console.log(herejes.__proto__ === PatreonPodcast.prototype); // true
        console.log(herejes instanceof PatreonPodcast); // true
        console.log(herejes instanceof Podcast); // true (because of prototype linking)
        console.log(herejes instanceof Object); // true
        console.log(herejes);
        /*
        PatreonPodcast {
        name: 'Herejes',
        episodes: [ { title: 'Hereje 1', duration: 60 } ],
        monthlyDonation: 100
        }
        */
        console.log(herejes.averageEpisodeDuration()); // 60
        console.log(herejes.annualEarnings()); // 12000
        ```

    -   ES6 classes

        ```JS
        class Person {
            constructor(name, age) {
                this.name = name;
                this.age = age;
            }
            greeting() {
                console.log(`My name is ${this.name} and I am ${this.age}`);
            }
            static fromBirthYear(name, year) {
                const currentYear = new Date().getFullYear();
                return new Person(name, currentYear - year);
            }
        }
        // Student class inherits Person
        class Student extends Person {
            constructor(name, age, major) {
                super(name, age); // Construction function of the parent class
                this.major = major;
            }
            // The following methods overwrite the parent class ones
            greeting() {
                console.log(
                    `My name is ${this.name} and I am ${this.age} and I study ${this.major}`
                );
            }
            static fromBirthYear(name, year, major) {
                const currentYear = new Date().getFullYear();
                return new Student(name, currentYear - year, major);
            }
        }
        const person1 = Student.fromBirthYear('John', 1990, 'Computer Science');
        person1.greeting(); // My name is John and I am 33 and I study Computer Science

        // With this approach the prototype chain is set automatically
        console.log(person1.__proto__ === Student.prototype); // true
        console.log(person1.__proto__.__proto__ === Person.prototype); // true
        console.log(person1.__proto__.__proto__.__proto__ === Object.prototype); // true
        ```

    -   `Object.create()`

        ```JS
        const Person = {
            calcAge() {
                return new Date().getFullYear() - this.birthYear;
            },
            init(firstName, lastName, birthYear) {
                this.firstName = firstName;
                this.lastName = lastName;
                this.birthYear = birthYear;
            },
        };

        const Student = Object.create(Person); // Student inherits from Person
        Student.init = function (firstName, lastName, birthYear, course) {
            Person.init.call(this, firstName, lastName, birthYear); // call the init method of the parent object
            this.course = course;
        };

        const john = Object.create(Student);
        john.init('John', 'Doe', 1992, 'Computer Science');
        console.log(john.calcAge()); // 31
        console.log(john.course); // Computer Science
        ```

        -   This is by far one of the most preferred approach for several developers since it's not faking classes

-   Encapsulation inside objects

    -   Not native on JavaScript, we currently have to fake it

        ```JS
        class User {
            constructor(name, email) {
                this.name = name;
                this.email = email;
                // Protected property
                this._password = '';
            }

            // Not a setter because we don't want to allow getting the password
            setPassword(password) {
                this._password = password;
            }
        }

        const user = new User('myUser', 'user@test.com');
        user.setPassword('MySecretPassword47??');
        console.log(user.name); // myUser
        console.log(user.email); // user@test.com
        console.log(user.password); // undefined
        console.log(user._password); // MySecretPassword47?? - Not completely secret
        ```

    -   Experimental feature Class Fields

        ```JS
        class User {
            access = 'public'; // Public field
            #password = ''; // Private field
            constructor(name, email) {
                this.name = name;
                this.email = email;
                console.log(this.#initialPassword());
            }
            // Public method
            setPassword(oldPassword, newPassword) {
                if (oldPassword === this.#password) {
                    this.#password = newPassword;
                    console.log('Password changed!');
                } else {
                    console.log('Wrong password!');
                }
            }
            // Private method
            #initialPassword() {
                this.#password = `NewPassword-${Math.round(Math.random() * 1)}`;
                return this.#password;
            }
        }

        const user = new User('myUser', 'user@test.com'); // NewPassword-15
        user.setPassword('NewPassword-1', 'MySecretPassword47??'); // Wrong password! or Password changed!
        console.log(user.name); // myUser
        console.log(user.email); // user@test.com
        console.log(user.password); // undefined
        console.log(user.#password); // SyntaxError: Private field '#password' must be declared in an enclosing class
        console.log(user.#initialPassword()); // SyntaxError: Private field '#initialPassword' must be declared in an enclosing class
        ```

-   Chaining methods

    ```JS
    class MathOperations {
        constructor() {
            this.results = [];
        }
        add(a, b) {
            const result = a + b;
            console.log(`Add: ${a} + ${b} = ${result}`);
            this.results.push(result);
            return this; // needed for chaining
        }
        multiply(a, b) {
            const result = a * b;
            console.log(`Multiply: ${a} * ${b} = ${result}`);
            this.results.push(result);
            return this;
        }
        divide(a, b) {
            const result = a / b;
            console.log(`Divide: ${a} / ${b} = ${result}`);
            this.results.push(result);
            return this;
        }
        subtract(a, b) {
            const result = a - b;
            console.log(`Subtract: ${a} - ${b} = ${result}`);
            this.results.push(result);
            return this;
        }
    }
    const mathOperations = new MathOperations();
    mathOperations.add(2, 3).multiply(3, 4).subtract(4, 2).divide(2, 2);
    /*
    Add: 2 + 3 = 5
    Multiply: 3 * 4 = 12
    Subtract: 4 - 2 = 2
    Divide: 2 / 2 = 1
    */
    console.log(mathOperations.results); // [ 5, 12, 2, 1 ]
    ```
