# Debuggen in Chrome

Bevor wir komplexeren Code schreiben, lass uns über Debuggen sprechen.

Alle modernen Browser und die meisten anderen Umgebungen unterstützen "debuggen" -- eine spezielle UI in den Entwicklerwerkzeugen, welches es einfacher macht Fehler zu finden und zu beheben.

Wir werden hier Chrome verwenden, da er wahrscheinlich das Funktionsreichste in diesem Bereich ist.

## Der "sources" Bereich

Deine Chrome Version sieht vielleicht etwas anders aus, aber es sollte trotzdem offensichtlich sein, was da ist.

- Öffne die [Beispielseite](debugging/index.html) in Chrome.
- Öffne die Entwicklerwerkzeugen mit `key:F12` (Mac: `key:Cmd+Opt+I`).
- Öffne den `sources` Bereich.

Folgendes sollten Sie sehen, wenn Sie dies zum ersten Mal machst:

![](chrome-open-sources.png)

Die Schaltfäche <span class="devtools" style="background-position:-168px -76px"></span> öffnet die Registerkarte mit den Dateien.

Wir klicken darauf und wählen `index.html` aus und danach `hello.js` in der Baumansicht. Hier ist, was erscheinen sollte:

![](chrome-tabs.png)

Hier können wir 3 Bereiche erkennen:

1. Der **Ressourcen Bereich** listet HTML, JavaScript, CSS und andere Dateien auf, einschließlich Bilder die in der Seite eingebunden.
2. Der **Source Bereich** zeigt den Source Code.
3. Der **Information und Kontroll Bereich** ist für das Debuggen, wir werden ihn bald erkunden.

Jetzt können Sie auf die selbe Schaltfläche <span class="devtools" style="background-position:-200px -76px"></span> erneut klicken um die Ressourcen Liste zu verstecken und dem Code platz zu schaffen.

## Console

Wenn wir  `Esc` drücken, dann öffnet sich darunter eine Console. Wir können dort Befehle eingeben und mit  `key:Enter` ausführen.

Nachdem eine Anweisung ausgeführt wurde, wird das Ergebnis darunter angezeigt.

Als Beispiel, hier `1+2` ergibt  `3`, und `hello("debugger")`  liefert nichts, sodass das Ergebnis  `undefined` ist:

![](chrome-sources-console.png)

## Breakpoints

 Lassen Sie uns untersuchen, was innerhalb des Codes der [Beispielseite](debugging/index.html) vor sich geht.. In `hello.js`, klicke auf die Zeilennummer  `4`. Ja, direkt auf die Zahl `4`, nicht im Code.

Herzlichen Glückwunsch! Sie haben einen Breakpoint gesetzt. Bitte klicken sie auch auf die Nummer für Zeile `8`.

Es sollte wie folgt aussehen (Blau markiert an welcher stelle sie klicken sollen):

![](chrome-sources-breakpoint.png)

Ein*breakpoint* ist ein Punkt im Code an der der Debugger automatisch anhalten wird, während der JavaScript ausführung.

Währen der Code angehalten ist können wir die aktuellen Variablen untersuchen, ausführen Befehle in der Console etc. In anderen Worten, wir können es debuggen.

Wir können immer eine Liste von Breakpoints im rechten Bereich finden. Dies ist nützlich, wenn wir viele Breakpoints in verschiedenen Dateien haben. Das erlaubt uns:
- Schnell zu einem Breakpoint im Code zu springen (durch klicken auf ihn im rechten Bereich).
- Temporär einen Breakpoint auszuschalten indem wir in abwählen.
- Den Breakpoint zu entfernen durch rechts klicken und entfernen auswählen .
- ...Und so weiter.

```smart header="Conditional breakpoints"
*Rechts-Klick* auf die Zeilennummer erlaubt es uns ein *bedingten* Breakpoint. Er wird nur ausgelöst wenn der gegebene  Ausdruck wahr ist.

Das ist praktisch, wenn wir nur für einen bestimmten Variablenwert oder für bestimmte Funktionsparameter anhalten müssen.
```

## Debugger Befehl

Wir können auch den Code anhalten durch das nutzen des `debugger` Befehles,  so wie hier:

```js
function hello(name) {
  let phrase = `Hello, ${name}!`;

*!*
  debugger;  // <-- der Debugger hält hier an
*/!*

  say(phrase);
}
```

Das ist sehr praktisch, wenn wir uns in einem Code-Editor befinden und nicht zum Browser wechseln und das Script in den Entwicklertools nachschlagen wollen, um den Haltepunkt zu setzen.


## Pause und umhersehen 

In unserem Beispiel, `hello()`  wir währen des Seitenladens aufgerufen, so das der einfachste Weg ist um den Debugger zu aktivieren, das Neuladen der Seite ist. Also lass uns  `key:F5` drücken (Windows, Linux) oder `key:Cmd+R` (Mac).

Ist der Breakpoint gesetzt, hält die Ausführung in der 4 Zeile an:

![](chrome-sources-debugger-pause.png)

Bitte öffne die Dropdown-Listen für Informationen auf der rechten Seite  (markiert mit Pfeilen). Diese erlaubt Ihnen den aktuellen Code-Zustand zu untersuchen:

1. **`Watch` -- zeigt aktuelle Werte für beliebige Ausdrücke an.**

    Sie können das Plus anklicken `+`und einen Ausdruck eingeben. Der Debugger wird den Wert zu jedem Moment anzeigen, er wird automatisch neu berechnet während die Ausführung läuft.

2. **`Call Stack` -- zeigt die verschachtelte Aufrufkette an.**

   Im aktuellen Moment ist der Debugger im `hello()` aufruf, aufgerufen durch ein Script in `index.html` (hier ist keine Funktion, daher wird es "anonym" aufgerufen).

    Wenn Sie auf ein Stack Item klicken, springt der Debugger zum zugehörigen Code, und alle seine Variablen können ebenfalls untersucht werden.
3. **`Scope` -- aktuelle Variablen.**

    `Local` zeigt lokale funktions Variablen. Sie können ihre Werte auch direkt über dem Code hervorgehoben sehen .

    `Global` hat globale Variablen (außerhalb von allen Funktionen).

    Dort ist auch das `this` Schlüsselwort, welches wir bisher nicht kennengelernt haben, aber das werden wir bald tun.

## Verfolgung der Ausführung

Nun ist es an der Zeit, das Skript zu verfolgen (*trace*).

Hierfür gibt es Schaltflächen im oberen rechten Bereich. Nehmen wir diese ins Visier.

<span class="devtools" style="background-position:-7px -76px"></span> -- die Ausführung weiter fortsetzen,  Kurztaste `key:F8`.
: Setzt die Ausführung fort. Gibt es keine weiteren Breakpoints, wird die Ausführung einfach fortgesetzt und der Debugger verliert die Kontrolle.

Hier ist, was wir nach einem Klick darauf sehen können:

![](chrome-sources-debugger-trace-1.png)

    Die Ausführung wurde fortgesetzt, erreicht einen anderen Breakpoint innerhalb von `say()` und hält dort an. Werfen Sie einen Blick auf den  "Call stack" auf der rechten Seite. Es hat sich um einen weiteren Anruf erhöht. Wir sind nun innerhalb von `say()`.

<span class="devtools" style="background-position:-137px -76px"></span> -- einen Schritt tun (den nächsten Befehl ausführen), aber *nicht in die Funktion hinein gehen*, Kurztaste `key:F10`.
: Wenn wir es jetzt anklicken, ein `alert` wird angezeigt. Das Wichtige dabei ist `alert` kann jede Funktion sein, die Ausführung "geht darüber hinweg", es überspringt den Funktionsinhalt.

<span class="devtools" style="background-position:-72px -76px"></span> -- einen Schritt tun, Kurztaste `key:F11`.
: Wie der Vorherige, allerdings "hineingehen" in geschachtelte Funktionen . Wenn Sie darauf klicken, werden alle Skript-Aktionen nacheinander ausgeführt.

<span class="devtools" style="background-position:-104px -76px"></span> -- fortsetzen der Ausführung bis zum Ende der aktuellen Funktion, Kurztaste `key:Shift+F11`.
: Die Ausführung stoppt an der aller letzten Zeile der aktuellen Funktion. Dies ist nett wenn man ausversehen eine verschachtelte Funktion aufgerufen hat <span class="devtools" style="background-position:-72px -76px"></span>, diese interessiert uns aber nicht, und wir wollen diese so schnell wie möglich wieder verlassen.

<span class="devtools" style="background-position:-7px -28px"></span> -- aktivieren/deaktivieren aller Breakpoints.
: Diese Schaltfläche bewegt die Ausführung nicht. Sie aktiviert/deaktiviert nur alle Breakpoints.

<span class="devtools" style="background-position:-264px -4px"></span> -- aktivieren/deaktivieren der automatischen Pause im Falle eines Fehlers.
: Ist dies aktiviert,und die Entwicklerwerkzeuge sind offen, ein Script Fehler führt zu einem automatischen Anhalten der Ausführung. Dann können wir die Variablen analysieren um zu sehen was falsch lief. Das heißt wenn unser Script mit einem Fehler stirbt, können wir den Debugger öffnen, diese Option aktivieren und die Seite neuladen um zu sehen an welcher Stelle es stirbt und was der Kontext an dieser Stelle ist..

```smart header="Continue to here"
Rechtsklick auf die Zeile öffnet das Kontext Menu mit einer großartigen Option mit dem Namen: "Continue to here".

Dies ist Nützlich wenn wir mehrere Schritte vorwärts wollen, aber wir zu faul sind um Breakpoints zu setzten.
```

## Logging

Um irgendetwas in der Console anzuzeigen , gibt es die `console.log` Funktion.

Zum Beispiel gibt dies Werte von `0` bis `4` in der Console aus:

```js run
// öffne die Console um es zu sehen
for (let i = 0; i < 5; i++) {
  console.log("value", i);
}
```

Normalerweise sieht der Nutzer diese Ausgabe nicht, er ist in der Console. Um ihn zu sehen, öffne entweder den Console Bereich in den Entwicklerwerkzeugen oder drücke `key:Esc` während Sie sich in einer anderen Registerkarte befinden: dies öffnet die Console an der Unterseite.

Wenn wir genügend Logging in unserem Code haben, dann können wir sehen, was in den Datensätzen vor sich geht, ohne den Debugger..

## Übersicht

Wie wir sehen können, gibt es drei Hauptmöglichkeiten ein Script zu unterbrechen:
1. Ein breakpoint.
2. Das `debugger` Statement.
3. Ein Fehler (wenn die Entwicklerwerkzeuge geöffnet sind und die Schaltfläche <span class="devtools" style="background-position:-264px -4px"></span> auf "on" ist)

Dann können wir Variablen untersuchen und weitermachen, um zu sehen , wo die Ausführung falsch läuft.

Es gibt noch viel mehr Möglichkeiten in den Entwicklerwerkzeugen als hier beschrieben sind. Das vollständige Handbuch finden Sie unter <https://developers.google.com/web/tools/chrome-devtools>.

Die Informationen aus diesem Kapitel reichen aus, um mit dem Debuggen zu beginnen, aber später, besonders wenn Sie viel Browserarbeit leisten, gehen Sie bitte dorthin und schauen Sie sich die erweiterten Funktionen der Entwicklerwerkzeuge an.

Oh, und auch Sie können an verschiedenen Stellen der Entwicklungswerkzeuge klicken und einfach sehen, was angezeigt wird. Das ist wahrscheinlich der schnellste Weg, um Entwicklungswerkzeuge zu erlernen. Vergiss auch den Rechtsklick nicht!
