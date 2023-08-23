# Advanced DOM and Events

-   How the DOM Really Works

    -   The DOM is the interface between the browser
    -   Allows to create, modify and delete HTML elements
    -   The DOM tree is generated from an HTML element
    -   The DOM has several methods and properties to interact with it, like `getQuerySelector()`
    -   Every element in the DOM is a node

        -   Every child inherits methods and properties from their parent node
        -   Nodes have event listeners like `click` and they're accessed with special methods

            ```JavaScript
            const callback = () => console.log('clicked');
            // It will print clicked on every click
            myNode.addEventListener('click', callback);
            myNode.removeEventListener('click', callback); // Only if you need to remove the listener
            ```

    -   `window` and `document` are special elements in the DOM and they're globally available

        -   To select the actual document you need to select it:

            ```JavaScript
            window // Window {window: Window, self: Window, ...} not a node
            document // The whole website
            document.documentElement // Selects the <html> node of the website
            ```

-   Selecting, Creating and Deleting Elements

    -   Selecting

        ```JavaScript
        // Select an element
        document.querySelector('.modal'); // Selects the first element with modal class
        document.querySelectorAll('.modal'); // Selects all the elements with modal class
        // Selection with more specificity (no selectors like . or # needed)
        document.getElementById('some-id'); // No # needed
        document.getElementsByClassName('some-class'); //
        document.getElementsByName('some-name');
        document.getElementsByTagName('some-tag'); // Returns a live collection
        // There are more, check the docs for them https://developer.mozilla.org/docs/Web/API/Document
        ```

    -   Creating

        ```JavaScript
        const myEl = document.createElement('div'); // Creates the DOM element
        myEl.textContent = 'Hello World'; // Adds text to the element
        myEl.innerHTML = '<h1>Hello World</h1>'; // Adds HTML to the element
        document.body.prepend(myEl); // Appends the element to the body before the other children
        document.body.append(myEl); // Appends the element to the body after the other children
        // Elements can only be in one place at a time, the previous code will only reflect the append
        document.body.prepend(myEl.cloneNode(true)); // This will place the prepend correctly
        // To add an element outside a node we can use before and after
        const header = document.querySelector('header');
        header.before(myEl.cloneNode(true)); // Adds the element before the node
        header.after(myEl.cloneNode(true)); // Adds the element after the node
        ```

    -   Delete

        ```JavaScript
        myEl.addEventListener('click', function (e) {
            this.remove(); // This is the node itself and it'll disappear when the user clicks on it
            // Older versions of JS have a removeChild approach
            this.parentElement.removeChild(this)
        });
        ```

-   Styles, Attributes and Classes

    -   Styles

        ```JavaScript
        myEl.style.backgroundColor = 'red';
        myEl.style.width = '2rem';
        // Styles can be checked with console.log(myEl.style);
        // but this doesn't have the new styles,
        // for that you'll need to get the computed styles
        console.log(getComputedStyle(myEl));// CSSStyleDeclaration {0: 'accent-color', ...}
        // the previous approach is very useful to get actual computed values like width, or height
        console.log(getComputedStyle(myEl).width); // 983px == 100vw
        ```

    -   Attributes

        ```JavaScript
        // Changing Root color variables
        document.documentElement.style.setProperty('--color-primary', 'red');
        const logo = document.getElementById('logo');
        // Get specific attributes
        console.log(logo.className); // nav__logo
        console.log(logo.getAttribute('alt')); // Bankist logo
        console.log(logo.src); // http://localhost:3000/img/logo.png -> Absolute path
        console.log(logo.getAttribute('src')); // img/logo.png -> Relative as in the element prop
        // src behavior is the same as in href attributes
        // Set specific attributes
        logo.setAttribute('aria-label', 'Beautiful minimalist logo');
        // Data attributes
        console.log(logo.dataset); // { smallDescription: "The brand logo" }
        console.log(logo.dataset.smallDescription); // The brand logo
        // This is the html from the element
        // <img src="img/logo.png" alt="Bankist logo" class="nav__logo" id="logo" data-small-description="The brand logo" />
        ```

    -   Classes

        ```JavaScript
        logo.classList.add('c', 'd'); // Adds classes to the element
        logo.classList.remove('c', 'd'); // Removes classes from the element
        logo.classList.toggle('c'); // Toggles the class on and off
        logo.classList.contains('c'); // true
        // Overwrite all the classes
        logo.className = 'nav__logo';
        ```

-   Implementing Smooth Scrolling

    ```JavaScript

    ```

-   Types of Events and Event Handlers

    ```JavaScript

    ```

-   Event Propagation: Bubbling and Capturing

    ```JavaScript

    ```

-   Event Delegation: Implementing Page Navigation

    ```JavaScript

    ```

-   DOM Traversing

    ```JavaScript

    ```

-   Building a Tabbed Component

    ```JavaScript

    ```

-   Parsing Arguments to Event Handlers

    ```JavaScript

    ```

-   Implementing a Sticky Navigation: The Scroll Event

    ```JavaScript

    ```

-   A Better Way: The Intersection Observer API

    ```JavaScript

    ```

-   Revealing Elements on Scroll

    ```JavaScript

    ```

-   Lazy Loading Images

    ```JavaScript

    ```

-   Building a Slider Component

    ```JavaScript

    ```

-   Lifecycle DOM Events

    ```JavaScript

    ```

-   Efficient Script Loading: defer and async

    ```JavaScript

    ```
