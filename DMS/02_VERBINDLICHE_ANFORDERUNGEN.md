# 02 – Verbindliche Anforderungen

Alle Anforderungen verwenden das Präfix `BTK-`.

## Strategie und Quellen

| ID | Anforderung | Status |
|---|---|---|
| BTK-STR-001 | Nur die in DMS 03 eingefrorene BTK-Strategie darf Orders erzeugen. | VERBINDLICH |
| BTK-STR-002 | Fehlende Indikator- oder Bastian-Regeln werden nicht erfunden. | VERBINDLICH |
| BTK-STR-003 | Indikatorname, Version, Inputs, Timeframe, Signal-/Zustandslogik werden vollständig dokumentiert. | OFFEN |
| BTK-STR-004 | Intrabar, Bar-Close und Repainting werden vor Implementierung geprüft. | OFFEN |
| BTK-STR-005 | Jede Entscheidung speichert Symbol, Zeit, Strategieversion, Quellen-/Parameterhash und Grund. | VERBINDLICH |
| BTK-STR-006 | Indikatorparität wird über Golden-/Black-Box-Referenzen nachgewiesen. | NACHWEIS AUSSTEHEND |
| BTK-SRC-001 | Primäre menschliche Quelle ist Bastian Keller. Andere Mentoren handeln nicht automatisch. | VERBINDLICH |
| BTK-SRC-002 | Live-/Update-Aussagen werden erst nach Strukturierung und Freshness-Prüfung handelbar. | VERBINDLICH |
| BTK-SRC-003 | Replay, alte Videos, Zuschauerfragen und historische Beschreibungen dürfen nicht als aktuelle Orders missverstanden werden. | VERBINDLICH |
| BTK-SRC-004 | Geschützte Rohtranskripte/Memberinhalte werden nicht öffentlich committed. | VERBINDLICH |
| BTK-SRC-005 | Jedes Content-Ereignis speichert Origin, Source-ID/URL oder private Referenz, Published-/Received-/Spoken-Time, Sprecher, Live/Replay, Hash und Parsingstatus. | VERBINDLICH |
| BTK-SRC-006 | Nur explizit allowgelistete offizielle Quellen dürfen den Bastian-Layer speisen; Termin-/Livestream-Erkennung erfolgt dynamisch und nicht über einen dauerhaft hart codierten Marketingkalender. | VERBINDLICH |
| BTK-SRC-007 | Für jede Quelle wird der technisch und rechtlich zulässige Capture-Pfad dokumentiert, z. B. offizielle Metadaten, Untertitel, Transkript/API oder andere freigegebene Methode. | OFFEN |
| BTK-SRC-008 | Rohtext, Speech-to-Text, NLP-/Parser-Zusammenfassung oder Confidence-Wert ist niemals allein orderautorisierend; ein `BASTIAN_ACTIONABLE_SIGNAL` benötigt die Pflichtfelder aus DMS 03. | VERBINDLICH |
| BTK-SRC-009 | Bei mehrdeutiger, unvollständiger, widersprüchlicher oder kritisch unsicherer Erfassung wird keine neue Order aus diesem Source-Ereignis erzeugt. | VERBINDLICH |
| BTK-SRC-010 | Konditionale Aussagen werden als wartende Regel gespeichert und dürfen erst auslösen, wenn Bedingung, Asset, Gültigkeit und Marktbeobachtung deterministisch bestätigt sind. | VERBINDLICH |
| BTK-SRC-011 | Eine neuere eindeutige Revision/Invalidierung darf älteren Bastian-Kontext gemäß eingefrorener Konfliktregel ersetzen; Historie wird nicht überschrieben. | VERBINDLICH |
| BTK-SRC-012 | Source-Health, Capture-Latenz, Parser-Latenz und End-to-End-Reaktionslatenz werden gemessen und auditierbar gespeichert. | VERBINDLICH |
| BTK-SRC-013 | Maximal zulässige Latenz, Freshness und Source-Priorität werden vor signalaktivem Paper/Live je Quellenklasse festgelegt. | OFFEN |
| BTK-SRC-014 | Stream-/Session-Lifecycle unterscheidet mindestens `SCHEDULED`, `LIVE`, `ENDED`, `REPLAY`, `STALE`, `UNAVAILABLE`. | VERBINDLICH |
| BTK-SRC-015 | Bei Source-Ausfall, Capture-Ausfall oder unklarer Sprechererkennung wird nicht auf Drittzusammenfassungen oder geratenen Inhalt ausgewichen. | VERBINDLICH |

## Märkte, Kapital und Risiko

| ID | Anforderung | Status |
|---|---|---|
| BTK-MKT-001 | Startuniversum: BTCUSDT, ETHUSDT, BNBUSDT, SOLUSDT, XRPUSDT, ADAUSDT, LINKUSDT, AVAXUSDT, DOTUSDT, DOGEUSDT. | VERBINDLICH |
| BTK-CAP-001 | Paper/Live startet mit 240 USDT gemeinsamem Cash. | VERBINDLICH |
| BTK-CAP-002 | Standard: maximal drei Slots à 80 USDT Zielnotional. | VERBINDLICH |
| BTK-CAP-003 | Backtests haben kein fixes Gewinnziel; Nettoperformance nach Kosten wird berichtet. | VERBINDLICH |
| BTK-CAP-004 | Kein automatisches Compounding in V1. | VERBINDLICH |
| BTK-RSK-001 | Kein Leverage, Margin, Futures oder Auszahlungsrecht. | VERBINDLICH |
| BTK-RSK-002 | Binance Filter (MinNotional, Tick, Step, Qty) werden vor Orders geprüft. | VERBINDLICH |
| BTK-RSK-003 | Ab 5 % Tagesverlust keine neuen Entries bis zum nächsten UTC-Tag. | VERBINDLICH |
| BTK-RSK-004 | Ab 20 % Drawdown vom Live-HWM global `HALTED`. | VERBINDLICH |
| BTK-RSK-005 | Vor Submit blockiert >25 bp Preisabweichung den Entry. | VERBINDLICH |

## Daten

| ID | Anforderung | Status |
|---|---|---|
| BTK-DAT-001 | OHLCV wird persistent und decimal-sicher gespeichert. | VERBINDLICH |
| BTK-DAT-002 | Startup prüft Zeitraum, Lücken, Duplikate, letzte finale Kerze und Frische. | VERBINDLICH |
| BTK-DAT-003 | Fehlende Daten werden inkrementell nachgeladen und erneut validiert. | VERBINDLICH |
| BTK-DAT-004 | Täglicher Vollaudit um 00:05 UTC. | VERBINDLICH |
| BTK-DAT-005 | Stream mit REST-Fallback; provisorische Bars bleiben markiert. | VERBINDLICH |
| BTK-DAT-006 | Ob offene Bars signalrelevant sind, entscheidet ausschließlich DMS 03. | OFFEN |

## Backtest, Replay und Vergleich

| ID | Anforderung | Status |
|---|---|---|
| BTK-BKT-001 | Primärbericht: drei vollständige Jahre je Paar plus Warm-up, soweit die eingefrorene Indikatorstrategie historische Reproduktion erlaubt. | VERBINDLICH |
| BTK-BKT-002 | Standard-Batch: 10 isolierte Coin-Tests mit je 250 USDT. | VERBINDLICH |
| BTK-BKT-003 | Einzelmodus: frei wählbares Paar mit 250 USDT. | VERBINDLICH |
| BTK-BKT-004 | Optionaler Portfolio-Spiegel: 240 USDT, 3×80 Slots. | VERBINDLICH |
| BTK-BKT-005 | Kostenbaseline je Seite: 10 bp Fee + 2 bp Spread + 3 bp Slippage; Stress: 10+10+20. | VERBINDLICH |
| BTK-BKT-006 | Kein Look-ahead, Survivorship-Bias oder synthetisches Preisauffüllen. | VERBINDLICH |
| BTK-BKT-007 | Jeder Run erzeugt Manifest, Datenqualitätsbericht und vollständige Trade-Liste. | VERBINDLICH |
| BTK-BKT-008 | Indicator-only, Bastian-only soweit fachlich reproduzierbar und Fusionsmodell werden getrennt ausgewiesen. | NACHWEIS AUSSTEHEND |
| BTK-BKT-009 | Bastian-Source-Replay muss Published-/Received-/Spoken-Time, Revisionen, Sessionstatus und Freshness chronologisch respektieren. | NACHWEIS AUSSTEHEND |
| BTK-BKT-010 | Der spätere Botvergleich verwendet denselben Daten-Snapshot, dieselben Märkte, Kosten, Kapitalregeln und denselben Forward-Paper-Zeitraum. | VERBINDLICH |
| BTK-BKT-011 | Vergleichsmetriken enthalten mindestens Netto-PnL, Netto-PnL/Tag, Drawdown, Profit Factor soweit stabil, Kosten, Kapitalnutzung, technische Ausfälle und Source-/Execution-Latenz. | VERBINDLICH |

## Execution

| ID | Anforderung | Status |
|---|---|---|
| BTK-EXE-001 | Signal, Intent, Börsenorder, Fill und Position bleiben getrennte Zustände. | VERBINDLICH |
| BTK-EXE-002 | Idempotency verhindert Doppelorders. | VERBINDLICH |
| BTK-EXE-003 | Restart beginnt mit Reconciliation gegen Börsenwahrheit. | VERBINDLICH |
| BTK-EXE-004 | Teilfill, Reject, Timeout, Rate-Limit und Netzwerkfehler werden explizit behandelt. | VERBINDLICH |
| BTK-EXE-005 | Marktorder ist V1-Baseline, sofern DMS 03 nichts anderes zwingend verlangt. | ANNAHME |
| BTK-EXE-006 | Nach 10 s unklarem Submit -> `UNKNOWN`, nicht blind erneut senden. | VERBINDLICH |
| BTK-EXE-007 | Ein Bastian-Source-Ereignis kann erst nach vollständiger Source-/Fusion-/Risk-/Capital-Prüfung ein `EXECUTION_INTENT` erzeugen. | VERBINDLICH |

## Betrieb und Freigabe

| ID | Anforderung | Status |
|---|---|---|
| BTK-OPS-001 | 24/7-Paper ist Pflicht vor Live. | VERBINDLICH |
| BTK-OPS-002 | Paper-Soak mindestens 30 Kalendertage. Die zusätzlich erforderliche Mindestzahl geschlossener Strategiebars je Symbol wird beim Strategie-Freeze aus dem tatsächlich verwendeten BTK-Timeframe abgeleitet. Liegen nach 30 Tagen weniger als 20 abgeschlossene Trades vor, läuft der Soak bis 20 Trades weiter, maximal 90 Tage. | VERBINDLICH |
| BTK-OPS-003 | P1/P2-Alerts gehen an Telegram; Ausfall kritischer Alarmierung pausiert neue Live-Entries. | VERBINDLICH |
| BTK-OPS-004 | Backup/Restore, Not-Aus, Daten- und Source-Health müssen vor Live getestet sein. | VERBINDLICH |
| BTK-OPS-005 | Live wird niemals allein durch einen positiven Backtest aktiviert. | VERBINDLICH |
| BTK-OPS-006 | 24/7-Betrieb überwacht unabhängig voneinander Marktfeed, Indicator Engine, Source Discovery, Source Capture, Parser/Validator, Conditional Watcher, Fusion, Execution und Alarmierung. | VERBINDLICH |

## UI

UI zeigt mindestens Modus, Health, Datenfrische, Source-Health je Quelle, Sessionstatus, Capture-/Parserstatus, aktuelle Bastian-Kontexte, Pending Conditions, Freshness/Expiry, Indikatorversion, offene Positionen, Equity/PnL, blockierte Signale und Chartbereiche Heute/1W/1M/1J/3J.
