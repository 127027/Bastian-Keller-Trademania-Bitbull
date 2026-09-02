# 09 – Systemarchitektur und Datenmodell

## Architekturprinzipien

- Strategy-/Source-Domain unabhängig von Börse, UI und Storage;
- derselbe Signal-/Decision-Core für Backtest, Replay, Paper und Live;
- Adapter für Markt-, Content- und Execution-Quellen;
- persistent, auditierbar, idempotent;
- UTC und Decimal für Geld/Preise;
- keine zweite Engine nur für Bastian-Inhalte.

## Systeme

### Backtest/Replay-Labor

Reproduziert Indikatorsignale, gelabelte Bastian-Ereignisse, Fusionsregeln, Kosten und Portfolioentscheidungen deterministisch.

### 24/7 Paper/Live

Verarbeitet Marktfeed und freigegebene Content-Quellen kontinuierlich, führt Reconciliation durch und erzeugt Orders nur nach allen Gates.

## Komponenten

- Config Loader/Validator
- Market Data Adapter
- Content Source Adapter
- Data/Source Quality
- Indicator Engine
- Bastian Event Parser/Validator
- Strategy/Fusion Engine
- Risk Guard
- Execution Adapter
- Portfolio Ledger
- Backtest/Replay Engine
- Scheduler
- API
- UI
- Observability/Alerts

## Referenzstack

- Python 3 für Service, Domain, Backtest und Adapter;
- SQLite/WAL als lokale Startdatenbank, solange Last/Concurrency ausreichend;
- lokale Web-API;
- TypeScript-UI;
- YAML/JSON-Konfiguration;
- Windows-Service für 24/7-Betrieb.

## Kernobjekte

### Markt

`candle`, `indicator_value`, `market_signal`.

### Bastian/Content

`source_event`, `content_fragment_ref`, `bastian_statement`, `bastian_context`, `actionable_signal`, `source_health`.

### Entscheidung/Execution

`strategy_decision`, `order_intent`, `exchange_order`, `fill`, `ledger_entry`, `position_snapshot`.

### Nachweise

`backtest_run`, `replay_run`, `data_quality_report`, `source_evidence`, `audit_event`.

## Mindestfelder `source_event`

- immutable ID;
- Origin;
- URL/private reference;
- Published-/Received-Time UTC;
- Live/Replay;
- Speaker;
- Assetbezug;
- Content-Hash;
- Parser-/Validation-Version;
- Status.

## Mindestfelder `strategy_decision`

- Decision-ID;
- Symbol;
- Event-/Barzeit;
- Strategieversion;
- Indicator-Referenz;
- Bastian-Kontext-/Actionable-Referenz;
- Fusionsregelversion;
- Risk-/Capital-Ergebnis;
- finale Aktion/Blockgrund.

## Persistenzwahrheit

Börse ist Ausführungswahrheit für Orders/Fills/Salden. Externe Content-Plattform ist Quellenwahrheit für Published-/Live-Metadaten. Lokale Datenbank speichert den auditierbaren Botzustand, darf aber externe Wahrheit nach Restart nicht ungeprüft überschreiben.