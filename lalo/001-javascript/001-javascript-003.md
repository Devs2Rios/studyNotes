# Developer Skills & Editor Setup

- Setup

  - Add Prettier extension to VS Code
  - default formatter `esbenp.prettier-vscode`
  - format on save `true`
  - toggle single quotes to `true` in the settings
  - select `avoid` in the Arrow Parens option
  - Add snippets
  - Go to `Code > Preferences > Configure User Snippets`
  - Write your snippets:
    ```JSON
    "Print to console": {
    "scope": "javascript,typescript",
    "prefix": "print",
    "body": ["console.log();"],
    "description": "Log output to console"
    }
    ```
  - Install [node.js](https://nodejs.org/en/)
  - Check which version of node you have `node -v`
  - NPM comes with node.js
  - Check which version of npm you have `npm -v`
  - Use a light server:
  - You can use a VS Extension
  - Or install it via NPM with the command `npm install live-server -g`
  - Run your server by using `live-server` on your working directory

- Developer mind
  - Goal
    - Realistic time based
    - Why are you learning? `Complement my career`
    - Imagine a project
    - Research technologies
  - Always understand the code by studying it and typing it
  - Reinforce knowledge
    - Use it
    - Take notes
    - Challenge yourself
      - [Codewars](https://www.codewars.com/)
    - Don't be in a hurry
  - Practice
    - Create your own challenges
    - Don't get stuck in "tutorial hell"
  - Write a lot and you'll be improving it
  - Refactor what you did
  - You'll never know everything so focus on your goal
  - Learn with other people and teach
  - Problem solver
    - Understand the problem
    - Divide and conquer
      - Break big problems into small steps
    - Do the necessary research
    - Write pseudocode before the actual code
  - Research tools, always ask the right questions
    - [MDN](https://developer.mozilla.org/en-US)
    - [StackOverflow](https://stackoverflow.com)
    - [Google](https://www.google.com)
  - Debugging
    - Bug: defect or problem in a computer program
      - Identify:
        - Discover the bug
        - Test software
        - Use reports
        - Check in contexts
      - Find:
        - Find the place where the bug is
      - Fix:
        - Correct the bug
      - Prevent:
        - Find it elsewhere
        - Write unit testing
    - Breakpoint:
      - useful console methods for debugging:
        ```JavaScript
        console.warn(); console.error(); console.table(object);
        ```
      - Chrome debugger:
        - `View > Developer > Inspect Element` or `⌘⌥C`
        - Go to sources and select the JavaScript file to debug
        - Add the desired breakpoints
        - Go step by step checking what's happening using `F9` or the step button
    - You can debug directly on VS Code by using `debugger;` before each breakpoint

