# Custom components

## Basic usage

-   To create a new component you need to use the following command:

    ```Bash
    ng generate component component-name
    ```

-   This will create a folder inside the `app` directory with the files ready to Modify

    -   It's important to check that this file has a selector inside the `*.component.ts` file

        ```Ts
        import { Component } from '@angular/core';

        @Component({
            selector: 'app-card',
            templateUrl: './card.component.html',
            styleUrls: ['./card.component.sass']
        })
        export class CardComponent {

        }
        ```

    -   This selector will allow us to re-use the component inside other components
        ```HTML
        <app-card></app-card>
        ```
        -   This will render the content of the `*.component.html` file in the other component

## The @Input decorator

-   If you have a database and you want to render its content into components you can create a new object inide your `*.component.ts`

    1. Import the data and add it to your component class

        ```Ts
        //app.component.js
        import { Component } from '@angular/core';
        // Data
        import { PANGRAMS } from '../content/db-data';

        @Component({
            selector: 'app-root',
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.sass'],
        })

        export class AppComponent {
            data = { title: 'EATangular' };
            // Import the data from your database
            pangrams = { ...PANGRAMS };
        }
        ```

        ```Ts
        // card.component.ts
        import { Component, Input } from '@angular/core';

        @Component({
            selector: 'app-card',
            templateUrl: './card.component.html',
            styleUrls: ['./card.component.sass'],
        })
        // Input will allow us to pass properties inside our component
        export class CardComponent {
            @Input()
            pangram: string = '';
        }
        ```

        ```HTML
        <!-- app.component.html -->
        <!-- Components from array -->
        <app-card [pangram]="pangrams[0]"></app-card>
        <app-card [pangram]="pangrams[1]"></app-card>
        ```

## The @Output decorator

-   With the `@Output` decorator we can send events to parent components

    -   Add a function that uses the event to be triggered

        ```Ts
        //app.component.js
        import { Component } from '@angular/core';
        // Data
        import { PANGRAMS } from '../content/db-data';

        @Component({
            selector: 'app-root',
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.sass'],
        })
        export class AppComponent {
            data = { title: 'EATangular' };

            pangrams = [...PANGRAMS];

            currentPangram = 0;

            changePangram(event: Event): void {
            this.currentPangram = Math.trunc(Math.random() * this.pangrams.length);
            }
        }
        ```

    -   Add a function that triggers the event from the child component

        ```Ts
        // card.component.ts
        import { Component, EventEmitter, Input, Output } from '@angular/core';

        @Component({
            selector: 'app-card',
            templateUrl: './card.component.html',
            styleUrls: ['./card.component.sass'],
        })
        export class CardComponent {
            @Input()
            pangram: string = '';

            @Output()
            pangramSelected = new EventEmitter<string>();

            onPangramClick() {
                // This event send the pangram to the app component
                this.pangramSelected.emit(this.pangram);
            }
        }
        ```

        -   Output allows custom naming

            ```Ts
            @Output('pangramEmitter')
            pangramSelected = new EventEmitter<string>();

            ```

    -   Add the `(click)` event in the parent and child files with the functions to be triggered, remember to add the `$event` argument in the component that will listent to it

        ```HTML
        <!-- card.component.html -->
        <p>{{ pangram }}</p>
        <button (click)="onPangramClick()">Change Pangram</button>
        ```

        ```HTML
        <!-- app.component.html -->
        <app-card [pangram]="pangrams[currentPangram]" (click)="changePangram($event)"></app-card>
        ```

## `ngFor`

-   You can use the `*ngFor` core directive to map a series of components from an `Array` or an `Object`

    ```HTML
    <app-card
        *ngFor="let pangram of pangrams"
        [pangram]="pangram"
    ></app-card>
    ```

    ```HTML
    <!-- With index -->
    <app-card
        *ngFor="let pangram of pangrams; index as i"
        [pangram]="pangram"
        [index]="i"
    ></app-card>
    ```

    ```HTML
    <!-- With first -->
    <app-card
        *ngFor="let pangram of pangrams; first as isFirst"
        [pangram]="pangram"
        [index]="i"
    ></app-card>
    ```

    -   Check the [`*ngFor` docs](https://angular.io/api/common/NgFor#description)

## Elvis operator

-   With this operator you can condition rendering
    ```HTML
    <p *ngFor="let author of authors" *ngIf="author.name; else noAuthor">{{author.name}}</p>
    <ng-template #noAuthor>
        <p>No author available</p>
    </ng-template>
    ```
    -   Everything passed into `*ngIf` will be coherced into a boolean, you can pass any value, even a function if you need to make complex checks
