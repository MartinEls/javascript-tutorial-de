# Code-Struktur

Die erste Sache die wir uns anschauen werden, sind die Grundbausteine für unseren Code.

## Anweisungen

Anweisungen (Statements) sind Syntaxkonstrukte und Kommandos die Dinge ausführen.

Wir haben schon die Anweisung `alert('Hello, world!')` gesehen, um eine Mitteilung auszugeben.

Unser Code kann beliebig viele Anweisungen enthalten. Aufeinander folgende Anweisungen werden mit einem Semikolon (;) getrennt.

Zum Beispiel können wir unsere Mitteilung in zwei Mitteilungen zerlegen:

```js run no-beautify
alert('Hello'); alert('World');
```

Für gewöhnlich wird jede Anweisung auf eine eigene Zeile geschrieben um die Lesbarkeit des Codes zu erhöhen:

```js run no-beautify
alert('Hello');
alert('World');
```

## Semikolons [#semicolon]

In den meisten Fällen können wir das Semikolon auch weglassen, wenn ein Zeilenumbruch vorhanden ist.

Beispielsweise funktioniert auch:

```js run no-beautify
alert('Hello')
alert('World')
```

Der Zeilenumbruch wird von JavaScript als implizites Semikolon interpretiert. Dieses verhalten wird auch "autmatisches Einfügen von Semikolons" ([automatic semicolon insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion)) genannt.

**In den meisten Fällen impliziert ein Zeilenumbruch ein Semikolon. Aber "in den meisten Fällen" ist nicht "immer"!**

Es gibt Fälle in denen ein Zeilenumbruch kein automatisches Semikolon erzeugt, zum Beispiel:

```js run no-beautify
alert(3 +
1
+ 2);
```

Dieser Code erzeugt die Ausgabe `6`, weil JavaScript hier keine Semikolons einfügt. In diesem Fall erkennen wir sofort, dass eine Zeile die mit einem Plus `"+"` endet, einen unvollständigen Ausdruck (incomplete expression) enthält und folglich kein Semikolon benötigt. In diesem Fall funktioniert es auch wie erwartet.

**Aber es gibt Fälle in denen JavaScript nicht erfolgreich errät wo Semikolons wirklich benötigt werden.**

Die Fehler die aus diesen Fällen resultieren sind oft sehr schwer zu finden und zu beheben.

````smart header="Beispiel für einen Fehler"
Ein konkretes Beispiel für einen solchen Fehler zeigt der folgende Code:

```js run
[1, 2].forEach(alert)
```

Im Moment kümmern wir uns nicht um die Bedeutung der eckigen Klammern `[]` und des `forEach`. Wir werden uns später um diese Sprachelemente kümmern, im Moment spielen sie keine besondere Rolle. Schauen wir uns nur kurz das Ergebnis an: wir bekommen zuerst `1` und dann `2` angezeigt.

Fügen wir jetzt ein `alert` vor dem Code ein, welches *nicht* mit einem Semikolon abgeschlossen wird:

```js run no-beautify
alert("Hier entsteht ein Fehler")

[1, 2].forEach(alert)
```

Jetzt wird nur der erste `alert`angezeigt, danach bekommen wir eine Fehlermeldung!

Allerdings ist wieder alles in Ordnung, wenn wir ein Semikolon nach dem ersten `alert` einfügen:
```js run
alert("Alles in Ordnung");

[1, 2].forEach(alert)  
```

Jetzt bekommen wir zuerst die "Alles in Ordnung" Meldung und dann  `1` und `2`.

Der Fehler in der semikolonfreien Variante entsteht, weil JavaScript keine impliziten Semikolons vor eckigen Klammern `[...]` einfügt. Daher wird der Code als eine einzige Anweisung interpretiert. So sieht die JavaScript-Engine unseren Code:

```js run no-beautify
alert("Hier entsteht ein Fehler")[1, 2].forEach(alert)
```

Gemeint hatten wir aber zwei getrennte Anweisungen, nicht eine einzelne. Die Zusammenführung der Anweisungen erzeugt hier den Fehler. Es gibt noch andere Situationen in denen dieses Problem auftritt.
````

Es wird empfohlen alle Anweisungen durch Semikolons zu trennen, auch wenn sie durch Zeilenumbrüche getrennt sind. Diese Regel findet in der Community eine breite Anwendung. Fassen wir noch einmal zusammen: *Es ist möglich* in vielen Fällen Semikolons weg zu lassen. Es ist aber sicherer und eine gute Angewohnheit -- besonders für Anfänger -- sie immer zu verwenden.

## Kommentare

Im Laufe der Zeit wird jedes Programm immer komplexer. Daher wird es notwendig *Kommentare* zum Code hinzuzufügen die beschreiben was im Code vor sich geht.

Kommentare dürfen an jeder Stelle im Script platziert werden. Sie beeinflussen nicht den Ablauf des Scriptes da sie wärend der Ausführung einfach ignoriert werden.

**Einzeilige Kommentare beginnen mit zwei Schrägstrichen `//`.**

Der Rest der Zeile hinter den Schrägstrichen ist ein Kommentar. Er kann eine einzelne, ganze Zeile einnehmen oder nach einer anderen Anweisung folgen.

So wie hier:
```js run
// Dieser Kommentar nimmt eine ganze Zeile für sich ein.
alert('Hello');

alert('World'); // Dieser Kommentar folgt auf eine Anweisung
```

**Mehrzeilige Kommentare beginnen mit einem Schrägstrich gefolgt von einem Sternchen <code>/&#42;</code> und enden mit einem Sternchen gefolgt von einem Schrägstrich <code>&#42;/</code>.**

So wie hier:

```js run
/* 
Ein Beispiel mit zwei Mitteilungen.
Dies ist ein mehrzeiliger Kommentar.
*/
alert('Hello');
alert('World');
```

Der Inhalt der Kommentare wird ignoriert, wenn wir also Code innerhalb von <code>/&#42; ... &#42;/</code> platzieren, wird dieser nicht ausgeführt.

Hin und wieder ist es praktisch mit Kommentaren Teile des Codes von der Ausführung auszunehmen:

```js run
/* Auskommentieren von Code
alert('Hello');
*/
alert('World');
```

```smart header="Nützliche Tastenkombinationen"
In vielen Texteditoren kann eine einzelne Codezeile mit der Tastenkombination `key:Ctrl+/` auskommentiert werden. Die Tastenkombination für mehrzeilige Kommentare (zuerst mehrere Zeilen auswählen) lautet oft `key:Ctrl+Shift+/` oder ähnlich. An einem Mac verwenden Sie `key:Cmd` anstelle von `key:Ctrl`.
```

````warn header="Verschachtelte Kommentare werden nicht unterstützt!"
Es sollte kein `/*...*/` innerhalb von `/*...*/` geben.

Dieser Code wird mit einer Fehlermeldung abbrechen:

```js run no-beautify
/*
  /* Verschachtelter Kommentar ?!? */
*/
alert( 'World' );
```
````

Bitte zögern Sie nicht, Ihren Code zu kommentieren!

Kommentare vergrößern zwar die Größe des Gesamtcodes, aber das stellt kein Problem dar. Es existieren zahlreiche Werkzeuge die unseren Code minimieren können bevor wie ihn auf einen Produktivserver laden. Diese entfernen unter anderem Kommentare, so dass diese nicht in den Scripten auftauchen, die an Endnutzer ausgeliefert werden. Kommentare haben also keinen Einfluss auf die ausgelieferte, produktive Seite.

Im weiteren Verlauf des Tutorials werden wir uns noch mit gutem Codierstil (<info:coding-style>) auseinander setzen. Hierbei werden wir auch beleuchtenwie man bessere und aussagekräftige Kommentare schreibt.
