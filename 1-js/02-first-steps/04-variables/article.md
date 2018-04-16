# Variablen

In sehr vielen Fällen muss eine JavaScript-Anwendung in irgendeiner Form mit Informationen arbeiten. Hier sind zwei Beispiele:
1. Ein Online-Shop -- die Informationen können die angebotenen Güter, ein Warenkorb oder gewährte Rabatte sein. 
2. Eine Chat-Anwendung -- die Informationen können Benutzernamen, Nachrichten, Bilder und noch vieles weitere sein.

Variablen werden in Programmen verwendet um solche Informationen zu speichern und zu verarbeiten.

## Allgemeines zu Variablen

Eine [Variable](https://de.wikipedia.org/wiki/Variable_(Programmierung)) ist ein abstrakter, benannter Behälter für Daten. Innerhalb von Variablen können wir in JavaScript beliebige Daten speichern.

Um eine Variable in JavaScript zu kreieren, wird die Anweisung `let` verwendet.

Die folgende Anweisung erzeugt (auch *deklariert* oder *definiert*) eine Variable mit dem Namen "mitteilung":

```js
let mitteilung;
```

Nun können wir mit dem Zuweisungsoperator `=` Daten in die Variable schreiben:

```js
let mitteilung;

*!*
mitteilung = 'Hallo'; // Speichert eine Zeichenkette
*/!*
```

Die Zeichenkette ist nun in einem Speicherbereich abgelegt, der mit dem Variablennamen assoziiert ist. Auf diesen können wir zugreifen, indem wir den Variablennamen verwenden:

```js run
let mitteilung;
mitteilung = 'Hallo!';

*!*
alert(mitteilung); // Zeigt den Inhalt der Variable an
*/!*
```

Um den Code etwas zu verkürzen, können wir die Variablendeklaration und die Zuweisung in einer Zeile zusammenführen:

```js run
let mitteilung = 'Hallo!'; // Definiert die Variable und weißt einen Wert zu

alert(mitteilung); // Hallo!
```

Wir können auch mehrere Variablen auf einer Zeile deklarieren:

```js no-beautify
let nutzer = 'Paul', alter = 25, mitteilung = 'Hallo';
```

Das ist zwar etwas kürzer, aber trotzdem nicht zu empfehlen. Um die Lesbarkeit zu erhöhen, sollte für jede Variable eine neue Zeile verwendet werden.

Die mehrzeilige Variante ist zwar etwas länger, aber auch viel einfacher zu lesen:

```js
let nutzer = 'Paul'; 
let alter = 25; 
let mitteilung = 'Hallo';
```

Manche Entwickler schreiben viele Variablendeklarationen auch so:

```js no-beautify
let nutzer = 'Paul',
  alter = 25, 
  mitteilung = 'Hallo';
```

...Oder auch mit vorgezogenen Kommata:

```js no-beautify
let nutzer = 'Paul'
  , alter = 25
  , mitteilung = 'Hallo';
```

Alle diese Varianten arbeiten genau identisch. Es ist also eine Frage des Geschmacks (oder einer Konvention, wenn Sie in einem Team entwickeln) wie die Deklarationen verwendet werden.

````smart header="`var` anstelle von `let`"
In älteren Scripten findet man auch eine andere Anweisung: `var` anstelle von `let`:

```js
*!*var*/!* mitteilung = 'Hallo';
```

Die Anweisung `var` ist *fast* identisch zu `let`. Auch hier wird eine Variable deklariert, aber auf eine etwas "veraltete" Weise. Die Unterschiede sollen uns im Moment nicht weiter kümmern, wir kommen darauf im Kapitel <info:var> zurück.
````

## Variablen -- eine Analogie

Eine intuitive Vorstellung vom Konzept einer Variable können wir erhalten, wenn wir uns Variablen wie Schachteln mit eindeutiger Beschriftung vorstellen.

Die Variable `mitteilung` wäre also eine Schachtel mit der Aufschrift `"mitteilung"`; im Inneren wäre die Botschaft `"Hallo!"` enthalten:

![](variable.png)

Wir können jeden beliebigen Wert in diese Schachtel packen. Wir können den Wert in der Schachtel auch verändern und das so oft wie wir wollen:

```js run
let mitteilung;

mitteilung = 'Hallo!';

mitteilung = 'Nutzer!'; // Geänderter Variablenwert

alert(mitteilung); 
```

Wenn man den Wert einer Variablen ändert, werden die alten Daten aus der Variablen entfernt:

![](variable-change.png)

Wir können auch mehrere Variablen deklarieren und Daten zwischen diesen hin und her kopieren:

```js run
let hallo = 'Hallo Nutzer!';

let mitteilung;

*!*
// kopiere 'Hallo Nutzer' von hallo nach mitteilung
mitteilung = hello;
*/!*

// now two variables hold the same data
alert(hallo); // Hallo Nutzer!
alert(mitteilung); // Hallo Nutzer!
```

```smart header="Funktionale Sprachen"
An dieser Stelle wollen wir noch erwähnen, dass es auch [funktionale](https://de.wikipedia.org/wiki/Funktionale_Programmierung) Programmiersprachen gibt, die das Ändern von Variablenwerten verbieten. Beispiele sind [Scala](http://www.scala-lang.org/) oder [Erlang](http://www.erlang.org/).

In diesen Sprachen bleiben die Werte, die man einmal in die "Schachtel" gepackt hat für immer in der "Schachtel" erhalten. Wenn wir andere Daten speichern wollen, zwingen uns diese Sprachen dazu eine neue Variable zu deklarieren (eine neue Schachtel zu verwenden). Wir können die alten nicht erneut verwenden.

Auch wenn dieses Vorgehen im ersten Moment etwas eigenartig wirkt, sind diese Sprachen doch mächtig genug, um auch ernsthafte Entwicklungsprojekte damit durchzuführen. In bestimmten Bereichen, wie etwa parallelem Computing, haben diese Limitierungen sogar große Vorteile. Die Beschäftigung mit so einer Sprache ist sehr vorteilhaft auch wenn man sie nicht direkt einzusetzen gedenkt. Wenn man neue Sprachen erlernt, kann man sehr gut seinen Horizont erweitern.
```

## Variablen Namen [#variable-naming]

Es gibt in JavaScript zwei Beschränkungen für Variablennamen:

1. Der Name darf nur Buchstaben, Ziffern und die Symbole `$` sowie `_` enthalten.
2. Das erste Zeichen des Names darf keine Ziffer sein.

Beispiele für gültige Namen sind:

```js
let nutzerName;
let test123;
```

Besteht der Name aus mehreren Wörtern, wird häufig die [camelCase](https://de.wikipedia.org/wiki/Binnenmajuskel)-Schreibweise verwendet. Dabei schreibt man die Wörter, ohne Leerzeichentrennung, direkt hintereinander. Jedes Wort beginnt mit einem großen Buchstaben: `einWirklichLangerName`.

Als weitere Zeichen können wir das Dollarzeichen `'$'` und den Unterstrich `'_'` in unseren Variablennamen verwenden. Sie wirken wie normale Zeichen, ohne spezielle Bedeutung.

Weitere gültige Variablennamen wären:

```js run untrusted
let $ = 1; // Eine Variable mit dem Namen "$"
let _ = 2; // Eine Variable mit dem Namen "_"

alert($ + _); // 3
```

Einige Beispiele für ungültige Variablennamen:

```js no-beautify
let 1a; // Darf nicht mit einer Ziffer beginnen

let my-name; // Bindestriche "-" sind nicht erlaubt
```

```smart header="Groß- und Kleinschreibung wird unterschieden"
Die Namen `apfel` und `ApfeL` bezeichnen zwei unterschiedliche Variablen.
```

````smart header="Nicht-Englische Buchstaben funktionieren auch"
Wir können jede andere Sprache für Variablennamen verwenden, auch deutsche Umlaute, kyrillische Buchstaben oder Hieroglyphen:

```js
let münze = '...';
let имя = '...';
let 我 = '...';
```

Wir erhalten hier keine Fehlermeldung, die Variablennamen sind erlaubt. Doch es ist eine gute Tradition Englische Variablennamen zu verwenden. Auch wenn wir nur kleine Scripte schreiben wollen, oft überdauern diese für eine lange Zeit und müssen vielleicht später mal bearbeitet werden.
````

````warn header="Reservierte Namen"
Es gibt eine Liste mit reservierten Namen, die wir nicht verwenden dürfen um unsere Variablen zu benennen, weil sie schon von der Sprache selbst verwendet werden. Beispiele sind `let`, `class`, `return` und `function`.

Der folgende Code produziert einen Fehler:

```js run no-beautify
let let = 5; // "let" ist kein gültiger Variablenname!
let return = 5; // "return" ist auch nicht zulässig!
```
````

````warn header="Zuweisungen ohne `use strict`"

Normalerweise müssen wir eine Variable deklarieren bevor wir sie benutzen können. In den alten Zeiten war es aber möglich, eine Variable zu erzeugen, indem man einfach einen Wert zugewiesen hat, ohne `let` zu verwenden. Das funktioniert auch heute noch, wenn wir nicht `use strict` verwenden. Dieses Verhalten wurde beibehalten um die Kompatibilität mit alten Scripten zu gewährleisten.

```js run no-strict
// kein "use strict" in diesem Beispiel

num = 5; // die Variable "num" wird erzeugt, wenn sie noch nicht vorhanden war

alert(num); // 5
```

Das ist eine schlechte Programmierpraxis, im "strict"-Modus erzeugt sie einen Fehler:

```js run untrusted
"use strict";

*!*
num = 5; // Fehler: "num" nicht definiert
*/!*
```

````

## Konstanten

Um Konstanten (Variablen, die ihren Wert nicht ändern) zu deklarieren können wir `const` anstelle von `let` verwenden:

```js
const myBirthday = '18.04.1982';
```

Versuchen wir eine Konstante zu verändern, erzeugen wir einen Fehler:

```js run
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // Fehler: Können keinen neuen Wert zuweisen!
```

Wenn wir sicher sind, dass eine Variable ihren Wert niemals ändern soll, können wir `const` verwenden um das zu garantieren. Außerdem zeigen wir so anderen Entwicklern direkt an, dass diese Variable einen unveränderlichen Wert enthält.

### Konstanten in Großbuchstaben

Es ist verbreitete Praxis Konstanten zu verwenden um schwierig zu merkenden Werten einen Namen zu geben. Es ist eine Konvention solche Werte mit Großbuchstaben und Unterstrichen zu benennen, so wie hier:

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...um eine der Farben zu verwenden
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

Vorteile:

- `COLOR_ORANGE` lässt sich sehr viel einfacher merken als `"#FF7F00"`.
- Man kann sich bei `"#FF7F00"` viel leichter vertippen als bei `COLOR_ORANGE` (besonders, wenn man die Codevervollständigung einer IDE verwendet).
- Ließt man den Code, dann ist `COLOR_ORANGE` sehr viel aussagekräftiger als`#FF7F00`.

Wann sollten wir unsere Konstanten nun in Großbuchstaben schreiben und wann normal? Sehen wir uns noch ein Beispiel an.

Eine Konstante enthält einfach Werte die sich niemals ändern. Es gibt aber Werte, die wir bereits vor der Ausführung des Scripts kennen (wie hexadezimale Farbwerte), diese erhalten Namen in Großbuchstaben. Werden jedoch Werte vom Script selber berechnet und dann in der Konstante abgespeichert, verwendet man einen normal geschriebenen Namen

Ein Beispiel wäre:
```js
const pageLoadTime = /* Zeit, bis die Seite geladen ist */;
```

Der Wert `pageLoadTime` ist nicht vor der Ausführung des Scripts bekannt, daher kein großgeschriebener Name. Der Wert kann sich aber nach der Zuweisung nicht mehr ändern, daher verwenden wir eine Konstante und keine gewöhnliche Variable.

## Gute Variablennamen

Es gibt zuletzt noch einen wichtigen Punkt über Variablen zu sagen. Benennen Sie Variablen unbedingt sorgfältig. Nehmen Sie sich einen augenblick Zeit um über einen guten Namen nachzudenken.

Variablenbenennung ist eine der wichtigsten Fähigkeiten für einen Programmierer. Ein kurzer Blick auf die verwendeten Variablennamen in einem Programm erlaubt uns zu entscheiden, ob der Code von einem Anfänger oder einem erfahrenen Entwickler geschrieben wurde.

In realen Projekten wird die meiste Zeit darauf verwendet existierenden Code zu verändern oder zu erweitern. Man arbeitet also mit der bestehenden Codebasis und schreibt relativ selten etwas komplett Neues von Grund auf. Kehren wir nach einiger Zeit zu unserem Code zurück ist es einfacher sich zurecht zu finden, wenn die Dinge richtig beschriftet sind; also wenn unsere Variablen gut gewählte Namen tragen.

Widmen Sie also der Suche nach einem guten Variablennamen etwas Zeit. Diese kleine Investition wird sich früher oder später sicher auszahlen.

Hier einige Richtlinien für gute Variablennamen:

- Verwenden Sie sprechende Variablennamen wie `userName` oder `shoppingCart`.
- Vermeiden Sie Abkürzungen: GDP scheint Ihnen jetzt völlig eindeutig, aber andere Entwickler, oder Sie selbst in einigen Monaten können damit vielleicht nichts mehr anfangen. Vor allem Einbuchstabennamen wie `a`, `b`, `c` sollten nur in Ausnahmen verwendet werden. Eine wichtige Ausnahme sind Schleifenzähler.
- Variablennamen sollten möglichst gut beschreiben was sie enthalten und eindeutig sein. Schlechte Beispiele wären `data` und `value`. Solche Namen sagen nichts aus und sollten höchsten Verwendet werden, wenn aus dem Kontext eindeutig hervor geht, welche "data" gemeint sind.
- Verständigen Sie sich auf einige Regeln, entweder im Team oder in Ihrem Kopf. Wenn ein Seitenbesucher "user" genannt wird, sollten damit verbundene Variablen eher `currentUser` oder `newUser` heißen, weniger `currentVisitor` oder `newManInTown`.

Sie finden das klingt einfach? Natürlich, aber in der Praxis ist es eine große Herausforderung durchgängig gute Variablennamen zu verwenden. Versuchen Sie es trotzdem.

```smart header="Wiederverwenden oder nicht?"
Zu guter Letzt, es gibt einige faule Programmierer, die, anstatt neue Variablen zu deklarieren, bereits existierende wiederverwenden.

Das führt dazu, dass Variablen wie eine Schachtel sind, in die verschiedene Sachen gestopft werden, ohne die Beschriftung zu ändern. Wir wollen wissen was gerade drin ist? Schwer zu sagen... Wir müssen erstmal genauer nachschauen.

Man spart zwar ein paar Sekunden bei der Deklaration von Variablen, aber verliert ein Vielfaches an Zeit, wenn man einen Fehler sucht oder später versucht zu verstehen, was der eigene Code tut.

Eine neue Variable zu deklarieren ist etwas Gutes, nicht des Teufels.

Codeoptimierer und Browser optimieren den Code gut genug, als das es keine Leistungsunterschiede gibt. Verwenden wir verschiedene Variablen für unterschiedliche Daten, kann das sogar der Engine helfen, unseren Code zu optimieren.
```

## Zusammenfassung

Mit den Anweisungen `let`, `var` oder `const` können wir Variablen deklarieren die dann Daten speichern können.

- `let` -- ist die moderne Deklarationsform. Der Code muss im `strict`-Modus vorliegen um `let` verwenden zu können (Chrome, V8).
- `var` -- ist die ältere Variablendeklaration. Normalerweise werden wir diese Form nicht verwenden, aber wir behandeln die kleinen Unterschiede zu `let` im Kapitel <info:var>, nur für den Fall, dass man mal darüber stolpert.
- `const` -- verhält sich wie `let`, doch der Inhalt der Variablen kann nicht verändert werden.

Variablen sollten so benannt sein, dass man einfach erkennen kann, was sie enthalten.