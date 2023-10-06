# JavaScript from Zero to Expert

## Intro

> -   Web development basics
>     -   HTML(Nouns) | CSS(Adjectives) | JS(Verbs)
>     -   Separation of concerns - Every file separated, not in the HTML
> -   Test with Console
>     -   Brave or Chrome - `⌘⌥J`
>     -   Safari - `⌘⌥C`
> -   JavaScript
>     -   High-Level - Not complex stuff (memory) worries
>     -   Object-Oriented - Data based on objects
>     -   Multi-Paradigm - Use different styles of programming
>     -   Programming language - Instruct computer to do things
>     -   ES5, ES6+
>         -   1995 - Mocha, first version of JavaScript created in just 10 days
>             -   A language to create interactive sites
>         -   1996
>             -   It has nothing to do with Java
>             -   Changes to LiveScript and to JavaScript to attract Java developers
>             -   Microsoft launches IE and copies JavaScript into JScript
>         -   1997 - ECMA releases ECMAScript 1 (ES1), the first standard for JavaScript
>         -   2009 - ES5 (ECMAScript 5) was released with a lot of new features
>         -   2015 - ES6 (ECMAScript 2015) was released (biggest update)
>             -   Changes to an annual release cycle
>     -   Don't break the web
>         -   Older code is still working
>         -   It's very buggy but still used
>     -   Development - Use the latest Chrome
>     -   Production - Transpile and polyfill the code to make it compatible with older browsers
>     -   ESNext - Future versions

## Content

-   [JavaScript1](./001-javascript-001.md)
-   [JavaScript2](./001-javascript-002.md)
-   [Developer Skills & Editor Setup](./001-javascript-003.md)
-   [HTML & CSS Crash Course](./001-javascript-004.md)
-   [JavaScript in the Browser: DOM and Events Fundamentals](./001-javascript-005.md)
-   [How JavaScript Works Behind the Scenes](./001-javascript-006.md)
-   [Data Structures, Modern Operators and Strings](./001-javascript-007.md)
-   [A Closer Look at Functions](./001-javascript-008.md)
-   [Working With Arrays](./001-javascript-009.md)
-   [Numbers, Dates, Intl and Timers](./001-javascript-010.md)
-   [Advanced DOM and Events](./001-javascript-011.md)
-   [Object-Oriented Programming (OOP) With JavaScript](./001-javascript-012.md)
-   [Asynchronous JavaScript: Promises, Async/Await, and AJAX](./001-javascript-013.md)
-   [Modern JavaScript Development: Modules, Tooling, and Functional](./001-javascript-014.md)

## General purpose tips

### Planning a project

1. User stories: describe the project from an user point of view
    - As an user I want to...
2. Features: Determine the features needed from the user stories
    - Add a queue to allow the user...
3. Flowchart: To describe the features
    - To define the application workflow
4. Architecture: How to build the project based on features
    - To determine how to organize resources
5. Development: Hands on the project

### All purpose tips

-   `localStorage` is just useful fo small amounts of data like tokens
-   Architecture
    -   In general:
        -   Helps keep the code clean and organized
        -   Allows better maintainability
        -   Prepares the project to be scaled
    -   We can create our own architecture, use a well-stablish pattern like MVC, or use a framework like React
    -   Component of any architecture
        -   Business logic: Code that solves the business problems
        -   State: All the data from the application
        -   HTTP library: Responsible of getting and sending requests
        -   Application logic (router): Implementation of the application itself
        -   Representation logic (UI Layer): Visible part of the application (displays the state)
    -   Examples:
        -   MVC
            -   Model: Business logic, state, HTTP library
            -   Controller: Application logic
            -   View: Presentation logic
-   Software design patterns

    -   Publisher-subscriber pattern
        -   Events are handled in the controller to keep the application logic there
        -   Events are listened in te view to remove DOM elements in the controller

-   Debugging by writing `debugger;` will create a breakpoint on the browser's developer tools
-   Some recommendations on documentation (JS Docs)

    ```JS
    import { icons } from '../../utils';

    /**
     * Represents a view for rendering data in a web application.
     */
    export class View {
      /**
       * Creates an instance of the View class.
       */
      constructor() {
        this.#markupCallback = () => {};
        this.#parentElement = null;
        this.#data = null;
        this.actionHandlers = {};
      }

      /**
       * Renders the data in the view.
       * @param {any} data - The data to be rendered.
       */
      render(data) {
        this.#data = data;
        this.clear();
        const markup = this.#generateMarkup();
        this.#parentElement.insertAdjacentHTML('afterbegin', markup);
      }

      /**
       * Updates the view with new data.
       * @param {any} data - The new data to update the view with.
       */
      update(data) {
        // ... method implementation ...
      }

      /**
       * Sets the parent element for rendering.
       * @param {HTMLElement} parentElement - The parent HTML element.
       */
      setParentElement(parentElement) {
        this.#parentElement = parentElement;
      }

      /**
       * Sets a callback function to generate markup for rendering.
       * @param {Function} markupCallback - A callback function to generate markup.
       */
      setMarkupCallback(markupCallback) {
        this.#markupCallback = markupCallback;
      }

      /**
       * Registers event handlers for rendering events.
       * @param {string[]} events - An array of event names to listen for.
       * @param {Function} callback - The callback function to execute when events occur.
       */
      renderHandler(events, callback) {
        events.forEach(event => window.addEventListener(event, callback));
      }

      /**
       * Displays a loading spinner in the view.
       */
      loadSpinner() {
        // ... method implementation ...
      }

      /**
       * Renders a message in the view.
       * @param {string} message - The message to display.
       * @param {boolean} isError - Indicates if the message is an error message (default is false).
       */
      renderMessage(message, isError = false) {
        // ... method implementation ...
      }

      /**
       * Clears the content of the parent element.
       */
      clear() {
        this.#parentElement.innerHTML = '';
      }

      /**
       * Generates the HTML markup based on the provided data and callback.
       * @returns {string} - The generated HTML markup.
       * @private
       */
      #generateMarkup() {
        return this.#markupCallback(this.#data);
      }
    }
    ```
