# HTML & CSS Crash Course

- HTML
  - HyperText Markup Language
  - Semantic HTML is a way to give the more accurated tag to an element so it can be mor readable
  - Structure:
    ```HTML
    <html>
      <head>
        <title>Example</title>
      </head>
      <body>
        <h1>Heading example</h1>
        <p>Paragraph example</p>
        <!-- Comment example -->
      </body>
    </html>
    ```
  - Attributes: `<a href="https://www.some.link"></a>`
  - Inline and block elements work together:
    - Inline `<span></span>` displays inside anoder block
    - Block `<p></p>` displays as a block inside html
  - Classes
    - Attribute that defines the name of one or several elements in order to style them
      ```HTML
      <h1 class="inverted">This is an inverted color heading</h1>
      <p class="inverted">This is an inverted color paragraph</p>
      <!-- Classes can be used several times -->
      ```
  - IDs
    - Special attribute that gives an element an unique identifier
      ```HTML
      <p id="special-paragraph">Special</p>
      <!-- Unique element -->
      ```
- CSS

  - Cascading Style Sheets
  - It's the way to give style to HTML elements
  - Structure
    - Inside HTML (not recommended)
      ```HTML
      <style>
        body {
          background-color: white;
        }
      </style>
      ```
    - Or in a .css file linked to the html
      ```HTML
      <!-- index.html -->
      <head>
        <link href="style.css" rel="stylesheet">
      </head>
      ```
      ```CSS
      /* style.css */
      body {
        background-color: white;
      }
      ```
  - Inheritance
    - Child elements inherit some properties from their parents, for example if you add `font-family: Arial;` into `body {}` all body's children will have the same font-family
    - Some properties like border are not inherited
  - Syntax
    - Regular selector `p {color: black;}`
    - ID selector `#my-ID {font-size: 10px;}`
    - Class selector `.my-class {background-color: blue;}`
    - Child selector `#my-ID code {font-family: Menlo;}`
  - Box model:
    |Element|Description|
    |---|---|
    |**Content** |Text, images, etc.|
    |**Padding** |Transparent area around the content inside the box|
    |**Border** |Around the padding and the content|
    |**Margin** |Space between boxes|
    |**Fill Area**|Area that gets filled with background color or image|

    ```

       Margin
        --------------------------------
       |                                |
       |      Padding                   |
       |                                |
       |       W   i   d   t   h        |
       |       -----------------  H     |
       |      |                 | e     |
       |      |     CONTENT     | i     |
       |      |     *******     | g     |
       |      |                 | h     |
       |       -----------------  t     |
       |      Border:                   |
       |      Line around the box       |
       |      padding and content.      |
       |                                |
       |                                |
        --------------------------------

    ```

    - For better control of your box size you can use `* {box-sizing: border-box;}` which will allow you to define widths and heights considering the paddings and margins

  - For reset properties globaly you'll need to use the asterix which goes for all elements `* {margin: 0;}`
