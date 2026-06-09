# Pilot01 — Kryptografischer Vorab-Nachweis (Pre-Registration of Data Integrity)

Dieses Repository dient **ausschließlich** als manipulationssicherer, datierter
Nachweis der Datenintegrität für die Pilotstudie *Pilot01* (Projekt „Erkennen").

## Hintergrund

In der Studie wurden 7 KI-Modelle systematisch befragt. Für eine **Blind-Kodierung**
wurden die Ergebnisse aufgeteilt in:

- eine Datei mit den **Antworten** (`coding_sheet.csv`) — Grundlage der Kodierung,
- eine **Schlüsseldatei** (`coding_key.csv`) — enthält die Zuordnung der Modellnamen.

Die kodierende Person besitzt beide Dateien lokal. Um die Glaubwürdigkeit der
Blindheit zu sichern, wird hier **vor Beginn der Kodierung** der kryptografische
Fingerabdruck (SHA-256) der Dateien öffentlich und datiert festgelegt.

## Was dieser Nachweis beweist

Der SHA-256-Hash ist eine Einbahnfunktion: Aus dem Hash lassen sich **die
Originaldaten nicht rekonstruieren** (die Blindheit bleibt gewahrt), aber jede
nachträgliche Änderung einer Datei — und sei es ein einziges Zeichen — würde
einen völlig anderen Hash erzeugen.

Durch das öffentliche, von GitHub datierte Commit (und den zugehörigen Release)
ist belegbar:

1. **Die Schlüsseldatei (`coding_key.csv`) wurde nach diesem Zeitpunkt nicht mehr
   verändert** — sie blieb bis zum Abschluss der Kodierung unangetastet.
2. **Es wurden genau diese Antwortdaten (`coding_sheet.csv`) kodiert** — keine
   nachträglich ausgetauschten Daten.
3. **Auch Rohdaten und Sekundärmaße sind festgelegt.**

## Verifikation

Die maßgeblichen Hashes stehen in [`MANIFEST.sha256.json`](MANIFEST.sha256.json).
Nach Abschluss der Studie (Veröffentlichung der Originaldateien) kann jede:r prüfen:

```bash
sha256sum coding_key.csv coding_sheet.csv raw_runs.jsonl secondary_entropy.csv
```

und die Ergebnisse mit den hier hinterlegten Werten vergleichen.

| Datei | SHA-256 |
|-------|---------|
| `coding_key.csv` | `3735b10fa168c069896f6fc61ded5fb674a8f5f4fcc4921ab7adff9962392cc4` |
| `coding_sheet.csv` | `c88f4ea2229358a7cff3d6de130b321ea679f28d16ea8e98ab7b3b097e1765bf` |
| `raw_runs.jsonl` | `312ac828c90f40724f918a39eee99be93c69b9db24a27a1e9d84d0d0807b884c` |
| `secondary_entropy.csv` | `33ddb6b86e474a20a83e344f773da4331593509a2fc02e278499e4246d366fbf` |

> **Wichtig:** Dieses Repository enthält bewusst **keine** Originaldaten, keine
> Modellnamen und keine Zugangsdaten — nur Prüfsummen. Die Originaldateien werden
> erst nach Abschluss der Kodierung offengelegt.

## Abschluss-Nachweis: Festschreibung der fertigen Kodierung

Nach **Abschluss der Blind-Kodierung** wird der kryptografische Fingerabdruck der
**fertig kodierten** `coding_sheet.csv` ebenfalls datiert festgeschrieben (siehe
[`coding_sheet.completed.sha256`](coding_sheet.completed.sha256) und den
zugehörigen Git-Tag/Release `coding-completed-2026-06-09`).

Dieser zweite Hash unterscheidet sich vom oben präregistrierten Wert — das ist
beabsichtigt: Der Vorab-Hash belegt, **welche Antwortdaten** kodiert wurden; der
Abschluss-Hash legt das **Kodier-Ergebnis** fest und macht jede spätere Änderung
der kodierten Datei nachweisbar.

| Datei | Zeitpunkt | SHA-256 |
|-------|-----------|---------|
| `coding_sheet.csv` (vor Kodierung) | präregistriert | `c88f4ea2229358a7cff3d6de130b321ea679f28d16ea8e98ab7b3b097e1765bf` |
| `coding_sheet.csv` (fertig kodiert) | nach Abschluss | `871fca65ead199db7f2e0e1fd3ea6c51882f1415fc6e14c7db7464df065fdc17` |
