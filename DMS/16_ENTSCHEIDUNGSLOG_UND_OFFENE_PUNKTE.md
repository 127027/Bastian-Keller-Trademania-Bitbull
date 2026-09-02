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
| BTK-DEC-027 | `Trademania - PVSRA Indicator` des TradingView-Publishers `BitbullTrading` ist öffentlich als realer TradeMania-/Bitbull-Kandidat verifiziert, aber noch **nicht** als finaler Zielindikator ausgewählt. | BESCHLOSSEN |
| BTK-DEC-028 | Vor dem Strategie-Freeze wird ein vollständiges Inventar aus öffentlichen und rechtmäßig zugänglichen Member-Quellen erstellt: Indicator Masterclass, Strategie-Indikator Masterclass, Discord und `trademania.app/bots`. | BESCHLOSSEN |
| BTK-DEC-029 | V1 soll keinen unnötigen Indikator-Stack erhalten. Gewählt wird der kleinste reproduzierbare Stack, den Bastian aktuell tatsächlich nutzt und der für ETH/Startuniversum geeignet ist. | BESCHLOSSEN |
| BTK-DEC-030 | Zielindikator-Auswahl erfolgt nach Bastian-Nähe, ETH-Eignung, Determinismus, Repainting, Automation/Alerts, Backtestbarkeit, Latenz, Rechte, Komplexität und Forward-Paper – nicht nach Marketing oder einem einzelnen guten historischen Lauf. | BESCHLOSSEN |
| BTK-DEC-031 | MACD, POC/VRVP/VPVR und RSI sind derzeit nur öffentlich belegte ergänzende Werkzeuge aus dem Bitbull-/TradeMania-Umfeld; sie werden erst V1-Bestandteil, wenn aktuelle Bastian-Evidence ihre konkrete Rolle bestätigt. | BESCHLOSSEN |

## B – Kritische offene Indikatorfragen

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-001 | Welcher Kandidat wird der finale Zielindikator bzw. minimale Zielstack? | OFFEN |
| BTK-OPEN-002 | Welche Plattform, Publisher-ID und aktuelle Version werden final verwendet? | OFFEN |
| BTK-OPEN-003 | Welche Inputs existieren und welche Defaults gelten? | OFFEN |
| BTK-OPEN-004 | Welcher Signal-Timeframe bzw. welche Multi-Timeframe-Abhängigkeit gilt? | OFFEN |
| BTK-OPEN-005 | Welche Daten/Preisquellen/Volumen-/Zusatzwerte werden benötigt? | OFFEN |
| BTK-OPEN-006 | Was ist ein Kauf-, Verkaufs-, Neutral-, Trend-, Level- oder Bestätigungssignal? | OFFEN |
| BTK-OPEN-007 | Darf auf offener Kerze gehandelt werden oder nur nach Bar-Close? | OFFEN |
| BTK-OPEN-008 | Repaintet/verschiebt der Zielindikator historische Signale/Levels? | OFFEN |
| BTK-OPEN-009 | Wie sind Warm-up und Initialzustand? | OFFEN |
| BTK-OPEN-010 | Wie wird ein Indikatorzustand in Entry/Exit/Ignore/Context übersetzt? | OFFEN |
| BTK-OPEN-011 | Gibt es Pyramiding, Reentry, TP, SL, Trailing oder Time-Exit? | OFFEN |
| BTK-OPEN-012 | Was passiert bei gleichzeitig gültigen Entry-Signalen und nur drei Slots? | OFFEN |
| BTK-OPEN-013 | Darf ein wegen voller Slots verpasstes Signal später nachgeholt werden? | OFFEN |
| BTK-OPEN-014 | Welche Overlays/Marker/Score-/Levelwerte müssen UI und Reports anzeigen? | OFFEN |
| BTK-OPEN-015 | Welche Alerts/Webhooks stehen zur Verfügung und entsprechen sie exakt den relevanten visuellen Zuständen? | OFFEN |
| BTK-OPEN-016 | Ist Sourcecode rechtmäßig zugänglich oder erfolgt Parität als Black-Box-Referenz? | OFFEN |

## C – Kritische offene Bastian-/Source-Fragen

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-017 | Welcher konkrete TradeMania-/Bastian-Indikator bzw. Stack wird nach Member-Inventar ausgewählt? | OFFEN |
| BTK-OPEN-018 | Welche offiziellen/member-only Quellen stehen technisch und rechtlich zur Verfügung? | OFFEN |
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

## D – Neue offene Punkte aus Registrierung und öffentlichem Kandidateninventar

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-033 | Welche Bots/Tools werden aktuell unter `trademania.app/bots` angezeigt und welche davon stammen tatsächlich aus Bastians Strategiepfad? | OFFEN |
| BTK-OPEN-034 | Welche Indikatoren, Versionen und Setup-Anleitungen sind aktuell im TradeMania-Discord/Indicator-Bereich sichtbar? | OFFEN |
| BTK-OPEN-035 | Nutzt Bastian den `Trademania - PVSRA Indicator` aktuell regelmäßig in seinen eigenen Lives/Analysen oder ist er primär Team-/Ausbildungswerkzeug? | OFFEN |
| BTK-OPEN-036 | Welche Teile von PVSRA sind für Bastian tatsächlich entscheidungsrelevant: Vector-Candles, Imbalance, POC, EMA, WIL, Sessions, Pivot/ADR oder Kombinationen? | OFFEN |
| BTK-OPEN-037 | Sind MACD, POC/Volume Profile oder RSI in Bastians aktuellem persönlichen Prozess Pflicht, optionaler Kontext oder nur Schulungsinhalt? | OFFEN |
| BTK-OPEN-038 | Welche Alerts/Webhooks/Exports bieten PVSRA und die Member-Indikatoren aktuell? | OFFEN |
| BTK-OPEN-039 | Welche konkreten Rechte/Nutzungsbedingungen gelten für automatisierte Auswertung der Member-Indikatoren und Bots? | OFFEN |
| BTK-OPEN-040 | Welche TradeMania-Bots sind überhaupt für unser Binance-Spot-/ETH-Ziel relevant und welche verfolgen andere Börsen, Futures, Scalping oder andere Strategien? | OFFEN |

## E – Vorgehen nach Registrierung/Erhalt

1. Zugangsdaten nicht in Git speichern.
2. **Zuerst vollständiges Tool-Inventar erstellen**: Discord, Indicator Masterclass, Strategie-Indikator Masterclass, `trademania.app/bots`, TradingView.
3. pro Kandidat Name/Version/Publisher/Zweck/Timeframe/Settings/Alerts/Repainting/Rechte dokumentieren.
4. markieren, welche Kandidaten Bastian persönlich aktuell verwendet.
5. für ETH mehrere aktuelle Bastian-Lives/Analysen mit sichtbaren Tools und Levels sammeln.
6. Zielindikator bzw. minimalen Stack anhand DMS-03-Auswahlkriterien wählen.
7. finalen Indikator mit UTC-Zeit/Symbol/Timeframe und Referenzfällen dokumentieren.
8. Open-Bar vs Close vs Reload testen.
9. Alerts/Webhooks/Exports prüfen.
10. offizielle Source-/Channel-IDs inventarisieren und allowlisten.
11. mehrere reale Bastian-Lives/Updates mit Sessionstatus und Zeitachse labeln.
12. Capture-Möglichkeiten je Quelle prüfen und Latenzen messen.
13. Sprecher-, Asset-, Entry-/Exit-/Manage-, Conditional- und Revision-Beispiele sammeln.
14. DMS 03 vervollständigen.
15. alle offenen Punkte schließen oder ausdrücklich als nicht strategie-/betriebsrelevant verwerfen.
16. Traceability/Config/Tests aktualisieren.
17. erst dann `BTK-INDICATOR-SPEC-1.0` einfrieren und signalaktiven Codeumbau starten.

## F – Nicht als offene Produktentscheidungen zu behandeln

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
