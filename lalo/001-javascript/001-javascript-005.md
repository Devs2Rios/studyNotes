# JavaScript in the Browser: DOM and Events Fundamentals

- The DOM (Document Object Model)
  - Structured representation of HTML documents
  - Allows JS to access HTML elements and manipulate them
  - JS interaction with the DOM reference is in WEB APIs
- Acces to an HTML node
  - Access by query selector `document.querySelector('.my-class');`
    - Query selector only acces the first incidence, if you want to get all just use `.querySelectorAll()`
    - The `.` is only used when you are looking for a class selector, other methods like `myNode.classList.remove('my-class-1', 'my-class-2');`
  - Access by ID
    ```JavaScript
    document.getElementByID('my-ID'); // Faster
    document.querySelector('#my-ID'); // Easier
    ```
  - You can modify properties of the element
    ```JavaScript
    document.querySelector('.my-class').textContent = 'New content';
    document.querySelector('#my-ID').textContent = 'New content';
    ```
  - Events
    - An event is something that happends in te page like a mouse movement
    - Every node is able to hold an `addEventListener()` method
    - Click example
      ```JavaScript
      const myNode = document.querySelector('.my-class');
      const myFunction = () => return true;
      myNode.addEventListener('click', function() {return true});
      myNode.addEventListener('click', myFunction);
      ```
