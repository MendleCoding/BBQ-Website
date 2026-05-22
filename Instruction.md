# Instruction.md

## Feste Arbeitsanweisung fuer Codex

Bei jeder Erweiterung, Aenderung oder neuen Funktion an dieser BBQ-Website muss zuerst diese Datei gelesen werden.

Diese Datei beschreibt die verbindliche Struktur, Navigation, Dateibenennung und Funktionslogik der digitalen BBQ-Speisekarten-Website. Neue Menues und Features muessen sich am aktuellen Apple-Bourbon-Smoke-Menue orientieren, damit spaeter alles gleich aufgebaut ist.

## Aktueller Standard

- Derzeit ist 1 Menue vorhanden.
- Weitere Menues folgen spaeter und sollen nach dem gleichen Muster aufgebaut werden.
- Die Website ist eine digitale Menue-App, keine Download-Sammlung.
- Rezept- und Einkaufslisteninhalte werden direkt in der Website als starke Informationsseiten aufgebaut.
- ODT-Dateien dienen als Inhaltsquelle, sollen aber nicht als sichtbare Hauptlinks angezeigt werden.
- Die obere Hauptnavigation ist die zentrale Navigation.
- Zusaetzliche Buttons wie `Zur Speisekarte`, `Zum Gang` oder `Zurueck` sollen nicht im Inhalt angezeigt werden, solange der Nutzer sie nicht ausdruecklich wuenscht.
- Speisekarten- und Gangbilder sollen per Klick als reine Grafikansicht angezeigt werden.

## Ziel der Website

Die Website stellt digitale BBQ-Speisekarten dar.

Der Nutzer startet in der Menue-Ansicht. Dort sieht er die Speisekarte und die vorhandenen Gang-Karten. Ueber die obere Navigation kann er jederzeit zwischen Menue, Vorspeise, Hauptspeise, Beilage und Dessert wechseln.

Eine vollstaendige Speisekarte kann aus folgenden Bereichen bestehen:

- Vorspeise
- Hauptspeise
- Beilage
- Dessert

Fehlende Bereiche sind erlaubt und werden nicht angezeigt.

## Verbindliches Funktionsdiagramm

```text
WEBSITE
|
|-- Obere Hauptnavigation
|   |-- Menue
|   |-- Vorspeise, falls vorhanden
|   |-- Hauptspeise, falls vorhanden
|   |-- Beilage, falls vorhanden
|   |-- Dessert, falls vorhanden
|
|-- Menue-Ansicht
|   |-- Speisekarte.png gross sichtbar
|   |-- Kurzbeschreibung des Menues
|   |-- Karten fuer alle vorhandenen Gaenge
|
|-- Gang-Ansicht
|   |-- Gangbild gross sichtbar
|   |-- Titel, Untertitel, Kurzbeschreibung
|   |-- Meta-Informationen, z. B. Portionen, Temperatur, Charakter
|   |-- Auswahlkarte Einkaufsliste
|   |-- Auswahlkarte Rezept
|
|-- Einkaufsliste-Unterseite
|   |-- Zutaten direkt als strukturierte Karten
|   |-- Keine ODT-Links anzeigen
|
|-- Rezept-Unterseite
|   |-- Zubereitungsschritte direkt als strukturierte Karten
|   |-- Setup, Timing und Profi-Hinweise als Zusatzkarten
|
|-- Reine Grafikansicht
|   |-- Klick auf Speisekarte.png oder Gangbild oeffnet nur die Grafik
|   |-- Keine zusaetzlichen Zurueck-Buttons in der Bildansicht
|   |-- Navigation weiterhin ueber die obere Hauptnavigation
```

## Erwartete Dateien pro vollstaendigem Menue

Wenn ein neues Menue geliefert wird, koennen die Dateien so aussehen:

```text
Speisekarte.png

Vorspeise.png
VorspeiseEinkaufsliste.odt
VorspeiseRezept.odt

Hauptspeise.png
HauptspeiseEinkaufsliste.odt
HauptspeiseRezept.odt

Beilage.png
BeilageEinkaufsliste.odt
BeilageRezept.odt

Dessert.png
DessertEinkaufsliste.odt
DessertRezept.odt
```

Die Dateinamen sind feste Konvention. Fuer die Website werden die Bilder kopiert und die ODT-Inhalte in strukturierte Website-Daten uebertragen.

## Asset-Struktur

Jedes Menue bekommt einen eigenen Asset-Ordner:

```text
assets/
|-- menue-id/
|   |-- Speisekarte.png
|   |-- Vorspeise.png
|   |-- Hauptspeise.png
|   |-- Beilage.png
|   |-- Dessert.png
```

Beispiel:

```text
assets/apple-bourbon-smoke/
```

Alte, nicht mehr verwendete Bilder sollen entfernt werden, wenn ein Menue ersetzt wird.

## Datenstruktur fuer Gaenge

Fuer die aktuelle Umsetzung ist pro Gang diese Struktur bevorzugt:

```js
{
  id: "vorspeise",
  label: "Vorspeise",
  title: "Gegrillte Mais-Tartelette",
  subtitle: "mit Apfel-Senf-Creme & Pickle-Fenchel",
  image: "assets/menue-id/Vorspeise.png",
  meta: ["6 Portionen", "Plancha 200-220 °C", "Frisch"],
  intro: "Kurzer Beschreibungstext des Gangs.",
  shopping: [
    ["Komponente", "Zutaten und Mengen"]
  ],
  steps: [
    "Zubereitungsschritt 1"
  ],
  panels: [
    ["Setup", "Zusatzinformation"]
  ]
}
```

`shopping`, `steps` und `panels` werden aus den gelieferten Rezept- und Einkaufslisten-Dateien aufgebaut.

## Schritt-fuer-Schritt-Anleitung fuer ein neues Menue

1. `Instruction.md` lesen.
2. Pruefen, welche Kategorien vorhanden sind: Vorspeise, Hauptspeise, Beilage, Dessert.
3. Einen neuen Asset-Ordner pro Menue anlegen, z. B. `assets/neues-menue/`.
4. Gelieferte Bilder nach fester Konvention in diesen Ordner kopieren.
5. Gelieferte ODT-Dateien nur als Quelle verwenden.
6. Text aus Rezepten und Einkaufslisten extrahieren.
7. Inhalte in die strukturierte Datenform uebertragen:
   - `shopping` fuer Zutaten und Mengen
   - `steps` fuer Zubereitungsschritte
   - `panels` fuer Setup, Timing, Servieren, Profi-Tipps oder wichtige Hinweise
8. Nur vorhandene Gaenge in Navigation und Menue-Ansicht anzeigen.
9. Pro Gang eine Gang-Ansicht erstellen:
   - Bild vollstaendig anzeigen
   - Titel, Untertitel, Beschreibung und Meta-Daten anzeigen
   - Auswahlkarten fuer Einkaufsliste und Rezept anzeigen
10. Pro Gang eine Einkaufsliste-Unterseite erstellen:
    - Zutaten gruppiert als Karten anzeigen
    - Mengen gut lesbar darstellen
11. Pro Gang eine Rezept-Unterseite erstellen:
    - Schritte klar nummeriert oder als Prozesskarten darstellen
    - Setup, Timing und Profi-Tipps als Zusatzkarten darstellen
12. Bildklick aktivieren:
    - Speisekarte und Gangbilder sollen als reine Grafikansicht oeffnen
    - Die Grafikansicht zeigt nur die Grafik
13. Navigation testen:
    - Menue
    - Vorspeise
    - Hauptspeise
    - Beilage
    - Dessert
    - Einkaufsliste pro Gang
    - Rezept pro Gang
    - Bildansicht pro Bild
14. Mobile Darstellung pruefen:
    - Bilder duerfen nicht abgeschnitten sein
    - Text darf nicht ueberlappen
    - Karten muessen sauber umbrechen
15. Erst nach Funktionspruefung committen und pushen, wenn der Nutzer es wuenscht.

## Navigationslogik

```text
Start
 |
 v
Menue-Ansicht
 |
 |-- obere Navigation: Menue
 |-- obere Navigation: Vorspeise
 |-- obere Navigation: Hauptspeise
 |-- obere Navigation: Beilage
 |-- obere Navigation: Dessert
 |
 v
Gang-Ansicht
 |
 |-- Einkaufsliste-Karte
 |     |
 |     v
 |     Einkaufsliste-Unterseite
 |
 |-- Rezept-Karte
 |     |
 |     v
 |     Rezept-Unterseite
 |
 |-- Klick auf Grafik
       |
       v
       Reine Grafikansicht
```

Die obere Hauptnavigation ist der Rueckweg und Hauptweg. Keine separaten Zurueck-Buttons im Inhalt verwenden.

## Sonderfall: reduzierte Menues

Es kann vorkommen, dass eine Speisekarte nicht aus allen Bereichen besteht.

Beispiel: Der Nutzer liefert nur ein Hauptgericht.

Dann fehlen Vorspeise, Beilage und Dessert absichtlich. In diesem Fall darf die Website keine leeren Bereiche fuer fehlende Kategorien anzeigen.

```text
WEBSITE
|
|-- Obere Hauptnavigation
|   |-- Menue
|   |-- Hauptspeise
|
|-- Menue-Ansicht
|-- Hauptspeise-Ansicht
|-- Einkaufsliste-Unterseite
|-- Rezept-Unterseite
|-- Reine Grafikansicht
```

Wichtig:

- Fehlende Kategorien sind kein Fehler.
- Fehlende Kategorien nicht als Platzhalter anzeigen.
- Nur vorhandene Dateien und Kategorien in Navigation und Menue-Ansicht zeigen.

## Gewuenschte Bedienung

- Die obere Hauptnavigation reicht fuer den Wechsel zwischen Menue und Gaengen aus.
- Die aktive Ansicht muss in der oberen Navigation sichtbar markiert werden.
- Kategorien sollen visuell als einzelne Karten dargestellt werden.
- Jede vorhandene Kategorie braucht ein Titelbild.
- Einkaufsliste und Rezept sollen getrennt aufrufbar sein.
- Einkaufsliste und Rezept sollen Website-Unterseiten sein, keine ODT-Downloadlinks.
- Bilder muessen anklickbar sein und als reine Grafik angezeigt werden koennen.
- Bilder duerfen auf Desktop und Mobilgeraeten nicht abgeschnitten werden.
- Nicht vorhandene Kategorien sollen ausgeblendet werden.
- Die Struktur soll spaeter leicht erweiterbar sein.

## Seitenstruktur

Die Website ist als Single-Page-App in `index.html` aufgebaut.

```text
index.html
|-- Header mit Hauptnavigation
|-- View: Menue
|-- View: Gang-Detail
|-- View: Einkaufsliste-Unterseite
|-- View: Rezept-Unterseite
|-- View: reine Bildansicht
```

Die Views duerfen per JavaScript dynamisch gerendert werden. Wichtig ist, dass die Navigation stabil bleibt und keine nicht vorhandenen Kategorien erzeugt werden.

## Designrichtung

Die Website soll wie eine digitale BBQ-Menuekarte wirken:

- BBQ-Atmosphaere
- klare Kartenstruktur
- grosse appetitliche Bilder
- einfache obere Hauptnavigation
- gut lesbare Texte
- keine ueberladene Startseite
- keine doppelten Navigationsbuttons im Inhalt
- der Nutzer soll direkt die Speisekarten benutzen koennen

## Bildregeln

- Grafiken immer vollstaendig anzeigen, nicht croppen.
- Fuer Speisekarten- und Ganggrafiken `object-fit: contain` verwenden.
- Klick auf Speisekarte oder Gangbild oeffnet eine reine Grafikansicht.
- In der reinen Grafikansicht keine Zusatzbuttons anzeigen, solange nicht ausdruecklich gewuenscht.
- Text und Bilder duerfen mobil nicht ueberlappen.

## Erweiterungsregeln

Wenn neue Speisekarten ergaenzt werden:

1. Neue Menues muessen im gleichen Muster wie das aktuelle Menue aufgebaut werden.
2. Die Datei `Speisekarte.png` ist das Hauptbild der Speisekarte.
3. Vorhandene Kategorien sollen anhand ihrer Dateien eingebunden werden.
4. Nicht vorhandene Kategorien sollen nicht angezeigt werden.
5. Jede vorhandene Kategorie soll ein Titelbild bekommen.
6. Rezept- und Einkaufslisteninhalte sollen direkt als Website-Inhalte aufgebaut werden.
7. Fehlende Inhalte sollen sichtbar abgefangen werden, z. B. mit `Noch kein Rezept vorhanden`.
8. Die obere Hauptnavigation muss immer funktionieren.
9. Die Website muss auf Desktop und Mobilgeraeten bedienbar bleiben.
10. Die reine Grafikansicht per Bildklick muss erhalten bleiben.
11. Zusatztasten wie `Zur Speisekarte`, `Zum Gang` oder `Zurueck` nicht einbauen, solange der Nutzer sie nicht ausdruecklich wuenscht.

## Prioritaet bei zukuenftigen Aenderungen

Bei Erweiterungen gilt folgende Reihenfolge:

1. Funktionierende obere Hauptnavigation
2. Verstaendliche Speisekarten-Struktur
3. Korrekte Behandlung fehlender Kategorien
4. Rezept- und Einkaufslisteninhalte direkt in der Website
5. Saubere mobile Darstellung
6. Gute Bilder und visuelle Wirkung
7. Animationen oder zusaetzliche Effekte erst danach

## Wichtigste Codex-Anweisung

Vor jeder Erweiterung oder groesseren Aenderung an dieser Website:

```text
Lies zuerst die Datei Instruction.md.
Baue jedes weitere Menue im gleichen Muster wie das aktuelle Apple Bourbon Smoke Menue.
Nutze die obere Hauptnavigation als zentrale Navigation.
Zeige nur Kategorien an, die fuer die jeweilige Speisekarte wirklich vorhanden sind.
Baue Einkaufsliste und Rezept als starke Informationsseiten in die Website ein.
Verwende ODT-Dateien als Inhaltsquelle, nicht als sichtbare Hauptlinks.
Zeige keine unnoetigen Zurueck-Buttons im Inhalt.
Erhalte die reine Grafikansicht per Bildklick.
Halte Bilder vollstaendig sichtbar und mobil sauber.
```
