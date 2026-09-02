# 15 – Traceability-Matrix

Diese Matrix verhindert, dass Anforderungen nur im Text existieren.

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-STR-001 nur eingefrorene BTK-Strategie | DMS 03 | Indicator/Strategy Engine | Referenzparität |
| BTK-STR-002 nichts erfinden | DMS 00/03 | DMS/Engineering | Review gegen Quellenpaket |
| BTK-STR-003 Identität/Inputs/Timeframe/Signale | DMS 03 | Config/Engine/UI | Quelleninventar + Golden-Fälle |
| BTK-STR-004 Bar-Close/Repainting | DMS 03 | Strategy/Data | Open-Bar/Reload-Test |
| BTK-STR-005 Signal-Audit | DMS 02/09 | Signal Store/UI | Persistenz-/Drill-down-Test |
| BTK-STR-006 Referenzvektoren | DMS 03/12 | CI/Testartefakt | Abweichungsreport |
| BTK-STR-007 eigenständiges BTK-Repository | DMS 00/21 | Git/Strategy | Repository-/Versionstest |
| BTK-MKT-001 zehn Paare | DMS 04 | Config/Data/UI | Schema-/Metadatenprüfung |
| BTK-CAP-001 240 USDT Paper/Live | DMS 04 | Ledger/UI | Startsaldo-Test |
| BTK-CAP-002 3×80 Slots | DMS 04 | Portfolio/Execution | Slotlimit-Test |
| BTK-CAP-004 kein fixes Gewinnziel | DMS 04/06 | Report | Ergebnisreview |
| BTK-CAP-005 neue Slotpriorität | DMS 03/04 | Strategy/Portfolio | simultane Signale |
| BTK-RSK-001 kein Leverage/Margin/Futures | DMS 04/11 | Config/Execution | Negativtest |
| BTK-RSK-002 Binance-Filter | DMS 04/07 | Execution | Tick/Step/MinNotional |
| BTK-RSK-003 Verlust-/Drawdown-Grenzen | DMS 04/20 | Risk/UI | UTC-/HWM-Test |
| BTK-DAT-001 OHLCV persistent | DMS 05 | DB/Data API | Schema/Roundtrip |
| BTK-DAT-002 Startup-Prüfung | DMS 05 | Startup/UI | Lücken-/Duplikat-Fixtures |
| BTK-DAT-003 inkrementelles Nachladen | DMS 05 | Data Adapter | Paging/Retry |
| BTK-DAT-004 00:05-Audit | DMS 05/10 | Scheduler | Scheduler-/DST-Test |
| BTK-DAT-005 Stream + REST-Fallback | DMS 05 | Data Adapter | Disconnect/Recovery |
| BTK-DAT-006 provisional-Verhalten | DMS 03/05 | Data/Strategy/UI | Open-Bar-Test |
| BTK-BKT-001 drei Jahre | DMS 06 | Backtest | Fenstergrenzen |
| BTK-BKT-002 Fillsemantik | DMS 03/06 | Backtest | Look-ahead-Negativtest |
| BTK-BKT-003 Kosten/Rundung | DMS 06 | Backtest/Execution | handgerechnete Fixtures |
| BTK-BKT-004 kein Bias/synthetische Preise | DMS 05/06 | Data/Backtest | Review/Quality |
| BTK-BKT-005 Metriken | DMS 06/18 | Report/UI | Formeltests |
| BTK-BKT-006 Run-Manifest | DMS 13 | Artifact Store | Reproduktionslauf |
| BTK-BKT-007 Parität getrennt von PnL | DMS 06 | Test/Report | Referenztest ohne Kapital |
| BTK-BKT-008 10×250 | DMS 04/06 | Backtest | zehn isolierte Ledger |
| BTK-BKT-009 Einzeltest 250 | DMS 06 | Backtest UI | ETH-only-Test |
| BTK-BKT-010 240/3×80 Spiegel | DMS 04/06 | Portfolio-Backtest | Paper-Parität |
| BTK-BKT-011 Baseline-/Stresskosten | DMS 06 | Backtest | Kostenfixtures |
| BTK-EXE-001 getrennte Zustände | DMS 07/09 | Domain/DB/UI | State-machine-Test |
| BTK-EXE-002 Idempotency | DMS 07 | Execution | Doppel-Submit-Test |
| BTK-EXE-003 Reconciliation | DMS 07/10 | Execution | Restart-Test |
| BTK-EXE-004 Teilfill/Fehler | DMS 07 | Execution/Ledger | Adapter-Szenarien |
| BTK-EXE-005 Not-Aus | DMS 07/20 | UI/Risk | E2E |
| BTK-EXE-006 Market-/Timeoutschutz | DMS 07 | Execution | 25-bps/10-s/30-s-Test |
| BTK-EXE-007 Signal→Aktion | DMS 03 | Strategy/Execution | Referenzszenarien |
| BTK-UI-001 Strategie-/Marktkarten | DMS 08 | Dashboard | UI-Abnahme |
| BTK-UI-002 fünf Chartzeiträume | DMS 08 | Chart | Grenztest |
| BTK-UI-003 neue Overlays | DMS 03/08 | Chart | Referenz-Screenshot/Datenvergleich |
| BTK-UI-004 provisional sichtbar | DMS 08 | Chart | UI-Test |
| BTK-UI-008 UI-Auflösung ≠ Signalberechnung | DMS 05/08 | Chart/API | Aggregationstest |
| BTK-OPS-001 Health | DMS 10 | Health/UI | Komponentenausfälle |
| BTK-OPS-004 Paper-Soak | DMS 10/12 | Operations | Soak-Nachweis |
| BTK-OPS-006 Telegram | DMS 10 | Alerts | Testalarm |
| BTK-SEC-001 keine Secrets | DMS 11 | alle | Secret-Scan |
| BTK-SEC-003 Live-Gates | DMS 12 | Config/UI | negativer Freischalttest |
| BTK-QLT-001 Traceability | DMS 12/15 | DMS/Test | Review |

## Pflege

Neue kritische Anforderungen erhalten positive und negative Tests. `OFFEN` darf nicht durch grüne Implementierungstests kaschiert werden. Vor dem Codeumbau müssen alle `BTK-STR-*`-Punkte, die die Handelsentscheidung beeinflussen, geschlossen sein.
