# Introduction to HTML Email

## Overview

-   More than 80 email clients that cannot be validated with regular web development tools like the [Markup Validation Service](https://validator.w3.org/)
-   Some clients are even trickier like Outlook which renders the markup with word, which is not pretty good for the task

## Best practices

-   The best approach to ensure responsiveness across the clients is to use `HTML tables` for most of the clients and `Ghost Tables` for Outlook
-   Design for mobile users and with a `max-width` of `600px`
-   Using safe fonts for Outlook (like `sans-serif`) and Google Fonts for the other ones
-   Use padding instead margin
-   Test a lot using validators like [Email on Acid](https://www.emailonacid.com)
-   Accessibility best practices
    -   GIFs instead videos (have more support)
    -   Dark mode
    -   Fallback images for non-playable content
-   HTML boilerplate structure for email templates

    ```HTML
    <!-- Best doctype for email templates -->
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" lang="en">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
        <!--Edge support -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <!--Responsive -->
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- Darkmode support -->
        <meta name="color-scheme" content="light dark">
        <meta name="supported-color-schemes" content="light dark">
        <!-- Useful when rendering in a browser, outside of the email client -->
        <title>HTML Email Template Boilerplate</title>
        <!--  -->
        <style type="text/css">
            /* Googel Font for clients other than Outlook */
            @import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700&display=swap');
            /* Media queries for responsiveness */
            @media screen and (max-width: 599.98px) {}
            @media screen and (max-width: 399.98px) {}
            /* Custom Dark Mode Colors */
            @media (prefers-color-scheme: dark) {}
        </style>
    </head>
    ```

## Resources

-   [Email Client Market Share](https://www.litmus.com/email-client-market-share/)
-   [Email Client Statistics 2022](https://www.litmus.com/blog/email-client-market-share-april-2022/) (check for updates in the future)
