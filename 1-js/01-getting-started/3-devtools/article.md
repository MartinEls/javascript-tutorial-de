# Entwicklerkonsole

Code ist immer anfällig für Fehler. Auch Sie werden wahrscheinlich Fehler machen... Nein was sage ich, Sie werden *ganz bestimmt* Fehler machen, zumindest wenn Sie ein Mensch sind und kein [Roboter](https://en.wikipedia.org/wiki/Bender_(Futurama)).

Im Browser allerdings sehen wir standardmäßig keine Fehlermeldungen. Wenn also etwas in unserem Script schief läuft bekommen wir nicht mit was los ist und können daher auch das Problem nicht beheben.

Um solche Fehler besser erkennen zu können und noch viele weitere nützliche Informationen über Scripte und deren Verhalten zu bekommen, besitzen Browser eingebaute Entwicklerwerkzeuge.

Die meisten Entwickler verwenden Chrome oder Firefox für Ihre Entwicklungen, da diese Browser über die umfangreichsten Entwicklerwerkzeuge verfügen. Andere Browser bieten auch Entwicklerwerkzeuge, zum Teil mit sehr nützlichen, zusätzlichen Funktionen. Generell laufen diese aber Chrome und Firefox etwas hinterher. Viele Entwickler haben einen "Lieblingsbrowser" und wechseln zu einem anderen, falls spezielle Probleme auftreten.

Die Entwicklerwerkzeuge sind wirklich mächtig und es gibt zahlreiche Funktionen. Zu Beginn schauen wir uns an, wie man sie im Browser öffnet, sich Fehler anschaut und wie man JavaScript-Befehle ausführt.

## Chrome

Öffnen Sie die Seite [bug.html](bug.html).

Im JavaScript-Code ist ein Fehler, der dem Auge des normalen Seitenbesuchers verborgen bleibt. Lassen Sie uns darauf einen Blick mithilfe der Entwicklerwerkzeuge werfen.

Drücken Sie `key:F12` oder, `key:Cmd+Opt+J` an einem Mac.

Standardmäßig öffnet sich der Konsolen-Tab, und es sieht ungefähr so aus:

![chrome](chrome.png)

Das genaue Aussehen hängt von der verwendeten Chrome-Version ab und ändert sich hin und wieder, sollte aber ähnlich aussehen.

- Wir sehen in rot eine Fehlermeldung, die besagt, dass unser Script einen unbekannten Befehl mit dem Namen "lalala" enthält.
- Auf der rechten Seite befindet sich ein anklickbarer Link `bug.html:12` der auf die Codezeile mit dem Fehler verweist.

Unterhalb der Fehlermeldung befindet sich ein blaues `>`-Symbol. Es markiert eine Eingabekonsole in die wir JavaScript-Befehle eingeben können. Ein druck auf `key:Enter` lässt den Code ablaufen (`key:Shift+Enter` erlaubt es mehrzeilige Anweisungen einzugeben).

So können wir Fehler einsehen und das ist an dieser Stelle erstmal genug. Wir gehen im Kapitel <info:debugging-chrome> noch einmal näher auf die Entwicklerwerkzeuge ein.

## Firefox, Edge und andere

In den meisten Browsern kann man mit `key:F12` die Entwicklerwerkzeuge öffnen.

Aussehen und Funktion ist sehr ähnlich. Hat man einen ausgiebiger kennengelernt, kann man leicht zu einem anderen Browser wechseln.

## Safari

Safari (der Mac-Browser, keine Windows/Linux-Versionen) ist etwas spezieller. Hier muss zuerst das sog. "Entwicklermenü" eingeschaltet werden.

Öffnen Sie "Einstellungen" und gehen auf "Erweitert". Dort gibt es eine Option zum Anzeigen des Entwickler-Menüs. Ist diese aktiviert erscheint ein weiterer Menüeintrag mit zahlreichen Befehlen und Optionen.

Nun erlaubt die Tastenkombination `key:Cmd+Opt+C` die Entwicklerkonsole zu öffnen.

## Zusammenfassung

- Entwicklerwerkzeuge erlauben uns Fehler zu erkennen, Befehle auszuführen, den Inhalt von Variablen zu inspizieren und einiges mehr.
- Sie werden durch `key:F12` unter Windows und Linux geöffnet. Chrome für Mac verwendet `key:Cmd+Opt+J` und Safari: `key:Cmd+Opt+C`.

Nun haben wir unseren Werkzeugkasten gefüllt. Im nächsten Kapitel beginnen wir mit der JavaScript-Entwicklung.
