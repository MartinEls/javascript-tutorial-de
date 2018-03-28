# Logische Operatoren

Es gibt drei logische Operatoren in JavaScript:
- ODER: `||` (OR)
- UND: `&&` (AND) 
- NICHT: `!` (NOT)

Obwohl sie ein "logisch" im Namen haben, können sie auf alle Variablentypen angewendet werden, nicht nur Boolesche Variablen. Die Rückgabewerte können ebenfalls ein beliebiger Variablentyp sein.

Aber schauen wir auf die Details.

## ODER ||

Der ODER-Operator (OR) wird durch zwei vertikale Linien dargestellt:

```js
result = a || b;
```

In klassischen Programmiersprachen ist der ODER-Operator lediglich vorgesehen um mit Booleschen Variablen zu arbeiten. Wenn eines der Argumente den Wert `true` (WAHR) hat, ist der Rückgabewert auch `true`, ansonsten `false` (FALSCH).

In JavaScript ist der Operator ein wenig diffiziler und mächtiger, aber zuerst schauen wir uns die Verwendung mit Booleschen Werten an.

Es gibt vier mögliche Eingabekombinationen:

```js run
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```

Wir sehen, dass der Rückgabewert immer `true` ist, außer wenn beide Operanden den Wert `false` haben.

Ist einer der Operanten kein Boolescher Wert, wird er zu einem Booleschen konvertiert, bevor die Operation durchgeführt wird.

Ein wichtiges Beispiel sind die Zahl `1` die als `true` und `0` die als `false` interpretiert werden:

```js run
if (1 || 0) { // Funktioniert wie if( true || false )
  alert( 'Wahr!' );
}
```

Sehr oft wird die ODER-Operation `||` in `if`-Statements verwendet um zu überprüfen ob *irgendeine* der Bedingungen WAHR ist.

Zum Beispiel:

```js run
let hour = 9;

*!*
if (hour < 10 || hour > 18) {
*/!*
  alert( 'Unser Büro ist geschlossen.' );
}
```

Durch Verkettung können auch mehr als zwei Eingaben verwendet werden:

```js run
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'Unser Büro ist geschlossen.' ); // Weil Wochenende ist
}
```

## ODER ermittelt den ersten wahren Wert

Unsere bisherigen Beobachtungen entsprechen ganz der klassischen Logik. JavaScript bringt aber noch einige interessante Aspekte neu hinzu.

Nehmen wir an, wir haben mehrere ODER-Verknüpfte Werte:

```js
Ergebnis = Wert1 || Wert2 || Wert3;
```

Der ODER-Operator `||` verhält sich nun wie folgt:

- Die Operanden werden von links nach rechts Ausgewertet.
- Jeder Operand wird in einen Booleschen Wert konvertiert. Wenn das Ergebnis `true` ist, wird die Auswertung gestoppt und der ursprüngliche (nicht konvertierte) Wert des Operanden zurückgegeben.
- Wurden alle Operanden bearbeitet (und alle liefern `false` zurück), wird der der Originalwert des letzten Operanden zurückgegeben.

Es wird immer der origignale, nicht konvertierte Wert des Operanden zurückgegeben.

Anders formuliert, liefert eine Kette von ODER-Operationen `"||"` den ersten wahr aussehenden Wert zurück oder den letzten Wert, falls kein wahrer Wert existiert.

Zum Beispiel:

```js run
alert( 1 || 0 ); // 1 
alert( true || 'Egal was hier steht' ); // true

alert( null || 1 ); // 1 
alert( null || 0 || 1 ); // 1 
alert( undefined || null || 0 ); // 0 (alle false, letzter Wert wird zurückgegeben)
```

Dieses Verhalten erlaubt einige interessante Verwendungsmöglichkeiten, die über die klassische, logische Verwendung des Booleschen ODER hinaus gehen.

1. **Getting the first truthy value from the list of variables or expressions.**

    Imagine we have several variables, which can either contain the data or be `null/undefined`. And we need to choose the first one with data.

    We can use OR `||` for that:

    ```js run
    let currentUser = null;
    let defaultUser = "John";

    *!*
    let name = currentUser || defaultUser || "unnamed";
    */!*

    alert( name ); // selects "John" – the first truthy value
    ```

    If both `currentUser` and `defaultUser` were falsy then `"unnamed"` would be the result.
2. **Short-circuit evaluation.**

    Operands can be not only values, but arbitrary expressions. OR evaluates and tests them from left to right. The evaluation stops when a truthy value is reached, and the value is returned. The process is called "a short-circuit evaluation", because it goes as short as possible from left to right.

    This is clearly seen when the expression given as the second argument has a side effect. Like a variable assignment.

    If we run the example below, `x` would not get assigned:

    ```js run no-beautify
    let x;

    *!*true*/!* || (x = 1);

    alert(x); // undefined, because (x = 1) not evaluated
    ```

    ...And if the first argument is `false`, then `OR` goes on and evaluates the second one thus running the assignment:

    ```js run no-beautify
    let x;

    *!*false*/!* || (x = 1);

    alert(x); // 1
    ```

    An assignment is a simple case, other side effects can be involved.

    As we can see, such a use case is a "shorter way to do `if`". The first operand is converted to boolean and if it's false then the second one is evaluated.

    Most of time it's better to use a "regular" `if` to keep the code easy to understand, but sometimes that can be handy.

## && (AND)

The AND operator is represented with two ampersands `&&`:

```js
result = a && b;
```

In classical programming AND returns `true` if both operands are truthy and `false` otherwise:

```js run
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

An example with `if`:

```js run
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
  alert( 'Time is 12:30' );
}
```

Just as for OR, any value is allowed as an operand of AND:

```js run
if (1 && 0) { // evaluated as true && false
  alert( "won't work, because the result is falsy" );
}
```


## AND seeks the first falsy value

Given multiple AND'ed values:

```js
result = value1 && value2 && value3;
```

The AND `&&` operator does the following:

- Evaluate operands from left to right.
- For each operand, convert it to a boolean. If the result is `false`, stop and return the original value of that operand.
- If all other operands have been assessed (i.e. all were truthy), return the last operand.

In other words, AND returns the first falsy value or the last value if none were found.

The rules above are similar to OR. The difference is that AND returns the first *falsy* value while OR returns the first *truthy* one.

Examples:

```js run
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

We can also pass several values in a row. See how the first falsy one is returned:

```js run
alert( 1 && 2 && null && 3 ); // null
```

When all values are truthy, the last value is returned:

```js run
alert( 1 && 2 && 3 ); // 3, the last one
```

````smart header="AND `&&` executes before OR `||`"
The precedence of the AND `&&` operator is higher than OR `||`, so it executes before OR.

In the code below `1 && 0` is calculated first:

```js run
alert( 5 || 1 && 0 ); // 5
```
````

Just like OR, the AND `&&` operator can sometimes replace `if`.

For instance:

```js run
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

The action in the right part of `&&` would execute only if the evaluation reaches it. That is: only if `(x > 0)` is true.

So we basically have an analogue for:

```js run
let x = 1;

if (x > 0) {
  alert( 'Greater than zero!' );
}
```

The variant with `&&` appears to be shorter. But `if` is more obvious and tends to be a little bit more readable.

So it is recommended to use every construct for its purpose. Use `if` if we want if. And use `&&` if we want AND.

## ! (NOT)

The boolean NOT operator is represented with an exclamation sign `!`.

The syntax is pretty simple:

```js
result = !value;
```

The operator accepts a single argument and does the following:

1. Converts the operand to boolean type: `true/false`.
2. Returns an inverse value.

For instance:

```js run
alert( !true ); // false
alert( !0 ); // true
```

A double NOT `!!` is sometimes used for converting a value to boolean type:

```js run
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

That is, the first NOT converts the value to boolean and returns the inverse, and the second NOT inverses it again. At the end we have a plain value-to-boolean conversion.

There's a little more verbose way to do the same thing -- a built-in `Boolean` function:

```js run
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```
