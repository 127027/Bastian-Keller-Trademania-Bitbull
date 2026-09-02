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
| BTK-SRC-005 | Content-Ereignisse speichern Origin, Published-/Received-Time, Sprecher, Live/Replay, Hash und Parsingstatus. | VERBINDLICH |

## Backtest

| ID | Anforderung | Status |
|---|---|---|
| BTK-BKT-001 | Primärbericht: drei vollständige Jahre je Paar plus Warm-up. | VERBINDLICH |
| BTK-BKT-002 | Standard-Batch: 10 isolierte Coin-Tests mit je 250 USDT. | VERBINDLICH |
| BTK-BKT-003 | Einzelmodus: frei wählbares Paar mit 250 USDT. | VERBINDLICH |
| BTK-BKT-004 | Optionaler Portfolio-Spiegel: 240 USDT, 3×80 Slots. | VERBINDLICH |
| BTK-BKT-005 | Kostenbaseline je Seite: 10 bp Fee + 2 bp Spread + 3 bp Slippage; Stress: 10+10+20. | VERBINDLICH |
| BTK-BKT-006 | Kein Look-ahead, Survivorship-Bias oder synthetisches Preisauffüllen. | VERBINDLICH |
| BTK-BKT-007 | Jeder Run erzeugt Manifest, Datenqualitätsbericht und vollständige Trade-Liste. | VERBINDLICH |
| BTK-BKT-008 | Indicator-only, Bastian-only soweit sinnvoll und Fusionsmodell werden getrennt ausgewiesen. | NACHWEIS AUSSTEHEND |

## Execution

| ID | Anforderung | Status |
|---|---|---|
| BTK-EXE-001 | Signal, Intent, Börsenorder, Fill und Position bleiben getrennte Zustände. | VERBINDLICH |
| BTK-EXE-002 | Idempotency verhindert Doppelorders. | VERBINDLICH |
| BTK-EXE-003 | Restart beginnt mit Reconciliation gegen Börsenwahrheit. | VERBINDLICH |
| BTK-EXE-004 | Teilfill, Reject, Timeout, Rate-Limit und Netzwerkfehler werden explizit behandelt. | VERBINDLICH |
| BTK-EXE-005 | Marktorder ist V1-Baseline, sofern DMS 03 nichts anderes zwingend verlangt. | ANNAHME |
| BTK-EXE-006 | Nach 10 s unklarem Submit -> `UNKNOWN`, nicht blind erneut senden. | VERBINDLICH |

## Betrieb und Freigabe

| ID | Anforderung | Status |
|---|---|---|
| BTK-OPS-001 | 24/7-Paper ist Pflicht vor Live. | VERBINDLICH |
| BTK-OPS-002 | Paper-Soak mindestens 30 Tage/720 geschlossene Strategiebars je Symbol; bei <20 abgeschlossenen Trades bis 20 Trades, maximal 90 Tage. | VERBINDLICH |
| BTK-OPS-003 | P1/P2-Alerts gehen an Telegram; Ausfall kritischer Alarmierung pausiert neue Live-Entries. | VERBINDLICH |
| BTK-OPS-004 | Backup/Restore, Not-Aus, Daten- und Source-Health müssen vor Live getestet sein. | VERBINDLICH |
| BTK-OPS-005 | Live wird niemals allein durch einen positiven Backtest aktiviert. | VERBINDLICH |

## UI

UI zeigt mindestens Modus, Health, Datenfrische, Source-Health, aktuelle Bastian-Kontexte, Indikatorversion, offene Positionen, Equity/PnL, blockierte Signale und Chartbereiche Heute/1W/1M/1J/3J.