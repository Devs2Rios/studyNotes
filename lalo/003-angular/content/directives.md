# Directives

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

## `ngClass`

-   Core directive to condition classes
    ```HTML
    <button [ngClass]="['disabled', 'red']">
    <button [ngClass]="{'disabled': false, 'red': true}">
    <button [ngClass]="paragraphClasses()">
    ```
    ```Ts
    paragraphClasses() {
        // Adds the disabled class if the element is loading
        return {
            'disabled': this.button.isLoading,
            'first': this.color === 'red'
        }
    }
    ```

## `ngStyle`

-   Core directive for custom style (useful for images)
    ```HTML
    <div [ngStyle]="cardStyles()"></div>
    ```
    ```Ts
    cardStyles() {
        return {'background-color': 'black'}
    }
    ```

## `ngSwitch`

-   Works like a `switch/case` expression
    ```HTML
    <p [ngSwitch]="el.day">
        <span class="day" *ngSwitchCase="one">1</span>
        <span class="day" *ngSwitchCase="two">2</span>
        <span class="day" *ngSwitchCase="three">3</span>
        <span class="day" *ngSwitchCase="four">4</span>
        <span class="day" *ngSwitchDefault>...</span>
    </p>
    ```

## `ngContainer`

-   It helps us to apply directives without creating a div
    ```HTML
    <ng-container *ngFor="let categorie of categories">
        <ng-container [ngSwitch]="categorie.name">
            <p *ngSwitchCase="'blue'" [ngStyle]="setColor(categorie.name)">
            {{ categorie.name }}
            </p>
            <p *ngSwitchCase="'red'" [ngStyle]="setColor(categorie.name)">
            {{ categorie.name }}
            </p>
            <p *ngSwitchDefault >{{ categorie.name }}</p>
        </ng-container>
    </ng-container>
    ```
