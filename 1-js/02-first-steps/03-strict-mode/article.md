# Moderne Spracheigenschaften: "use strict"

Für eine lange Zeit entwickelte sich JavaScript ohne irgendwelche Kompatibilitätsprobleme aufzuwerfen. Neue Features wurden einfach hinzugefügt, doch die alte Funktionalität wurde nicht verändert.

Das hatte den Vorteil, dass existierender Code immer lauffähig blieb. Nachteilig war, dass alle kleinen Schludereien oder fragwürdigen Designentscheidungen aus der frühen Zeit von JavaScript auf ewig der Sprache erhalten blieben.

Das blieb so bis 2009 der ECMAScript 5 Standard (ES5) erschien. Es wurden neue Features zur Sprache hinzugefügt und einige der existierenden Eigenschaften wurden verändert. Um alten Code lauffähig zu halten sind die meisten dieser Änderungen standardmäßig deaktiviert. Sie müssen erst durch eine spezielle Direktive eingeschaltet werden: `"use strict"`.

## "use strict"

Die Direktive erscheint wie ein String: `"use strict"` oder `'use strict'`. Wenn diese am Anfang des Scripts platziert wird, arbeitet das ganze Script nach den modernen Regeln, zum Beispiel:

```js
"use strict";

// Dieser Code arbeitet nach den modernen Regeln
...
```

Wir werden bald Funktionen in JavaScript (eine Gruppierung von Anweisungen) kennen lernen. Hier nur soviel, dass wir `"use strict"` auch am Anfang einer Funktion verwenden können, anstatt für das ganze Script. Der `strict`-Modus ist dann nur für diese Funktion aktiviert. Für gewöhnlich verwendet man den `strict`-Modus aber für ein ganzes Script.

````warn header="Versichern Sie sich, dass \"use strict\" am Anfang des Scriptest steht"
Please make sure that `"use strict"` is on the top of the script, otherwise the strict mode may not be enabled.

There is no strict mode here:

```js no-strict
alert("some code");
// "use strict" below is ignored, must be on the top

"use strict";

// strict mode is not activated
```

Only comments may appear above `"use strict"`.
````

```warn header="There's no way to cancel `use strict`"
There is no directive `"no use strict"` or alike, that would return the old behavior.

Once we enter the strict mode, there's no return.
```

## Always "use strict"

The differences of `"use strict"` versus the "default" mode are still to be covered.

In the next chapters, as we learn language features, we'll make notes about the differences of the strict mode. Luckily, there are not so many. And they actually make our life better.

At this point in time it's enough to know about it in general:

1. The `"use strict"` directive switches the engine to the "modern" mode, changing the behavior of some built-in features. We'll see the details as we study.
2. The strict mode is enabled by `"use strict"` at the top. Also there are several language features like "classes" and "modules" that enable strict mode automatically.
3. The strict mode is supported by all modern browsers.
4. It's always recommended to start scripts with `"use strict"`. All examples in this tutorial assume so, unless (very rarely) specified otherwise.
