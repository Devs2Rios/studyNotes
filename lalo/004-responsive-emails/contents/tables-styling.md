# Tables and Styling

-   `border-spacing: 0;` is very important to avoid inner gaps between the elements
-   Always think in the `max-width: 600px`
-   Tables should have `margin: 0 auto;`
-   Never use `margin` use `padding` and `<br />` if you need a gap between several tables
-   If you have a complex column layout inside a table you can always use nested tables controlling the width of the tables

    ```HTML
    <table>
        <tr>
            <th style="padding: 20px">Name</th>
        </tr>
        <tr style="padding: 0">
            <table>
                <tr>
                    <td
                        style="
                            padding: 20px;
                            background-color: red;
                            width: 300px;
                        "
                        colspan="2"
                    >
                        Bill
                    </td>
                    <td
                        style="
                            padding: 20px;
                            background-color: green;
                            width: 300px;
                        "
                        colspan="2"
                    >
                        Bob
                    </td>
                </tr>
            </table>
        </tr>
        <tr style="padding: 0">
            <table>
                <tr>
                    <td
                        style="
                            padding: 20px;
                            background-color: red;
                            width: 200px;
                        "
                    >
                        Bill
                    </td>
                    <td
                        style="
                            padding: 20px;
                            background-color: green;
                            width: 200px;
                        "
                    >
                        Bob
                    </td>
                    <td
                        style="
                            padding: 20px;
                            background-color: yellow;
                            width: 200px;
                        "
                    >
                        Bart S
                    </td>
                </tr>
            </table>
        </tr>
    </table>
    ```

-   Check the [simple table example](../examples/01-simple-table/index.html)
-   I order to get better support from Microsoft Outlook you can target Outlook 2000 and Internet Explorer
    ```HTML
    <!--[if (gte mso 9)|(IE)]>
        <style type="text/css">
            body {background-color:#dde0e1!important;}
        </style>
    <![endif]-->
    ```
-   Centering uses the `<center>` tag, only valid for HTML template design
    ```HTML
    <center></center>
    ```

## Resources

-   [Outlook conditioning](https://stackoverflow.design/email/base/mso/)
