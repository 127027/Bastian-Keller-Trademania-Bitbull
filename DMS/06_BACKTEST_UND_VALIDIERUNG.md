# 06 – Backtest und Validierung

## Zweck

Vier Nachweise werden getrennt behandelt:

1. **Kandidatenauswahl:** Wurde der Zielindikator/-stack aus dem real verfügbaren TradeMania-/Bitbull-Inventar begründet ausgewählt, statt nach einem günstigen Testergebnis?
2. **Indicator-Parität:** Reagiert die technische Implementierung auf denselben Originalindikatorzustand korrekt und verwendet sie dieselben relevanten Datenquellen/Mappings?
3. **Bastian-Source-Parität:** Wird dieselbe tatsächlich vorhandene, gelabelte Bastian-Aussage chronologisch korrekt erfasst, strukturiert und bewertet?
4. **Performance:** Was ergibt die eingefrorene Logik unter realistischen Kosten und Kapitalregeln?

Ein positiver Backtest beweist keine zukünftige Rendite.

## Kandidatenphase vor Backtest

Bevor Performancewerte zur Auswahl verwendet werden dürfen:

- Public-/Member-Inventar gemäß DMS 03/22 erstellen;
- Kandidaten nach Bastian-Nähe, ETH-Eignung, Determinismus, Repainting, Datenbedarf, Alerts/Automation, Rechte und technischer Reproduzierbarkeit bewerten;
- finalen Zielstack auswählen und Auswahlversion/hash festhalten;
- danach Strategieparameter/Settings einfrieren.

Performance darf einen fachlich geeigneten Kandidaten später **validieren oder verwerfen**, aber nicht rückwirkend eine unkontrollierte Suche nach dem höchsten historischen PnL treiben.

## Historische Testfenster

### Indicator-/Marktdatenpfad

- primär exakt drei vollständige Jahre je Coin, soweit die eingefrorene Indikatorstrategie historisch reproduzierbar ist;
- `[start,end)` in UTC;
- erforderlicher Warm-up liegt vor `start`;
- Datenlücken invalidieren den Lauf und verschieben nicht still das Fenster.

### Bastian-Source-Pfad

Für Bastian-Aussagen existiert **keine künstliche Drei-Jahres-Vorgabe**. Getestet wird ausschließlich über tatsächlich vorhandene, zeitlich belastbare Evidence und danach über Forward-Paper. Fehlende historische Lives, Aussagen oder Revisionen werden nicht erfunden, interpoliert oder aus späterem Wissen rekonstruiert.

## Indicator-Data-Source-Parität

Ein Indicator-Backtest ist nur dann als paritätsnah gültig, wenn die signalrelevanten Datenquellen der eingefrorenen Referenz entsprechen.

Zu manifestieren sind mindestens:

- Chart-/Preisprovider und Symbolmapping;
- Volumenprovider und Symbolmapping;
- Cross-Exchange-/Volume-Override;
- Marktart `spot|perpetual|futures|other`;
- Sessiontimezone/DST;
- Footprint-/POC-Provider und Auflösung, falls relevant;
- weitere Zusatzdaten;
- Mapping-/Provider-Hashes soweit verfügbar.

Für den öffentlichen Kandidaten `Trademania - PVSRA Indicator` ist besonders zu prüfen, ob Bastian einen Volume Override verwendet. Ein Backtest mit Binance-Preis + Binance-Volumen ist **nicht automatisch paritätisch**, wenn die Referenzeinstellung z. B. anderen Chartpreis oder anderes Volumen nutzt.

POC-/Footprint-Werte dürfen nicht aus grobem OHLCV angenähert und anschließend als Originalparität bewertet werden. Nicht exakt reproduzierbare Teile werden als `BLACK_BOX_EXTERNAL` oder `NOT_REPRODUCIBLE` gekennzeichnet und getrennt bewertet.

## Standardläufe

- Kandidaten-/Auswahlreview;
- Indicator-Golden-/Parity-Test;
- Indicator-Data-Source-Parity-Test;
- Bastian-Source-Replay gegen gelabelte echte/eigene zulässige Referenzfälle;
- Capture-/Parser-/Validation-Replay;
- Pending-Condition-/Revision-/Expiry-Replay;
- zehn isolierte Coin-Backtests à 250 USDT für historisch reproduzierbare Strategieanteile;
- frei wählbarer Einzeltest à 250 USDT;
- Aggregatübersicht;
- optionaler 240-USDT-/3×80-Spiegellauf;
- Buy-and-Hold/Cash-Benchmarks;
- Kosten-Stress;
- chronologisches Gesamt-Replay;
- Walk-Forward/OOS nur wenn Parameter tatsächlich optimiert wurden.

## Ereignisreihenfolge

Die Fill- und Signalsemantik wird nach DMS 03 endgültig eingefroren. Grundsatz: Keine Entscheidung darf Informationen aus einer Zukunftskerze, einem später veröffentlichten Content-Ereignis oder einer späteren Bastian-Revision vorwegnehmen.

Für Source-Replay gilt insbesondere:

1. Sessionstatus bis zum Zeitpunkt `t`;
2. bis `t` tatsächlich verfügbare Source-Ereignisse;
3. Capture-/Parser-/Validation-Zustand bis `t`;
4. aktuelle Freshness/Expiry/Revision;
5. Marktdaten bis `t`;
6. Fusions-/Risk-/Capital-Entscheidung;
7. erst danach Intent/Fillmodell.

## Kostenbaseline

Je Seite:

- Fee: 10 bp;
- Spread: 2 bp;
- Slippage: 3 bp.

Stress je Seite: 10 + 10 + 20 bp.

Börsenfilter, Step-/Tick-Rundung und Mindestnotional werden simuliert.

## Bastian-Source-Replay

Für jedes gelabelte Source-Ereignis werden mindestens berücksichtigt:

- Source-/Session-ID und Origin;
- Published-Time;
- Received-Time;
- Spoken-Time/Offset soweit verfügbar;
- `LIVE|ENDED|REPLAY|UPDATE|...`;
- Sprecher;
- Asset(s);
- Aussageklasse;
- Preis/Zone/Bedingung soweit relevant;
- Freshness/Expiry;
- Pending-Condition-State;
- Revision/Supersede/Conflict;
- Capture-/Parser-/Validation-Version;
- gemessene bzw. historische Latenz soweit bekannt.

Der Replay-Runner darf keine spätere Korrektur rückwirkend vorziehen. Ein Replay darf außerdem nicht so tun, als wäre die damals tatsächlich eingetretene Netzwerk-/Capture-Latenz null, wenn ein belastbarer Zeitstempel vorhanden ist.

## Fusionsvergleich vor Freeze

Fachlich plausible Kandidaten dürfen getrennt untersucht werden:

- `INDICATOR_PRIMARY`;
- `BASTIAN_PRIMARY`;
- `DUAL_CONFIRMATION`;
- `SOURCE_SPECIFIC`.

Genau ein Modell wird für V1 eingefroren. Kein Modell wird nur wegen des höchsten historischen Gewinns ausgewählt; zuerst müssen Quellen-/Strategietreue, Robustheit und Forward-Paper-Verhalten stimmen.

## Pflichtmetriken

Mindestens:

- Net PnL;
- Net PnL/Tag;
- Rendite;
- Max Drawdown;
- Tradezahl/Winrate;
- Profit Factor soweit statistisch stabil;
- Exposure/Kapitalnutzung;
- Gebühren/Spread/Slippage;
- durchschnittlicher Trade und Haltedauer;
- blockierte/verpasste Signale;
- Indicator-Parity-/Data-Source-Parity-Status;
- Source-/Capture-/Parser-/E2E-Latenz soweit beteiligt;
- Pending Conditions created/met/expired/invalidated;
- Source-/Parser-Abweichungen;
- Benchmark.

## Anti-Overfitting

- Zielstack vor Performanceoptimierung dokumentieren;
- Parameter vor Testfenster einfrieren;
- keine schlechten Coins nachträglich entfernen;
- keine Zielrendite rückwärts optimieren;
- keine Bastian-Regel nachträglich aus dem Ausgang eines Trades ableiten;
- keine zusätzlichen MACD/RSI/POC-Filter nur deshalb hinzufügen, weil sie einen historischen Lauf verbessern;
- Sensitivität/OOS bei Tuning;
- jede Methodikänderung versionieren;
- nach Beginn eines fairen A/B-Vergleichs kein Zwischenstands-Tuning.

## Gültiger Lauf

Nur gültig, wenn Kandidaten-/Auswahlversion, Datenqualität, Indicator-Data-Source-Mapping, Strategieversion, Config, Kostenmodell, Hashes, Indicator-Parität, Source-/Replay-Parität und Artefakte vollständig nachvollziehbar sind. Ein Lauf darf einzelne nicht verfügbare Source-/Indicator-Anteile ausdrücklich als `NOT_REPRODUCIBLE` ausweisen; er darf sie nicht still simulieren.

## Fairer späterer Bot-gegen-Bot-Vergleich

Die BTK-Variante wird später gegen den separat betriebenen Referenzbot unter **identischen äußeren Bedingungen** verglichen. Der Vergleich darf nicht dadurch verzerrt werden, dass ein Bot bessere Daten, niedrigere Kostenannahmen oder einen günstigeren Zeitraum erhält.

Verbindlich identisch bzw. explizit begründet abweichend:

- dieselben zehn Märkte;
- derselbe historische Daten-Snapshot und dieselben Berichtsgrenzen für vergleichbare Marktpfade;
- dieselbe Gebühren-, Spread- und Slippage-Baseline;
- dieselbe Startkapital-/Slotbasis im jeweiligen Vergleichsmodus;
- dieselben Exchange-Filter und Rundungsregeln;
- derselbe Forward-Paper-Zeitraum;
- keine nachträgliche Parameter- oder Zielstackänderung während des Vergleichs.

Bastian-Source-Evidence und spezifische Indicator-Source-Mappings sind strategiespezifische Inputs des BTK-Bots und werden nicht künstlich in den Referenzbot eingespeist. Umgekehrt werden dessen strategiespezifische Inputs nicht dem BTK-Bot zugeschlagen.

Verglichen werden mindestens Netto-PnL und Netto-PnL/Tag, Max Drawdown, Profit Factor soweit stabil, Tradezahl, Exposure, Gesamtkosten, Kapitalnutzung, blockierte/ausgelassene Signale, technische Ausfälle, Source-/Execution-Latenz und Reproduzierbarkeit.

**Gewinner ist nicht automatisch der Bot mit dem höchsten Bruttogewinn.** Die Entscheidung berücksichtigt Nettoperformance, Risiko, Stabilität und operativen Aufwand. Beide vollständigen Ergebnisberichte bleiben erhalten; kein schlechterer Lauf wird gelöscht oder durch einen günstigeren Zeitraum ersetzt.
