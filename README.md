# Netzplan-Tool

Eine eigenständige Webapp zum Erstellen und Berechnen von **Netzplänen (Vorgangsknotennetz, AON)**
nach **DIN 69900**. Kein Server, kein Build-Schritt — einfach `index.html` im Browser öffnen.

## Funktionen

- Vorgänge anlegen/bearbeiten/löschen (Code, Bezeichnung, Dauer, Vorgänger mit Mindestabstand)
- Automatische **Vorwärts-/Rückwärtsrechnung**: FAZ, FEZ, SAZ, SEZ, Gesamtpuffer, freier Puffer
- **Kritischer Pfad** wird automatisch ermittelt und rot hervorgehoben (Tabelle + Diagramm)
- Grafischer Netzplan als SVG mit dem klassischen 7-Felder-Knoten (DIN 69900), per Drag & Drop verschiebbar
- Auto-Layout (Ebenen nach Vorgängertiefe), Zyklenerkennung/-validierung
- Beispielprojekt, JSON-Export/Import, SVG-Export, Drucken/PDF
- Eingebautes Regel- und Hilfefenster ("Regeln & Hilfe")

## Nutzung

1. `index.html` doppelklicken / im Browser öffnen (Chrome, Edge, Firefox).
2. "Beispiel laden" klicken, um die Funktionsweise zu sehen, oder eigene Vorgänge anlegen.
3. Knoten im Diagramm können frei per Drag & Drop verschoben werden; "Auto-Layout" ordnet neu an.

## Dateien

- `index.html` – Struktur/UI
- `style.css` – Styling
- `netzplan-core.js` – reine Berechnungslogik (Vorwärts-/Rückwärtsrechnung, Zyklenerkennung, kritischer Pfad); ohne DOM-Abhängigkeiten, auch unter Node.js testbar
- `app.js` – UI-Logik (Formular, Tabelle, SVG-Rendering, Drag & Drop, Import/Export)

## Berechnungsregeln (Kurzfassung)

- FAZ = max(FEZ aller Vorgänger + Abstand); FEZ = FAZ + Dauer
- SEZ = min(SAZ aller Nachfolger − Abstand); SAZ = SEZ − Dauer
- Gesamtpuffer = SAZ − FAZ; Freier Puffer = min(FAZ Nachfolger − Abstand) − FEZ
- Kritischer Pfad = durchgehende Kette von Vorgängen mit Gesamtpuffer = 0

Details siehe "Regeln & Hilfe" in der Anwendung.

## Tests

Die Kernlogik lässt sich isoliert mit Node.js prüfen:

```bash
node -e "
const core = require('./netzplan-core.js');
console.log(core.calculate([
  {id:1,code:'A',name:'A',duration:2,preds:[]},
  {id:2,code:'B',name:'B',duration:3,preds:[{id:1,lag:0}]}
]));
"
```
