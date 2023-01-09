# Typescript

> -   Combination between strong typed languages like C# and dynamically-typed languages like JavaScript.
> -   Any JavaScript program is also a valid Typescript program, you just need to add the types of data.
> -   Is built this way to maximize its compatibility with existing JavaScript codebases.
> -   Type annotations are optional, so if you're using a JS library, you'll need to define your own types.

## Environment

-   Use Typescript within an NPM project:

    ```bash
    # start a project
    cd project
    npm init # follow the steps
    # install Typescript
    npm install --save-dev typescript
    # setup a Typescript compiler configuration file tsconfig.json
    ./node_modules/.bin/tsc --init
    # install ts-node to run the files
    npm install --save-dev ts-node
    # Run your files
    ./node_modules/.bin/ts-node file-name.ts
    ```

## The Typescript Type System Key Concepts

#### 1. Type Inference is always on:

-   Check this example:
    ```Typescript
    let user = {};
    user.name = 'John';
    ```
    ```Bash
    Error:(54, 6) TS2339:Property 'name' does not exist on type '{}'.
    ```
-   The error is raised because there's no name property in user

    -   This could fix the error:

        ```Typescript
        let user = { name: 'John' };
        user.name = 'Claire';
        ```

        -   And this is because the second assignation is the same type as the first one, if we do this another error would be raised.

            ```Typescript
            let user = { name: 'John' };
            user.name = 'Claire';
            user.days = 1
            ```

            ```Bash
            Error:(59, 8) TS2339:Property 'days' does not exist on type '{ name: string; }'.
            ```

            -   This is because user is not the type of `any` and it has a `name` property defined inside so we cannot assign any other property, that's why when we try to add days it points to `name` and is not possible to overwrite it.
            -   Here's when `interface` (keyword to create custom types and objects) comes in handy:

                ```Typescript
                interface User {
                    name:string;
                }
                let user : User = {
                    name: 'John'
                };
                user.name = 'Claire';
                user.days = 20;
                ```

            -   We'll still get the same error but this will lead to the next key concept.

#### 2. Types are defined by the collection of their properties

-   Type system is based on structural subtyping.
    -   What defines a type is a collection of specific properties and their types.

#### 3. Type compatibility depends on the list of properties of a type

-   The same list of properties must match an object assigned to that type

    -   Using an `interface`:

        ```Typescript
        interface User {
            name:string;
            days:number;
        }
        let user : User = {
            name: 'John',
            days: 20
        };
        user.age = 12;
        // Will raise an error
        ```

        -   You can fix this error by defining the age type in the `interface` and `user` or by adding it as an optional type.

            ```Typescript
            interface User {
                name:string;
                days:number;
                age?:number;
            }
            ```

            -   Objects can have all of their properties as optional, allowing enmpty object initialization.

    -   Using an `any`[^1] type object:

        ```Typescript
        let user : any = {
            name: 'John',
            days: 20
        };
        user.age = 12;
        // Will assign a new property
        ```

-   There will be some scenarios where assigning the type will be impossible, for those cases you can use `noImplicityAny`.

## Typescript TypeDefinitions

#### What are the multiple scenarios for Typescript Type Definitions?

-   Typescript ^2
    -   No type denitions.
    -   Type denitions available and shipped together with the compiler.
    -   A library doesn't ship with type denitions, but they can be installed.
    -   A library ships with its own type denitions built-in.

#### How do I use libraries that don't have Type Definitions available?

-   The `any` type can be used to avoid errors:
    ```Ts
    let someVar: any;
    console.log(typeof someVar, someVar);
    // undefined undefined
    someVar = 23;
    console.log(typeof someVar, someVar);
    // number 23
    someVar = 'Dope';
    console.log(typeof someVar, someVar);
    // string Dope
    ```
-   Install the types if available:
    ```bash
    # Install the library
    npm install --save-dev uuid
    # Install the types
    npm install --save-dev @types/uuid
    ```

#### How do I use types included in specific libraries

-   Import them:
    ```Ts
    import axios from 'axios';
    import {AxiosPromise} from "axios";
    const response: AxiosPromise = axios.get('/lessons', {
    ...
    ```

#### Do we really need type annotations to get typesafety?

-   Not always sometimes they are auto-completed.

#### How to make the most of Typescript type definitions

-   By adding setting `"noImplicitAny": true,` inside the `tsconfig.json` you'll be able to get more advantage of type definitions.
    -   The compiler will be able to infer almost all types in your program, at the expense of only a few type annotations, especially in function arguments.

#### Forcing type compatibility

-   You can create custom types:

    ```ts
    import axios from 'axios';
    import {AxiosPromise} from "axios";
    // We create this interface
    interface Lesson {
        id:number;
        description: string;
    }
    // To force the compatibility with the AxiosPromise item
    function getLesson(lessonId:number): AxiosPromise<Lesson> {
        return axios.get(`lessons/${lessonId}`);
    }
    const promise = getLesson(1);
    promise.then(response => {
        const lesson: Lesson = response.data;
        ...
    });
    ```

-   Or use types from other libraries:
    -   When you install `@types` with NPM, you'll make them available in your current scope.
        -   Before installing them it's important to check if the package has built-in types or if they come with the compiler to avoid `duplicate type definition`[^2].
        -   It's also good to add the `"skipDefaultLibCheck"` to the `tsconfig.json` to ensure that only our program is checked by the compiler.
            -   This prevents the more recent versions of the compiler to throw errors against ancient libraries and also to increase performance.

#### Guidelines for Using the multiple Type Definitions available

-   Knowing which types to use will lead to a better developer experience.
-   The compiler always adds more features, but libraries might not leverage them yet.
-   Using the compiler built-in types (the lib flag) maximize the type safety.
    -   Just check that they don't conflict with types that we already imported.
    -   And that they don't affect third party types if not needed by using `skipLibCheck`[^3].

#### When should we use `@types`?

-   Use the built-in types of each module instead of using @types systematically.
-   Use @types strategically if necessary (with modules like Express or Sequelize).
-   Plain Javascript modules have great types available on `@types`.
-   Newer modules usually come with built-in types.
-   `@types/node` are essential to writing any node program.
-   Take a look at the built-in types or node module types to see if there is anything there similar to what you are looking for.

## Conclusions

-   Structural subtyping system -> Compatibility achieved by comparing properties
-   Multiple types of Type Definitions -> Know when to use each and why

## Reference

-   [Typescript Jumpstart Book](https://angular-university.io/ebook/EBOOK_TYPESCRIPT?utm=fb-ts-eb&grpp=f)
-   [Typescript related videos](https://blog.angular-university.io/why-typescript-video-list/)
-   [The Typescript Handbook](https://www.typescriptlang.org/docs/handbook)

[^1]: Word of advise, use it the least possible
[^2]: Always try to choose packages with built-in types and use them via Type Inference
[^3]: They are turned off by default because of backwards compatibility with part of the existing ecosystem
