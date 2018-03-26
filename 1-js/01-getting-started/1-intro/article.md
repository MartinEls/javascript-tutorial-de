# Eine Einführung in JavaScript

Was ist das Besondere an [JavaScript](https://de.wikipedia.org/wiki/JavaScript), was können wir damit machen und welche anderen Technologien können wir mit JavaScript verwenden?

## Was ist JavaScript?

*JavaScript* wurde ursprünglich entwickelt um *"Webseiten lebendig werden zu lassen"*.

Die Programme in dieser Sprache heißen *Scripte*. Sie können direkt innerhalb von [HTML](https://de.wikipedia.org/wiki/Hypertext_Markup_Language) geschrieben werden und kommen automatisch zur Ausführung wenn die Seite geladen wird.

Scripte werden als einfache Textdateien (plain text) geschrieben und auch ausgeführt. Sie benötigen keine besondere Vorbereitung und auch keine Kompilierung zur Ausführung.

In diesem Aspekt ist JavaScript sehr verschieden von der Programmiersprache [Java](https://de.wikipedia.org/wiki/Java_(Programmiersprache)), mit der es sich vor allem den Namen teilt.

```smart header="Warum <u>Java</u>Script?"
Als JavaScript entwickelt wurde, hatte es zuerst einen anderen Namen: "LiveScript". Allerdings war die Sprache Java zu dieser Zeit sehr populär und man entschied, dass die Positionierung der neuen Sprache als "jüngerer Bruder" von Java hilfreich sein könnte.

Mit der Evolution von JavaScript wurde es zu einer völlig unabhängigen Sprache mit einer eigenen Spezifikation, [ECMAScript](http://en.wikipedia.org/wiki/ECMAScript). JavaScript steht heute in keinerlei Beziehung zu Java.
```

Mittlerweile kann JavaScript nicht nur im Browser, sondern auch auf dem Server ausgeführt werden. Genauer gesagt läuft JavaScript auf jedem Gerät für das ein spezielles Programm geschrieben wurde, die so genannte [JavaScript-Engine](https://en.wikipedia.org/wiki/JavaScript_engine).

Browser besitzen eine eingebettete JavaScript-Engine, manchmal auch "Virtuelle JavaScript Maschine" genannt, in Anlehnung an die "Virtuelle Java Maschine".

Unterschiedliche Browser verwenden verschiedene Engines mit einer Reihe von Codenamen. Hier ein paar Beispiele:

- [V8](https://de.wikipedia.org/wiki/V8_(JavaScript-Implementierung)) -- in Chrome.
- [SpiderMonkey](https://de.wikipedia.org/wiki/SpiderMonkey) -- in Firefox.
- ...Es gibt noch einige weitere, wie "Trident", "Chakra" für verschiedene Versionen des Internet Explorers, "ChakraCore" für Microsoft Edge, "Nitro" und "SquirrelFish" für Safari etc.

Man sollte von diesen Namen gehört haben, da sie immer mal wieder in Entwicklerartikeln im Internet und auch in diesem Tutorial auftauchen. Aussagen wie "das Feature X wird von V8 unterstützt" bedeuten, dass etwas wahrscheinlich in Chrome funktionieren wird.

```smart header="Wie arbeiten Engines?"

Engines sind recht kompliziert, aber die Grundlagen sind einfach.

1. Die Engine (eine eingebettete, wenn wir einen Browser verwenden) ließt ("[parst](https://de.wikipedia.org/wiki/Parser)") das Script.
2. Dann wird das Script in die Maschinensprache übersetzt ("[compiliert](https://de.wikipedia.org/wiki/Compiler)").
3. Anschließend läuft dieser Maschinencode, meistens recht schnell.

In jedem dieser Schritte, versucht die Engine den Code zu optimieren. Die Engine beobachtet auch den laufenden Code und analysiert den auftretenden Datenfluss. Basierend auf diesen Daten wird der Maschinencode weiter optimiert was zu wirklich hohen Ausführungsgeschwindigkeiten führen kann.
```

## Was ist mit JavaScript im Browser möglich?

Modernes JavaScript ist eine "sichere" Programmiersprache. Es sind keine systemnahen Zugriffe auf den Speicher oder die CPU möglich, da diese für den Einsatz im Browser auch nicht nötig sind.

Die resultierenden Möglichkeiten werden sehr stark von der Umgebung beeinflusst in der wir JavaScript ausführen. Beispielsweise unterstützt [Node.JS](https://de.wikipedia.org/wiki/Node.js) Funktionen die es uns erlauben beliebige Dateien zu lesen und schreiben oder Netzwerkabfragen zu senden.

JavaScript im Browser bietet uns alle Möglichkeiten im Zusammenhang mit Webseitenmanipulation, Nutzerinteraktion und Interaktion mit dem Webserver.

Zum Beispiel kann JavaScript im Browser:

- Neue HTML-Daten zur Seite hinzufügen, existierende Inhalte verändern oder CSS-Styles verändern.
- Auf Nutzeraktivitäten wie Mauszeiger, Mausklicks oder Tastatureingaben reagieren.
- Abfragen über das Netzwerk zu Servern senden um Dateien hoch oder runter zu laden (so genannte [AJAX](https://de.wikipedia.org/wiki/Ajax_(Programmierung)) oder [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) Techniken).
- Das Setzen und Abfragen von Cookies, die Ausgabe von Meldungen und das Einlesen von Nutzerdaten.
- Speichern von Daten auf dem Gerät des Nutzers ("local storage").

## Was kann JavaScript im Browser NICHT?

Die Fähigkeiten von JavaScript innerhalb des Browser sind beschnitten um die Sicherheit der Nutzer zu erhöhen. Damit soll verhindert werden das bösartige Webseiten private Informationen des Nutzers abgreifen können oder das System des Nutzers beschädigen.

Beispiele derartiger Restriktionen sind:

- JavaScript auf einer Webseite kann nicht auf beliebige Dateien der Festplatte zugreifen oder lokale Programme ausführen. Es hat auch keinen direkten Zugriff auf Betriebssystemfunktionen.

    Moderne Browser erlauben es uns allerdings mit lokalen Dateien zu arbeiten, allerdings nur wenn der Nutzer gewisse Aktionen ausführt, so wie ziehen einer Datei ins Browserfenster oder auswählen einer Datei über ein `<input>`-Tag.

    Es gibt auch die Möglichkeit mit Kameras und Mikrofonen sowie anderen Hardwarekomponenten zu arbeiten, aber hier ist eine explizite Erlaubnis vom Nutzer notwendig. Eine JavaScript-Webseite kann also nicht heimlich die Webcam aktivieren und Überwachungsbilder senden.
- Verschiedene Browserfenster oder -tabs wissen nichts voneinander. Ausnahmen sind wenn ein Fenster JavaScript nutzt um ein weiteres zu öffnen, aber auch dann kann JavaScript von einer Seite nicht auf Daten der anderen Seite zugreifen, wenn sie aus verschiedenen Quellen (Domains, Protokoll, Port, etc.) kommen.

    Dieses Verhalten wird "Same Origin Policy" genannt. Um es zu umgehen müssen *beide Seiten* speziellen JavaScript-Code enthalten, die den Datenaustausch handhaben.

    Diese Einschränkungen dienen wiederrum der Sicherheit der Nutzer. Ein Seite `http://anysite.com` die der Nutzer öffnet darf nicht auf einen geöffneten Tab `http://gmail.com` zugreifen und Daten daraus stehlen.
- JavaScript kann sehr leicht über das Netzwerk mit dem Server kommunizieren von dem es geladen wurde. Doch die Fähigkeiten mit anderen Domains zu kommunizieren sind beschnitten. Obwohl grundsätzlich möglich, benötigen diese eine explizite Zustimmung (über HTTP-Header) von der entfernten Stelle. Auch diese Einschränkung dient der Nutzersicherheit.

![](limitations.png)

Diese Einschränkungen bestehen nicht, wenn JavaScript außerhalb eines Browsers ausgeführt wird, beispielsweise auf einem Server. Moderne Browser erlauben es außerdem Erweiterungen oder Plug-ins zu installieren, die erweiterte Rechte erhalten können.

## Was macht JavaScript so besonders?

Es gibt mindestens *drei* wirklich großartige Dinge in JavaScript:

```compare
+ Vollständige Integration in HTML/CSS.
+ Einfache Dinge sind einfach.
+ Unterstützung durch alle gängigen Browser, standardmäßig aktiviert.
```

In dieser Kombination gibt es diese drei Eigenschaften nur bei JavaScript und bei keiner anderen Browsertechnik.

Das macht JavaScript einzigartig und das ist der Grund weshalb es das meistgenutzte Werkzeug für Nutzerschnittstellen im Browser ist.

Macht man sich daran eine neue Technik zu erlernen, lohnt es sich deren Perspektiven zu betrachten. Daher blicken wir noch kurz auf einige neue Trends unter den Sprachen und Browsern.

## JavaScript und verwandte Sprachen

Die Syntax von JavaScript erfüllt nicht die Bedürfnisse und Wünsche aller Nutzer. Verschiedene Leute wünschen sich verschiedene Eigenschaften.

Das ist nichts weiter besonderes, da die Projekte und Anforderungen für jeden verschieden sind.

In letzter Zeit entstand so ein Strauß neuer Sprachen welche in JavaScript-Code übertragen (*transpiled*) werden, bevor sie im Browser ausgeführt werden.

Moderne Werkzeuge erlauben eine schnelle und transparente Übertragung nach JavaScript. Diese erlauben es Entwicklern in einer anderen Sprache zu programmieren, welche im Hintergrund automatisch zu JavaScript-Code umgewandelt wird.

Einige Beispiele sind:

- [CoffeeScript](http://coffeescript.org/) ist "syntaktischer Zucker" (syntactic sugar) für JavaScript. Es führt kürzere Syntax ein, die es erlaubt präziseren und klareren Code zu schreiben. Ruby-Entwickler fühlen sich hier schnell heimisch.
- [TypeScript](http://www.typescriptlang.org/) bringt starke Typisierung (strict data typing) um die Entwicklung und Wartung  komplexerer Systeme zu vereinfachen. TypeScript wird von Microsoft aktiv weiter entwickelt.
- [Dart](https://www.dartlang.org/) ist eine allein-lauffähige Sprache mit einer eigenen Engine die auch außerhalb des Browsers arbeiten kann (zum Beispiel in mobilen Apps). Ursprünglich von Google als ein JavaScript-Ersatz entwickelt, erfordern Browser eine Übertragung des Codes nach JavaScript wie auch in den anderen Fällen.

Es gibt noch einige mehr. Auch wenn wir uns entscheiden sollten in einer dieser Sprachen entwickeln zu wollen, ist es eine gute Idee JavaScript zu beherrschen um zu verstehen was in unserem Code passiert.

## Zusammenfassung

- Ursprünglich wurde JavaScript entwickelt um lediglich innerhalb eines Browsers zu laufen, mitlerweile wird es aber auch in vielen anderen Bereichen eingesetzt.
- Derzeit ist JavaScript die am weitesten verbreitete Browserprogrammiersprache mit HTML- und CSS-Fähigkeiten.
- Es gibt einige Sprachen die zu JavaScript-Code übertragen werden und einige neue Eigenschaften zu JavaScript hinzufügen. Wenn man in die Grundlagen von JavaScript eingedrungen ist, lohnt sich ein Blick auf diese Alternativen.
