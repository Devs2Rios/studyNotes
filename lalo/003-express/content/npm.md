# NPM

-   The node package manager comes with node
    -   Solutions for different problems that we might had in the past
-   An infinite world of packages to use within our projects

    -   Local installation of a package `npm install some-package`
    -   Global installation of a package `sudo npm install -g some-package`
        -   `sudo` comes for super do and it's a way to authorize admin privileges
        -   Rule of thumb, it's better to manage the packages locally
        -   There's a command called `npx` which allows to execute a package without installing it, which is a better alternative then the global install
    -   Uninstall with `npm uninstall some-package`
    -   A project with packages will need to have a `package.json` file

        -   Create it by using the following methods in your root directory
            -   `npm init` (step by step)
            -   `npm init -y` (default values)
            -   Manually
        -   Structure

            ```JSON
            {
                "name": "test",
                "version": "1.0.0",
                "description": "Test project",
                "main": "app.js",
                "scripts": {
                    "test": "echo \"Error: no test specified\" && exit 1"
                },
                "author": "Lalo",
                "license": "MIT",
                "dependencies": {
                    "express": "^4.18.2"
                }
            }

            ```

            -   Dependencies are the packages installed for our projects
            -   Dev dependencies are dependencies that are only required in development environment and they can be skipped on production

                -   `npm install some-package -D` or `npm install some-package --save-dev`

                    ```JSON
                    {
                        "name": "test",
                        "version": "1.0.0",
                        "description": "Test project",
                        "main": "app.js",
                        "scripts": {
                            "test": "echo \"Error: no test specified\" && exit 1"
                        },
                        "author": "Lalo",
                        "license": "MIT",
                        "dependencies": {
                            "express": "^4.18.2"
                        },
                        "devDependencies": {
                            "nodemon": "^2.0.22"
                        }
                    }
                    ```

            -   Versions of dependencies and devDependencies are very important to ensure the functionality of the app
                -   They use Semantic versioning `0.0.0` Major changes, Minor changes, Patches
            -   Scripts are custom commands that we run in our environment

                -   A script to run the development environment

                    ```JSON
                    "scripts": {
                        "dev": "nodemon app.js"
                    },
                    ```

                    ```BASH
                    $ npm run dev
                    ```

        -   This file will be crucial when we're downloading projects from repositories, because the modules are skipped in the `.gitignore` file, which means that they're not uploaded

            ```BASH
            $ git clone some-repo
            $ cd some-repo
            some-repo $ npm install # We'll install the dependencies required for the project
            ```
