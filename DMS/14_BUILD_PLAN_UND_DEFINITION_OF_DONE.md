# 14 – Build-Plan und Definition of Done

Der Bot wird nicht experimentell neu erfunden. Erst wird die BTK-Strategie fachlich geschlossen, danach werden bewährte technische Komponenten gezielt übernommen und nur um die nach DMS erforderliche Bastian-Source-Schicht ergänzt.

## Phase 0 – Eigenständiges Repository und DMS

- Repository `127027/Bastian-Keller-Trademania-Bitbull` initialisieren;
- vollständigen DMS-Satz auf Bastian Keller / TradeMania / Bitbull ausrichten;
- strategieneutrale technische Baseline spiegeln;
- keine fremde Strategiespezifikation übernehmen;
- Strategieaufnahme DMS 03 vorbereiten;
- öffentliche TradeMania-/Bastian-Quellen dokumentieren.

DoD: DMS kann echten Indikator und Bastian-Evidence ohne Strukturumbau aufnehmen.

## Phase 1 – Originalindikator aufnehmen

- Zugang rechtmäßig erhalten;
- Name/Version/Settings/Alerts erfassen;
- Screenshots/Referenzfälle sammeln;
- Timeframe, Daten, Repainting, Entry/Exit, Slotlogik klären;
- Veröffentlichungsrechte bestimmen.

DoD: keine kritische Indikatorfrage offen.

## Phase 2 – Bastian-Evidence und Quelleninventar aufnehmen

- mehrere echte Lives/Updates beobachten;
- offizielle Source-/Channel-IDs allowlisten;
- Source-Typen, Sessionstatus, Sprecher, Assets, Bedingungen, Freshness und Konflikte labeln;
- Entry/Exit/Manage-Sprache reproduzierbar klassifizieren;
- Replay-vs-Live und Revisionen testen;
- zulässigen Capture-Pfad je Quelle bestimmen;
- reale Source-/Capture-/Parser-Latenzen messen.

DoD: Quellenidentität und technisch/rechtlich zulässige Erfassung sind dokumentiert; Bastian-Regeln sind deterministisch beschreibbar.

## Phase 3 – Live-Reaktionsmodell schließen

- Session-Lifecycle festlegen;
- Actionable-Pflichtfelder festlegen;
- `NO_TRADE` bei Unsicherheit verbindlich machen;
- Freshness, Expiry, Konflikte und Revisionen schließen;
- Conditional-Watcher-Regeln für „wenn X, dann Y“ schließen;
- maximal zulässige Latenz je Source-/Tradingart festlegen;
- genau ein Fusionsmodell Indikator ↔ Bastian auswählen.

DoD: dieselbe gelabelte Aussage führt bei denselben Marktbedingungen reproduzierbar zur selben Strategieentscheidung.

## Phase 4 – `BTK-INDICATOR-SPEC-1.0` einfrieren

- DMS 03 finalisieren;
- Config/Traceability/Tests synchronisieren;
- Golden-/Source-Evidence-Version festhalten;
- alle kritischen `OFFEN`-Punkte schließen.

DoD: unabhängiger Entwickler kann die Strategie ohne Interpretation implementieren.

## Phase 5 – Bot-Unterbau übernehmen und gezielt anpassen

Vor jeder Änderung prüfen, welche generische Funktion bereits passt.

- Daten-/Ledger-/Risk-/Execution-/Backtest-/UI-Grundkomponenten übernehmen;
- Indicator Engine gemäß eingefrorener Spezifikation implementieren/anpassen;
- Source Discovery / Session Watcher ergänzen;
- erforderliche Capture-/Transcript-/Parser-Adapter ergänzen;
- Bastian Event Validator und Context Store ergänzen;
- Conditional Watcher ergänzen, falls V1 ihn benötigt;
- Fusionslogik in denselben Strategy Core integrieren;
- keine parallele zweite Execution-Engine;
- neue Felder nur soweit DMS verlangt.

## Phase 6 – Parität und Source-Replay

- Indicator-Golden/Black-Box;
- Source-Session-Replay;
- Capture-/Parser-Fixtures;
- Zuschauer-/anderer-Mentor-Negativtests;
- Pending-Condition-/Expiry-/Revisionstests;
- chronologische Fusionsentscheidungen;
- keine ungeklärte Signalabweichung.

## Phase 7 – Backtests

- Daten aktualisieren;
- drei Jahre, soweit die eingefrorene Indikatorstrategie dies reproduzierbar zulässt;
- 10×250;
- Einzeltest, insbesondere ETHUSDT;
- optional 240/3×80;
- Kosten-/Stressszenarien;
- Indicator-only / Bastian-only soweit sinnvoll / Fusion getrennt;
- Reports/Manifest.

Historische Bastian-Aussagen werden nur dort backgetestet, wo zeitlich belastbare Source-Evidence existiert. Fehlende Historie wird nicht erfunden.

## Phase 8 – UI und Paper 24/7

- Indicator-, Session-, Capture-, Parser-, Bastian-Kontext- und Pending-Condition-Zustände sichtbar;
- echte Marktdaten;
- echte erlaubte Source-Überwachung;
- gleiche Strategy/Risk/Intentlogik wie Live;
- Latenzmessung;
- Failure Injection/Reconciliation;
- Soak gemäß DMS 10/12.

## Phase 9 – fairer Referenzvergleich

Beide Bots werden unter identischer bzw. fachlich vergleichbarer Basis gegenübergestellt:

- gleicher Daten-Snapshot/Zeitraum;
- gleiche Märkte;
- gleiche Gebühren-/Slippageannahmen;
- gleiche Kapitalbasis;
- gleicher Forward-Paper-Zeitraum;
- keine nachträgliche Parameteroptimierung anhand des Zwischenstands.

Bewertung mindestens nach Netto-PnL/Tag, Drawdown, Profit Factor soweit stabil, Kosten, Kapitalnutzung, Ausfällen und Latenz.

## Phase 10 – kontrollierte Live-Freigabe

Live erst nach separatem Gate. Ein positiver Backtest oder einzelne erfolgreiche Bastian-Signale reichen nicht.

## Gesamt-DoD

- DMS 03 eingefroren;
- Indicator-Parität belegt;
- Bastian-Source-/Session-/Capture-/Parser-Parität belegt;
- Freshness/Revision/Conditional-Watcher reproduzierbar;
- keine unnötige Strukturänderung;
- Daten vollständig;
- Backtests/Replays reproduzierbar;
- UI/Health korrekt;
- Paper-Soak bestanden;
- Security/Audit/Reconciliation/Backup/Restore bestanden;
- fairer Vergleich dokumentiert;
- Live separat freigegeben.

Ziel ist nicht, dass der Bot nur „wie Bastian klingt“, sondern dass dieselbe beobachtbare Information unter denselben Bedingungen reproduzierbar zur dokumentierten Entscheidung führt.
