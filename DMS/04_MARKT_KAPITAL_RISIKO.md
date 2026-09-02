# 04 – Märkte, Kapital und Risiko

Status: `VERBINDLICH` für den technischen Baseline-Unterbau; indikatorabhängige Slotpriorität bleibt `OFFEN`.

## Initiales Marktuniversum

BTC/USDT, ETH/USDT, BNB/USDT, SOL/USDT, XRP/USDT, ADA/USDT, LINK/USDT, AVAX/USDT, DOT/USDT, DOGE/USDT.

Die Liste wird für den ersten Vergleich nicht nach Backtestergebnissen nachträglich optimiert. Vor Aktivierung muss Binance Spot-Handel und alle aktuellen Filter bestätigen.

## Paper/Live

- Startkapital: 240 USDT gemeinsamer Cashpool.
- Standard: maximal drei Positionsslots à 80 USDT Zielnotional.
- maximal eine Long-Position je Paar, solange DMS 03 nichts anderes freigibt.
- kein Kredit, kein negativer Cashbestand.
- kein automatisches Compounding in V1.

## Backtest-Labor

- Standard-Batch: zehn isolierte Tests mit je 250 USDT.
- Einzeltest: frei wählbares Paar mit 250 USDT.
- optionaler Portfolio-Spiegel: 240 USDT, drei Slots à 80 USDT.
- kein festes Gewinnziel.

## Positionsgröße

Menge wird auf Binance-Step-Size abgerundet. MinQty/MinNotional und verfügbarer Cash werden vor jeder Order geprüft. Nicht investierbarer Rest bleibt Cash.

## Slotvergabe

Die Slotpriorität wird erst nach Analyse des Originalindikators und des endgültigen Fusionsmodells eingefroren. Bei mehr gültigen Entry-Kandidaten als freien Slots darf keine spontane, performancegetriebene Auswahl erfolgen.

## Schutzregeln

Schutzregeln können Signale blockieren, aber keine neuen Signale erzeugen:

- stale/lückenhafte Daten;
- Source-Health unklar;
- Systemzeit unklar;
- Börsenfilter fehlen;
- API-/Authentifizierungsfehler;
- unbekannte offene Order/Positionsabweichung;
- Mittel reichen nicht;
- Not-Aus;
- Live nicht freigegeben;
- Preisabweichung >25 bp vor Submit.

## Verlustkontrollen

| Kontrolle | Verhalten |
|---|---|
| Not-Aus | keine neuen Entries; Exits separat behandeln |
| Max. offene Positionen | 3 Baseline |
| Tagesverlust | ab 5 % ggü. Start-of-Day-Equity keine neuen Entries bis nächster UTC-Tag |
| Live-Drawdown | ab 20 % unter High-Water-Mark global `HALTED` |
| Preisabweichung | >25 bp vor Order blockiert |
| stale Feed | 90 s ohne Update -> `DEGRADED`; finale Strategiebar >120 s überfällig -> pausieren/recovern |

## Benchmark

Jede Auswertung vergleicht mindestens mit Buy-and-Hold desselben Assets und 100 % Cash; optional zusätzlich gleichgewichtetem Buy-and-Hold-Portfolio.