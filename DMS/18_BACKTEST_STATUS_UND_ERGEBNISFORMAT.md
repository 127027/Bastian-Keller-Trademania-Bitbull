# 18 – Backteststatus und Ergebnisformat

## Wahrheitsgemäßer Ist-Stand

Stand **02.09.2026** wurde für die Bitbull-/TradeMania-/Bastian-Keller-Variante **kein valider Backtest ausgeführt**.

Grund: Der tatsächliche neue Indikator wurde dem Projekt noch nicht bereitgestellt. Deshalb fehlen:

- eingefrorene `BTK-INDICATOR-SPEC-1.0`;
- Strategieparameter/Signaldefinition;
- Referenz-/Golden-Artefakte;
- angepasster Botcode;
- gültige BTK-Backtestresultate.

Jede konkrete BTK-Rendite-, Trefferquote-, Trade- oder Drawdownzahl wäre derzeit erfunden.

## Verbindlicher späterer Testumfang

- Referenz-/Signalparität;
- 10×250-USDT-Batch;
- Einzelmodus 250 USDT;
- primär drei vollständige Jahre plus Warm-up;
- rechnerische Aggregation der zehn isolierten Resultate;
- optional 240/3×80-Spiegel;
- volle Historie als Zusatz;
- Baseline-/Stresskosten;
- Buy-and-Hold;
- Run-Manifest + Datenqualitätsbericht.

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
| Nettorendite | zu berechnen |
| Referenzparität | bestanden/nicht bestanden/nicht geprüft |
| Max Drawdown | zu berechnen |
| Trades | zu berechnen |
| Gewinnquote | zu berechnen |
| Profit Factor | zu berechnen |
| Gebühren | zu berechnen |
| Slippage | zu berechnen |
| Exposure | zu berechnen |
| Buy-and-Hold | zu berechnen |
| Qualitätsstatus | valid/invalid/stale |

## Batch-/Portfolioübersicht

- Batch-Startkapital: 2.500 USDT rechnerisch, 10×250 isoliert;
- Spiegelportfolio: 240 USDT gemeinsamer Cashpool, 3×80 Slots;
- Netto-PnL;
- Drawdown;
- Tradezahl/Kapitalnutzung;
- bester/schlechtester Beitrag sichtbar;
- Gesamtkosten.

## Trade-Liste

Jeder Trade:

- Symbol;
- Entry-/Exit-Signal-ID und Signalzeit;
- Intent-/Order-/Fill-Referenz;
- Mengen/Preise;
- Brutto-/Netto-PnL;
- Fees/Slippage;
- Haltedauer;
- Strategie-/Config-/Datenversion;
- Exitgrund;
- ggf. Mark-to-market-Kennzeichen.

## Reportwarnungen

- Strategieparität fehlt;
- weniger als drei Jahre;
- Datenlücke/Revision;
- Kostenabweichung;
- zu wenige Trades;
- In-sample-Optimierung;
- stale Strategie-/Datenversion;
- offene Endposition;
- ungeklärte Slotpriorisierung;
- Black-Box-Parität mit begrenzter Beweisstärke.

## Status der Bastian-Live-Evidence

Noch nicht vorhanden sind ein vollständiger Zielindikator, gelabelte Bastian-Live-Ereignisse, eine belastbare Freshness-Regel, eine Fusionsregel und ein Forward-Paper-Datensatz. Deshalb existiert **keine** belastbare Aussage, dass die Variante Bastians reale Performance repliziert.

Spätere Reports müssen Indicator-only und Bastian-Fusion getrennt ausweisen, damit sichtbar bleibt, ob Mehr-/Minderperformance tatsächlich aus der Live-Schicht stammt.
