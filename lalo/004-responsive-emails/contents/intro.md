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

## Resources

-   [Email Client Market Share](https://www.litmus.com/email-client-market-share/)
-   [Email Client Statistics 2022](https://www.litmus.com/blog/email-client-market-share-april-2022/) (check for updates in the future)
