# Local Template Querying

## ViewChild

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

-   Multiple view query configuration

    ```TS
    // App component
    import { Component, ViewChild, ElementRef } from '@angular/core';
    import { SomeComponent } from './some.component.component'

    ...

    export class AppComponent {
        elements: [...ELEMENTS]

        @ViewChild('htmlRef1')
        selection1: SomeComponent;

        // With this configuration the app will read the element as ElementRef
        @ViewChild('htmlRef2', {read: ElementRef})
        selection2: ElementRef;

        // Inject an html element reference
        @ViewChild('htmlRef3')
        contentDiv: ElementRef;

        onElSelected(el: SomeElement) {
            // Do something with the elements
        }
    }
    ```

    ```HTML
    <!-- App -->
    <some-component #htmlRef1
        (elSelected)="onElSelected($event)"
        [selection]="elements[0]"
    >
    </some-component>
    <some-component #htmlRef2
        (elSelected)="onElSelected($event)"
        [selection]="elements[1]"

    >
    <some-component #htmlRef3
        (elSelected)="onElSelected($event)"
        [selection]="elements[1]"

    >
    </some-component>
    ```

-   To understand the moment when the child element is rendered we could use the lifecycle hook `AfterViewInit`

    ```TS
    // App component
    import { Component, ViewChild, ElementRef, AfterViewInit } from '@angular/core';
    import { SomeComponent } from './some.component.component'

    ...

    export class AppComponent implements AfterViewInit {
        elements: [...ELEMENTS]

        @ViewChild('htmlRef1')
        selection1: SomeComponent;

        // With this configuration the app will read the element as ElementRef
        @ViewChild('htmlRef2', {read: ElementRef})
        selection2: ElementRef;

        // Inject an html element reference
        @ViewChild('htmlRef3')
        contentDiv: ElementRef;

        ngAfterViewInit() {
            // Do something
        }

        onElSelected(el: SomeElement) {
            // Do something with the elements
        }
    }
    ```

-   The scope of `ViewChild` is on the template query itself, cannot reference references inside the reference

## ViewChildren

-   Similar to viewChild but it's intended to render several elements

    ```TS
    // App component
    import { Component, ViewChildren, ElementRef, AfterViewInit, QueryList } from '@angular/core';
    import { SomeComponent } from './some.component.component'

    ...

    export class AppComponent implements AfterViewInit {
        @ViewChild(SomeComponent, {read: ElementRef})
        cards: QueryList<SomeComponent>;

        ngAfterViewInit() {
            // Check for changes in the list
            this.cards.suscribe(cards => console.log(cards))
        }
    }
    ```

    ```HTML
    <!-- App -->
    <some-component *ngFor="el of elements" #htmlRefs
        (elSelected)="onElSelected($event)"
        [selection]="elements[0]"
    >
    </some-component>
    ```
