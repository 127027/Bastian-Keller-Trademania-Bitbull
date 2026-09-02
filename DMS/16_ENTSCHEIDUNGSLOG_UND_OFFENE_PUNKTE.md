# 16 – Entscheidungslog und offene Punkte

Dieses Dokument ist die zentrale Sammelstelle für Entscheidungen der **Bitbull / TradeMania / Bastian-Keller-Variante**.

Beschlussstand dieser Vorbereitung: **02.09.2026, Europe/Berlin**.

## A – Bereits beschlossen / geerbt

| ID | Beschluss | Status |
|---|---|---|
| BTK-DEC-001 | Eigenständiges Repository `127027/Bastian-Keller-Trademania-Bitbull`; `main` dieses Repositories ist die BTK-Hauptlinie. | BESCHLOSSEN |
| BTK-DEC-002 | Bestehender Bot-Unterbau wird wiederverwendet; kein unnötiger Neubau. | BESCHLOSSEN |
| BTK-DEC-003 | Zuerst DMS vollständig vorbereiten; Codeumbau erst nach korrektem Strategie-Freeze. | BESCHLOSSEN |
| BTK-DEC-004 | Neuer Indikator wird nicht erraten. Fehlende technische Details bleiben `OFFEN`. | BESCHLOSSEN |
| BTK-DEC-005 | Zehn Binance-Spot-Paare BTC, ETH, BNB, SOL, XRP, ADA, LINK, AVAX, DOT, DOGE gegen USDT bleiben initiales Universum. | GEERBT/BESCHLOSSEN |
| BTK-DEC-006 | Paper-/Live-Baseline: 240 USDT gemeinsamer Cashpool, 3 Slots à 80 USDT. | GEERBT/BESCHLOSSEN |
| BTK-DEC-007 | Backtest-Baseline: 10×250 USDT isoliert; Einzeltest 250 USDT; optional 240/3×80 Spiegel. | GEERBT/BESCHLOSSEN |
| BTK-DEC-008 | Kein fixes Gewinnziel; reale Nettoperformance nach Kosten. | BESCHLOSSEN |
| BTK-DEC-009 | Long-only/kein Leverage/Margin/Futures bleibt sicherer Baselinezustand, solange die neue Strategie nichts anderes explizit erfordert und der Eigentümer keine Änderung beschließt. | GEERBT |
| BTK-DEC-010 | Kostenbaseline 10 bp Fee + 2 bp Spread + 3 bp Slippage je Seite; Stress 10+10+20. | GEERBT |
| BTK-DEC-011 | 5 % Tagesverlustpause, 20 % HWM-Drawdown-Halt, 25 bp Vorab-Preisabweichung, Order-Reconciliation bleiben bestehen. | GEERBT |
| BTK-DEC-012 | Startup-/Daten-/Backup-/Telegram-/Recovery-/Auditregeln bleiben bestehen. | GEERBT |
| BTK-DEC-013 | Der tatsächliche Bastian-Keller-Indikator und vom Eigentümer bereitgestellte Referenzen werden die Grundlage von DMS 03. | BESCHLOSSEN |
| BTK-DEC-014 | Schulungen/Lives dürfen zur Interpretation herangezogen werden, ersetzen aber keinen reproduzierbaren technischen Nachweis. | BESCHLOSSEN |

## B – Kritische offene Strategiefragen

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

## C – Vorgehen nach Erhalt des Indikators

1. Zugangsdaten nicht in Git speichern.
2. exakten Namen/Version/Settings erfassen.
3. mehrere Signale mit UTC-Zeit/Symbol/Timeframe dokumentieren.
4. Open-Bar vs Close vs Reload testen.
5. Alerts prüfen.
6. relevante offizielle Erklärungen mit Datum/Quelle zuordnen.
7. DMS 03 ausfüllen.
8. alle offenen Punkte oben schließen oder ausdrücklich als nicht für die Strategie relevant verwerfen.
9. Traceability/Config/Tests aktualisieren.
10. erst dann `BTK-INDICATOR-SPEC-1.0` einfrieren und Codeumbau starten.

## D – Nicht als offene Produktentscheidungen zu behandeln

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
Erforderliche Tests/Backtests:
```

## E – Neue Beschlüsse aus der Bastian-Zieldefinition

| ID | Beschluss | Status |
|---|---|---|
| BTK-DEC-015 | Offizieller Markenname in der DMS ist `TradeMania`; `Bitbull` bleibt Bastians etablierter Kanal-/Markenbezug. | BESCHLOSSEN |
| BTK-DEC-016 | Primäre menschliche Strategiequelle ist Bastian Keller, nicht automatisch das gesamte Mentorenteam. | BESCHLOSSEN |
| BTK-DEC-017 | Bot läuft 24/7 und kann neue Bastian-Inhalte in seinen Strategiekontext aufnehmen. | BESCHLOSSEN |
| BTK-DEC-018 | Live-/Video-Aussagen müssen vor Orderauslösung strukturiert, zeitlich gültig und eindeutig sein. | BESCHLOSSEN |
| BTK-DEC-019 | Geschützte Rohinhalte/Transkripte werden nicht in das öffentliche Repository kopiert. | BESCHLOSSEN |
| BTK-DEC-020 | Historische Bastian-Performance wird nicht rückwirkend erfunden; fehlende Source-Historie wird durch Forward-Paper-Evidence ersetzt. | BESCHLOSSEN |

## F – Zusätzliche offene Bastian-Fragen

| ID | Frage | Status |
|---|---|---|
| BTK-OPEN-017 | Welcher konkrete TradeMania-Indikator ist der Zielindikator? | OFFEN |
| BTK-OPEN-018 | Welche offiziellen/member-only Quellen stehen nach Registrierung technisch und rechtlich zur Verfügung? | OFFEN |
| BTK-OPEN-019 | Darf eine eindeutige Bastian-Aussage selbst einen Entry erzeugen oder nur den Indikator bestätigen/blockieren? | OFFEN |
| BTK-OPEN-020 | Wie lange bleibt eine Aussage gültig (Scalp/Intraday/Swing, explizite oder abgeleitete Freshness)? | OFFEN |
| BTK-OPEN-021 | Wie werden Teilverkäufe, „Gewinne sichern“, Stop-Nachziehen und Zielzonen übersetzt? | OFFEN |
| BTK-OPEN-022 | Wie werden konditionale Sätze („wenn X, dann Long“) als wartende Regeln behandelt? | OFFEN |
| BTK-OPEN-023 | Welche Bastian-Quellen sind schneller/maßgeblicher bei Konflikten: Live, Telegram, Discord/Memberbereich, Updatevideo? | OFFEN |
| BTK-OPEN-024 | Welche maximale End-to-End-Latenz ist technisch erreichbar und für die jeweilige Tradingart ausreichend? | OFFEN |
