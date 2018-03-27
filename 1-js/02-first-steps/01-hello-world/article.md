# Hello, world!

Dieses Tutorial behandelt Java-Script, im Kern eine plattformunabhängige Technik. Später wenden wir uns Node.js und anderen Plattformen zu die JavaScript verwenden.

Doch zunächst benötigen wir eine Umgebung in der wir unsere Scripte ausführen können. Da dies ein Online-Buch ist, liegt es nahe, den Browser zu verwenden. Wir vermeiden so weit als möglich browserspezifische Anweisungen (wie `alert`) so dass Sie keine Zeit darauf verlieren, wenn ihr späteres Augenmerk eigentlich Node.js sein soll. Interessieren Sie sich aber für die Browserdetails, so behandeln wir diese ausführlich im [nächsten Teil](/ui) des Tutorials.

Fangen wir aber damit an, wie man ein Script in eine Webseite einbettet. Befinden Sie sich in einer serverseitigen Umgebung können Sie ein Script mit einem Kommando wie `"node my.js"` mit Node.js ausführen.


## Das "script"-Tag

JavaScript-Programme können überall innerhalb eines HTML-Dokuments mit Hilfe des `<script>`-Tags platziert werden.

Zum Beispiel:

```html run height=100
<!DOCTYPE HTML>
<html>

<body>

  <p>Vor dem Script...</p>

*!*
  <script>
    alert( 'Hello, world!' );
  </script>
*/!*

  <p>...Nach dem Script.</p>

</body>

</html>
```

```online
Sie können die Beispiele in diesem Tutorial laufen lassen, indem Sie den "Play"-Knopf in der oberen rechten Ecke anklicken.
```

Das `<script>`-Tag beinhaltet JavaScript-Code der automatisch ausgeführt wird, wenn der Browser den Tag erreicht.

## Der moderne Dialekt

Das `<script>`-Tag besitzt einige Attribute die heute nicht mehr eingesetzt werden, die man aber in älterem Code finden kann:

**Das `type`-Attribut: <code>&lt;script <u>type</u>=...&gt;</code>**

Der alte HTML4-Standard sah vor, dass Scripte einen Typ haben müssen, typischerweise `type="text/javascript"`. Der aktuelle HTML-Standard nimmt diesen Typ als Standardwert an; eine Angabe des Attributes ist nicht notwendig.

**Das `language`-Attribut: <code>&lt;script <u>language</u>=...&gt;</code>**

Dieses Attribut sollte die Programmiersprache des Scripts anzeigen. Da diese standardmäßig JavaScript ist, gibt es keine Notwendigkeit das Attribut zu verwenden.

**Kommentare vor und nach Scripten**

In sehr alten Anleitungen, Büchern und Codes findet man Kommentare innerhalb von `<script>`, so wie diesen:
```html no-beautify
<script type="text/javascript"><!--
...
//--></script>
```

Solche Kommentare sollten den Script-Code vor älteren Browsern verstecken, die mit dem `<script>`-Tag noch nichts anfangen konnten. Aber alle Browser aus mindestens den letzten 15 Jahren haben dieses Problem nicht. Wir zeigen dieses Idiom hier als ein Warnzeichen. Wenn Sie es irgendwo entdecken, können Sie davon ausgehen, dass der Code wirklich sehr alt ist und es sich nicht lohnt, sich näher damit zu befassen.

## Externe Scripte

Wenn wir sehr viel JavaScript-Code auf unserer Seite haben, können wir diesen in einer separaten Datei platzieren. Die Datei wird mit dem `src`-Attribute zur HTML-Webseite hinzugefügt:

```html
<script src="/pfad/zum/script.js"></script>
```

`/fad/zum/script.js` ist eine absolute Pfadangabe zur Script-Datei, ausgehend vom Wurzelverzeichnis der Seite.

Alternativ können auch relative Pfade angegeben werden. Zum Beispiel heißt `src="script.js"` das eine Datei `"script.js"` im aktuellen Ordner verwendet werden soll.

Auch eine vollständige URL kann angegeben werden:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js"></script>
```

Mehrere Scripte können mit mehreren `script`-Tags geladen werden:

```html
<script src="/js/script1.js"></script>
<script src="/js/script2.js"></script>
…
```

```smart
Nur die aller einfachsten Scripte sollten direkt in eine HTML-Datei geschrieben werden. Komplexere Dinge landen in einer eigenen Datei.

Ein Vorteil davon ist, dass Browser diese Dateien in ihrem [Cache](https://de.wikipedia.org/wiki/Cache) vorhalten, nachdem sie einmal geladen wurden. Verwendet eine andere Seite das selbe Script, kann dieses aus dem Cache genommen werden und muss nicht nochmal aus dem Web geladen werden. Das spart Web-Traffic und beschleunigt Seiten.
```

````warn header="Wenn `src` gesetzt wurde, wird der Inhalt von `<script>` ignoriert."
Ein einzelner `<script>`-Tag kann kein `src`-Attribute und JavaScript-Code beinhalten.

Das hier würde nicht funktionieren:

```html
<script *!*src*/!*="file.js">
  alert(1); // Der Inhalt wird ignoriert, das src verwendet wird
</script>
```

Wir können das Beispiel in zwei Scripte aufteilen um es lauffähig zu machen:

```html
<script src="file.js"></script>
<script>
  alert(1);
</script>
```
````

## Zusammenfassung

- Wir können das `<script>`-Tag verwenden um JavaScript-Code zu einer Webseite hinzuzufügen.
- Die Attribute `type` und `language` werden nicht länger benötigt.
- Ein Script aus einer anderen Datei kann mit `<script src="pfad/zum/script.js"></script>` geladen werden.

Es gibt noch viel mehr über Scripte im Browser und deren Interaktion mit Webseiten zu sagen. In diesem Teil des Tutorials soll es aber nur um die Sprache JavaScript gehen und wir wollen uns davon zunächst nicht ablenken. Wir nutzen den Browser zunächst als eine bequeme Möglichkeit um JavaScript-Code ablaufen zu lassen.