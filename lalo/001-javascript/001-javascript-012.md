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
