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
Versichern Sie sich, dass `"use strict"` am Anfang des Scriptest steht, sonst wird der `strict`-Modus möglicherweise nicht aktiviert.

Hier wird der `strict`-Modus nicht verwendet:

```js no-strict
alert("some code");
// "use strict" weiter unten wird ignoriert, es müsste am Anfang stehen

"use strict";

// `strict`-Modus ist nicht aktiviert
```

Lediglich Kommentare dürfen vor `"use strict"` auftreten.
````

```warn header="Man kann `use strict` nicht wieder abschalten"
Es gibt keine Direktive `"no use strict"` oder ähnliches, die die alte Verhaltensweise wieder herstellt.

Hat man in einem Script den `strict`-Modus eingeschaltet, gibt es dort kein Zurück mehr.
```

## Verwenden Sie immer "use strict"

Mit den genauen Unterschiede von `"use strict"` und dem alten "Default"-Modus müssen wir uns später noch genauer auseinandersetzen.

In den nächsten Kapiteln, wenn wir die Spracheigenschaften behandeln, werden wir immer wieder auf die Unterschiede hinweisen. Glücklicherweise gibt es nicht besonders viele und die, die es gibt machen unser Leben einfacher.

Zum jetzigen Zeitpunkt genügt es uns das Folgende zu wissen:

1. Die `"use strict"`-Direktive schaltet die Engine in den "modernen" Modus und verändert das Verhalten einiger eingebauter Funktionen.
2. Der `strict`-Modus wird mit `"use strict"` am Anfang des Scripts eingeschaltet. Es gibt auch einige Sprachfeatures wie Klassen und Module die den `strict`-Modus automatisch einschalten.
3. Alle modernen Browser unterstützen den `strict`-Modus.
4. Es ist grundsätzlich empfehlenswert Scripte mit `"use strict"` zu beginnen. Alle Beispiele in diesem Tutorial verwenden es; außer (sehr selten) es ist anders angegeben.
