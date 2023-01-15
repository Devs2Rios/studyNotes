# Local Template Querying

-   When we need more complex conditionals to represent a component `<ng-component>` might not be enough, here's when `@ViewChild()` comes in handy

    ```TS
    // App component
    import { Component, ViewChild } from '@angular/core';
    import { SomeComponent } from './some.component.component'

    ...

    export class AppComponent {
        elements: [...ELEMENTS]

        @ViewChild(SomeComponent)
        selection: SomeComponent;

        onElSelected(el: SomeElement) {
            // Do something with the element
        }
    }
    ```

    ```HTML
    <!-- App -->
    <some-component
        (elSelected)="onElSelected($event)"
        [selection]="elements[0]"
    >
    </some-component>
    ```
