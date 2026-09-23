# Logbuch – Zufallsbild-Generator

## 1. Projektübersicht

**Projekt:** Zufallsbild-Generator  
**Aktueller Stand:** 23. September 2026  
**Hauptdatei:** `index.html`  
**Bilderordner:** `Bilder/`

Der Zufallsbild-Generator ist eine browserbasierte Anwendung für den Unterricht. Er wählt zufällig eine Zeichenanleitung aus einer Bildsammlung aus. Die Anwendung benötigt keine Installation und kann lokal sowie über eine statische Website verwendet werden.

## 2. Ziele

Die Anwendung soll:

- für Lehrpersonen einfach bedienbar sein,
- auf einem Beamer gut funktionieren,
- Bilder zufällig auswählen,
- verwendete Bilder vorübergehend aus der Auswahl entfernen,
- Bilder nach Kategorien filtern,
- acht Zeichenschritte einzeln vergrössern,
- die Bildverwaltung direkt zugänglich machen,
- möglichst ohne externe Bibliotheken auskommen.

## 3. Projektstruktur

```text
Zufallsgenerator/
├── index.html
├── Logbuch.md
├── README.md
└── Bilder/
    ├── Eis_am_Stiel.png
    ├── Elefant.png
    ├── Faultier.png
    ├── Giraffe.png
    ├── Muffin.png
    ├── Panda.png
    └── Wichtel.png
```

Die Datei `index.html` enthält Oberfläche, Gestaltung und Programmlogik. Die vorbereiteten Bilder werden über relative Pfade aus dem Ordner `Bilder` geladen.

## 4. Bildsammlung und Kategorien

Aktuell sind sieben Bilder registriert:

| Bild | Kategorie |
|---|---|
| Elefant | Tiere |
| Faultier | Tiere |
| Giraffe | Tiere |
| Panda | Tiere |
| Wichtel | Fantasy |
| Eis am Stiel | Dinge, Kawaii |
| Muffin | Dinge, Kawaii |

Ein Bild kann einer oder mehreren Kategorien angehören. Mehrfach kategorisierte Bilder erscheinen im Filter jeder zugewiesenen Kategorie, unter „Alle Kategorien“ aber nur einmal.

Verfügbare Kategorien:

- Tiere
- Pflanzen
- Dinge
- Comics
- Kawaii
- Gebäude
- Fantasy

## 5. Zufallsauswahl

Die Lehrperson kann eine Kategorie oder „Alle Kategorien“ auswählen. Der Generator zieht danach zufällig eines der aktiven Bilder.

Nach einer Auswahl stehen folgende Aktionen zur Verfügung:

- **Bild erledigt:** Das aktuelle Bild wird deaktiviert und vorläufig nicht erneut gezogen.
- **Bild aktiv lassen:** Das Bild bleibt in der Auswahl und es wird weitergezogen.
- **Nächstes Bild:** Es wird ein weiteres aktives Bild ausgelost.
- **Kategorie zurücksetzen:** Alle Bilder der gewählten Kategorie werden wieder aktiviert.
- **Alle Bilder zurücksetzen:** Die gesamte Sammlung wird wieder aktiviert.

Der Aktiv-/Inaktiv-Status wird im `localStorage` des verwendeten Browsers gespeichert. Dieser Status gilt nur für das jeweilige Gerät und Browserprofil.

## 6. Bild-Vollbildmodus

Der Knopf **„Bild im Vollbild“** vergrössert nur den Bildbereich, nicht die gesamte Bedienoberfläche. Das Bild wird vollständig vor schwarzem Hintergrund dargestellt.

Der Vollbildmodus kann mit `Esc` oder durch erneutes Betätigen verlassen werden.

## 7. Lupenansicht der acht Schritte

Die Zeichenanleitungen bestehen aus acht Teilbildern in zwei Reihen mit je vier Schritten.

Ein Klick auf einen Schritt öffnet eine vergrösserte Einzelansicht. Die Navigation erfolgt über:

- **Zurück** und **Weiter**,
- die Pfeiltasten `←` und `→`,
- `Esc` oder `✕` zum Schliessen.

Nach Schritt 8 wird wieder Schritt 1 angezeigt. In der Gegenrichtung folgt auf Schritt 1 der Schritt 8.

### Automatische Rastererkennung

Da sich die Positionen der Raster zwischen den Vorlagen leicht unterscheiden, verwendet die Anwendung keine ausschliesslich festen Ausschnitte mehr. Sie analysiert die roten Schrittnummern und berechnet daraus die Positionen der beiden Bildreihen.

Jeder berechnete Ausschnitt erhält zusätzlich einen kleinen Rand. Dadurch soll der vollständige schwarze Rahmen des Teilbildes in der Lupenansicht sichtbar bleiben.

Wenn die automatische Erkennung bei einem Bild nicht möglich ist, greift die Anwendung auf ein Standardraster zurück.

## 8. Öffentliche Bildverwaltung

Die Bildverwaltung ist ohne Passwortabfrage direkt über den Knopf **„Bildverwaltung“** zugänglich.

## 9. Bilder einzeln hinzufügen

In der Bildverwaltung kann ein Bild als lokale Datei oder über eine Bild-URL hinzugefügt werden. Zusätzlich werden ein Name und eine Kategorie erfasst.

Lokale Bilder werden als Data-URL eingelesen. Bei externen URLs kann der Import an den CORS-Regeln der jeweiligen Website scheitern. In diesem Fall muss das Bild zuerst lokal gespeichert und anschliessend als Datei ausgewählt werden.

## 10. Bilderordner importieren

Über **„Bilderordner einlesen“** kann ein ganzer Ordner ausgewählt werden.

Beim Import:

- werden unterstützte Bilddateien eingelesen,
- wird der Dateiname ohne Endung als Bildname verwendet,
- erhalten neue Bilder die aktuell gewählte Kategorie,
- werden bereits vorhandene Bildnamen übersprungen,
- werden importierte Bilder für den späteren Export eingebettet.

Eine lokale HTML-Datei darf aus Sicherheitsgründen Ordner nicht selbstständig durchsuchen. Deshalb muss der Ordnerimport bewusst durch die Benutzerin oder den Benutzer gestartet werden.

## 11. Bildverwaltung

Die Sammlung zeigt alle registrierten Bilder als Karten. Für jedes Bild werden Name, Kategorie beziehungsweise Kategorien und Aktivstatus angezeigt.

Mögliche Aktionen:

- Bild aktivieren,
- Bild deaktivieren,
- Bild löschen,
- neues Bild hinzufügen,
- Bilderordner einlesen,
- Browserstatus löschen,
- fertige HTML-Datei exportieren.

## 12. Exportfunktion

Mit **„Fertige HTML-Datei erstellen“** wird eine neue HTML-Datei erzeugt, die den aktuellen Stand der Bildsammlung enthält.

Wichtig:

- Änderungen in der laufenden Browseransicht überschreiben die ursprüngliche `index.html` nicht.
- Nach Änderungen muss die Exportfunktion verwendet werden, wenn die neue Sammlung dauerhaft in einer HTML-Datei gespeichert werden soll.
- Bereits über relative Pfade eingebundene Bilder benötigen weiterhin den Ordner `Bilder`.
- Über die Bildverwaltung importierte Dateien werden als Data-URLs in die exportierte Datei eingebettet.

## 13. Tastatursteuerung

| Taste | Funktion |
|---|---|
| Leertaste | Zufallsbild auswählen |
| Enter | Aktuelles Bild als erledigt markieren und weiterziehen |
| Pfeil links | Vorheriger Schritt in der Lupenansicht |
| Pfeil rechts | Nächster Schritt in der Lupenansicht |
| Esc | Lupen- oder Vollbildansicht verlassen |

## 14. Technische Grundlagen

Die Anwendung verwendet:

- HTML für die Struktur,
- CSS für Gestaltung, Vollbild- und Lupenansicht,
- JavaScript für Zufallsauswahl, Kategorien, Status und Bildverwaltung,
- die Fullscreen API für den Bild-Vollbildmodus,
- Canvas für die vergrösserten Schrittausschnitte,
- `localStorage` für den Nutzungsstatus,
- FileReader und Data-URLs für lokale Bildimporte.

Es werden keine externen JavaScript- oder CSS-Bibliotheken geladen.

## 15. Bekannte Grenzen

- Neue Dateien im Ordner `Bilder` werden nicht automatisch erkannt. Sie müssen importiert oder in `INITIAL_IMAGES` eingetragen werden.
- Die automatische Rastererkennung setzt voraus, dass die Vorlagen rote Schrittnummern und ein Raster mit vier Spalten und zwei Reihen besitzen.
- Bei stark abweichenden Vorlagen kann das Standardraster verwendet werden und der Ausschnitt weniger genau sein.
- Der Browserstatus wird nicht zwischen Geräten synchronisiert.
- Der Passwortschutz einer statischen HTML-Datei ist kein Hochsicherheitsschutz.
- Externe Bild-URLs können durch CORS blockiert werden.

## 16. Bedienungsablauf für den Unterricht

1. `index.html` im Browser öffnen.
2. Gewünschte Kategorie auswählen.
3. „Zufallsbild auswählen“ anklicken.
4. Bei Bedarf „Bild im Vollbild“ verwenden.
5. Einen der acht Schritte anklicken, um die Lupenansicht zu öffnen.
6. Mit den Pfeilen Schritt für Schritt weitergehen.
7. Lupenansicht schliessen.
8. Bild als erledigt markieren oder aktiv lassen.

## 17. Mögliche Weiterentwicklungen

- Manuelle Feinkalibrierung der acht Ausschnitte pro Bild
- Mehrfachauswahl von Kategorien beim Import
- Bearbeiten von Namen und Kategorien bestehender Bilder
- Import und Export einer separaten Sammlungsdatei
- Weitergabe-Modus mit zurückgesetztem Nutzungsstatus
- Anzeige von Statistiken pro Kategorie

## 18. Aktueller Projektstatus

Der Zufallsbild-Generator ist als funktionsfähige Unterrichtsanwendung umgesetzt. Zufallsauswahl, Mehrfachkategorien, Bild-Vollbild, Lupenansicht, automatische Rastererkennung, Ordnerimport, Export und öffentlich zugängliche Bildverwaltung sind vorhanden.

Vor der Verwendung mit einer neuen Bildserie sollte kontrolliert werden, ob alle acht Rahmen in der Lupenansicht vollständig sichtbar sind.
