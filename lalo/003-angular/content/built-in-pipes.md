# Built-In Pipes

## Dates

-   They help us formatting data

    ```Ts
    export class Component {
        now = new Date():
    }
    ```

    ```HTML
    <p>{{ now | date }}</p>
    <!-- Jan 13, 2023 -->
    ```

    ```HTML
    <p>{{ now | date: 'dd/MM/YYYY' }}</p>
    <!-- 13/01/2023 -->
    ```

-   Letter case

    ```Ts
    export class Component {
        title = 'AMEGA':
    }
    ```

    ```HTML
    <p>{{ title | lowercase }}</p>
    <!-- amega -->
    ```

-   Numbers

    ```Ts
    export class Component {
        price = 10:
    }
    ```

    ```HTML
    <p>{{ price | number }}</p>
    <!-- 10 -->
    ```

    ```HTML
    <p>{{ price | number: '4.4-10' }}</p>
    <!-- 0,010.0000 -->
    ```

    ```HTML
    <p>{{ price | currency }}</p>
    <!-- $10.00 -->
    ```

    ```HTML
    <p>{{ price | currency: 'EUR' }}</p>
    <!-- €10.00 -->
    ```

    ```HTML
    <p>{{ price | percent }}</p>
    <!-- 1,000% -->
    ```

-   Loops

    ```HTML
    <p
        *ngFor="let item of myObject | slice:0,2"
    >{{ item }}</p>
    ```

-   JSON

    ```HTML
    <p>{{ myObject | json }}</p>
    <!-- JSON.stringify(myObject) -->
    ```

-   KeyValue
    ```HTML
    <ng-container *ngFor="let pair of myObject | keyvalue">
    <p>{{ pair.key }}: {{ pair.value | json }}</p>
    </ng-container>
    ```
