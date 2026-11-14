# Logbuch 2 – Weiterentwicklung des Zufallsbild-Generators

## 1. Projektstand

**Projekt:** Zufallsbild-Generator  
**Stand:** 14. November 2026  
**Hauptdatei:** `index.html`  
**Bilderordner:** `Bilder/`

Der Zufallsbild-Generator ist eine browserbasierte Anwendung für den Unterricht. Aus einer Sammlung von Zeichenanleitungen wird zufällig ein aktives Bild ausgewählt. Die Anwendung läuft ohne Installation direkt im Browser und benötigt keine externen Bibliotheken.

In dieser Entwicklungsphase wurden vor allem die Bildsammlung, die Kategorien und die Bildverwaltung erweitert. Zudem wurde sichergestellt, dass alle mitgelieferten Bilder wieder aktiv starten. Zuletzt wurde das Bild **Cactus** durch **Kaktus 2** ersetzt.

## 2. Ziel der Weiterentwicklung

Die bestehende Anwendung sollte so ausgebaut werden, dass:

- mehr Zeichenanleitungen zur Verfügung stehen,
- Bilder mehreren passenden Kategorien zugeordnet werden können,
- die gesamte Sammlung übersichtlich verwaltet werden kann,
- neue Bilder einzeln oder ordnerweise ergänzt werden können,
- alle Bilder beim aktuellen Start wieder aktiv sind,
- die Anwendung weiterhin einfach, offline und beamerfreundlich bleibt.

## 3. Aktuelle Bildsammlung

Zurzeit sind 50 Bilder fest in der Anwendung registriert:

| Bild | Kategorie beziehungsweise Kategorien |
|---|---|
| Babydrache | Fantasy |
| Bananenbaum | Pflanzen |
| Baumhaus | Gebäude, Fantasy |
| Biber | Tiere |
| Café | Gebäude, Dinge |
| Campingbus | Dinge |
| Dackel | Tiere |
| Delfin | Tiere |
| Eis am Stiel | Dinge |
| Elefant | Tiere |
| Erdbeerpflanze | Pflanzen |
| Faultier | Tiere |
| Flamingo 2 | Tiere |
| Fliegenpilz 2 | Pflanzen, Fantasy |
| Fussballspieler | Comics |
| Giraffe | Tiere |
| Gitarre | Dinge |
| Handy | Dinge |
| Haus | Gebäude |
| Heissluftballon | Dinge |
| Iglu | Gebäude |
| Kaffeetasse | Dinge |
| Kaktus 2 | Pflanzen |
| Katze | Tiere |
| Lebkuchenmann | Weihnachten |
| Leuchtturm | Gebäude |
| Mädchen | Comics |
| Monsterchen | Fantasy |
| Muffin | Dinge |
| Oktopus | Tiere |
| Palme | Pflanzen |
| Panda | Tiere |
| Pilzhaus | Gebäude, Fantasy |
| Pinguin | Tiere |
| Piratenschiff | Dinge |
| Rakete | Dinge |
| Rentier | Weihnachten |
| Roboter | Dinge, Comics |
| Saturn | Dinge |
| Schaf | Tiere |
| Schildkröte | Tiere |
| Schloss | Gebäude, Fantasy |
| Schneemann | Weihnachten |
| Skateboarder | Comics |
| Sonnenblume | Pflanzen |
| Velofahrerin | Comics |
| Wecker | Dinge |
| Weihnachtsbaum | Weihnachten |
| Wichtel | Weihnachten |
| Zauberin | Fantasy, Comics |

Alle 50 dazugehörigen Dateien befinden sich im Ordner `Bilder/` und sind in `index.html` eingetragen. Die drei älteren, nicht mehr verwendeten Dateien `Delfin.jpg`, `Octopus.jpg` und `Schaf.jpg` wurden gelöscht. Sie sind durch PNG-Versionen ersetzt.

## 4. Kategorien

Die Anwendung bietet folgende Kategorien:

- Tiere
- Pflanzen
- Dinge
- Comics (ersetzt die frühere Kategorie «Figuren»)
- Gebäude
- Fantasy
- Weihnachten
- Alle Kategorien

Ein Bild kann einer einzelnen oder mehreren Kategorien zugewiesen sein. Beispielsweise gehört das Café sowohl zu **Gebäude** als auch zu **Dinge**. Bei der Auswahl **Alle Kategorien** erscheint jedes Bild trotzdem nur einmal.

## 5. Zufallsauswahl

Die Lehrperson wählt zuerst eine Kategorie und lässt danach ein zufälliges aktives Bild anzeigen.

Folgende Aktionen stehen zur Verfügung:

- **Zufallsbild auswählen:** Zieht ein zufälliges Bild aus der aktuellen Auswahl.
- **Bild zurück:** Zeigt das vorher angezeigte Bild nochmals an. Mehrmaliges Klicken geht weiter zurück. Wurde das Bild als erledigt markiert, wird es dabei wieder aktiviert.
- **Bild erledigt:** Setzt das angezeigte Bild auf inaktiv und zieht anschliessend weiter.
- **Nächstes Bild:** Zieht ein weiteres Bild, ohne den Status des aktuellen Bildes zu verändern. Das gerade angezeigte Bild wird dabei nicht sofort nochmals gezogen (ausser es ist das letzte aktive Bild).
- **Kategorie zurücksetzen:** Aktiviert sämtliche Bilder der ausgewählten Kategorie.
- **Alle Bilder zurücksetzen:** Aktiviert die gesamte Bildsammlung.

Sind alle Bilder einer Kategorie erledigt, erscheint direkt in der Bildfläche eine Meldung mit dem Button **Kategorie zurücksetzen** (bzw. **Alle Bilder zurücksetzen**).

Zusätzlich steht ein **Zeichen-Timer** zur Verfügung (siehe Abschnitt 18).

## 6. Aktiv- und Inaktivstatus

Jedes Bild besitzt einen Aktivstatus:

- **aktiv:** Das Bild kann vom Zufallsgenerator ausgewählt werden.
- **inaktiv:** Das Bild wurde erledigt oder in der Verwaltung deaktiviert und wird nicht gezogen.

Der Status wird im lokalen Browserspeicher (`localStorage`) gespeichert. Dadurch bleibt er beim Schliessen und erneuten Öffnen auf demselben Gerät erhalten.

### Zurücksetzen des bisherigen Status

Am 24. September 2026 wurde der Speicherschlüssel von `zufallsbild_status_v1` auf `zufallsbild_status_v2` geändert. Damit werden ältere Inaktiv-Markierungen nicht mehr übernommen. Beim ersten Öffnen dieser Version starten deshalb alle mitgelieferten Bilder aktiv. Später ergänzte Bilder besitzen zunächst ebenfalls automatisch den Status `active: true`.

Nach diesem einmaligen Neustart speichert die Anwendung neue Statusänderungen weiterhin wie gewohnt.

Später wurde der Schlüssel ein weiteres Mal auf `zufallsbild_status_v3` erhöht. Dies ist der aktuell verwendete Speicherschlüssel.

## 7. Bildverwaltung

Die Bildverwaltung ist über einen eigenen Reiter ohne Passwort erreichbar. Sie zeigt alle Bilder als Karten mit folgenden Informationen:

- Vorschaubild,
- Name,
- Kategorie oder Kategorien,
- Aktiv- beziehungsweise Inaktivstatus.

Für jedes Bild stehen Schaltflächen zum Aktivieren, Deaktivieren und Löschen bereit. Oberhalb der Sammlung wird zusätzlich angezeigt, wie viele Bilder insgesamt, aktiv und inaktiv sind.

## 8. Neue Bilder hinzufügen

Ein neues Bild kann auf zwei Arten hinzugefügt werden:

1. als lokale Bilddatei,
2. über eine direkte Bild-URL.

Zusätzlich werden ein eindeutiger Name und eine Kategorie erfasst. Neu hinzugefügte Bilder sind automatisch aktiv.

Lokale Dateien werden als Data-URL eingelesen. Beim Laden über eine URL können die Sicherheitseinstellungen der fremden Website den Zugriff verhindern. In diesem Fall muss das Bild zuerst heruntergeladen und anschliessend als lokale Datei ausgewählt werden.

## 9. Bilderordner importieren

Über **Bilderordner einlesen** lassen sich mehrere Bilder auf einmal importieren.

Dabei gilt:

- Es werden nur unterstützte Bilddateien übernommen.
- Der Dateiname ohne Dateiendung wird als Bildname verwendet.
- Alle neu eingelesenen Bilder erhalten die aktuell ausgewählte Kategorie.
- Bereits vorhandene Bildnamen werden übersprungen.
- Alle importierten Bilder werden aktiv angelegt.

Der Ordner muss bewusst über den Dateidialog ausgewählt werden, weil Browser aus Sicherheitsgründen nicht selbstständig auf lokale Ordner zugreifen dürfen.

## 10. Exportfunktion

Mit **Fertige HTML-Datei erstellen** lässt sich der aktuelle Stand der Bildsammlung als neue HTML-Datei exportieren.

Dabei werden:

- Namen und Kategorien übernommen,
- neu importierte Bilder direkt eingebettet,
- keine persönlichen Aktiv- oder Inaktivmarkierungen in die Bilddaten übernommen,
- alle Bilder in der exportierten Grundsammlung wieder als aktiv initialisiert.

Die bestehende `index.html` wird vom Browser nicht automatisch überschrieben. Die erzeugte Datei wird stattdessen als neue Datei heruntergeladen.

## 11. Vollbild- und Tastaturbedienung

Das angezeigte Bild kann durch Anklicken oder über **Bild im Vollbild** gross dargestellt werden. Der Vollbildmodus lässt sich mit `Esc` wieder verlassen.

Zusätzlich stehen folgende Tastenkürzel zur Verfügung:

| Taste | Funktion |
|---|---|
| Leertaste | Zufallsbild auswählen |
| Enter | Angezeigtes Bild als erledigt markieren und weiterziehen |
| Esc | Vollbildmodus verlassen |

## 12. Technische Umsetzung

Die Anwendung besteht aus einer einzigen zentralen Datei `index.html`. Darin befinden sich:

- HTML für Aufbau und Inhalte,
- CSS für Gestaltung und responsive Darstellung,
- JavaScript für Auswahl, Status, Kategorien, Import und Export.

Weitere verwendete Browserfunktionen sind:

- `localStorage` für den Aktivstatus und die Liste der gelöschten Bilder,
- IndexedDB für selbst hinzugefügte Bilder (dauerhaft im Browser gespeichert),
- FileReader und Data-URLs für lokale Bilder,
- Fullscreen API für die Grossansicht,
- Blob und Object-URL für den HTML-Export.

Die vorbereiteten Bilder liegen als separate Dateien im Ordner `Bilder/`. Bilder, die über die Verwaltung importiert und danach exportiert werden, werden direkt in die neu erzeugte HTML-Datei eingebettet.

### Farbkonzept

Der Rotton der nummerierten Zeichenschritte wird als wiederkehrende Akzentfarbe eingesetzt. Der aus den Bildern ermittelte Hauptton `#FD5855` erscheint beim aktiven Reiter **Generator** sowie auf den Schaltflächen **Zufallsbild auswählen** und **Nächstes Bild**. Der Button **Bild erledigt**, die Kategorieanzeigen und der Hinweisbalken unter dem Vorschaubild verwenden passend zum Button **Bild im Vollbild** den neutralen Grauton `#E8EDF5`. Schwarz, Weiss und weitere zurückhaltende neutrale Farben bilden den Rahmen der Oberfläche.

## 13. Überprüfung

Nach der letzten Anpassung wurde kontrolliert:

- `index.html` enthält 50 Bildeinträge, und zu jedem Eintrag gibt es die passende Datei im Ordner `Bilder/` (Stand 14. November 2026).
- Die Grundinitialisierung setzt jedes Bild auf `active: true`.
- Einzel- und Ordnerimporte legen neue Bilder ebenfalls aktiv an.
- Durch den neuen Speicherschlüssel werden alte Inaktiv-Markierungen nicht mehr geladen.

## 14. Bekannte Grenzen

- Der Aktivstatus sowie hinzugefügte und gelöschte Bilder werden nur im jeweiligen Browser und auf dem jeweiligen Gerät gespeichert. Für ein anderes Gerät muss eine fertige HTML-Datei exportiert werden.
- Neue Dateien im Ordner `Bilder/` werden nicht automatisch erkannt; sie müssen importiert oder im Programmcode ergänzt werden.
- Direkte Bild-URLs können durch CORS-Regeln der Quellwebsite blockiert werden.
- Eine exportierte HTML-Datei mit relativen Bildpfaden benötigt weiterhin den zugehörigen Ordner `Bilder/`.
- Änderungen in der geöffneten Anwendung verändern die ursprüngliche HTML-Datei nicht automatisch.

## 15. Aktueller Abschlussstand

Der Zufallsbild-Generator ist einsatzbereit. Die Bildsammlung umfasst 50 Zeichenanleitungen, die Kategorien und Mehrfachzuordnungen funktionieren, und die Bilder können direkt in der Anwendung verwaltet werden.

Alle aktuell mitgelieferten Bilder starten in dieser Version aktiv. Damit steht für den nächsten Einsatz eine vollständig zurückgesetzte Sammlung zur Verfügung.

## 16. Fehlerbehebungen (14. November 2026)

Bei einer Durchsicht des Codes wurden vier Fehler gefunden und behoben.

### Enter-Taste löste zwei Aktionen aus

**Problem:** Nach einem Klick auf «Zufallsbild auswählen» blieb dieser Button ausgewählt. Ein anschliessendes Drücken von Enter markierte das Bild als erledigt und löste zusätzlich den Button aus. Dadurch wurden zwei Bilder gezogen.

**Lösung:** Die Enter-Taste führt jetzt nur noch «Bild erledigt» aus. Die Standardaktion des Browsers wird unterdrückt. In Eingabefeldern hat Enter keine Wirkung auf den Generator.

### «Nächstes Bild» zeigte manchmal dasselbe Bild

**Problem:** Das aktuell angezeigte Bild wurde bei der Auswahl nicht ausgeschlossen. Bei wenigen aktiven Bildern erschien oft dasselbe Bild nochmals.

**Lösung:** Das aktuelle Bild wird beim Ziehen ausgeschlossen, solange mindestens ein anderes aktives Bild vorhanden ist.

### Hinzugefügte Bilder verschwanden beim Neuladen

**Problem:** Im Browser wurde nur der Aktivstatus gespeichert, nicht die Bilder selbst. Bilder, die in der Verwaltung hinzugefügt und nicht exportiert wurden, gingen beim Neuladen verloren. Gelöschte Bilder erschienen nach dem Neuladen wieder.

**Lösung:**

- Hinzugefügte Bilder (einzeln oder per Ordnerimport) werden in der IndexedDB des Browsers gespeichert. Diese bietet deutlich mehr Platz als `localStorage`.
- Gelöschte Bilder werden in einer Liste (`zufallsbild_geloescht_v1`) im `localStorage` vermerkt und beim Start ausgeblendet.
- Schlägt das Speichern fehl, erscheint ein Hinweis, die Sammlung sofort zu exportieren.
- Bilder, die nach einem Export bereits in der HTML-Datei stehen, werden nicht doppelt geladen.
- Die Schaltfläche **Browser-Speicher für diese Datei löschen** setzt jetzt alles zurück: Erledigt-Status, hinzugefügte und gelöschte Bilder. Vorher erscheint eine Rückfrage, die erklärt, was verloren geht.

### Exportierte Datei war unnötig gross

**Problem:** Der Export kopierte die Seite im aktuell angezeigten Zustand. Eingebettete Bilder standen dadurch mehrfach in der Datei (Bilddaten, Bildsammlung, Vorschau). Zudem öffnete sich die exportierte Datei auf dem Reiter «Bildverwaltung».

**Lösung:** Beim Laden der Seite wird der saubere Ausgangszustand gesichert und für den Export verwendet. Jedes Bild steht nun nur einmal in der Datei, und die exportierte Datei startet auf dem Reiter «Generator». Zusätzlich werden Sonderzeichen in Bildnamen so maskiert, dass sie den Programmcode nicht beschädigen können.

### Angepasste Hinweistexte

Die Erklärungen im Bereich «Änderungen dauerhaft in dieser HTML-Datei speichern» wurden an das neue Verhalten angepasst. Sie weisen darauf hin, dass Änderungen im Browser gespeichert bleiben, für andere Geräte aber ein Export nötig ist.

## 17. Weitere Anpassungen (14. November 2026)

### Programm startete nicht mehr (Git-Konflikt)

**Problem:** Beim Wiederherstellen eines älteren, zwischengespeicherten Stands («Stash») in Git wurden zwei Versionen von `index.html` vermischt. Git schrieb Konfliktmarkierungen (`<<<<<<<`, `=======`, `>>>>>>>`) in den Code. Der Browser konnte das Skript deshalb nicht mehr ausführen, und die Anwendung blieb leer.

Zusätzlich enthielt ein Kommentar im Code die Zeichenfolge `</script>`. Der Browser liest diese Zeichenfolge auch innerhalb eines Kommentars als Ende des Skripts und schnitt den restlichen Code ab.

**Lösung:** Die beiden Versionen wurden zusammengeführt:

- Übernommen aus dem aktuellen Stand: alle Bilder, die Fehlerbehebungen aus Abschnitt 16 und das rote Farbkonzept.
- Übernommen aus dem älteren Stand: die neuen Kategorien (Comics statt Figuren sowie Fantasy).
- Nicht übernommen: der Button «Bild aktiv lassen», weil er genau dasselbe machte wie «Nächstes Bild».

Der Kommentar mit `</script>` wurde umformuliert. Ausserdem zeigt die Anwendung die mitgelieferten Bilder jetzt sofort an. Im Browser gespeicherte Bilder werden kurz danach ergänzt. Die Seite bleibt dadurch nie leer, auch wenn der Browser-Speicher langsam reagiert.

**Lehre:** Nach einem Stash oder Merge in Git lohnt es sich, die Dateien nach Konfliktmarkierungen zu durchsuchen und den Konflikt anschliessend in Git als gelöst zu markieren.

### Bildsammlung und Kategorien erweitert

Die Sammlung wurde auf 50 Bilder erweitert, unter anderem mit Weihnachtsmotiven, Gebäuden und Fantasy-Figuren (siehe Abschnitt 3). Die Kategorie «Weihnachten» kam neu dazu, und die vorübergehend eingeführte Kategorie «Kawaii» wurde wieder entfernt.

### Symbole auf den Buttons entfernt

Die Symbole auf den Buttons (zum Beispiel ⛶, ✓, ↻, ＋, 📁, 💾) stammten aus anderen Schriften als der Text (Arial). Dadurch wirkte die Oberfläche uneinheitlich. Sie wurden entfernt. Der farbige Würfel 🎲 bleibt im Titel und auf dem Button «Zufallsbild auswählen».

Ein schwarz-weisser Würfel (⚄) wurde ausprobiert, gefiel aber weniger gut und wurde wieder durch 🎲 ersetzt.

### Neuer Button «Bild zurück»

Links neben «Bild erledigt» gibt es neu den Button **Bild zurück**:

- Er zeigt das zuvor angezeigte Bild nochmals an. Mehrmaliges Klicken geht weiter zurück.
- Wurde das vorherige Bild als erledigt markiert, wird es beim Zurückgehen wieder aktiviert. So lässt sich ein versehentliches «Bild erledigt» rückgängig machen.
- Der Button ist ausgegraut, solange kein vorheriges Bild vorhanden ist.
- Beim Wechsel der Kategorie und beim Zurücksetzen wird der Verlauf geleert.

~~**Grenze:** Ist nach «Bild erledigt» kein aktives Bild mehr übrig, springt «Bild zurück» zum Bild davor und nicht zum zuletzt erledigten Bild.~~ (Behoben, siehe Abschnitt 18.)

### Zähler wird sofort aktualisiert

Die Anzeige «Aktiv: x von y» wurde nach «Bild erledigt» bisher nicht aktualisiert. Sie stimmt jetzt sofort.

### Fehler im Button «Bild zurück» behoben

Der Button funktionierte zuerst nicht: Beim Zurückgehen wurde der ganze Verlauf auf einmal gelöscht statt nur der letzte Eintrag. Der Fehler wurde korrigiert und mit einem automatischen Klicktest überprüft.

## 18. Zeichen-Timer und Meldungen (14. November 2026)

### Zeichen-Timer

Unter den Buttons beim Bild befindet sich die neue Zeile **Zeichenzeit**:

- Wählbar sind 3, 5, 10, 15 oder 20 Minuten (Voreinstellung: 5 Minuten).
- **Timer starten** startet den Countdown. Der Button wechselt danach zu **Pause** bzw. **Weiter**.
- **Timer zurücksetzen** blendet die Anzeige aus. Dasselbe geschieht, wenn eine andere Zeit gewählt wird.
- Die Restzeit erscheint gross **rechts unten** im Bild. So bleibt der Titel der Zeichenanleitung oben frei. Das Feld ist dunkel mit dickem weissem Rand und Schatten und ist deshalb auf hellen und dunklen Bildern gut sichtbar.
- Im Vollbildmodus wird der Timer noch grösser angezeigt.
- Während einer Pause wird die Anzeige blasser.
- Ist die Zeit abgelaufen, erscheint **«Zeit ist um!»** auf rotem Hintergrund und pulsiert einige Male. Bewusst wird kein Ton abgespielt.
- Der Timer läuft weiter, wenn ein neues Bild gezogen wird.

Technisch berechnet der Timer die Restzeit aus der Endzeit (`Date.now()`). Dadurch bleibt er auch dann genau, wenn der Browser kurz beschäftigt ist.

### Meldungen in der Seite statt Popup-Fenster

Bisher erschienen Hinweise wie «Alle Bilder wurden verwendet» als graues Popup-Fenster des Browsers (`alert`). Auf dem Beamer wirkte das störend.

Neu gilt:

- Die Meldung erscheint in weisser Schrift direkt in der Bildfläche.
- Darunter steht ein Button **Kategorie zurücksetzen** bzw. **Alle Bilder zurücksetzen**.
- «Bild erledigt» und «Nächstes Bild» sind dabei ausgegraut.
- Auch der Hinweis «Vollbildmodus wird nicht unterstützt» erscheint als Text statt als Popup.

### Grenze von «Bild zurück» behoben

Wird das letzte Bild einer Kategorie erledigt, führt **Bild zurück** jetzt zu genau diesem Bild zurück und aktiviert es wieder.

### Aufräumen

Die nicht mehr verwendeten Dateien `Delfin.jpg`, `Octopus.jpg` und `Schaf.jpg` wurden aus dem Ordner `Bilder/` gelöscht.

### Überprüfung

Mit einem automatischen Klicktest in Edge wurde geprüft:

- Nach dem Erledigen aller 5 Weihnachtsbilder erscheint die Meldung mit dem Reset-Button.
- «Bild zurück» holt das letzte erledigte Bild zurück (Aktiv: 1 von 5).
- Der Reset-Button aktiviert die Kategorie wieder (Aktiv: 5 von 5).
- Der Timer startet, pausiert, läuft ab («Zeit ist um!») und lässt sich zurücksetzen.

Die neue Grösse und Position des Timers konnten nicht automatisch geprüft werden. Sie müssen im Browser und am Beamer angeschaut werden.
