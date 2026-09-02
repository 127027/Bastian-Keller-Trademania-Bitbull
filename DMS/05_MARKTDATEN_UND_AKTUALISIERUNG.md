# 05 – Marktdaten und Aktualisierung

Status: `VERBINDLICH` für Datenplattform; tatsächlicher Strategie-Timeframe und Zusatzdaten bleiben bis DMS-03-Freeze `OFFEN`.

## Börsendaten

Primärquelle ist Binance Spot. Gespeichert werden pro Symbol/Timeframe mindestens Open-/Close-Time UTC, OHLC, Volumen, `closed/provisional`, Datenquelle, Abrufzeit und Import-Batch-ID. Preise und Mengen werden decimal-sicher verarbeitet.

## Strategie-Timeframe

Es wird kein Timeframe aus einem anderen System automatisch übernommen. Die Datenplattform muss die für den Originalindikator benötigten Timeframes nach DMS 03 vollständig unterstützen. UI-Zeiträume sind keine Trading-Timeframes.

## Historie

- mindestens drei vollständige Jahre vor Backtestende;
- zusätzlicher Warm-up gemäß DMS 03;
- Datenquelle und Symbolmapping je Import festhalten;
- Providerwechsel erzeugt neuen Datensatzstand.

## Startup-Sequenz

1. Konfiguration/Schema validieren.
2. Systemuhr/UTC prüfen.
3. DB-Integrität prüfen.
4. Börsenmetadaten/Filter für alle zehn Paare laden.
5. Zeitraum, Duplikate, Lücken und OHLC-Konsistenz prüfen.
6. fehlende Bereiche paginiert nachladen.
7. offene Kerze als `provisional` markieren.
8. finale Bars freigeben.
9. nach Strategie-Freeze Indikatorzustand/Warm-up rekonstruieren.
10. Paper/Live: Orders, Fills, Positionen, Salden abgleichen.
11. erst bei gesundem Zustand Signalverarbeitung aktivieren.

Historische Signale werden beim Start nicht als verspätete Live-Orders nachgesendet.

## Laufende Aktualisierung

- Stream/WebSocket für Klines;
- REST-Fallback und Gap-Recovery;
- finale Bar genau einmal verarbeiten;
- Reconnect mit Backoff/Jitter;
- 90 s ohne Streamupdate -> `DEGRADED`;
- erwartete finale Strategiebar >120 s verspätet -> Symbol pausieren/recovern.

Intrabar-Handel bleibt deaktiviert, bis DMS 03 ihn ausdrücklich und reproduzierbar verlangt.

## Täglicher Audit

Um **00:05 UTC**:

- alle zehn Paare prüfen;
- fehlende abgeschlossene Bars nachladen;
- Duplikate/Raster/OHLC/Frische validieren;
- Symbolstatus und Börsenfilter aktualisieren;
- Datenqualitätsreport schreiben;
- abhängige Backtests bei historischen Korrekturen `STALE` markieren.

Keine synthetischen Kerzen ohne dokumentierte Providerbegründung.

## Content-Datenstrom

Neben OHLCV gibt es Bastian-/TradeMania-Quellenereignisse. Pro Ereignis mindestens:

- Origin;
- Source-ID/URL oder private Referenz;
- Published-/Received-Time;
- Live/Replay;
- Sprecher;
- Content-Hash;
- Parsing-/Validationstatus.

Börsenzeit und Contentzeit werden niemals gleichgesetzt.

## Terminfindung

Der Bot darf keinen Wochenplan als ewige Strategie-Wahrheit hardcoden. Öffentliche Terminankündigungen und Plattform-Metadaten werden dynamisch beobachtet. Aktuell recherchierte Routinen stehen in DMS 22 und dienen nur als Erwartungsfenster.

Wenn ein angekündigter Stream nicht startet oder technisch nicht auswertbar ist, entstehen keine synthetischen Aussagen. Der Content-Layer geht auf `DEGRADED_SOURCE`; Markt-/Indikatorzustand bleibt separat sichtbar.