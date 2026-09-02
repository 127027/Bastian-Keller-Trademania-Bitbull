# 20 – Betriebsrunbook

Status: `VERBINDLICH` für den BTK-Betriebsunterbau; signalaktive Strategie bleibt bis zum Freeze gesperrt.

## Vor jedem ersten Start

1. Modus `BACKTEST` oder `PAPER`; `LIVE` aus.
2. DMS-/Strategie-/Configversion prüfen.
3. `BTK-INDICATOR-SPEC-1.0` muss eingefroren sein, bevor signalaktive BTK-Verarbeitung aktiviert werden darf.
4. zehn Coins, Börse, Strategie-Timeframe und Kostenmodell prüfen.
5. Source-Allowlist, Session-Discovery, Capture-Modi, Freshness-/Konflikt-/Latenzregeln prüfen.
6. Secret-Referenzen testen; Werte nie anzeigen.
7. Speicher, Systemzeit, Backupziel prüfen.
8. Startup-Report vollständig abwarten.
9. nur bei `HEALTHY` und bestandener Strategie-/Source-Parität Paper-Signale freigeben.

## Täglicher Betreibercheck

- Modus/Health;
- letzte erwartete finale Marktdaten;
- letzte 00:05-UTC-Synchronisation;
- Indicator Health;
- Source Discovery / Capture / Parser Health;
- aktuelle/erwartete Source-Sessions und deren Status;
- aktive Bastian-Kontexte und Pending Conditions inkl. Expiry;
- Source-/Capture-/Parser-/End-to-End-Latenzen;
- offene/ungeklärte Orders;
- Reconciliation/Salden;
- Datenlücken;
- Backup;
- P1/P2-Alarme;
- Scheduler/Speicherplatz;
- aktive Strategie-/Quellen-/Configversion.

## Erkannter Bastian-Livestart

1. offizielle allowgelistete Source-ID verifizieren;
2. Session als `LIVE` speichern;
3. Capture-Adapter und Zeitstempel prüfen;
4. Speaker-Validator aktivieren;
5. Latenzmessung starten;
6. keine Order nur wegen Livestart;
7. erst validierte Source-Ereignisse durch DMS-03-Pipeline führen.

## Geplanter Neustart

1. neue Entries pausieren;
2. offene Orders/Positionen ansehen;
3. aktive Source-Sessions/Pending Conditions sichern;
4. geordnet stoppen;
5. Wartung;
6. `LIVE_DISABLED`/Paper starten;
7. Startup-Sync/Reconciliation;
8. Source-Sessions neu erkennen;
9. Pending Conditions auf Freshness/Expiry/Invalidation prüfen – nicht blind reaktivieren;
10. Versionen/Config prüfen;
11. Modus explizit wieder freigeben.

## Marktfeed stale

- ab definierter Stale-Grenze ohne Streamupdate oder überfälliger finaler Bar;
- betroffene Symbole und darauf basierende Pending Conditions pausieren;
- REST/Provider/Systemzeit prüfen;
- Lücken schließen;
- Strategie-Zustand aus gültigen Daten rekonstruieren;
- keine alten Signale nachholen;
- bei Dauerproblem Incident.

## Source/Session stale oder unavailable

1. keine Aussage erfinden oder durch Drittzusammenfassung ersetzen;
2. Source-/Capture-Layer auf `DEGRADED` setzen;
3. betroffene neue Bastian-Events blockieren;
4. vorhandene Kontexte nur bis zu ihrer expliziten Freshness weiterführen;
5. Pending Conditions nur weiterführen, wenn DMS 03 dies trotz Source-Ausfall ausdrücklich erlaubt;
6. Reconnect/Sessionstatus prüfen;
7. späteres Replay nicht automatisch als aktuelles Live behandeln.

## Unklares oder fehlerhaftes Transkript/Parser-Ergebnis

1. kein neues `EXECUTION_INTENT`;
2. Event `UNKNOWN`/`CAPTURE_UNCERTAIN`/`PARSER_UNCERTAIN` markieren;
3. Rohreferenz, Zeit, Source und Parserversion sichern;
4. keine fehlenden Preis-/Asset-/Aktionsdetails ergänzen;
5. Event nur nach neuer eindeutiger Source-Evidence neu bewerten – Historie nicht umschreiben.

## Bastian revidiert/invalidiert eine Aussage

1. neues Source-Ereignis anlegen;
2. ältere Event-ID referenzieren (`supersedes_event_id` oder eingefrorene Konfliktbeziehung);
3. Context Store aktualisieren;
4. betroffene Pending Conditions nach DMS 03 invalidieren/ändern;
5. bestehende Position nur dann managen/schließen, wenn die eingefrorene Strategie dies für diese Aussageklasse vorsieht;
6. vollständigen Auditpfad behalten.

## Streamende

1. Session `ENDED` markieren;
2. Capture sauber beenden;
3. offene Events finalisieren;
4. Kontext/Conditions nicht automatisch löschen oder verlängern;
5. Freshness-/Expiry-Regeln anwenden;
6. späteres Replay als neue Session-/Source-Form behandeln.

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
- keine automatische Liquidation allein wegen des HWM-Halts;
- Wiederaufnahme nur nach Ursachen-/Ledger-/Daten-/Configprüfung.

## Telegram gestört

UI/Log, >5 min kritischer Live-Alarmweg gestört → `DEGRADED`, Entries pausieren, Secret-Referenz prüfen, Testalarm, dann freigeben.

## Positions-/Saldodifferenz

Live-Entries global pausieren, lokale Fills/Ledger mit Börse vergleichen, keine Werte still überschreiben, Ursache auditieren, Reconciliation wiederholen.

## Not-Aus

Blockiert neue Entries. Offene Orders/Positionen separat beurteilen. Schließen nur nach bestätigter Aktion bzw. eingefrorener Notfallregel.

## Delisting/Handelspause

Symbol `HALTED`, Status/Position prüfen, kein automatischer Ersatzcoin, Universumsänderung versionieren und neu testen.

## Fehlgeschlagener Datenaudit

Ursache/Coins prüfen, sicheren Audit neu starten, bei Historienänderung Runs stale, Wiederholung eskalieren.

## Restore

Isoliert, `LIVE_DISABLED`, Backuphash, DB/Config/Artefakte, Secrets separat, Startup-Data-Check, bekannten Backtest/Replay reproduzieren, Source-Allowlist/Sessionzustand prüfen, Reconciliation trocken, Bericht freigeben.

## Referenzabweichung Originalindikator

Wenn der Bot bei gleichem Symbol/Timeframe/Settings vom Originalindikator abweicht:

1. keine Strategieänderung aus Performancegründen;
2. Signal/UTC-Bar/Settings/Quelle sichern;
3. prüfen, ob Originalsignal intrabar/repaintend war;
4. Datenprovider-/Zeitzonen-/Timeframe-Abweichung ausschließen;
5. DMS 03 und Evidence prüfen;
6. Code oder Spezifikation nur mit dokumentierter Ursache ändern;
7. alle betroffenen Runs stale/invalid markieren;
8. Referenztest wiederholen.

## Incidentabschluss

Ursache verstanden, Kapital-/Orderauswirkung abgeglichen, Versionen korrigiert, dauerhafte Korrektur getestet, Monitoring/Test ergänzt, DMS/Runbook aktualisiert, Ownerfreigabe.
