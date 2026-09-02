# 14 – Build-Plan und Definition of Done

Der Bot wird nicht experimentell neu erfunden. Erst wird die BTK-Strategie fachlich geschlossen, danach werden bewährte technische Komponenten gezielt übernommen.

## Phase 0 – Eigenständiges Repository und DMS

- Repository `127027/Bastian-Keller-Trademania-Bitbull` initialisieren;
- vollständigen DMS-Satz auf Bastian Keller / TradeMania / Bitbull ausrichten;
- technische Baseline festhalten;
- keine fremde Strategiespezifikation übernehmen;
- Strategieaufnahme DMS 03 vorbereiten.

DoD: DMS kann echten Indikator und Bastian-Evidence ohne Strukturumbau aufnehmen.

## Phase 1 – Originalindikator aufnehmen

- Zugang rechtmäßig erhalten;
- Name/Version/Settings/Alerts erfassen;
- Screenshots/Referenzfälle sammeln;
- Timeframe, Daten, Repainting, Entry/Exit, Slotlogik klären;
- Veröffentlichungsrechte bestimmen.

DoD: keine kritische Indikatorfrage offen.

## Phase 2 – Bastian-Evidence aufnehmen

- mehrere echte Lives/Updates beobachten;
- Source-Typen, Sprecher, Assets, Bedingungen, Freshness und Konflikte labeln;
- Entry/Exit/Manage-Sprache reproduzierbar klassifizieren;
- Replay-vs-Live und Revisionen testen.

DoD: Bastian-Regeln sind deterministisch beschreibbar.

## Phase 3 – `BTK-INDICATOR-SPEC-1.0` einfrieren

- DMS 03 finalisieren;
- genau ein Fusionsmodell freigeben;
- Config/Traceability/Tests synchronisieren;
- Golden-/Source-Evidence-Version festhalten.

DoD: unabhängiger Entwickler kann die Strategie ohne Interpretation implementieren.

## Phase 4 – Bot-Unterbau übernehmen und gezielt anpassen

Vor jeder Änderung prüfen, welche generische Funktion bereits passt.

- Daten-/Ledger-/Risk-/Execution-/Backtest-/UI-Grundkomponenten übernehmen;
- nur Strategieschicht und erforderliche Source-Adapter ergänzen;
- keine parallele zweite Engine;
- neue Felder nur soweit DMS verlangt.

## Phase 5 – Parität und Replay

- Indicator-Golden/Black-Box;
- Bastian-Source-Replay;
- chronologische Fusionsentscheidungen;
- keine ungeklärte Signalabweichung.

## Phase 6 – Backtests

- Daten aktualisieren;
- drei Jahre;
- 10×250;
- Einzeltest, insbesondere ETHUSDT;
- optional 240/3×80;
- Kosten-/Stressszenarien;
- Reports/Manifest.

## Phase 7 – UI und Paper 24/7

- Indikator-/Bastian-Zustände sichtbar;
- echte Marktdaten;
- gleiche Strategy/Risk/Intentlogik wie Live;
- Failure Injection/Reconciliation;
- Soak gemäß DMS 10/12.

## Phase 8 – kontrollierte Live-Freigabe

Live erst nach separatem Gate. Ein positiver Backtest reicht nicht.

## Gesamt-DoD

- DMS 03 eingefroren;
- Indicator- und Bastian-Parität belegt;
- keine unnötige Strukturänderung;
- Daten vollständig;
- Backtests reproduzierbar;
- UI/Health korrekt;
- Paper-Soak bestanden;
- Security/Audit/Reconciliation/Backup/Restore bestanden;
- Live separat freigegeben.

Ziel ist nicht, dass der Bot nur „wie Bastian klingt“, sondern dass dieselbe beobachtbare Information unter denselben Bedingungen reproduzierbar zur dokumentierten Entscheidung führt.