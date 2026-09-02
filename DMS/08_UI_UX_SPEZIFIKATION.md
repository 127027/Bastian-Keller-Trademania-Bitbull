# 08 – UI/UX-Spezifikation

## Grundsätze

- deutsche Oberfläche;
- Modus und System-/Source-Health jederzeit sichtbar;
- keine Gewinnversprechen;
- keine versteckte Strategieänderung über UI;
- pro Order nachvollziehbare Quelle und Entscheidungskette.

## Navigation

1. Übersicht
2. Chart
3. Positionen/Orders
4. Bastian/Quellen
5. Backtests
6. Datenqualität
7. System/Logs
8. Einstellungen
9. Dokumentation

## Dashboard

Pro Coin mindestens Kurs, aktueller Indikatorzustand, letzter gültiger Bastian-Kontext, Position, unrealisiertes PnL, letzter Signal-/Orderzeitpunkt und Health.

Global: Modus, Equity, Cash, belegte Slots, Tages-PnL, Drawdown, Feed-Health, Source-Health und Not-Aus.

## Chart

Zeiträume:

- Heute
- 1 Woche
- 1 Monat
- 1 Jahr
- 3 Jahre

Darstellung nach DMS 03:

- Candles;
- Originalindikator-Overlays/Marker soweit reproduzierbar;
- Bastian-Ereignismarker getrennt von Indikatorsignalen;
- Order-/Fillmarker;
- Position und Entry;
- provisorische Bars sichtbar markieren.

Strategiefremde Alt-Overlays werden nicht angezeigt.

## Bastian-/Source-Ansicht

Zeigt ausschließlich auditierbare Metadaten/abgeleitete Zusammenfassungen:

- Quelle/Origin;
- Published-/Received-Time;
- Live/Replay;
- Sprecher;
- Asset;
- Klassifikation (`CONTEXT`, `WATCH`, `ENTRY`, `EXIT`, ...);
- Freshness;
- Validationstatus;
- daraus entstandene oder blockierte Aktion.

Geschützte Volltranskripte gehören nicht in die öffentliche UI, sofern Rechte das nicht erlauben.

## Backtest-UI

Startmodi:

- alle 10 Coins ×250 USDT;
- einzelner Coin ×250 USDT;
- optional 240/3×80 Portfolio-Spiegel;
- Source-Replay/Parity.

Vor Start zeigt die UI Strategieversion, Config, Datenzeitraum, Kostenmodell und Source-/Golden-Version.

## Einstellungen

Strategierelevante Werte sind nach Freeze versioniert. Änderungen invalidieren abhängige Backtests. Live-relevante Änderungen benötigen bewusste Bestätigung und Audit.

## Bedienungssicherheit

`LIVE` darf optisch nicht mit `PAPER` verwechselbar sein. Not-Aus, Source-Ausfall, Datenlücke, Reconciliation-Fehler und globale Halt-Zustände müssen prominent sichtbar sein.