# Angular Core Deep Dive

## Environment

-   Node JS
-   Text editor like VS Code
-   Angular CLI
    -   `npm install -g @angular/cli`
    -   `ng --help`
    -   Now you can create a new app
        -   `ng new angular-app`
        -   When it's done you can serve your app with the script `start` of your `package.json`
            ```bash
            npm start
            ```
            ```JSON
            "scripts": {
                "start": "ng serve",
            },
            ```
        -   Go to your page at `http://localhost:4200/` and start hacking
-   TypeScript

## Content

1. [Typscript](./content/typescript.md)
2. [Intro](./content/intro.md)
3. [Custom Components](./content/custom-components.md)
4. [Directives](./content/directives.md)
5. [Built-In Pipes](./content/built-in-pipes.md)
6. [Local Template Querying](./content/local-template-querying.md)
