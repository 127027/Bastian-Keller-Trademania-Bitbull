# 15 – Traceability-Matrix

Diese Matrix verhindert, dass Anforderungen nur im Text existieren. Sie ist auf die aktuell in DMS 02 definierten IDs ausgerichtet.

## Strategie und Quellen

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-STR-001 nur eingefrorene BTK-Strategie | DMS 03 | Strategy/Fusion Engine | Freigabegate + Negativtest |
| BTK-STR-002 nichts erfinden | DMS 00/03 | DMS/Engineering | Quellenreview |
| BTK-STR-003 Identität/Inputs/Timeframe/Signale | DMS 03 | Config/Indicator/UI | Quelleninventar + Golden-Fälle |
| BTK-STR-004 Bar-Close/Repainting | DMS 03 | Indicator/Data | Open-Bar/Reload-Test |
| BTK-STR-005 Entscheidungs-Audit | DMS 02/09 | Decision Store/UI | Persistenz-/Drill-down-Test |
| BTK-STR-006 Indicator-Parität | DMS 03/12 | Testartefakt | Golden-/Black-Box-Abweichungsreport |
| BTK-SRC-001 Bastian primäre Person | DMS 00/03 | Source Validator | Sprecher-/Mentor-Negativtest |
| BTK-SRC-002 Struktur + Freshness vor Handel | DMS 03 | Event Validator | Actionable-/Freshness-Test |
| BTK-SRC-003 Replay/alt/Frage nicht live | DMS 03 | Session/Event Validator | Replay-/Frage-Negativtest |
| BTK-SRC-004 geschützte Rohinhalte nicht Public Git | DMS 11/21/23 | Storage/Git | Secret-/Content-Scan |
| BTK-SRC-005 Source-Event-Zeiten/Hash/Status | DMS 03/09 | Source Store | Schema-/Roundtrip-Test |
| BTK-SRC-006 Allowlist + dynamische Sessionerkennung | DMS 03/13/22 | Source Discovery | Fake-Source-/Terminänderungstest |
| BTK-SRC-007 zulässiger Capture-Pfad je Quelle | DMS 03/11/13 | Capture Adapter | Provider-/Rechtecheck |
| BTK-SRC-008 Rohtext/Confidence nicht allein handelbar | DMS 03 | Parser/Validator | direkte-Order-Negativtests |
| BTK-SRC-009 Unsicherheit/Widerspruch -> keine neue Order | DMS 03/19 | Validator | Low-confidence-/Conflict-Test |
| BTK-SRC-010 konditionale Aussage wartet | DMS 03/09 | Conditional Watcher | Pending/Met/Expired-Tests |
| BTK-SRC-011 Revision ersetzt Kontext ohne Historienrewrite | DMS 03/09 | Context Store | Revision-/Supersede-Test |
| BTK-SRC-012 Source-/Parser-/E2E-Latenz messen | DMS 09/10 | Observability | Latenztelemetrie-Test |
| BTK-SRC-013 Latenz/Freshness/Priorität vor Paper/Live fixieren | DMS 03/13 | Config/Gate | Config-Negativtest |
| BTK-SRC-014 Session-Lifecycle | DMS 03/09 | Session Store/UI | State-machine-Test |
| BTK-SRC-015 kein Dritt-/Rate-Ersatz bei Source-Ausfall | DMS 10/20 | Source Health | Outage-Negativtest |

## Markt, Kapital und Risiko

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-MKT-001 zehn USDT-Paare | DMS 04 | Config/Data/UI | Schema-/Metadatenprüfung |
| BTK-CAP-001 240 USDT Paper/Live | DMS 04 | Ledger/UI | Startsaldo-Test |
| BTK-CAP-002 max. 3×80 Slots | DMS 04 | Portfolio/Execution | Slotlimit-Test |
| BTK-CAP-003 kein fixes Gewinnziel | DMS 04/06 | Report | Ergebnisreview |
| BTK-CAP-004 kein Auto-Compounding | DMS 04/13 | Ledger | Sizing-/Saldo-Test |
| BTK-RSK-001 kein Leverage/Margin/Futures | DMS 04/11 | Config/Execution | Negativtest |
| BTK-RSK-002 Binance-Filter | DMS 04/07 | Execution | Tick/Step/MinNotional |
| BTK-RSK-003 5% Tagesverlustpause | DMS 04/20 | Risk/UI | UTC-Day-Test |
| BTK-RSK-004 20% HWM-Drawdown-Halt | DMS 04/20 | Risk/UI | HWM-Test |
| BTK-RSK-005 25-bp Preisabweichungsblock | DMS 07 | Execution | Deviation-Test |

## Daten

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-DAT-001 OHLCV persistent/decimal | DMS 05 | DB/Data API | Schema/Roundtrip |
| BTK-DAT-002 Startup-Prüfung | DMS 05 | Startup/UI | Lücken-/Duplikat-Fixtures |
| BTK-DAT-003 inkrementelles Nachladen | DMS 05 | Data Adapter | Paging/Retry |
| BTK-DAT-004 00:05-UTC-Audit | DMS 05/10 | Scheduler | Scheduler-Test |
| BTK-DAT-005 Stream + REST-Fallback | DMS 05 | Data Adapter | Disconnect/Recovery |
| BTK-DAT-006 offene Bars nur nach DMS 03 | DMS 03/05 | Data/Strategy/UI | Open-Bar-Test |

## Backtest, Replay und Vergleich

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-BKT-001 drei Jahre + Warm-up soweit reproduzierbar | DMS 06 | Backtest | Fenstergrenzen |
| BTK-BKT-002 10×250 isoliert | DMS 04/06 | Backtest | zehn Ledger |
| BTK-BKT-003 Einzelmodus 250 | DMS 06 | Backtest/UI | ETH-only-Test |
| BTK-BKT-004 optional 240/3×80 | DMS 04/06 | Portfolio Backtest | Paper-Parität |
| BTK-BKT-005 Baseline-/Stresskosten | DMS 06 | Backtest | Kostenfixtures |
| BTK-BKT-006 kein Look-ahead/Bias/Synthpreis | DMS 05/06 | Data/Backtest | Negativtests |
| BTK-BKT-007 Manifest/Quality/Trades | DMS 06/13/18 | Artifact Store | Reproduktionslauf |
| BTK-BKT-008 Indicator/Bastian/Fusion getrennt | DMS 06 | Report | Modusvergleich |
| BTK-BKT-009 chronologischer Source-Replay | DMS 03/06 | Replay Engine | Zeit-/Revisionstest |
| BTK-BKT-010 fairer Botvergleich gleiche Basis | DMS 06/12/14 | Comparison Report | Baseline-Hash-Prüfung |
| BTK-BKT-011 Vergleichsmetriken vollständig | DMS 06/12/18 | Report/UI | Metriktests |

## Execution und Betrieb

| Anforderung | Fachquelle | Zielkomponente/UI | Haupttest/Nachweis |
|---|---|---|---|
| BTK-EXE-001 getrennte Zustände | DMS 07/09 | Domain/DB/UI | State-machine-Test |
| BTK-EXE-002 Idempotency | DMS 07 | Execution | Doppel-Submit-Test |
| BTK-EXE-003 Reconciliation | DMS 07/10 | Execution | Restart-Test |
| BTK-EXE-004 Teilfill/Reject/Timeout/Netz | DMS 07 | Execution/Ledger | Adapter-Szenarien |
| BTK-EXE-005 Market-Baseline | DMS 07/13 | Execution | Ordertype-Test nach Freeze |
| BTK-EXE-006 10s UNKNOWN | DMS 07/20 | Execution | Timeout-Test |
| BTK-EXE-007 Source -> Fusion/Risk -> Intent | DMS 03/07/09 | Strategy/Execution | E2E-Source-Order-Test |
| BTK-OPS-001 24/7 Paper vor Live | DMS 10/12 | Operations | Soak-Nachweis |
| BTK-OPS-002 30 Tage + timeframe-abgeleitete Barabdeckung + 20 Trades/max. 90 Tage | DMS 02/10/13 | Operations | Soak-Report + Timeframe-Ableitung |
| BTK-OPS-003 Telegram P1/P2 | DMS 10 | Alerts | Testalarm |
| BTK-OPS-004 Backup/Restore/Not-Aus/Data+Source Health | DMS 10/20 | Operations | Restore-/Failure-Test |
| BTK-OPS-005 Live nicht nur wegen Backtest | DMS 12 | Release Gate | Freigabe-Negativtest |
| BTK-OPS-006 Komponenten getrennt überwachen | DMS 09/10 | Health/UI | Component-Failure-Matrix |

## Pflege

Neue kritische Anforderungen erhalten positive und negative Tests. `OFFEN` darf nicht durch grüne Implementierungstests kaschiert werden. Vor dem signalaktiven Codeumbau müssen alle Strategie-/Source-Punkte geschlossen sein, die Handelsentscheidung, Freshness, Capture, Revision, Latenz oder Fusionslogik beeinflussen.
