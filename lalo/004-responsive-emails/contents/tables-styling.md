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
-   All images except GIFs need the property `border="0"` for some old clients
    ```HTML
    <img
        alt="Instagram"
        title="Instagram"
        src="https://i.ibb.co/x8G1NMz/circle-instagram.png"
        width="32"
        border="0"
    />
    ```
-   For GIFs the best approach is to use them as background
    -   GIFs don't work on Outlook, you'll need to use Vector Markup Language as fallback
        ```HTML
        <tr>
            <td
                background="https://i.ibb.co/hMhVbjT/stats2.gif"
                width="600"
                height="332"
                style="background-position: center top"
            >
                <!--[if (gte mso 9)|(IE)]>
                    <v:rect
                        xmlns:v="urn:schemas-microsoft-com:vml"
                        fill="true"
                        stroke="false"
                        style="width: 600px; height: 332px;"
                    >
                    <v:fill type="title" src="https://i.ibb.co/hMhVbjT/stats2.gif"/>
                    <v:textbox inset="0,0,0,0">
                <![endif]-->
                <!--[if (gte mso 9)|(IE)]>
                    </v:textbox>
                    </v:rect>
                <![endif]-->
            </td>
        </tr>
        ```

## Resources

-   [Outlook conditioning](https://stackoverflow.design/email/base/mso/)
