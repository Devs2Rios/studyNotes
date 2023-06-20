# Media Queries

-   Media queries are commonly applied to column selectors that change their behavior when the screen shrinks
-   The gray background disappears on 599.98px
-   We usually have two media queries:

    -   Medium (mostly tablet and non-wide desktops)

        ```CSS
        @media screen and (max-width: 599.98px) {
            .banner {
                height: auto !important;
                padding-top: 40px !important;
                padding-bottom: 60px !important;
            }

            .two-columns .padding,
            .two-third-columns .padding,
            .three-columns .padding {
                padding-right: 0 !important;
                padding-left: 0 !important;
            }

            img.two-col-img {
                width: 300px !important;
                max-width: 300px !important;
            }

            .two-third-columns .padding.first {
                padding-bottom: 0 !important;
            }

            .two-third-columns .padding.last {
                padding-top: 0 !important;
            }

            img.one-third-col-img,
            img.three-col-img-last {
                width: 200px !important;
                max-width: 200px !important;
            }

            .two-third-columns .content {
                text-align: center !important;
            }
        }
        ```

    -   Small (mostly mobile)

        ```CSS
        @media screen and (max-width: 399.98px) {
            @media screen and (max-width: 399.98px) {
                .banner {
                    padding-top: 10px !important;
                    padding-bottom: 40px !important;
                }

                img.three-col-img {
                    width: 200px !important;
                    max-width: 200px !important;
                }
            }
        }
        ```

    -   Check them in action [here](../examples/02-starter-example/)
