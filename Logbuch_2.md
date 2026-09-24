# Logbuch 2 – Weiterentwicklung des Zufallsbild-Generators

## 1. Projektstand

**Projekt:** Zufallsbild-Generator  
**Stand:** 24. September 2026  
**Hauptdatei:** `index.html`  
**Bilderordner:** `Bilder/`

Der Zufallsbild-Generator ist eine browserbasierte Anwendung für den Unterricht. Aus einer Sammlung von Zeichenanleitungen wird zufällig ein aktives Bild ausgewählt. Die Anwendung läuft ohne Installation direkt im Browser und benötigt keine externen Bibliotheken.

In dieser Entwicklungsphase wurden vor allem die Bildsammlung, die Kategorien und die Bildverwaltung erweitert. Zudem wurde sichergestellt, dass alle mitgelieferten Bilder wieder aktiv starten.

## 2. Ziel der Weiterentwicklung

Die bestehende Anwendung sollte so ausgebaut werden, dass:

- mehr Zeichenanleitungen zur Verfügung stehen,
- Bilder mehreren passenden Kategorien zugeordnet werden können,
- die gesamte Sammlung übersichtlich verwaltet werden kann,
- neue Bilder einzeln oder ordnerweise ergänzt werden können,
- alle Bilder beim aktuellen Start wieder aktiv sind,
- die Anwendung weiterhin einfach, offline und beamerfreundlich bleibt.

## 3. Aktuelle Bildsammlung

Zurzeit sind 15 Bilder fest in der Anwendung registriert:

| Bild | Kategorie beziehungsweise Kategorien |
|---|---|
| Bananenbaum | Pflanzen |
| Cactus | Pflanzen |
| Elefant | Tiere |
| Eis am Stiel | Dinge, Kawaii |
| Faultier | Tiere |
| Giraffe | Tiere |
| Kaffeetasse | Dinge |
| Kaktus | Pflanzen, Kawaii |
| Katze | Tiere |
| Mädchen | Comics |
| Muffin | Dinge, Kawaii |
| Octopus | Tiere |
| Palme | Pflanzen |
| Panda | Tiere |
| Skateboarder | Comics |

Alle 15 dazugehörigen Dateien befinden sich im Ordner `Bilder/` und sind in `index.html` eingetragen.

## 4. Kategorien

Die Anwendung bietet folgende Kategorien:

- Tiere
- Pflanzen
- Dinge
- Comics
- Kawaii
- Gebäude
- Fantasy
- Alle Kategorien

Ein Bild kann einer einzelnen oder mehreren Kategorien zugewiesen sein. Beispielsweise gehört der Kaktus sowohl zu **Pflanzen** als auch zu **Kawaii**. Bei der Auswahl **Alle Kategorien** erscheint jedes Bild trotzdem nur einmal.

## 5. Zufallsauswahl

Die Lehrperson wählt zuerst eine Kategorie und lässt danach ein zufälliges aktives Bild anzeigen.

Folgende Aktionen stehen zur Verfügung:

- **Zufallsbild auswählen:** Zieht ein zufälliges Bild aus der aktuellen Auswahl.
- **Bild erledigt:** Setzt das angezeigte Bild auf inaktiv und zieht anschliessend weiter.
- **Bild aktiv lassen:** Belässt das Bild in der Auswahl und zieht weiter.
- **Nächstes Bild:** Zieht ein weiteres Bild, ohne den Status des aktuellen Bildes zu verändern.
- **Kategorie zurücksetzen:** Aktiviert sämtliche Bilder der ausgewählten Kategorie.
- **Alle Bilder zurücksetzen:** Aktiviert die gesamte Bildsammlung.

Sind alle Bilder einer Kategorie erledigt, weist die Anwendung darauf hin, dass die Kategorie zurückgesetzt werden kann.

## 6. Aktiv- und Inaktivstatus

Jedes Bild besitzt einen Aktivstatus:

- **aktiv:** Das Bild kann vom Zufallsgenerator ausgewählt werden.
- **inaktiv:** Das Bild wurde erledigt oder in der Verwaltung deaktiviert und wird nicht gezogen.

Der Status wird im lokalen Browserspeicher (`localStorage`) gespeichert. Dadurch bleibt er beim Schliessen und erneuten Öffnen auf demselben Gerät erhalten.

### Zurücksetzen des bisherigen Status

Am 24. September 2026 wurde der Speicherschlüssel von `zufallsbild_status_v1` auf `zufallsbild_status_v2` geändert. Damit werden ältere Inaktiv-Markierungen nicht mehr übernommen. Beim ersten Öffnen dieser Version starten deshalb alle 15 mitgelieferten Bilder aktiv.

Nach diesem einmaligen Neustart speichert die Anwendung neue Statusänderungen weiterhin wie gewohnt.

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

- `localStorage` für den Aktivstatus,
- FileReader und Data-URLs für lokale Bilder,
- Fullscreen API für die Grossansicht,
- Blob und Object-URL für den HTML-Export.

Die vorbereiteten Bilder liegen als separate Dateien im Ordner `Bilder/`. Bilder, die über die Verwaltung importiert und danach exportiert werden, werden direkt in die neu erzeugte HTML-Datei eingebettet.

## 13. Überprüfung

Nach der letzten Anpassung wurde kontrolliert:

- Der Ordner `Bilder/` enthält 15 Bilddateien.
- `index.html` enthält 15 passende Bildeinträge.
- Die Grundinitialisierung setzt jedes Bild auf `active: true`.
- Einzel- und Ordnerimporte legen neue Bilder ebenfalls aktiv an.
- Durch den neuen Speicherschlüssel werden alte Inaktiv-Markierungen nicht mehr geladen.

## 14. Bekannte Grenzen

- Der Aktivstatus wird nur im jeweiligen Browser und auf dem jeweiligen Gerät gespeichert.
- Neue Dateien im Ordner `Bilder/` werden nicht automatisch erkannt; sie müssen importiert oder im Programmcode ergänzt werden.
- Direkte Bild-URLs können durch CORS-Regeln der Quellwebsite blockiert werden.
- Eine exportierte HTML-Datei mit relativen Bildpfaden benötigt weiterhin den zugehörigen Ordner `Bilder/`.
- Änderungen in der geöffneten Anwendung verändern die ursprüngliche HTML-Datei nicht automatisch.

## 15. Aktueller Abschlussstand

Der Zufallsbild-Generator ist einsatzbereit. Die Bildsammlung umfasst 15 Zeichenanleitungen, die Kategorien und Mehrfachzuordnungen funktionieren, und die Bilder können direkt in der Anwendung verwaltet werden.

Alle aktuell mitgelieferten Bilder starten in dieser Version aktiv. Damit steht für den nächsten Einsatz eine vollständig zurückgesetzte Sammlung zur Verfügung.
