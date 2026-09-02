# 20 – Betriebsrunbook

Status: `VERBINDLICH` für den BTK-Betriebsunterbau; signalaktive Strategie bleibt bis zum Freeze gesperrt.

## Vor jedem ersten Start

1. Modus `BACKTEST` oder `PAPER`; `LIVE` aus.
2. DMS-/Strategie-/Configversion prüfen.
3. Kandidateninventar-/Auswahlversion und finalen Zielstack prüfen.
4. `BTK-INDICATOR-SPEC-1.0` muss eingefroren sein, bevor signalaktive BTK-Verarbeitung aktiviert werden darf.
5. zehn Coins, Börse, Strategie-Timeframe und Kostenmodell prüfen.
6. Indicator-Data-Source-Mapping prüfen: Preisprovider, Volumenprovider/Override, Marktart, Sessiontimezone/DST, Footprint-/POC-Pfad soweit relevant.
7. Source-Allowlist, Session-Discovery, Capture-Modi, Freshness-/Konflikt-/Latenzregeln prüfen.
8. Secret-Referenzen testen; Werte nie anzeigen.
9. Speicher, Systemzeit, Backupziel prüfen.
10. Startup-Report vollständig abwarten.
11. nur bei `HEALTHY` und bestandener Indicator-/Data-Source-/Bastian-Source-Parität Paper-Signale freigeben.

## Täglicher Betreibercheck

- Modus/Health;
- finaler Target Stack/Version;
- letzte erwartete finale Marktdaten;
- letzte 00:05-UTC-Synchronisation;
- Indicator Data Source Mapping/Health;
- aktiver Volume Override/Provider soweit relevant;
- Footprint-/POC-/Session-Provider soweit signalrelevant;
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

## Indicator-Provider/Mapping stimmt nicht

Wenn Target Stack/Settings zwar stimmen, aber Preis-/Volumen-/Session-/Footprint-Mapping von der eingefrorenen Referenz abweicht:

1. neue signalabhängige Entries pausieren;
2. keine Ersatzquelle automatisch einsetzen;
3. Config-/Provider-/Symbol-/Market-Type-/Timezone-Werte mit DMS 03/13 vergleichen;
4. bei PVSRA insbesondere Volume Override und Volumensymbol prüfen;
5. bei POC/Footprint prüfen, ob der Wert exakt verfügbar oder nur `BLACK_BOX_EXTERNAL` ist;
6. Referenz-/Golden-Fall wiederholen;
7. betroffene Runs bei echter Mappingänderung `STALE`/`INVALID` markieren;
8. erst nach dokumentierter Parität wieder freigeben.

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
8. Target Stack und Indicator-Source-Mapping neu laden/prüfen;
9. Source-Sessions neu erkennen;
10. Pending Conditions auf Freshness/Expiry/Invalidation prüfen – nicht blind reaktivieren;
11. Versionen/Config prüfen;
12. Modus explizit wieder freigeben.

## Markt-/Indicator-Feed stale

- ab definierter Stale-Grenze ohne erwartetes Streamupdate oder überfälliger finaler Bar/Indicator-Feed;
- betroffene Symbole und darauf basierende Pending Conditions pausieren;
- Provider/Systemzeit/Mapping prüfen;
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

Ursache/Coins/Indicator-Provider prüfen, sicheren Audit neu starten, bei Historien- oder Source-Mappingänderung Runs stale, Wiederholung eskalieren.

## Restore

Isoliert, `LIVE_DISABLED`, Backuphash, DB/Config/Artefakte, Secrets separat, Target Stack/Indicator-Source-Mapping prüfen, Startup-Data-Check, bekannten Backtest/Replay reproduzieren, Source-Allowlist/Sessionzustand prüfen, Reconciliation trocken, Bericht freigeben.

## Referenzabweichung Originalindikator

Wenn der Bot bei gleichem Symbol/Timeframe/Settings vom Originalindikator abweicht:

1. keine Strategieänderung aus Performancegründen;
2. Signal/UTC-Bar/Settings/Quelle sichern;
3. Target-Stack-/Indikatorversion prüfen;
4. prüfen, ob Originalsignal intrabar/repaintend war;
5. Chartpreis-, Volumen-, Volume-Override-, Market-Type-, Session-/Timezone- und ggf. Footprint-/POC-Abweichung ausschließen;
6. DMS 03/05/13 und Evidence prüfen;
7. Code oder Spezifikation nur mit dokumentierter Ursache ändern;
8. alle betroffenen Runs stale/invalid markieren;
9. Referenztest wiederholen.

## Incidentabschluss

Ursache verstanden, Kapital-/Orderauswirkung abgeglichen, Versionen korrigiert, dauerhafte Korrektur getestet, Monitoring/Test ergänzt, DMS/Runbook aktualisiert, Ownerfreigabe.
