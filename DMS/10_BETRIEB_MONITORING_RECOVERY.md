# 10 – Betrieb, Monitoring und Recovery

## Systemzustände

`STARTING`, `HEALTHY`, `DEGRADED`, `HALTED`, `STOPPING`.

Zusätzlich werden getrennt geführt:

- `MARKET_DATA_HEALTH`
- `INDICATOR_HEALTH`
- `SOURCE_DISCOVERY_HEALTH`
- `SOURCE_CAPTURE_HEALTH`
- `SOURCE_PARSER_HEALTH`
- `BASTIAN_CONTEXT_HEALTH`
- `EXECUTION_HEALTH`

## Scheduler / 24/7-Watcher

- Marktfeed/Bar-Finalisierung: kontinuierlich;
- Source Discovery für freigegebene Kanäle/Ankündigungen: kontinuierlich bzw. nach erlaubtem Providerverfahren;
- Live-/Sessionstatus: während erwarteter/erkannter Sessions engmaschig;
- Content Capture: ereignis-/streamgetrieben soweit technisch möglich;
- Freshness-/Pending-Condition-Watchdog: spätestens alle 30 s oder enger, falls DMS 03 dies verlangt;
- Order-/Position-Reconciliation: ereignisgetrieben + periodisch;
- Daten-Vollaudit: täglich 00:05 UTC;
- tägliches Backup nach Audit;
- wöchentliche Integritätsprüfung;
- Backtests/Replays manuell oder freigegeben geplant.

Ein öffentlicher Wochenplan dient nur als Erwartungsfenster. Der Bot darf keinen dauerhaft hart codierten Streamkalender als Strategie-Wahrheit verwenden, wenn offizielle Ankündigungen/Termine dynamisch verfügbar sind.

## Healthchecks

Mindestens:

- DB erreichbar/integer;
- Systemzeit plausibel;
- Binance erreichbar;
- Marktfeed frisch;
- erwartete Bars vollständig;
- Börsenfilter aktuell;
- offene Orders/Positionen reconciled;
- allowgelistete Content-Quellen erreichbar bzw. sauber als unavailable markiert;
- Sessionstatus plausibel;
- Capture-Adapter aktiv;
- letzte Source-Metadaten plausibel;
- Capture-/Parser-/Validation-Version geladen;
- Source-/Capture-/Parser-/End-to-End-Latenz innerhalb der nach DMS 03 freigegebenen Grenzen;
- Pending Conditions nicht über Expiry hinaus aktiv;
- Telegram/Alarmweg verfügbar;
- Backupziel verfügbar.

## Source-Ausfälle

Ein Bastian-Source-Ausfall erzeugt **keine erfundene Aussage**. Der betreffende Layer wird `DEGRADED_SOURCE` bzw. komponentenspezifisch `DEGRADED`.

Nicht zulässig:

- Drittzusammenfassungen als Ersatzquelle;
- alte Replays still als Live zu behandeln;
- zuletzt bekannten Kontext ohne Freshness weiterlaufen zu lassen;
- unvollständiges Transkript durch Vermutung zu ergänzen.

Ob Indicator-only bei Source-Ausfall weiter handeln darf, entscheidet ausschließlich das eingefrorene Fusionsmodell.

Solange `BTK-INDICATOR-SPEC-1.0` nicht eingefroren ist, darf das System keinen signalaktiven Paper-/Live-Modus für BTK ausführen.

## Sessionende und Kontextablauf

Bei `ENDED` oder `REPLAY` werden keine noch offenen Aussagen automatisch dauerhaft aktiv gehalten. Jeder Bastian-Kontext und jede Pending Condition folgt ihrer eigenen Freshness-/Expiry-/Invalidation-Regel. Streamende allein ist weder automatisch Exit noch automatische Kontextverlängerung, außer DMS 03 definiert dies ausdrücklich.

## Latenzmonitoring

Pro Source-Ereignis werden, soweit messbar, gespeichert:

- Source/Published → Received;
- Received → Capture;
- Capture → Parse;
- Parse → Validation/Fusion;
- Fusion → Intent;
- Intent → Submit/Fill.

Überschreitung der für die Quellenklasse freigegebenen Latenz kann das Ereignis blockieren, auch wenn die Aussage inhaltlich korrekt war.

## Alerts

- P1: globaler Halt, unbekannte Order/Position, schwerer Reconciliation-/DB-Fehler;
- P2: starke Execution-Abweichung, kritischer Daten-/Source-/Capture-/Parser-Ausfall, kritische Latenzüberschreitung, Telegram-Ausfall;
- P3: nichtkritische Daten-/Source-Lücke, Session unerwartet unavailable, Backtest stale;
- P4: Info/Status.

P1/P2 gehen an Telegram. Ist kritische Live-Alarmierung >5 Minuten nicht verfügbar, werden neue Live-Entries pausiert.

## Backup

Backups verschlüsselt außerhalb des öffentlichen Repositories und außerhalb der aktiven DB halten. Zielretention:

- 7 tägliche;
- 4 wöchentliche;
- 12 monatliche.

Konfiguration/Deployment-Metadaten einschließen, niemals Secrets oder geschützte Rohinhalte unverschlüsselt. Fehlendes Backupziel blockiert Live-Freigabe.

## Restore

Restore-Test vor Live und danach mindestens quartalsweise. Restore endet in `LIVE_DISABLED`, bis Daten, Börse, Orders, Positionen, Source-Sessions, Pending Conditions und Quellenstatus neu reconciled sind. Alte Pending Conditions werden nach Restore nicht blind reaktiviert; Freshness/Expiry wird neu geprüft.

## Paper-Soak

Mindestens **30 Kalendertage**. Zusätzlich muss pro Symbol eine Mindestabdeckung geschlossener Strategiebars erreicht werden, die beim Freeze aus dem tatsächlich verwendeten BTK-Timeframe abgeleitet wird. Beispiel: Bei `1h` entsprechen 30 vollständige Tage 720 erwarteten Stundenbars; bei einem anderen Timeframe gilt eine entsprechend andere Zahl.

Falls nach 30 Tagen weniger als 20 abgeschlossene Trades vorliegen, wird der Soak bis 20 Trades fortgesetzt, maximal 90 Tage. Bastian-Source-Replay und reale Forward-Source-Ereignisse werden separat gezählt und dokumentiert.

Für den Bastian-Layer muss der Paper-Soak zusätzlich reale oder reproduzierbare Fälle für Live-Start, klare Aussage, konditionale Aussage, Revision, Source-Ausfall und Streamende enthalten.
