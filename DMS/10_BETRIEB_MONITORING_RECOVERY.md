# 10 – Betrieb, Monitoring und Recovery

## Systemzustände

`STARTING`, `HEALTHY`, `DEGRADED`, `HALTED`, `STOPPING`.

Zusätzlich werden `MARKET_DATA_HEALTH` und `BASTIAN_SOURCE_HEALTH` getrennt geführt.

## Scheduler

- Marktfeed/Bar-Finalisierung: kontinuierlich;
- Content-/Live-Quellenmonitoring: kontinuierlich bzw. nach erlaubtem Providerverfahren;
- Freshness-Watchdog: spätestens alle 30 s;
- Order-/Position-Reconciliation: ereignisgetrieben + periodisch;
- Daten-Vollaudit: täglich 00:05 UTC;
- tägliches Backup nach Audit;
- wöchentliche Integritätsprüfung;
- Backtests/Replays manuell oder freigegeben geplant.

## Healthchecks

Mindestens:

- DB erreichbar/integer;
- Systemzeit plausibel;
- Binance erreichbar;
- Marktfeed frisch;
- erwartete Bars vollständig;
- Börsenfilter aktuell;
- offene Orders/Positionen reconciled;
- Content-Quelle erreichbar bzw. sauber als unavailable markiert;
- letzte Source-Metadaten plausibel;
- Parser-/Validation-Version geladen;
- Telegram/Alarmweg verfügbar;
- Backupziel verfügbar.

## Source-Ausfälle

Ein Bastian-Source-Ausfall erzeugt keine erfundene Aussage. Der betreffende Layer wird `DEGRADED_SOURCE`. Ob Indicator-only weiter handeln darf, wird erst mit dem eingefrorenen Fusionsmodell entschieden.

Solange `BTK-INDICATOR-SPEC-1.0` nicht eingefroren ist, darf das System keinen signalaktiven Paper-/Live-Modus für BTK ausführen.

## Alerts

- P1: globaler Halt, unbekannte Order/Position, schwerer Reconciliation-/DB-Fehler;
- P2: starke Execution-Abweichung, kritischer Daten-/Source-Ausfall, Telegram-Ausfall;
- P3: nichtkritische Daten-/Source-Lücke, Backtest stale;
- P4: Info/Status.

P1/P2 gehen an Telegram. Ist kritische Live-Alarmierung >5 Minuten nicht verfügbar, werden neue Live-Entries pausiert.

## Backup

Backups verschlüsselt außerhalb des öffentlichen Repositories und außerhalb der aktiven DB halten. Zielretention:

- 7 tägliche;
- 4 wöchentliche;
- 12 monatliche.

Konfiguration/Deployment-Metadaten einschließen, niemals Secrets unverschlüsselt. Fehlendes Backupziel blockiert Live-Freigabe.

## Restore

Restore-Test vor Live und danach mindestens quartalsweise. Restore endet in `LIVE_DISABLED`, bis Daten, Börse, Orders, Positionen und Quellenstatus neu reconciled sind.

## Paper-Soak

Mindestens 30 Tage und 720 geschlossene Strategiebars je Symbol. Falls weniger als 20 abgeschlossene Trades vorliegen, Soak bis 20 Trades fortsetzen, maximal 90 Tage. Bastian-Source-Replay und reale Forward-Source-Ereignisse werden separat gezählt und dokumentiert.