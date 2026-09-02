# 09 – Systemarchitektur und Datenmodell

## Architekturprinzipien

- Strategy-/Source-Domain unabhängig von Börse, UI und Storage;
- derselbe Signal-/Decision-Core für Backtest, Replay, Paper und Live;
- Adapter für Markt-, Content- und Execution-Quellen;
- persistent, auditierbar, idempotent;
- UTC und Decimal für Geld/Preise;
- keine zweite Execution-Engine nur für Bastian-Inhalte;
- Roh-Capture, Parser-Ergebnis, validierter Kontext und handelbare Entscheidung bleiben getrennte Zustände.

## Systeme

### Backtest/Replay-Labor

Reproduziert Indikatorsignale, gelabelte Bastian-Ereignisse, Sessionstatus, Revisionen, Pending Conditions, Fusionsregeln, Kosten und Portfolioentscheidungen deterministisch.

### 24/7 Paper/Live

Verarbeitet Marktfeed und freigegebene Content-Quellen kontinuierlich, erkennt Sessions/Updates, misst Source-Latenzen, führt Reconciliation durch und erzeugt Orders nur nach allen Gates.

## Komponenten

- Config Loader/Validator
- Market Data Adapter
- **Source Discovery / Session Watcher**
- **Content Capture Adapter** je freigegebener Quelle
- **Transcript/Caption/STT Adapter** nur soweit technisch/rechtlich erforderlich und freigegeben
- **Source Normalizer** für Zeit, Sprecher, Sessionstatus und Origin
- **Bastian Event Parser** für Asset/Aussage/Aktion/Bedingung/Horizont
- **Bastian Event Validator** für Pflichtfelder, Unsicherheit, Freshness, Konflikte und Revisionen
- **Context Store** für aktuell gültige Bastian-Kontexte
- **Conditional Watcher** für `PENDING_CONDITION`
- Data/Source Quality
- Indicator Engine
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

Die konkrete Transkript-/Sprachtechnik wird **nicht vorab festgelegt**. Erst nach Prüfung der tatsächlich verfügbaren TradeMania-/YouTube-/Telegram-/Member-Quellen wird entschieden, ob offizielle Untertitel, Transkript/API, lokales Speech-to-Text oder ein anderer zulässiger Adapter erforderlich ist.

## Kernobjekte

### Markt

`candle`, `indicator_value`, `market_signal`, `market_condition_state`.

### Bastian/Content

`source_session`, `source_event`, `content_fragment_ref`, `capture_result`, `bastian_statement`, `bastian_context`, `pending_condition`, `actionable_signal`, `source_health`.

### Entscheidung/Execution

`strategy_decision`, `order_intent`, `exchange_order`, `fill`, `ledger_entry`, `position_snapshot`.

### Nachweise

`backtest_run`, `replay_run`, `data_quality_report`, `source_evidence`, `latency_sample`, `audit_event`.

## Mindestfelder `source_session`

- Session-ID;
- Origin/Channel-ID;
- URL/private reference;
- Status `SCHEDULED|LIVE|ENDED|REPLAY|STALE|UNAVAILABLE|UNKNOWN`;
- announced/start/end/observed timestamps UTC;
- allowlist version;
- capture mode/version;
- source health.

## Mindestfelder `source_event`

- immutable Event-ID;
- Session-ID;
- Origin;
- URL/private reference;
- Published-/Received-/Spoken-Time UTC;
- Live/Replay;
- Speaker;
- Assetbezug;
- Statement class;
- Content-Hash/private reference;
- Capture-/Parser-/Validation-Version;
- Capture-/Parser-Confidence;
- Freshness deadline;
- Supersedes-/Conflict-Referenz;
- Status.

## Mindestfelder `pending_condition`

- Condition-ID;
- Source-Event-ID;
- Symbol;
- Operator/Schwelle/Zone/Timeframe soweit definiert;
- Aktion bei Erfüllung;
- Created-/Expiry-Time;
- Invalidation;
- aktueller Zustand `PENDING|MET|INVALIDATED|EXPIRED`;
- letzte Marktprüfung.

## Mindestfelder `strategy_decision`

- Decision-ID;
- Symbol;
- Event-/Barzeit;
- Strategieversion;
- Indicator-Referenz;
- Bastian-Kontext-/Actionable-/Condition-Referenz;
- Fusionsregelversion;
- Source-/Capture-/Parser-/End-to-End-Latenz;
- Risk-/Capital-Ergebnis;
- finale Aktion/Blockgrund.

## Zustandsgrenzen

`capture_result` ist keine Handelsentscheidung. `bastian_statement` ist keine Handelsentscheidung. `bastian_context` ist keine Handelsentscheidung. Erst ein validiertes `actionable_signal` oder eine erfüllte `pending_condition` darf in die Strategy/Fusion Engine gelangen. Erst danach kann ein `order_intent` entstehen.

## Persistenzwahrheit

Börse ist Ausführungswahrheit für Orders/Fills/Salden. Externe Content-Plattform ist Quellenwahrheit für Published-/Live-Metadaten. Lokale Datenbank speichert den auditierbaren Botzustand, darf aber externe Wahrheit nach Restart nicht ungeprüft überschreiben.
