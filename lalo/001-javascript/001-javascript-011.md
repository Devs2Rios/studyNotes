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
    const section1 = document.querySelector('#section--1');
    const btnScrollTo = document.querySelector('.btn--scroll-to');

    // Old approach
    btnScrollTo.addEventListener('click', function (e) {
        const s1coords = section1.getBoundingClientRect(); // Returns the coordinates of the element relative to the viewport
        console.log(s1coords); // {left: ..., top: ..., right: ..., bottom: ...}
        console.log(e.target.getBoundingClientRect()); // Same as above
        console.log('Current scroll (X/Y)', window.pageXOffset, window.pageYOffset); // Current scroll position in pixels
        console.log(
            'height/width viewport',
            document.documentElement.clientHeight,
            document.documentElement.clientWidth
        ); // Viewport dimensions in pixels (they don't include the scroll bars)
        window.scrollTo({
            left: s1coords.left + window.pageXOffset, // x position relative to the document
            top: s1coords.top + window.pageYOffset, // y position relative to the document
            behavior: 'smooth', // smooth scroll
        }); // Smooth scroll to the coordinates, window.scrollTo(left, top) won't work with smooth scroll
    });

    // New Approach: Only works in modern browsers
    btnScrollTo.addEventListener('click', function (e) {
        section1.scrollIntoView({ behavior: 'smooth' });
    });
    ```

-   Types of Events and Event Handlers

    ```JavaScript
    const h1 = document.querySelector('h1');
    const alertEnter = () => {
        alert('You entered the heading!');
    };
    // Recommended way
    h1.addEventListener('mouseenter', alertEnter);
    // Removing the event listeners after 3 seconds
    setTimeout(() => h1.removeEventListener('mouseenter', alertEnter), 3000);
    // The old way
    h1.onmouseenter = alertEnter;
    ```

    ```HTML
    <!-- Older than old -->
    <h1 onclick="alert('HTML alert')">
    ```

-   Event Propagation: Bubbling and Capturing

    -   Events are triggered at the root of the document, this is called **capturing phase**
    -   The **target phase** is when events travel from the root to the element that catches them, passing through every parent of the node
    -   The **bubbling phase** is when the event is caught and sent back to the root

        ```JavaScript
        document.querySelector('.nav__links').addEventListener('click', function (e) {
            this.style.backgroundColor = ranColor(); // A click here will bubble the event up to the nav element.
        });
        document.querySelector('.nav').addEventListener('click', function (e) {
            this.style.backgroundColor = ranColor();
        });
        ```

        -   We can catch the origin of the event by using the target `e.target` and compare it with `e.currentTarget` if they are the same the the event occurs in the same element, if not the event was bubbled
        -   We can stop the bubbling by using `e.stopPropagation()`
        -   If we need to catch the event when capturing instead of bubbling, we can add the use capture argument to the event listeners `el.addEventListener('click', () => {}, true)`

-   Event Delegation: Implementing Page Navigation

    -   It's useful when we have a lot of elements that share some functionality, instead of using `forEach` we can delegate the function from the parent

        ```JavaScript
        // Select the parent element
        document.querySelector('.nav__links').addEventListener('click', function (e) {
            e.preventDefault();
            // Matching strategy
            if (e.target.classList.contains('nav__link')) {
                const id = e.target.getAttribute('href');
                document.querySelector(id).scrollIntoView({ behavior: 'smooth' });
            }
        });
        ```

-   DOM Traversing

    -   Useful when we need to select related elements

        ```JavaScript
        const h1 = document.querySelector('h1');

        // Downwards the parent
        console.log(h1.querySelectorAll('.highlight')); // Children with specific class
        console.log(h1.childNodes); // All children including whitespace
        console.log(h1.children); // Only direct children
        h1.firstElementChild.style.color = 'white'; // First child element
        h1.lastElementChild.style.color = 'white'; // Last child element

        // Upwards the parent
        console.log(h1.parentNode); // Parent node object if present
        console.log(h1.parentElement); // Element object representing parent element
        console.log(h1.closest('.header')); // Closest specific element

        // Siblings
        console.log(h1.previousElementSibling); // Previous sibling element
        console.log(h1.nextElementSibling); // Next sibling element
        console.log(h1.previousSibling); // Previous sibling node
        console.log(h1.nextSibling); // Next sibling node
        console.log(h1.parentElement.children); // All children of parent element
        ```

-   Building a Tabbed Component

    ```JavaScript
    tabsContainer.addEventListener('click', function (e) {
        const clicked = e.target.closest('.operations__tab');

        // Guard clause
        if (!clicked) return;

        // Remove active classes
        tabs.forEach(t => t.classList.remove('operations__tab--active'));
        tabsContent.forEach(c => c.classList.remove('operations__content--active'));

        // Activate tab
        clicked.classList.add('operations__tab--active');

        // Activate content area
        document
            .querySelector(`.operations__content--${clicked.dataset.tab}`)
            .classList.add('operations__content--active');
    });
    ```

-   Parsing Arguments to Event Handlers

    -   Useful when some logic is shared between callbacks

        ```JavaScript
        const handleHover = function (e) {
            if (e.target.classList.contains('nav__link')) {
                const link = e.target;
                const siblings = link.closest('.nav').querySelectorAll('.nav__link');
                const logo = link.closest('.nav').querySelector('img');
                siblings.forEach(el => {
                    if (el !== link) el.style.opacity = this;
                });
                logo.style.opacity = this;
            }
        };
        // Passing "argument" into handler
        nav.addEventListener('mouseover', handleHover.bind(0.5));
        nav.addEventListener('mouseout', handleHover.bind(1));
        ```

-   Implementing a Sticky Navigation: The Scroll Event

    ```JavaScript
    // Bad performance on older computers and mobiles
    const initialCoords = section1.getBoundingClientRect();
    window.addEventListener('scroll', function () {
        if (window.scrollY > initialCoords.top) nav.classList.add('sticky');
        else nav.classList.remove('sticky');
    });
    ```

-   A Better Way: The Intersection Observer API

    -   Allows our code to observe changes

        ```JavaScript
        // Define a function to be executed when the IntersectionObserver triggers
        const stickyNav = function (entries) {
            // Get the first entry from the array of entries
            const [entry] = entries;

            // If the observed element is not intersecting (i.e., not visible in the viewport)
            if (!entry.isIntersecting) {
                // Add the 'sticky' class to the navigation element
                nav.classList.add('sticky');
            } else {
                // Remove the 'sticky' class from the navigation element
                nav.classList.remove('sticky');
            }
        };

        // Create a new IntersectionObserver instance
        const headerObserver = new IntersectionObserver(stickyNav, {
            // Use the entire viewport as the root for intersection checking
            root: null,
            // Trigger the callback function when the observed element starts intersecting
            threshold: 0,
            // Add a negative root margin to adjust the trigger point
            rootMargin: `-${nav.getBoundingClientRect().height}px`,
        });

        // Start observing the 'header' element with the IntersectionObserver
        headerObserver.observe(header);
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
