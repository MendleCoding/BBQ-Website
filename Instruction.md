# Instruction.md

## Feste Arbeitsanweisung fuer Codex

Bei jeder Erweiterung, Aenderung oder neuen Funktion an dieser BBQ-Website muss zuerst diese Datei gelesen werden.

Diese Datei beschreibt die gewuenschte Struktur, Navigation, Dateibenennung und Funktionslogik der digitalen Speisekarten-Website. Neue Features sollen sich an diesem Ablauf orientieren und die bestehende Seitenlogik nicht brechen.

## Ziel der Website

Die Website stellt digitale BBQ-Speisekarten dar.

Der Nutzer startet im Hauptmenue. Dort sieht er verschiedene Speisekarten. Wenn er auf eine Speisekarte klickt, geht die Navigation eine Ebene tiefer und zeigt die vorhandenen Menuebestandteile.

Eine vollstaendige Speisekarte kann aus folgenden Bereichen bestehen:

- Vorspeise
- Hauptspeise
- Beilage
- Dessert

Jeder vorhandene Bereich soll ein Titelbild haben. Zu jedem vorhandenen Bereich koennen eine Einkaufsliste und ein Rezept aufrufbar sein.

## Funktionsdiagramm

```text
HAUPTMENUE
└── Speisekarten-Uebersicht
    ├── Speisekarte 1
    ├── Speisekarte 2
    ├── Speisekarte 3
    └── Speisekarte n

Beim Klick auf eine Speisekarte:

SPEISEKARTE
├── Speisekarte.png
│
├── Vorspeise
│   ├── Vorspeise.png
│   ├── VorspeiseEinkaufsliste.odt
│   └── VorspeiseRezept.odt
│
├── Hauptspeise
│   ├── Hauptspeise.png
│   ├── HauptspeiseEinkaufsliste.odt
│   └── HauptspeiseRezept.odt
│
├── Beilage
│   ├── Beilage.png
│   ├── BeilageEinkaufsliste.odt
│   └── BeilageRezept.odt
│
└── Dessert
    ├── Dessert.png
    ├── DessertEinkaufsliste.odt
    └── DessertRezept.odt
```

## Erwartete Dateien pro vollstaendiger Speisekarte

Wenn ein neues Rezept beziehungsweise eine neue Speisekarte geliefert wird, koennen die Dateien so aussehen:

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

Die Dateinamen sind als feste Konvention zu behandeln. Wenn moeglich, sollen neue Speisekarten anhand dieser Namen automatisch oder halbautomatisch eingebunden werden.

## Sonderfall: einzelne Gerichte

Es kann vorkommen, dass eine Speisekarte nicht aus allen Bereichen besteht.

Beispiel:

Der Nutzer sagt, dass es nur ein Hauptgericht gibt.

Dann fehlen Vorspeise, Beilage und Dessert absichtlich, weil sie nicht benoetigt werden. In diesem Fall darf die Website keine leeren Bereiche fuer fehlende Kategorien anzeigen.

Die Navigation soll dann vereinfacht werden:

```text
HAUPTMENUE
└── Speisekarte
    └── Hauptspeise
        ├── Hauptspeise.png
        ├── HauptspeiseEinkaufsliste.odt
        └── HauptspeiseRezept.odt
```

Wenn nur ein einzelnes Gericht vorhanden ist, soll die Speisekarte direkt und klar zu diesem Gericht fuehren. Danach soll der Nutzer einfach zurueck zum Hauptmenue oder zur Speisekarten-Uebersicht kommen.

Wichtig:

- Fehlende Kategorien sind kein Fehler.
- Fehlende Kategorien sollen nicht als leere Platzhalter angezeigt werden.
- Der Nutzer muss vorher sagen, wenn nur bestimmte Elemente vorhanden sind.
- Nur vorhandene Dateien und Kategorien sollen in der Navigation erscheinen.

## Navigationslogik fuer vollstaendige Speisekarten

```text
Start
 ↓
Hauptmenue mit mehreren Speisekarten
 ↓ Klick auf Speisekarte
Detailansicht der gewaehlten Speisekarte
 ↓
Vorspeise | Hauptspeise | Beilage | Dessert
 ↓ Klick auf Kategorie
Kategorie oeffnet sich
 ↓
Einkaufsliste oder Rezept auswaehlbar
 ↓
Zurueck zur Kategorie, zur Speisekarte oder zum Hauptmenue
```

## Navigationslogik fuer reduzierte Speisekarten

```text
Start
 ↓
Hauptmenue mit mehreren Speisekarten
 ↓ Klick auf Speisekarte
Nur vorhandene Kategorie anzeigen
 ↓
Einkaufsliste oder Rezept auswaehlbar
 ↓
Zurueck zur Speisekarte oder direkt zum Hauptmenue
```

## Gewuenschte Bedienung

- Blättern zwischen den vorhandenen Bereichen soll moeglich sein.
- Der Nutzer soll jederzeit zur aktuellen Speisekarte zurueck koennen.
- Der Nutzer soll jederzeit zurueck zum Hauptmenue koennen.
- Kategorien sollen visuell als einzelne Bereiche oder Karten dargestellt werden.
- Jede vorhandene Kategorie braucht ein Titelbild.
- Einkaufsliste und Rezept sollen getrennt aufrufbar sein.
- Die Struktur soll spaeter leicht erweiterbar sein.
- Nicht vorhandene Kategorien sollen ausgeblendet werden.

## Empfohlene Seitenstruktur

```text
index.html
├── Hauptmenue
│   └── Speisekarten-Karten
│
├── Speisekarten-Detailansicht
│   ├── Vorspeise, falls vorhanden
│   ├── Hauptspeise, falls vorhanden
│   ├── Beilage, falls vorhanden
│   └── Dessert, falls vorhanden
│
├── Detailbereich Einkaufsliste
│
└── Detailbereich Rezept
```

## Empfohlene Datenstruktur

Speisekarten sollen moeglichst strukturiert gepflegt werden.

Beispiel fuer eine vollstaendige Speisekarte:

```js
const speisekarten = [
  {
    id: "bbq-menue-1",
    titel: "BBQ Menue 1",
    bild: "assets/bbq-menue-1/Speisekarte.png",
    kategorien: {
      vorspeise: {
        titel: "Vorspeise",
        bild: "assets/bbq-menue-1/Vorspeise.png",
        einkaufsliste: "assets/bbq-menue-1/VorspeiseEinkaufsliste.odt",
        rezept: "assets/bbq-menue-1/VorspeiseRezept.odt"
      },
      hauptspeise: {
        titel: "Hauptspeise",
        bild: "assets/bbq-menue-1/Hauptspeise.png",
        einkaufsliste: "assets/bbq-menue-1/HauptspeiseEinkaufsliste.odt",
        rezept: "assets/bbq-menue-1/HauptspeiseRezept.odt"
      },
      beilage: {
        titel: "Beilage",
        bild: "assets/bbq-menue-1/Beilage.png",
        einkaufsliste: "assets/bbq-menue-1/BeilageEinkaufsliste.odt",
        rezept: "assets/bbq-menue-1/BeilageRezept.odt"
      },
      dessert: {
        titel: "Dessert",
        bild: "assets/bbq-menue-1/Dessert.png",
        einkaufsliste: "assets/bbq-menue-1/DessertEinkaufsliste.odt",
        rezept: "assets/bbq-menue-1/DessertRezept.odt"
      }
    }
  }
];
```

Beispiel fuer eine reduzierte Speisekarte mit nur Hauptspeise:

```js
const speisekarten = [
  {
    id: "bbq-hauptgericht-1",
    titel: "BBQ Hauptgericht",
    bild: "assets/bbq-hauptgericht-1/Speisekarte.png",
    kategorien: {
      hauptspeise: {
        titel: "Hauptspeise",
        bild: "assets/bbq-hauptgericht-1/Hauptspeise.png",
        einkaufsliste: "assets/bbq-hauptgericht-1/HauptspeiseEinkaufsliste.odt",
        rezept: "assets/bbq-hauptgericht-1/HauptspeiseRezept.odt"
      }
    }
  }
];
```

## Erweiterungsregeln

Wenn neue Speisekarten ergaenzt werden:

1. Neue Speisekarten muessen im Hauptmenue erscheinen.
2. Die Datei `Speisekarte.png` ist das Hauptbild der Speisekarte.
3. Vorhandene Kategorien sollen anhand ihrer Dateien eingebunden werden.
4. Nicht vorhandene Kategorien sollen nicht angezeigt werden.
5. Jede vorhandene Kategorie soll ein Titelbild bekommen.
6. Jede vorhandene Kategorie soll eine Einkaufsliste und ein Rezept besitzen, sofern die Dateien geliefert wurden.
7. Fehlende Inhalte sollen sichtbar abgefangen werden, zum Beispiel mit `Noch kein Rezept vorhanden`.
8. Die Navigation zurueck zur Speisekarte oder zum Hauptmenue darf nicht verloren gehen.
9. Die Website soll auf Desktop und Mobilgeraeten bedienbar bleiben.

## Designrichtung

Die Website soll wie eine digitale Menuekarte wirken:

- BBQ-Atmosphaere
- klare Kartenstruktur
- grosse appetitliche Bilder
- einfache Navigation
- gut lesbare Texte
- keine ueberladene Startseite
- der Nutzer soll direkt die Speisekarten benutzen koennen

## Prioritaet bei zukuenftigen Aenderungen

Bei Erweiterungen gilt folgende Reihenfolge:

1. Funktionierende Navigation
2. Verstaendliche Speisekarten-Struktur
3. Korrekte Behandlung fehlender Kategorien
4. Saubere mobile Darstellung
5. Gute Bilder und visuelle Wirkung
6. Animationen oder zusaetzliche Effekte erst danach

## Wichtigste Codex-Anweisung

Vor jeder Erweiterung oder groesseren Aenderung an dieser Website:

```text
Lies zuerst die Datei Instruction.md.
Halte dich an die dort beschriebene Speisekarten-Logik.
Beachte die feste Dateinamen-Konvention.
Zeige nur Kategorien an, die fuer die jeweilige Speisekarte wirklich vorhanden sind.
Erweitere die Website nur so, dass Hauptmenue, Speisekarte, Kategorien, Einkaufsliste und Rezept weiterhin klar zusammenhaengen.
```
