# Express Router

-   Middleware function in `express.js` that allows you to create modular, mountable route handlers
-   The main advantage is that it makes the logic of the server easier to read and maintain
-   Check this example with the users route logic separated from the app logic

    ```JS
    // ./routes/users.js
    const express = require('express'),
        sqlite3 = require('sqlite3').verbose(),
        router = express.Router(),
        dbPath = './database.db';

    router.use(express.json());

    router.get('/', (req, res) => {
        const db = new sqlite3.Database(dbPath);
        db.all('SELECT username FROM users', (err, rows) => {
            if (err) {
                res.status(500).json({ error: err.message });
                return;
            }
            db.close();
            const prettyJson = JSON.stringify(rows, null, 2);
            res.setHeader('Content-Type', 'application/json');
            res.status(200).send(prettyJson);
        });
    });

    router.post('/login', (req, res) => {
        const { username, password } = req.body,
            db = new sqlite3.Database(dbPath);
        db.get('SELECT * FROM users WHERE username = ?', [username], (err, row) => {
            if (err) {
                res.status(500).json({ error: err.message });
                return;
            }
            db.close();
            if (!row || row.password !== password) {
                res.status(401).json({
                    error: 'Username or password is incorrect',
                });
                return;
            }
            res.status(200).send(`Welcome back ${row.username}`);
        });
    });

    module.exports = router;
    ```

    ```JS
    // ./index.js
    const express = require('express'),
        morgan = require('morgan'),
        app = express(),
        port = 8080,
        users = require('./routes/users');

    app.use(morgan('tiny'));
    app.use('/users', users);

    app.get('/', (req, res) => {
        res.send('Hello World');
    });

    app.all('*', (req, res) => {
        res.status(404).send('Not Found');
    });

    app.listen(port, () => {
        console.log(`Listening on port ${port}`);
    });
    ```

-   We can make the app even easier to maintain by using controllers

    ```JS
    // ./controllers/users-controller.js
    const sqlite3 = require('sqlite3').verbose(),
        dbPath = './database.db';

    const getUsers = (req, res) => {
        const db = new sqlite3.Database(dbPath);
        db.all('SELECT username FROM users', (err, rows) => {
            if (err) {
                res.status(500).json({ error: err.message });
                return;
            }
            db.close();
            const prettyJson = JSON.stringify(rows, null, 2);
            res.setHeader('Content-Type', 'application/json');
            res.status(200).send(prettyJson);
        });
    };

    const login = (req, res) => {
        const { username, password } = req.body,
            db = new sqlite3.Database(dbPath);
        db.get('SELECT * FROM users WHERE username = ?', [username], (err, row) => {
            if (err) {
                res.status(500).json({ error: err.message });
                return;
            }
            db.close();
            if (!row || row.password !== password) {
                res.status(401).json({
                    error: 'Username or password is incorrect',
                });
                return;
            }
            res.status(200).send(`Welcome back ${row.username}`);
        });
    };

    module.exports = {
        getUsers,
        login,
    };
    ```

    ```JS
    // ./routes/users.js
    const express = require('express'),
        router = express.Router(),
        { getUsers, login } = require('../controllers/users-controller');

    router.use(express.json());
    router.get('/', getUsers);
    router.post('/login', login);

    module.exports = router;
    ```

    -   Now we can keep the logic from the requests separated from the routes and just importing and passing them ass callbacks
    -   Try the previous concepts in [this repo](https://github.com/Devs2Rios/express-router-example)

-   If a route is the same for several methods you can chain them

    ```JS
    router.route('/:id').put(editUser).delete(deleteUser);
    ```
