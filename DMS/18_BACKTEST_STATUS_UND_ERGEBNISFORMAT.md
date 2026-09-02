# 18 – Backteststatus und Ergebnisformat

## Wahrheitsgemäßer Ist-Stand

Stand **02.09.2026** wurde für den Bitbull-/TradeMania-/Bastian-Keller-Bot **kein valider Backtest oder Source-Replay ausgeführt**.

Grund: Der tatsächliche neue Indikator und die nach Registrierung nutzbaren Bastian-/Member-Quellen wurden dem Projekt noch nicht vollständig bereitgestellt. Deshalb fehlen:

- eingefrorene `BTK-INDICATOR-SPEC-1.0`;
- Strategieparameter/Signaldefinition;
- Source-Allowlist/Capture-Pfade;
- Referenz-/Golden-Artefakte;
- gelabelte Bastian-Live-/Update-Ereignisse;
- Freshness-/Revision-/Conditional-/Fusionsregeln;
- signalaktiver BTK-Botcode;
- gültige BTK-Backtest-/Replay-/Paperresultate.

Jede konkrete BTK-Rendite-, Trefferquote-, Trade-, Latenz- oder Drawdownzahl wäre derzeit erfunden.

## Verbindlicher späterer Testumfang

- Indicator-Referenz-/Signalparität;
- Bastian-Source-/Session-Replay;
- Capture-/Parser-/Validation-Fixtures;
- Pending-Condition-/Revision-/Expiry-Replay;
- 10×250-USDT-Batch;
- Einzelmodus 250 USDT;
- primär drei vollständige Jahre plus Warm-up, soweit Indicator-Historie reproduzierbar ist;
- rechnerische Aggregation der zehn isolierten Resultate;
- optional 240/3×80-Spiegel;
- volle Historie als Zusatz;
- Baseline-/Stresskosten;
- Buy-and-Hold/Cash-Benchmark;
- Indicator-only / Bastian-only soweit reproduzierbar / Fusion getrennt;
- Run-Manifest + Datenqualitäts-/Source-Evidence-Bericht;
- 24/7 Forward-Paper;
- fairer Vergleich mit dem separat betriebenen Referenzbot.

## Ergebnistabelle je Coin

| Feld | Wert |
|---|---|
| Symbol | festgelegte Liste |
| Zeitraum | UTC Start/Ende |
| Strategieversion | BTK-INDICATOR-SPEC-x.y |
| Signal-Timeframe | aus DMS 03 |
| Startkapital | 250 USDT |
| Endkapital | zu berechnen |
| Netto-PnL | zu berechnen |
| Netto-PnL/Tag | zu berechnen |
| Nettorendite | zu berechnen |
| Indicator-Parität | bestanden/nicht bestanden/nicht geprüft |
| Bastian-Source-Parität | bestanden/nicht bestanden/nicht geprüft |
| Max Drawdown | zu berechnen |
| Trades | zu berechnen |
| Gewinnquote | zu berechnen |
| Profit Factor | zu berechnen/soweit stabil |
| Gebühren | zu berechnen |
| Slippage | zu berechnen |
| Exposure | zu berechnen |
| blockierte/verpasste Signale | zu berechnen |
| Source-/E2E-Latenz | zu berechnen, wenn Source-Layer beteiligt |
| Buy-and-Hold/Cash | zu berechnen |
| Qualitätsstatus | valid/invalid/stale |

## Source-Replay-Ergebnis

Pro Replay mindestens:

- Evidence-/Label-Version;
- Session-ID/Origin;
- Source-/Channel-ID;
- Sessionstatus;
- Published-/Received-/Spoken-Time;
- Capture-/Parser-/Validation-Version;
- Anzahl Events;
- korrekt klassifizierte Events;
- `NO_TRADE`-Negativfälle;
- Pending Conditions: created/met/expired/invalidated;
- Revision-/Supersede-Fälle;
- Source-/Capture-/Parser-/E2E-Latenzen;
- erwartete vs tatsächliche Strategy Decisions;
- Abweichungen mit Ursache.

## Batch-/Portfolioübersicht

- Batch-Startkapital: 2.500 USDT rechnerisch, 10×250 isoliert;
- Spiegelportfolio: 240 USDT gemeinsamer Cashpool, 3×80 Slots;
- Netto-PnL und Netto-PnL/Tag;
- Drawdown;
- Tradezahl/Kapitalnutzung;
- bester/schlechtester Beitrag sichtbar;
- Gesamtkosten;
- Source-beeinflusste vs Indicator-only Entscheidungen.

## Trade-Liste

Jeder Trade:

- Symbol;
- Entry-/Exit-Signal-ID und Signalzeit;
- Indicator-/Bastian-/Pending-Condition-Referenz;
- Source-Session/Event-ID soweit beteiligt;
- Intent-/Order-/Fill-Referenz;
- Mengen/Preise;
- Brutto-/Netto-PnL;
- Fees/Slippage;
- Source-/E2E-Latenz soweit beteiligt;
- Haltedauer;
- Strategie-/Config-/Daten-/Source-Version;
- Exitgrund;
- ggf. Mark-to-market-Kennzeichen.

## Fairer Referenzbot-Vergleich

Vergleichsreport dokumentiert zwingend:

- beide Commit-/Strategieversionen;
- identischen Daten-Snapshot bzw. fachlich begründete Abweichung;
- identische Märkte;
- identische Gebühren-/Slippageannahmen;
- identische Kapitalbasis;
- identischen Forward-Paper-Zeitraum;
- Parameterfreeze vor Vergleichsbeginn;
- Netto-PnL, Netto-PnL/Tag, Drawdown, Profit Factor soweit stabil, Kosten, Exposure/Kapitalnutzung, Ausfälle und Latenzen.

Ein Sieger wird nicht nur nach Bruttogewinn bestimmt.

## Reportwarnungen

- Strategieparität fehlt;
- Source-Parität fehlt;
- weniger als drei Jahre, obwohl für den Indicator-Test erforderlich und verfügbar;
- Datenlücke/Revision;
- Source-Lücke/ungeklärter Sessionstatus;
- Kostenabweichung;
- zu wenige Trades/Source-Fälle;
- In-sample-Optimierung;
- stale Strategie-/Daten-/Source-Version;
- offene Endposition;
- ungeklärte Slotpriorisierung;
- ungeklärte Freshness/Latenz;
- Black-Box-Parität mit begrenzter Beweisstärke;
- Vergleichsbasen nicht identisch.

## Status der Bastian-Live-Evidence

Noch nicht vorhanden sind ein vollständiger Zielindikator, ausreichende gelabelte Bastian-Live-Ereignisse, finale Source-Allowlist/Capture-Pfade, belastbare Freshness-/Revision-/Conditional-Regeln, ein eingefrorenes Fusionsmodell und ein Forward-Paper-Datensatz. Deshalb existiert **keine** belastbare Aussage, dass der Bot Bastians reale Performance repliziert.

Spätere Reports müssen Indicator-only, Bastian-beeinflusste und Fusionsentscheidungen getrennt ausweisen, damit sichtbar bleibt, wodurch Mehr-/Minderperformance tatsächlich entsteht.
