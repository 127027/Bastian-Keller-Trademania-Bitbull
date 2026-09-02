# Vorlage – BTK Backtest-/Replay-Run-Manifest

## Identität

- Run-ID:
- Run-Typ: `INDICATOR_BACKTEST / SOURCE_REPLAY / FUSION_REPLAY / PAPER_MIRROR / REFERENCE_COMPARISON`
- Erzeugt UTC:
- Status: `VALID / INVALID / FAILED / STALE / NOT_REPRODUCIBLE`
- Verantwortlich:

## Versionen und Hashes

- Code/Build:
- Strategieversion: `BTK-INDICATOR-SPEC-x.y`
- normative Strategiequelle: `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md`
- normative Spec Git-Commit:
- Originalindikator-/Source-Identity:
- Indicator-/Artefakt-SHA-256:
- Settings-SHA-256:
- Referenz-Evidence-Set-ID:
- Source-Allowlist-Version:
- Source-Rules-Version:
- Capture-/Parser-/Validation-Version:
- Session-/Freshness-/Revision-Policy-Version:
- Fusionsmodell-Version:
- Konfigurations-SHA-256:
- Daten-Snapshot-SHA-256:
- Dependency-Lock-SHA-256:
- DMS-Version:

## Marktdaten

- Börse/Provider:
- Symbole:
- Strategie-Timeframe:
- Warm-up Start UTC:
- Bericht Start UTC:
- Bericht Ende UTC:
- Bars erwartet/vorhanden:
- Lücken/Ausnahmen:
- Datenqualitätsbericht:

## Bastian-/Source-Evidence

- Evidence-Zeitraum:
- Origins/Source-IDs:
- Session-IDs:
- Evidence-/Label-Version:
- Events gesamt:
- Live/Replay/Update-Verteilung:
- Published-/Received-/Spoken-Time verfügbar:
- Capture-Methode:
- Source-/Capture-/Parser-Latenz verfügbar:
- Pending-Condition-Fälle:
- Revision-/Supersede-Fälle:
- bekannte Evidence-Lücken:
- geschützte Rohartefakte: `NOT_IN_PUBLIC_GIT` / Referenz:

## Handelsannahmen

- Startkapital je isoliertem Symbol: 250 USDT
- Run-Modus: `all_ten_isolated / single_symbol / paper_live_mirror / source_replay / fusion_replay`
- Einzeltest-Symbol:
- Spiegelportfolio: 240 USDT / 3 Slots / 80 USDT
- Positionsgröße:
- Pyramiding:
- Compounding: false
- Signalzeitsemantik:
- Source-Zeitsemantik:
- Freshness-/Expiry-Regel:
- Conditional-Watcher-Regel:
- Revision-/Conflict-Regel:
- Fillmodell:
- Ordertyp:
- Baselinekosten: 10 bp Fee + 2 bp Spread + 3 bp Slippage je Seite
- Stresskosten: 10 + 10 + 20 bp je Seite
- Tick-/Step-/Mindestnotional-Stand:
- offene Position am Testende:

## Validierung

- Strategie-Spec-Freeze:
- Indicator-Referenzparität:
- Bastian-Source-Parität:
- Capture-/Parser-Negativtests:
- chronologische Replay-Parität:
- Pending-Condition-/Revision-Parität:
- Reproduktionslauf:
- Holdout-/Optimierungsstatus:
- bekannte Einschränkungen:

## Fairer Referenzvergleich – falls zutreffend

- Referenzbot/Version:
- gleicher Daten-Snapshot:
- gleiche Märkte:
- gleiche Kostenannahmen:
- gleiche Kapitalbasis:
- gleicher Forward-Paper-Zeitraum:
- Parameter vor Vergleich eingefroren:
- begründete Abweichungen:

## Artefakte

- Indicator-Evidence-/Parity-Report:
- Source-Replay-/Parity-Report:
- Datenqualitätsbericht:
- Einzelmetriken:
- Portfoliometriken:
- Vergleichsreport:
- Trades:
- Equity/Drawdown:
- Latenzreport:
- Pending-Condition-/Revision-Report:
- Benchmark:
- Laufprotokoll:
