# Vorlage – BTK Backtest-Run-Manifest

## Identität

- Run-ID:
- Erzeugt UTC:
- Status: `VALID / INVALID / FAILED / STALE`
- Verantwortlich:

## Versionen und Hashes

- Code/Build:
- Strategieversion: `BTK-INDICATOR-SPEC-x.y`
- normative Strategiequelle: `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md`
- normative Spec Git-Commit:
- Originalindikator-/Source-Identity:
- Source-/Artefakt-SHA-256:
- Settings-SHA-256:
- Referenz-Evidence-Set-ID:
- Konfigurations-SHA-256:
- Daten-Snapshot-SHA-256:
- Dependency-Lock-SHA-256:
- DMS-Version:

## Daten

- Börse/Provider:
- Symbole:
- Strategie-Timeframe:
- Warm-up Start UTC:
- Bericht Start UTC:
- Bericht Ende UTC:
- Bars erwartet/vorhanden:
- Lücken/Ausnahmen:
- Datenqualitätsbericht:

## Handelsannahmen

- Startkapital je isoliertem Symbol: 250 USDT
- Run-Modus: `all_ten_isolated / single_symbol / paper_live_mirror`
- Einzeltest-Symbol:
- Spiegelportfolio: 240 USDT / 3 Slots / 80 USDT
- Positionsgröße:
- Pyramiding:
- Compounding: false
- Signalzeitsemantik:
- Fillmodell:
- Ordertyp:
- Baselinekosten: 10 bp Fee + 2 bp Spread + 3 bp Slippage je Seite
- Stresskosten: 10 + 10 + 20 bp je Seite
- Tick-/Step-/Mindestnotional-Stand:
- offene Position am Testende:

## Validierung

- Strategie-Spec-Freeze:
- Referenzparität:
- Black-Box-/Source-Paritätstyp:
- Replay = Batch:
- Reproduktionslauf:
- Holdout-/Optimierungsstatus:
- bekannte Einschränkungen:

## Artefakte

- Evidence-/Parity-Report:
- Einzelmetriken:
- Portfoliometriken:
- Trades:
- Equity/Drawdown:
- Benchmark:
- Laufprotokoll:
