# Dark Mode

-   It needs to have all the tags that allows the document to be rendered as dark-mode

    ```HTML
    <meta name="color-scheme" content="light dark">
    <meta name="supported-color-schemes" content="light dark">
    ```

-   And add the styles (this can be commented if you need to deactivate it)
    ```CSS
    :root {
        color-scheme: light dark;
        supported-color-schemes: light dark;
    }
    @media (prefers-color-scheme: dark) {
        body, center, table {
            background: #2d2d2d!important;
            color: #ffffff!important;
        }
        .darkmode-transparent {
            background-color: transparent!important;
        }
    }
    ```
-   Specific items need to be handled inline
