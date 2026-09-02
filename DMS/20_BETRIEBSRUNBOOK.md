# 20 – Betriebsrunbook

Status: `GEERBT`, ergänzt um Strategie-Freeze-Prüfung.

## Vor jedem ersten Start

1. Modus `BACKTEST` oder `PAPER`; `LIVE` aus.
2. DMS-/Strategie-/Configversion prüfen.
3. Für BTK-Variante: `BTK-INDICATOR-SPEC-1.0` muss eingefroren sein, bevor Signalverarbeitung aktiviert werden darf.
4. zehn Coins, Börse, Timeframe und Kostenmodell prüfen.
5. Secret-Referenzen testen; Werte nie anzeigen.
6. Speicher, Systemzeit, Backupziel prüfen.
7. Startup-Report vollständig abwarten.
8. nur bei `HEALTHY` und bestandener Strategieparität Paper-Signale freigeben.

## Täglicher Betreibercheck

- Modus/Health;
- letzte erwartete finale Marktdaten;
- letzte 00:05-UTC-Synchronisation;
- offene/ungeklärte Orders;
- Reconciliation/Salden;
- Datenlücken;
- Backup;
- P1/P2-Alarme;
- Scheduler/Speicherplatz;
- aktive Strategie-/Quellen-/Configversion.

## Geplanter Neustart

1. neue Entries pausieren;
2. offene Orders/Positionen ansehen;
3. geordnet stoppen;
4. Wartung;
5. `LIVE_DISABLED`/Paper starten;
6. Startup-Sync/Reconciliation;
7. Versionen/Config prüfen;
8. Modus explizit wieder freigeben.

## Feed stale

- ab 90 s ohne Streamupdate oder gemäß Strategie-Timeframe überfälliger finaler Bar;
- betroffene Symbole pausieren;
- REST/Provider/Systemzeit prüfen;
- Lücken schließen;
- Strategie-Zustand aus finalen Daten rekonstruieren;
- keine alten Signale nachholen;
- bei Dauerproblem Incident.

## Orderstatus `UNKNOWN`

1. keine Ersatzorder;
2. Client-Order-ID prüfen;
3. Orders/Trades seit Signalzeit;
4. Salden;
5. Fills ins Ledger;
6. Restunsicherheit → `HALTED`;
7. dokumentierte Reconciliation vor Entsperrung.

## Verlust-/Drawdown-Grenzen

- 5 % Tagesverlust → neue Entries bis nächster UTC-Tag pausieren;
- 20 % globaler HWM-Drawdown → `HALTED`;
- keine automatische Liquidation;
- Wiederaufnahme nur nach Ursachen-/Ledger-/Daten-/Configprüfung.

## Telegram gestört

UI/Log, >5 min Liveausfall → `DEGRADED`, Entries pausieren, Secret-Referenz prüfen, Testalarm, dann freigeben.

## Positions-/Saldodifferenz

Live-Entries global pausieren, lokale Fills/Ledger mit Börse vergleichen, keine Werte still überschreiben, Ursache auditieren, Reconciliation wiederholen.

## Not-Aus

Blockiert neue Entries. Offene Orders/Positionen separat beurteilen. Schließen nur nach bestätigter Aktion.

## Delisting/Handelspause

Symbol `HALTED`, Status/Position prüfen, kein automatischer Ersatzcoin, Universumsänderung versionieren und neu backtesten.

## Fehlgeschlagener Datenaudit

Ursache/Coins prüfen, sicheren Audit neu starten, bei Historienänderung Runs stale, Wiederholung eskalieren.

## Restore

Isoliert, `LIVE_DISABLED`, Backuphash, DB/Config/Artefakte, Secrets separat, Startup-Data-Check, bekannten Backtest reproduzieren, Reconciliation trocken, Bericht freigeben.

## Spezieller BTK-Incident: Referenzabweichung

Wenn der Bot bei gleichem Symbol/Timeframe/Settings vom Originalindikator abweicht:

1. keine Strategieänderung aus Performancegründen;
2. Signal/UTC-Bar/Settings/Quelle sichern;
3. prüfen, ob Originalsignal intrabar/repaintend war;
4. Datenprovider-/Zeitzonen-/Timeframe-Abweichung ausschließen;
5. DMS 03 und Evidence prüfen;
6. Code oder Spezifikation nur mit dokumentierter Ursache ändern;
7. alle betroffenen Backtests stale/invalid markieren;
8. Referenztest wiederholen.

## Incidentabschluss

Ursache verstanden, Kapital-/Orderauswirkung abgeglichen, Versionen korrigiert, dauerhafte Korrektur getestet, Monitoring/Test ergänzt, DMS/Runbook aktualisiert, Ownerfreigabe.

## Störung: Bastian-Quelle unklar oder widersprüchlich

1. keine neue Order aus dem betroffenen Source Event;
2. Event als `UNKNOWN` oder `SOURCE_CONFLICT` speichern;
3. Quelle/Empfangszeit/Asset im UI sichtbar machen;
4. keine alte Aussage automatisch wieder aktivieren;
5. Indikatorpfad nur so weiterbetreiben, wie es der eingefrorene Fusion Mode erlaubt;
6. nach Klärung neue Aussage als neues Source Event verarbeiten – niemals Historie umschreiben.

## Störung: Stream/Untertitel nicht verfügbar

Nicht mit Zusammenfassungen Dritter oder geratenem Inhalt ersetzen. Source-Layer `DEGRADED`; später eintreffendes Replay nur handeln, wenn seine Freshness-Regel das ausdrücklich zulässt.
