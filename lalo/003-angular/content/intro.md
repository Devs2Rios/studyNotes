# Intro

## How it works

-   The container of our web App is the `index.html` file inside `src/app/`
-   Our `app.component.html` has the data that is rendered into the `<app-root></app-root>` tag inside `index.js`
-   There is also a `app.component.ts` that contains the props and elements that can be used inside our component

    ```Ts
    import { Component } from '@angular/core';

    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.sass'],
    })
    export class AppComponent {
        title = 'EATangular'; // This can be used inisde app.component.html
    }
    ```

    ```HTML
    <!-- With this interpolation syntax -->
    <!-- you can pass the properties to your component -->
    <span>{{ title }} app is running!</span>
    ```

    -   This is a simple example, but you can also pass an object as property

        ```Ts
        export class AppComponent {
            data = { title: 'EATangular' };
        }
        ```

-   And finally you'll have a style file inside your component, this file will allow you to modify your components appearance, here's an example with a SASS file `app.component.sass`

    ```SASS
    $txt-color: #FFF
    $bg-color: #000

    input.demo
        color: $txt-color
        background-color: $bg-color
        font-size: 2rem

        &::placeholder
            color: $txt-color
    ```

## The key features of Angular Core

-   You can link properties with components by using this special syntax
    ```HTML
    <input [value]="data.title"/>
    ```
-   There's also a special syntax for events

    -   In your typescript file you'll define the functions to handle the event

        ```Ts
        export class AppComponent {
            data = { title: 'EATangular' };

            onKeyUp(str: string): void {
                // The title property is changed here
                this.data.title = str;
            }
        }
        ```

    -   And in the html file you'll link the event with the handler
        ```HTML
        <input
            class="demo"
            placeholder="Input"
            [value]="data.title"
            (keypress)="onKeyUp(currentInput.value)"
            #currentInput
        />
        ```
        -   Here the `#currentInput` will serve as reference and it will be read as argument for the keypress handler

-   These features are built with safety in mind, if an attacker wants to change our `.ts` file with inner HTML (like a `<script>` tag), the angular engine will scape the string so it won't allow the attack
