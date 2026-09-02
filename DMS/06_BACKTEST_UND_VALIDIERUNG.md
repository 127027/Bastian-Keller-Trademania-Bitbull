# 06 – Backtest und Validierung

## Zweck

Zwei Nachweise werden getrennt behandelt:

1. **Strategie-/Quellenparität:** Reagiert der Bot auf denselben Indikatorzustand bzw. dieselbe gelabelte Bastian-Aussage korrekt?
2. **Performance:** Was ergibt die eingefrorene Logik unter realistischen Kosten und Kapitalregeln?

Ein positiver Backtest beweist keine zukünftige Rendite.

## Primärfenster

- exakt drei vollständige Jahre je Coin;
- `[start,end)` in UTC;
- erforderlicher Warm-up liegt vor `start`;
- Datenlücken invalidieren den Lauf und verschieben nicht still das Fenster.

## Standardläufe

- Indicator-Golden-/Parity-Test;
- Bastian-Source-Replay gegen gelabelte Beispiele;
- zehn isolierte Coin-Backtests à 250 USDT;
- frei wählbarer Einzeltest à 250 USDT;
- Aggregatübersicht;
- optionaler 240-USDT-/3×80-Spiegellauf;
- Buy-and-Hold/Cash-Benchmarks;
- Kosten-Stress;
- chronologisches Replay;
- Walk-Forward/OOS nur wenn Parameter tatsächlich optimiert wurden.

## Ereignisreihenfolge

Die Fill- und Signalsemantik wird nach DMS 03 endgültig eingefroren. Grundsatz: keine Entscheidung darf Informationen aus einer Zukunftskerze oder einem später veröffentlichten Content-Ereignis verwenden.

## Kostenbaseline

Je Seite:

- Fee: 10 bp;
- Spread: 2 bp;
- Slippage: 3 bp.

Stress je Seite: 10 + 10 + 20 bp.

Börsenfilter, Step-/Tick-Rundung und Mindestnotional werden simuliert.

## Bastian-Replay

Für gelabelte Source-Ereignisse werden Published-Time, Received-Time, Spoken-Time/Offset, Live-vs-Replay, Sprecher, Asset, Aussageklasse, Bedingung und Freshness berücksichtigt. Der Replay-Runner darf keine spätere Korrektur rückwirkend vorziehen.

## Fusionsvergleich

Vor Freeze des Fusionsmodells getrennt ausweisen:

- `INDICATOR_PRIMARY`;
- `BASTIAN_PRIMARY`;
- `DUAL_CONFIRMATION`;
- `SOURCE_SPECIFIC` soweit fachlich sinnvoll.

Kein Modell wird nur wegen des höchsten Backtestgewinns ausgewählt; zuerst müssen fachliche Übereinstimmung und Forward-Paper-Verhalten stimmen.

## Pflichtmetriken

Net PnL, Rendite, Max Drawdown, Tradezahl, Winrate, Profit Factor soweit stabil, Exposure, Kosten, durchschnittlicher Trade, Dauer, blockierte Signale, ausgelassene Signale, Source-Latenz und Benchmark.

## Anti-Overfitting

- Parameter vor Testfenster einfrieren;
- keine schlechten Coins nachträglich entfernen;
- keine Zielrendite rückwärts optimieren;
- Sensitivität/OOS bei Tuning;
- jede Methodikänderung versionieren.

## Gültiger Lauf

Nur gültig, wenn Datenqualität, Strategieversion, Config, Kostenmodell, Hashes, Source-/Signalparität und Artefakte vollständig nachvollziehbar sind.