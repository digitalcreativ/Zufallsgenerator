# Logbuch – Zufallsbild-Generator als offline HTML

## Projektziel

Entwicklung einer einzelnen, vollständig offline funktionierenden HTML-Datei für den Unterricht. Die Datei soll Zeichnungsanleitungen als Bilder verwalten und daraus zufällig ein Bild für die Klasse auswählen.

## 1. Ausgangsidee

Der Zufallsgenerator soll aus einer Sammlung von Bildern jeweils ein noch aktives Bild auswählen.

Nach der Bearbeitung kann die Lehrperson entscheiden:

- **Bild erledigt** → Bild wird inaktiv und kann in der aktuellen Runde nicht mehr ausgewählt werden.
- **Bild aktiv lassen** → Bild bleibt aktiv und kann später erneut ausgewählt werden.

Wenn alle Bilder einer Auswahl inaktiv sind, kann die Liste zurückgesetzt und eine neue Runde begonnen werden.

## 2. Anforderungen

### Bildverwaltung

Die Bilder sollen direkt in der HTML-Datei gespeichert werden.

Für jedes Bild gibt es klar benannte Felder:

- **Bild**
- **Name**
- **Kategorie**

Die Bilddatei soll möglichst einfach über die Benutzeroberfläche hinzugefügt werden können.

### Zufallsauswahl

Der Benutzer soll:

1. eine Kategorie auswählen können,
2. ein zufälliges aktives Bild ziehen können,
3. das Bild gross und beamerfreundlich sehen,
4. das Bild als erledigt markieren oder aktiv lassen können,
5. danach zum nächsten Bild wechseln können.

### Speicherung

Der Status eines Bildes soll zwischen verschiedenen Nutzungen auf demselben Computer erhalten bleiben. Dafür wird `localStorage` verwendet.

## 3. Kategorien

Für die Zeichnungsanleitungen wurden sieben Kategorien festgelegt:

1. Tiere
2. Pflanzen
3. Dinge
4. Comics
5. Kawaii
6. Gebäude
7. Fantasy

Zusätzlich gibt es **Alle Kategorien**.

Der Zufallsgenerator berücksichtigt beim Ziehen sowohl den gewählten Kategoriefilter als auch den Aktiv/Inaktiv-Status.

## 4. Zurücksetzen

Die Bezeichnung für das Zurücksetzen einer einzelnen Kategorie wurde ausdrücklich festgelegt:

> **Kategorie zurücksetzen**

Zusätzlich gibt es:

> **Alle Bilder zurücksetzen**

Damit kann entweder nur die aktuell gewählte Kategorie oder die gesamte Sammlung wieder aktiviert werden.

## 5. Technische Lösung

### Bilder

Die Bilder werden als Data-URLs/Base64-Daten in der HTML-Datei gespeichert.

Beispielhafte interne Struktur:

```javascript
{
    id: "...",
    name: "Katze",
    category: "Tiere",
    image: "data:image/png;base64,..."
}
```

Dadurch benötigt die fertige Datei keine separaten Bilddateien.

### Aktiv/Inaktiv-Status

Der Status wird separat über `localStorage` gespeichert.

Dadurch bleiben die Bilder selbst Bestandteil der HTML-Datei, während der persönliche Nutzungsverlauf des jeweiligen Computers lokal gespeichert wird.

## 6. Beamer-Funktionen

Die Oberfläche wurde auf eine grosse Darstellung ausgelegt.

Enthalten sind:

- grosse Bildfläche
- kontrastreiche Darstellung
- grosse Bedienknöpfe
- Vollbildfunktion
- Anzeige von Bildname und Kategorie
- Anzeige der Anzahl aktiver Bilder
- Tastatursteuerung

Die Leertaste kann für die Zufallsauswahl verwendet werden.

## 7. Bildverwaltung

Es gibt eine separate Ansicht **Bildverwaltung**.

Der Eingabeprozess ist bewusst einfach:

### Feld 1 – Bild

Auswahl einer lokalen Bilddatei.

### Feld 2 – Name

Kurzer Name der Zeichnungsanleitung.

Beispiel:

> Katze

### Feld 3 – Kategorie

Auswahl aus:

- Tiere
- Pflanzen
- Dinge
- Comics
- Kawaii
- Gebäude
- Fantasy

Danach wird das Bild über **Bild zur Sammlung hinzufügen** aufgenommen.

## 8. Bildsammlung

In der Verwaltung wird eine Übersicht aller Bilder angezeigt.

Zu jedem Bild werden angezeigt:

- Vorschaubild
- Name
- Kategorie
- aktueller Status
- Aktivieren/Deaktivieren
- Löschen

## 9. Speicherung und Weitergabe

Die HTML-Datei kann problemlos an andere Lehrpersonen weitergegeben werden.

### Übertragbar

In der HTML-Datei enthalten sind:

- Bilder
- Bildnamen
- Kategorien
- Programmcode
- Oberfläche
- Zufallslogik

### Nicht automatisch übertragbar

Der gespeicherte Aktiv/Inaktiv-Status liegt im Browser des jeweiligen Computers.

Wenn eine Lehrperson die Datei weitergibt, erhält die andere Lehrperson die Bildsammlung, aber nicht automatisch den persönlichen Nutzungsverlauf.

## 10. Exportfunktion

Die aktuelle Version enthält:

> **Fertige HTML-Datei erstellen**

Damit kann die aktuelle Bildsammlung inklusive eingebetteter Bilder als neue eigenständige HTML-Datei ausgegeben werden.

Die erzeugte Datei kann anschliessend unabhängig weitergegeben und offline verwendet werden.

## 11. Aktuelle Datei

Erstellt wurde:

`Zufallsbild-Generator.html`

Die Datei ist eine einzelne HTML-Datei und benötigt keine externe Bibliothek und keine Internetverbindung.

## 12. Bereits umgesetzt

- [x] Einzelne HTML-Datei
- [x] Offline-Funktion
- [x] Bilder direkt in der HTML-Datei
- [x] Bildname
- [x] Kategorien
- [x] Sieben Kategorien
- [x] Filter „Alle Kategorien“
- [x] Zufallsauswahl
- [x] Aktive/inaktive Bilder
- [x] „Bild erledigt“
- [x] „Bild aktiv lassen“
- [x] „Nächstes Bild“
- [x] „Kategorie zurücksetzen“
- [x] „Alle Bilder zurücksetzen“
- [x] Speicherung des Status mit `localStorage`
- [x] Bildverwaltung
- [x] Bilder hinzufügen
- [x] Bilder löschen
- [x] Bilder manuell aktivieren/deaktivieren
- [x] Vollbildmodus
- [x] Beamerfreundliche Darstellung
- [x] Tastatursteuerung
- [x] Export einer neuen HTML-Datei

## 13. Mögliche Weiterentwicklungen

### A. Weitergabe-Modus

Ein eigener Button:

> **Kopie für Weitergabe erstellen**

Dieser sollte eine saubere HTML-Datei erzeugen, in der alle Bilder wieder aktiv sind und kein persönlicher Nutzungsverlauf weitergegeben wird.

### B. Schnelleres Einpflegen vieler Bilder

Für eine grosse Sammlung wäre eine noch effizientere Eingabemaske sinnvoll, beispielsweise:

- mehrere Bilder auswählen
- Namen automatisch aus Dateinamen übernehmen
- Kategorie anschliessend schnell festlegen
- mehrere Bilder hintereinander bearbeiten

### C. Bearbeiten bestehender Bilder

Ein bestehender Datensatz könnte direkt bearbeitet werden:

- Bild ersetzen
- Name ändern
- Kategorie ändern

### D. Statistiken

Mögliche Anzeige:

> 24 Bilder insgesamt · 17 aktiv · 7 verwendet

und zusätzlich je Kategorie.

### E. Schutz vor versehentlichem Zurücksetzen

Die Reset-Funktionen könnten eine kurze Bestätigung verlangen.

## 14. Grundsätze für die weitere Entwicklung

Die Anwendung soll weiterhin:

- **offline funktionieren**
- **ohne Installation** auskommen
- **eine einzelne HTML-Datei** bleiben
- für Lehrpersonen **einfach zu bedienen** sein
- am Beamer **gross und übersichtlich** erscheinen
- möglichst wenig technische Kenntnisse voraussetzen

Die Bildverwaltung soll deshalb klarer und einfacher sein als die technische Struktur der HTML-Datei.

## 15. Technische Erkenntnis zur Bilderkennung

Eine vollständig offline laufende HTML-Datei kann Bilder zuverlässig speichern und verwalten. Eine automatische inhaltliche Bilderkennung („Dieses Bild zeigt eine Katze“) wäre dagegen eine wesentlich komplexere Aufgabe und würde ein Bildanalysemodell benötigen.

Für dieses Projekt ist deshalb die manuelle Kategorisierung über das Feld **Kategorie** die robuste und transparente Lösung.

## 16. Stand des Projekts

**Status:** Funktionsfähiger Prototyp erstellt.

**Datei:** `Zufallsbild-Generator.html`

**Nächster sinnvoller Entwicklungsschritt:** Verbesserung der Weitergabe- und Importfunktionen sowie Vereinfachung der Eingabe einer grösseren Bildsammlung.
