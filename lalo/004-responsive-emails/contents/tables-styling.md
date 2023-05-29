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
-   Buttons need to be anchors and have a border to be displayed correctly in Outlook
    ```HTML
    <tr>
        <td align="center">
            <table
                class="darkmode-transparent"
                cellpadding="0"
                cellspacing="0"
                role="presentation"
            >
                <tr
                    style="border-radius: 10px"
                    bgcolor="#eff8fe"
                >
                    <a
                        href="#"
                        target="_blank"
                        style="
                            font-size: 17px;
                            font-weight: bold;
                            text-decoration: none;
                            color: #1e5d7b;
                            background-color: #eff8fe;
                            border: 1px solid
                                #eff8fe;
                            border-radius: 10px;
                            padding: 12px 20px;
                            display: inline-block;
                        "
                        >VIEW DEMO</a
                    >
                </tr>
            </table>
        </td>
    </tr>
    ```
-   Two column layouts need to have nested ghost tables and to control the spacing between the elements (check widths and paddings)

```HTML
<tr>
    <td style="padding: 35px 0 30px 0">
        <table
            width="100%"
            style="border-spacing: 0"
            role="presentation"
        >
            <tr>
                <td
                    class="two-columns"
                    style="
                        padding: 0;
                        font-size: 0;
                        text-align: center;
                    "
                >
                    <!--[if (gte mso 9)|(IE)]>
                        <table
                            width="100%"
                            style="border-spacing: 0;"
                            role="presentation"
                        >
                        <tr>
                        <td
                            width="300"
                            valign="top"
                            style="padding: 0;"
                        >
                    <![endif]-->
                    <table
                        class="column"
                        style="
                            border-spacing: 0;
                            vertical-align: top;
                            width: 100%;
                            max-width: 300px;
                            display: inline-block;
                        "
                        role="presentation"
                    >
                        <!-- vertical-align: top; and display: inline-block; are key players to ensure the columns to display properly -->
                        <tr>
                            <td
                                class="padding"
                                style="padding: 20px"
                            >
                                <table
                                    class="content"
                                    style="
                                        border-spacing: 0;
                                        text-align: left;
                                    "
                                    role="presentation"
                                >
                                    <tr>
                                        <td
                                            style="
                                                background-color: #fafdfe;
                                                padding: 20px
                                                    0;
                                                text-align: center;
                                            "
                                        >
                                            <a
                                                href="#"
                                                target="_blank"
                                            >
                                                <img
                                                    alt="Man"
                                                    src="https://i.ibb.co/Tmg3qbV/man-teal.jpg"
                                                    width="260"
                                                    style="
                                                        max-width: 260px;
                                                        border-radius: 8px;
                                                    "
                                                    border="0"
                                                />
                                            </a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td
                                            style="
                                                padding: 10px
                                                    10px
                                                    20px
                                                    10px;
                                            "
                                        >
                                            <p
                                                style="
                                                    font-size: 17px;
                                                    font-weight: bold;
                                                "
                                            >
                                                Build
                                                Responsive
                                                Emails
                                            </p>
                                            <p
                                                style="
                                                    font-size: 15px;
                                                    line-height: 20px;
                                                "
                                            >
                                                Responsive
                                                HTML Email
                                                Templates
                                                that you can
                                                build around
                                                to master
                                                email
                                                development.
                                            </p>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td
                                            align="left"
                                            style="
                                                padding-left: 10px;
                                            "
                                        >
                                            <table
                                                border="0"
                                                cellpadding="0"
                                                style="
                                                    border-spacing: 0;
                                                "
                                                role="presentation"
                                            >
                                                <td
                                                    align="center"
                                                >
                                                    <table
                                                        class="darkmode-transparent"
                                                        cellpadding="0"
                                                        cellspacing="0"
                                                        role="presentation"
                                                    >
                                                        <tr
                                                            style="
                                                                border-radius: 10px;
                                                            "
                                                            bgcolor="#1e5d7b"
                                                        >
                                                            <a
                                                                href="#"
                                                                target="_blank"
                                                                style="
                                                                    font-size: 16px;
                                                                    font-weight: bold;
                                                                    text-decoration: none;
                                                                    color: #fff;
                                                                    background-color: #1e5d7b;
                                                                    border: 1px
                                                                        solid
                                                                        #1e5d7b;
                                                                    border-radius: 10px;
                                                                    padding: 10px
                                                                        25px;
                                                                    display: inline-block;
                                                                "
                                                                >HTML
                                                                Email</a
                                                            >
                                                        </tr>
                                                    </table>
                                                </td>
                                            </table>
                                        </td>
                                    </tr>
                                </table>
                            </td>
                        </tr>
                    </table>
                    <!--[if (gte mso 9)|(IE)]>
                        </td>
                        <td
                            width="300"
                            valign="top"
                            style="padding: 0;"
                            role="presentation"
                        >
                    <![endif]-->
                    <table
                        class="column"
                        style="
                            border-spacing: 0;
                            vertical-align: top;
                            width: 100%;
                            max-width: 300px;
                            display: inline-block;
                        "
                        role="presentation"
                    >
                        <tr>
                            <td
                                class="padding"
                                style="padding: 20px"
                            >
                                <table
                                    class="content"
                                    style="
                                        border-spacing: 0;
                                        text-align: left;
                                    "
                                    role="presentation"
                                >
                                    <tr>
                                        <td
                                            style="
                                                background-color: #fafdfe;
                                                padding: 20px
                                                    0;
                                                text-align: center;
                                            "
                                        >
                                            <a
                                                href="#"
                                                target="_blank"
                                            >
                                                <img
                                                    alt="Man"
                                                    src="https://i.ibb.co/nQn29Sg/woman-teal.jpg"
                                                    width="260"
                                                    style="
                                                        max-width: 260px;
                                                        border-radius: 8px;
                                                    "
                                                    border="0"
                                                />
                                            </a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td
                                            style="
                                                padding: 10px
                                                    10px
                                                    20px
                                                    10px;
                                            "
                                        >
                                            <p
                                                style="
                                                    font-size: 17px;
                                                    font-weight: bold;
                                                "
                                            >
                                                Create
                                                Custom
                                                Designs
                                            </p>
                                            <p
                                                style="
                                                    font-size: 15px;
                                                    line-height: 20px;
                                                "
                                            >
                                                Responsive
                                                HTML Email
                                                Templates
                                                that you can
                                                build around
                                                to master
                                                email
                                                development.
                                            </p>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td
                                            align="left"
                                            style="
                                                padding-left: 10px;
                                            "
                                        >
                                            <table
                                                border="0"
                                                cellpadding="0"
                                                style="
                                                    border-spacing: 0;
                                                "
                                                role="presentation"
                                            >
                                                <td
                                                    align="center"
                                                >
                                                    <table
                                                        class="darkmode-transparent"
                                                        cellpadding="0"
                                                        cellspacing="0"
                                                        role="presentation"
                                                    >
                                                        <tr
                                                            style="
                                                                border-radius: 10px;
                                                            "
                                                            bgcolor="#1e5d7b"
                                                        >
                                                            <a
                                                                href="#"
                                                                target="_blank"
                                                                style="
                                                                    font-size: 16px;
                                                                    font-weight: bold;
                                                                    text-decoration: none;
                                                                    color: #fff;
                                                                    background-color: #1e5d7b;
                                                                    border: 1px
                                                                        solid
                                                                        #1e5d7b;
                                                                    border-radius: 10px;
                                                                    padding: 10px
                                                                        25px;
                                                                    display: inline-block;
                                                                "
                                                                >Get
                                                                Started</a
                                                            >
                                                        </tr>
                                                    </table>
                                                </td>
                                            </table>
                                        </td>
                                    </tr>
                                </table>
                            </td>
                        </tr>
                    </table>
                    <!--[if (gte mso 9)|(IE)]>
                        </td>
                        </tr>
                        </table>
                    <![endif]-->
                </td>
            </tr>
        </table>
    </td>
</tr>
```

## Resources

-   [Outlook conditioning](https://stackoverflow.design/email/base/mso/)
