# Bézierkurven

Bézierkurven werden in der Computergrafik verwendet um Formen zu beschreiben, für CSS-Animationen und auch an vielen anderen Stellen.

Sie sind letztlich eine recht einfache Konstruktion, die es sich einmal detailliert zu studieren lohnt um sich in der Welt der Vektorgrafik und der Animationen heimisch zu fühlen.

## Kontrollpunkte

Eine [Bézierkurve](https://de.wikipedia.org/wiki/Bézierkurve) wird durch Kontrollpunkte definiert.

Es kann 2, 3, 4 oder auch mehr geben.

Zum Beispiel sieht eine Bézierkurve mit zwei Kontrollpunkten wie folgt aus:

![](bezier2.png)

Eine Bézierkurve mit drei Kontrollpunkten:

![](bezier3.png)

Und eine Bézierkurve mit vier Kontrollpunkten:

![](bezier4.png)

Ein etwas genauerer Blick auf diese Kurven offenbart uns einige interessante Eigenschaften:

1. **Kontrollpunkte müssen nicht auf der Kurve liegen.** Wir werden später sehen, wie genau die Bézierkurven konstruiert werden.
2. **Die Ordnung der Kurve ist gleich die Anzahl der Kontrollpunkte minus eins**
Aus zwei Kontrollpunkten erhalten wir eine gerade Linie, aus drei Punkten eine quadratische Kurve und aus vier Kontrollpunkten eine kubische Kurve.
3. **Die Bézierkurve liegt immer innerhalb der [konvexen Hülle](https://de.wikipedia.org/wiki/Konvexe_Hülle) der Kontrollpunkte:**

    ![](bezier4-e.png) ![](bezier3-e.png)

Von der letzten Eigenschaft können wir gebrauch machen, wenn wir Kurven auf Überschneidungen testen wollen. Überschneiden sich die konvexen Hüllen nicht, dann tun es die zugehörigen Bézierkurven auch nicht. Prüft man also zuerst ob keine Überschneidungen der konvexen Hüllen vorliegen, so hat man einen schnellen Ausschlusstest für die Kurvenüberschneidung. Da die konvexen Hüllen eine einfacherer Form haben als die Kurven selbst, ist hier ein schnellerer Test auf Überschneidungen möglich.

Einen großen Wert bieten Bézierkurven beim Erstellen von Zeichnungen. Verschiebt man die Kontrollpunkte, verändert die Kurve ihre Form in einer sehr intuitiven Art und Weise.

Versuchen Sie die Kontrollpunkte im untenstehenden Beispiel mit der Maus zu verschieben und sehen Sie, was dabei passiert:

[iframe src="demo.svg?nocpath=1&p=0,0,0.5,0,0.5,1,1,1" height=370]

**Man kann feststellen, dass sich die Bézierkurve entlang der Tangenten zwischen 1 -> 2 und 3 -> 4 erstreckt.**

Mit etwas Übung schafft man es schnell, die Punkte so zu platzieren, dass man die gewünschte Kurve erhält. Aus der Verbindung mehrerer Kurven kann man praktisch jedes Objekt modellieren, hier ein paar Beispiele:

![](bezier-car.png) ![](bezier-letter.png) ![](bezier-vase.png)

## Die Mathematik dahinter

Bézierkurven werden durch vergleichsweise einfache Formeln beschrieben. Wir werden bald sehen, dass man diese nicht unbedingt kennen muss, aber zur Vollständigkeit schauen wir sie uns kurz an.

Die Kontrollpunkte <code>P<sub>i</sub></code> lauten: Der erste Kontrollpunkt hat die Koordinaten <code>P<sub>1</sub> = (x<sub>1</sub>, y<sub>1</sub>)</code>, der zweite Kontrollpunkt: <code>P<sub>2</sub> = (x<sub>2</sub>, y<sub>2</sub>)</code>, und so weiter. Die Koordinaten der Bézierkurve werden von Gleichungen beschrieben die vom Parameter `t` im Interval `[0, 1]` abhängen.

- Die Formel für eine 2-Punktkurve lautet:

    <code>P = (1-t)P<sub>1</sub> + tP<sub>2</sub></code>
- Für eine 3-Punktkurve:

    <code>P = (1−t)<sup>2</sup>P<sub>1</sub> + 2(1−t)tP<sub>2</sub> + t<sup>2</sup>P<sub>3</sub></code>
- Für eine 4-Punktkurve:

    <code>P = (1−t)<sup>3</sup>P<sub>1</sub> + 3(1−t)<sup>2</sup>tP<sub>2</sub>  +3(1−t)t<sup>2</sup>P<sub>3</sub> + t<sup>3</sup>P<sub>4</sub></code>

Diese drei Gleichungen sind Vektorgleichungen.

Wir können die Gleichungen auch für jede Koordinate einzeln aufschreiben. Die 3-Punktkurve wird dann zum Beispiel zu:

- <code>x = (1−t)<sup>2</sup>x<sub>1</sub> + 2(1−t)tx<sub>2</sub> + t<sup>2</sup>x<sub>3</sub></code>
- <code>y = (1−t)<sup>2</sup>y<sub>1</sub> + 2(1−t)ty<sub>2</sub> + t<sup>2</sup>y<sub>3</sub></code>

Wir ersetzen dann <code>x<sub>1</sub>, y<sub>1</sub>, x<sub>2</sub>, y<sub>2</sub>, x<sub>3</sub>, y<sub>3</sub></code> durch die Koordinaten von unseren Kontrollpunkten.

Lauten also zum Beispiel unsere Kontrollpunkte `(0, 0)`, `(0.5, 1)` und `(1, 0)`, werden unsere Gleichungen zu:

- <code>x = (1−t)<sup>2</sup> * 0 + 2(1−t)t * 0.5 + t<sup>2</sup> * 1 = (1-t)t + t<sup>2</sup> = t</code>
- <code>y = (1−t)<sup>2</sup> * 0 + 2(1−t)t * 1 + t<sup>2</sup> * 0 = 2(1-t)t = –t<sup>2</sup> + 2t</code>

Läuft nun unser Parameter `t` von `0` bis `1`, ein `(x,y)`-Wertepaar für jedes `t` beschreibt die Form der Kurve.

Diese Beschreibung ist vielleicht nicht sehr intuitiv, denn es ist nicht sehr offensichtlich wie die resultierende Bézierkurve aussehen wird und wie die Position der Kontrollpunkte beeinflusst wird.

Schauen wir uns daher einen Algorithmus an, der die Bézierkurve konstruiert und etwas intuitiver zugänglich ist.

## De-Casteljau-Algorithmus

Der [De-Casteljau-Algorithm](https://de.wikipedia.org/wiki/De-Casteljau-Algorithmus) ist identisch zur oben gegebenen mathematischen Definition, zeigt aber visuell, wie die Bézierkurve konstruiert wird.

Schauen wir uns die Funktionsweise des Algorithmusses anhand des 3-Punktbeispiels an. Zunächst eine kleine Demo und anschließend die Erklärungen.

Die Punkte können mit der Maus verschoben werden. Drücken Sie den "Play"-Knopf um den Algorithmus ablaufen zu lassen.

[iframe src="demo.svg?p=0,0,0.5,1,1,0&animate=1" height=370]

**Der De-Casteljau-Algorithmus zur Konstruktion einer 3-Punkt-Bézierkurve:**

1. Einzeichnen der Kontrollpunkte. In unserem Beispiel heißen diese `1`, `2` und `3`.
2. Konstruiere Verbindungslinien zwischen den Kontrollpunkten 1 -> 2 und 2 -> 3. In unserem Beispiel in <span style="color:#825E28">braun</span> eingezeichnet.
3. Der Parameter `t` läuft wieder von `0` bis `1`. In unserem Beispiel verwenden wir eine Schrittweite von `0.05`: `t` nimmt also die Werte `0, 0.05, 0.1, 0.15, ... 0.95, 1` an.

    Für jeden dieser Werte von `t`:

    - Auf jedem der <span style="color:#825E28">braunen</span> Segmente suchen wir einen Punkt der um den Anteil `t` vom Anfang entfernt liegt. Da es zwei <span style="color:#825E28">braune</span> Segmente gibt, erhalten wir auch zwei Punkte.

        Zum Beispiel liegen für `t = 0` beide Punkte am Anfang der Segmente; für `t = 0.25` liegen die Punkte 25% der Segmentlänge vom Anfang entfernt; für `t = 0.5` in der Mitte der Segmente; und für `t = 1` am Ende der Segmente.

    - Verbinde die so erhaltenen Punkte. In der folgenden Abbildung ist die Verbindungslinie in <span style="color:#167490">blau</span> eingezeichnet.


| Für `t=0.25`             | Für `t=0.5`            |
| ------------------------ | ---------------------- |
| ![](bezier3-draw1.png)   | ![](bezier3-draw2.png) |

4. Auf dem neuen <span style="color:#167490">blauen</span> Segment suchen wir einen Punkt der um den Anteil `t` vom Anfang entfernt liegt. Für `t = 0.25` (die linke Abbildung) erhalten wir einen Punkt ein Viertel der Segmentlänge vom Ende entfernt. Für `t = 0.5` (die rechte Abbildung) liegt der Punkt in der Segmentmitte. Der neue Punkt ist mit <span style="color:red">rot</span> in den Abbildungen eingezeichnet.

5. Läuft nun `t` von `0` bis `1`, wird für jeden Wert von `t` ein Punkt der Kurve hinzugefügt. Alle diese Punkte zusammen bilden die Bézierkurve.

Analog zu diesem Beispiel einer 3-Punktkurve, funktioniert auch die Konstruktion für eine 4-Punktkurve.

In der folgenden Demo können wieder die Punkte mit der Maus verschoben werden:

[iframe src="demo.svg?p=0,0,0.5,0,0.5,1,1,1&animate=1" height=370]

Der Algorithmus wird zu:

- Die vier Kontrollpunkte werden durch die drei <span style="color:#825E28">braunen</span> Segmente 1 -> 2, 2 -> 3 und 3 -> 4 verbunden.
- Für jedes `t` aus dem Interval von `0` bis `1`:
    - Suchen wir einen Punkt auf jedem Segment, der um den Anteil `t` vom Anfang entfernt liegt. Diese Punkte werden verbunden, so das wir zwei neue <span style="color:#0A0">grüne</span> Segmente erhalten.
    - Auf diesen Segmenten suchen wir wieder Punkte die `t` vom Anfang entfernt liegen und wir erhalten ein neues <span style="color:#167490">blaues</span> Segment.
    - Auf diesem <span style="color:#167490">blauen</span> Segment suchen wir wiederum einen Punkt der um `t` vom Anfang entfernt liegt. In unserem Beispiel ein <span style="color:red">roter</span> Punkt.
- Diese Punkte zusammen bilden die Bézierkurve.

Der Algorithmus arbeitet rekursiv und kann daher für eine beliebige Anzahl von Kontrollpunkten verallgemeinert werden.

Haben wir `N` Kontrollpunkte vorliegen, verbinden wir diese und erhalten anfänglich `N - 1` Segmente.

Für jedes `t` von `0` bis `1`:
- Suche auf jedem Segment einen Punkt der um den Anteil `t` vom Anfang entfernt liegt und verbinde diese; man erhält `N - 2` Segmente.
- Wiederhole diesen Schritt, bis nur noch ein Punkt übrig bleibt. Diese Punkte bilden die Bézierkurve.

Hier einige Beispiele:

[iframe src="demo.svg?p=0,0,0,0.75,0.25,1,1,1&animate=1" height=370]

Mit anderen Punkten:

[iframe src="demo.svg?p=0,0,1,0.5,0,0.5,1,1&animate=1" height=370]

Eine Schleife:

[iframe src="demo.svg?p=0,0,1,0.5,0,1,0.5,0&animate=1" height=370]

Nicht stetige Bézierkurven:

[iframe src="demo.svg?p=0,0,1,1,0,1,1,0&animate=1" height=370]

Da der Algorithmus rekursiv arbeitet können wir Bézierkurven jeder beliebiger Ordnung, mit 5, 6 oder mehr Kontrollpunkten konstruieren. Von praktischer Bedeutung sind jedoch nur solche mit 2-4 Kontrollpunkten. Komplexere Figuren werden durch Verknüpfung mehrerer Kurven erstellt. Diese sind einfacher zu konstruieren und zu berechnen.

```smart header="Wie zeichnet man eine Linie durch *gegebene* Punkte?"
Bézierkurven werden durch ihre Kontrollpunkte definiert. Mit der Ausnahme von linearen Bézierkurven, liegen die Kontrollpunkte nicht nur auf der Kurve selbst.

Möchten wir also eine durchgehende Kurve durch *einige gegebene* Punkte zeichnen sind Bézierkurven nicht geeignet. Diese Aufgabe heißt [Interpolation](https://de.wikipedia.org/wiki/Interpolation_(Mathematik)), und wir gehen hier nicht näher darauf ein.

Es gibt einige mathematische Verfahren zur [Polynominterpolation](https://de.wikipedia.org/wiki/Polynominterpolation) und in der Computergrafik verwendet man die [Spline-Interpolation](https://de.wikipedia.org/wiki/Spline-Interpolation) um viele Punkte durch eine optisch ansprechende Kurve zu verbinden.
```

## Zusammenfassung

Bézierkurven werden durch ihre Kontrollpunkte definiert. Wir haben uns zwei Möglichkeiten angeschaut um sie zu konstruieren:

1. Verwendung der Vektorgleichungen.
2. Der intuitive Zeichnungsweg mit dem De-Casteljau-Algorithmus

Vorteilhafte Eigenschaften von Bézierkurven:

- Wir können geschwungene Linien mit der Maus zeichnen, indem wir Kontrollpunkte bewegen.
- Komplexe Formen können erstellt werden, indem man mehrere Bézierkurven miteinander verbindet.

Verwendung:

- In der Computergrafik und Modellierung, in Vektorgrafikeditoren und für viele Schriftarten.
- In der Webentwicklung für Grafiken zum Beispiel im SVG-Format. Übrigens sind die obigen Live-Beispiele in SVG geschrieben. Es ist immer die selbe Datei der verschiedene Startpunkte als Parameter übergeben werden. Sie können die Datei in einem separaten Fenster öffnen und den Quelltext betrachten [demo.svg](demo.svg?p=0,0,1,0.5,0,0.5,1,1&animate=1).
- Bei CSS-Animationen um den Weg und die Geschwindigkeit der Animation zu kontrollieren.
