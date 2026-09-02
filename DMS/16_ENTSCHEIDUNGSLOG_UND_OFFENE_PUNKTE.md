# 16 – Entscheidungslog und offene Punkte

Dieses Dokument ist die zentrale Sammelstelle für Entscheidungen des **Bitbull / TradeMania / Bastian-Keller-Bots**.

Beschlussstand dieser Vorbereitung: **02.09.2026, Europe/Berlin**.

## A – Bereits beschlossen

| ID | Beschluss | Status |
|---|---|---|
| BTK-DEC-001 | Eigenständiges Repository `127027/Bastian-Keller-Trademania-Bitbull`; `main` dieses Repositories ist die BTK-Hauptlinie. | BESCHLOSSEN |
| BTK-DEC-002 | Strategieneutrale technische Komponenten dürfen wiederverwendet werden; keine unnötige Neuerfindung des Bot-Unterbaus. | BESCHLOSSEN |
| BTK-DEC-003 | Zuerst DMS vollständig vorbereiten; signalaktiver Codeumbau erst nach korrektem Strategie-Freeze. | BESCHLOSSEN |
| BTK-DEC-004 | Neuer Indikator wird nicht erraten. Fehlende technische Details bleiben `OFFEN`. | BESCHLOSSEN |
| BTK-DEC-005 | Startuniversum: BTC, ETH, BNB, SOL, XRP, ADA, LINK, AVAX, DOT, DOGE gegen USDT. | BESCHLOSSEN |
| BTK-DEC-006 | Paper-/Live-Baseline: 240 USDT gemeinsamer Cashpool, 3 Slots à 80 USDT. | BESCHLOSSEN |
| BTK-DEC-007 | Backtest-Baseline: 10×250 USDT isoliert; Einzeltest 250 USDT; optional 240/3×80 Spiegel. | BESCHLOSSEN |
| BTK-DEC-008 | Kein fixes Gewinnziel; reale Nettoperformance nach Kosten. | BESCHLOSSEN |
| BTK-DEC-009 | V1 bleibt Spot/Long-only ohne Leverage/Margin/Futures, solange neue Evidence und Eigentümerentscheidung nichts anderes festlegen. | BESCHLOSSEN |
| BTK-DEC-010 | Kostenbaseline 10 bp Fee + 2 bp Spread + 3 bp Slippage je Seite; Stress 10+10+20. | BESCHLOSSEN |
| BTK-DEC-011 | 5 % Tagesverlustpause, 20 % HWM-Drawdown-Halt, 25 bp Vorab-Preisabweichung und Order-Reconciliation bleiben Sicherheitsbaseline. | BESCHLOSSEN |
| BTK-DEC-012 | Startup-/Daten-/Backup-/Telegram-/Recovery-/Auditregeln bleiben technische Baseline. | BESCHLOSSEN |
| BTK-DEC-013 | Der tatsächliche Bastian-Keller-/TradeMania-Indikator und bereitgestellte Referenzen werden die Grundlage von DMS 03. | BESCHLOSSEN |
| BTK-DEC-014 | Schulungen/Lives dürfen als Strategie-Evidence ausgewertet werden, ersetzen aber keinen reproduzierbaren technischen Nachweis. | BESCHLOSSEN |
| BTK-DEC-015 | Offizieller Markenname in der DMS ist `TradeMania`; `Bitbull` bleibt Bastians etablierter Kanal-/Markenbezug. | BESCHLOSSEN |
| BTK-DEC-016 | Primäre menschliche Strategiequelle ist Bastian Keller, nicht automatisch das gesamte Mentorenteam. | BESCHLOSSEN |
| BTK-DEC-017 | Bot läuft 24/7 und überwacht Markt, Indikator und freigegebene Bastian-Quellen unabhängig voneinander. | BESCHLOSSEN |
| BTK-DEC-018 | Live-/Video-/Update-Aussagen müssen vor Orderauslösung strukturiert, zeitlich gültig, widerspruchsfrei genug und eindeutig sein. | BESCHLOSSEN |
| BTK-DEC-019 | Geschützte Rohinhalte/Transkripte/Medien werden nicht in das öffentliche Repository kopiert. | BESCHLOSSEN |
| BTK-DEC-020 | Historische Bastian-Performance wird nicht rückwirkend erfunden; fehlende Source-Historie wird durch Replay vorhandener Evidence und Forward-Paper-Evidence ersetzt. | BESCHLOSSEN |
| BTK-DEC-021 | Öffentliche Terminmuster sind keine hart codierte Strategie-Wahrheit; Streams/Updates sollen dynamisch über allowgelistete offizielle Quellen erkannt werden. | BESCHLOSSEN |
| BTK-DEC-022 | Rohtranskript, Speech-to-Text, Parserzusammenfassung oder Confidence-Wert darf niemals allein eine Order autorisieren. | BESCHLOSSEN |
| BTK-DEC-023 | Konditionale Aussagen werden als `PENDING_CONDITION` geführt und erst bei deterministisch bestätigter Bedingung innerhalb Freshness weiterverarbeitet. | BESCHLOSSEN |
| BTK-DEC-024 | Neue eindeutige Bastian-Revisionen erzeugen neue Events und dürfen älteren Kontext nach eingefrorener Regel superseden; Historie wird nicht umgeschrieben. | BESCHLOSSEN |
| BTK-DEC-025 | Source-/Capture-/Parser-/End-to-End-Latenzen werden gemessen und können ein ansonsten inhaltlich korrektes Signal wegen Veralterung blockieren. | BESCHLOSSEN |
| BTK-DEC-026 | Der spätere Vergleich mit dem separat betriebenen Referenzbot erfolgt mit derselben Daten-, Kosten-, Kapital- und Forward-Paper-Basis und ohne Zwischenstands-Tuning. | BESCHLOSSEN |

## B – Kritische offene Indikatorfragen

Diese Punkte werden geschlossen, sobald der Eigentümer den echten Indikator bereitstellt.

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-001 | Wie lautet der exakte Indikator-/Produktname? | OFFEN |
| BTK-OPEN-002 | Welche Plattform, Publisher-ID und Version werden verwendet? | OFFEN |
| BTK-OPEN-003 | Welche Inputs existieren und welche Defaults gelten? | OFFEN |
| BTK-OPEN-004 | Welcher Signal-Timeframe bzw. welche Multi-Timeframe-Abhängigkeit gilt? | OFFEN |
| BTK-OPEN-005 | Welche Daten/Preisquellen/Volumen-/Zusatzwerte werden benötigt? | OFFEN |
| BTK-OPEN-006 | Was ist ein Kauf-, Verkaufs-, Neutral-, Trend- oder Bestätigungssignal? | OFFEN |
| BTK-OPEN-007 | Darf auf offener Kerze gehandelt werden oder nur nach Bar-Close? | OFFEN |
| BTK-OPEN-008 | Repaintet/verschiebt der Indikator historische Signale? | OFFEN |
| BTK-OPEN-009 | Wie sind Warm-up und Initialzustand? | OFFEN |
| BTK-OPEN-010 | Wie wird ein Signal in Entry/Exit/Ignore übersetzt? | OFFEN |
| BTK-OPEN-011 | Gibt es Pyramiding, Reentry, TP, SL, Trailing oder Time-Exit? | OFFEN |
| BTK-OPEN-012 | Was passiert bei gleichzeitig gültigen Entry-Signalen und nur drei Slots? | OFFEN |
| BTK-OPEN-013 | Darf ein wegen voller Slots verpasstes Signal später nachgeholt werden? | OFFEN |
| BTK-OPEN-014 | Welche Overlays/Marker/Scorewerte müssen UI und Reports anzeigen? | OFFEN |
| BTK-OPEN-015 | Welche Alerts stehen zur Verfügung und entsprechen sie exakt den visuellen Signalen? | OFFEN |
| BTK-OPEN-016 | Ist Sourcecode rechtmäßig zugänglich oder erfolgt Parität als Black-Box-Referenz? | OFFEN |

## C – Kritische offene Bastian-/Source-Fragen

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-017 | Welcher konkrete TradeMania-/Bastian-Indikator ist der Zielindikator? | OFFEN |
| BTK-OPEN-018 | Welche offiziellen/member-only Quellen stehen nach Registrierung technisch und rechtlich zur Verfügung? | OFFEN |
| BTK-OPEN-019 | Darf eine eindeutige Bastian-Aussage selbst einen Entry erzeugen oder nur den Indikator bestätigen/blockieren/managen? | OFFEN |
| BTK-OPEN-020 | Wie lange bleibt eine Aussage je Tradinghorizont gültig? | OFFEN |
| BTK-OPEN-021 | Wie werden Teilverkäufe, „Gewinne sichern“, Stop-Nachziehen und Zielzonen übersetzt? | OFFEN |
| BTK-OPEN-022 | Welche exakte Syntax/Marktbedingung wird aus konditionalen Sätzen („wenn X, dann Long“) erzeugt? | OFFEN |
| BTK-OPEN-023 | Welche Quellen sind bei Konflikten maßgeblicher: Live, Telegram, Member-/Discord-Inhalt, Updatevideo? | OFFEN |
| BTK-OPEN-024 | Welche maximale End-to-End-Latenz ist für die jeweilige Tradingart zulässig? | OFFEN |
| BTK-OPEN-025 | Welche offiziellen Channel-/Account-/Source-IDs gehören in die Allowlist? | OFFEN |
| BTK-OPEN-026 | Wie wird Live vs Replay vs Update je Provider technisch sicher erkannt? | OFFEN |
| BTK-OPEN-027 | Welcher Capture-Pfad ist je Quelle verfügbar und zulässig: offizielle Untertitel, Transkript/API, lokales Speech-to-Text oder anderer Weg? | OFFEN |
| BTK-OPEN-028 | Welche Mindestqualität/Pflichtfelder müssen Capture und Parser erfüllen, bevor `BASTIAN_ACTIONABLE_SIGNAL` möglich ist? | OFFEN |
| BTK-OPEN-029 | Wie wird Sprecheridentität bei mehreren Personen im Live abgesichert? | OFFEN |
| BTK-OPEN-030 | Wie wird eine Revision/Invalidierung zeitlich und fachlich einem älteren Event zugeordnet? | OFFEN |
| BTK-OPEN-031 | Was passiert mit aktivem Bastian-Kontext bei Source-Ausfall oder Streamende? | OFFEN |
| BTK-OPEN-032 | Welche Pending Conditions überleben einen Neustart und unter welchen Freshness-/Reconciliation-Regeln? | OFFEN |

## D – Vorgehen nach Registrierung/Erhalt

1. Zugangsdaten nicht in Git speichern.
2. exakten Indikatornamen, Version und Settings erfassen.
3. offizielle Source-/Channel-IDs inventarisieren und allowlisten.
4. mehrere Signale mit UTC-Zeit/Symbol/Timeframe dokumentieren.
5. Open-Bar vs Close vs Reload testen.
6. Alerts prüfen.
7. mehrere reale Bastian-Lives/Updates mit Sessionstatus und Zeitachse labeln.
8. Capture-Möglichkeiten je Quelle prüfen und Latenzen messen.
9. Sprecher-, Asset-, Entry-/Exit-/Manage-, Conditional- und Revision-Beispiele sammeln.
10. DMS 03 vervollständigen.
11. alle offenen Punkte schließen oder ausdrücklich als nicht strategie-/betriebsrelevant verwerfen.
12. Traceability/Config/Tests aktualisieren.
13. erst dann `BTK-INDICATOR-SPEC-1.0` einfrieren und signalaktiven Codeumbau starten.

## E – Nicht als offene Produktentscheidungen zu behandeln

Später fehlende Testresultate, Backtestzahlen, Paper-Soak, API-Key-Nachweis, Telegram-Testalarm oder Restore sind **Nachweise**, keine Strategieentscheidungen.

## Änderungsformat

```text
Entscheidung: BTK-DEC-xxx
Datum/Zeitzone:
Entschieden von:
Beschluss:
Begründung:
Quelle/Evidence:
Betroffene Anforderungen/Dokumente:
Neue Strategie-/Configversion:
Erforderliche Tests/Backtests/Replays:
```
