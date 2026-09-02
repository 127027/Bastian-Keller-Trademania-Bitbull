# 09 – Systemarchitektur und Datenmodell

## Architekturprinzipien

- Strategy-/Source-Domain unabhängig von Börse, UI und Storage;
- derselbe Signal-/Decision-Core für Backtest, Replay, Paper und Live;
- Adapter für Markt-, Indicator-Data-, Content- und Execution-Quellen;
- persistent, auditierbar, idempotent;
- UTC und Decimal für Geld/Preise;
- keine zweite Execution-Engine nur für Bastian-Inhalte;
- Roh-Capture, Parser-Ergebnis, validierter Kontext und handelbare Entscheidung bleiben getrennte Zustände;
- Kandidateninventar und Zielstack-Auswahl sind versionierte Konfiguration/Evidence, keine versteckte Codeentscheidung.

## Systeme

### Backtest/Replay-Labor

Reproduziert Indikatorsignale, Indicator-Data-Source-Mappings, gelabelte Bastian-Ereignisse, Sessionstatus, Revisionen, Pending Conditions, Fusionsregeln, Kosten und Portfolioentscheidungen deterministisch.

### 24/7 Paper/Live

Verarbeitet Marktfeed, indikatorrelevante Datenprovider und freigegebene Content-Quellen kontinuierlich, erkennt Sessions/Updates, misst Source-Latenzen, führt Reconciliation durch und erzeugt Orders nur nach allen Gates.

## Komponenten

- Config Loader/Validator
- **Candidate Inventory / Target Stack Registry**
- Market Data Adapter
- **Indicator Data Source Adapter/Router** für Preis, Volumen, Cross-Exchange-Override, Session-/Footprint-/POC-Zusatzdaten
- **Indicator Data Source Health/Mapping Validator**
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

Ebenso wird keine Footprint-/POC-Engine nur deshalb neu gebaut, weil ein Kandidat solche Werte anzeigt. Zuerst wird geprüft, ob der finale Zielstack diese Information signalrelevant benötigt und ob sie rechtmäßig/exakt verfügbar ist. Nicht exakt rekonstruierbare Werte bleiben `BLACK_BOX_EXTERNAL` oder werden aus dem signalrelevanten V1-Pfad ausgeschlossen.

## Kernobjekte

### Kandidat/Zielstack

`indicator_candidate`, `candidate_evidence`, `target_stack_version`, `indicator_data_source_mapping`.

### Markt/Indikator

`candle`, `indicator_source_sample`, `indicator_value`, `market_signal`, `market_condition_state`, `indicator_health`.

### Bastian/Content

`source_session`, `source_event`, `content_fragment_ref`, `capture_result`, `bastian_statement`, `bastian_context`, `pending_condition`, `actionable_signal`, `source_health`.

### Entscheidung/Execution

`strategy_decision`, `order_intent`, `exchange_order`, `fill`, `ledger_entry`, `position_snapshot`.

### Nachweise

`backtest_run`, `replay_run`, `data_quality_report`, `indicator_parity_report`, `source_evidence`, `latency_sample`, `audit_event`.

## Mindestfelder `indicator_candidate`

- Candidate-ID;
- Name/Publisher/Version;
- Evidence-Referenzen;
- Public/Member-Origin;
- Märkte/Timeframes;
- aktuelle Bastian-Nutzung;
- Repainting-/Automation-/Rechte-Status;
- Auswahlstatus;
- Auswahl-/Ablehnungsgrund.

## Mindestfelder `indicator_data_source_mapping`

- Target-Stack-Version;
- Funktion/Komponente;
- Provider;
- Symbolmapping;
- Marktart;
- Timeframe/Aggregation;
- Volume-Override soweit vorhanden;
- Sessiontimezone/DST;
- Footprint-/POC-Provider/Auflösung soweit vorhanden;
- Black-Box-Status;
- Evidence-/Config-Hash.

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
- Target-Stack-/Strategieversion;
- Indicator-Referenz;
- Indicator-Data-Source-Mapping-Referenz;
- Bastian-Kontext-/Actionable-/Condition-Referenz;
- Fusionsregelversion;
- Source-/Capture-/Parser-/End-to-End-Latenz;
- Risk-/Capital-Ergebnis;
- finale Aktion/Blockgrund.

## Zustandsgrenzen

`indicator_candidate` ist keine Strategie. `capture_result` ist keine Handelsentscheidung. `bastian_statement` ist keine Handelsentscheidung. `bastian_context` ist keine Handelsentscheidung. Erst der eingefrorene Zielstack plus ein validiertes `actionable_signal` oder eine erfüllte `pending_condition` darf nach DMS 03 in die Strategy/Fusion Engine gelangen. Erst danach kann ein `order_intent` entstehen.

## Persistenzwahrheit

Börse ist Ausführungswahrheit für Orders/Fills/Salden. Der eingefrorene Indicator-Provider/Source-Mapping ist Datenwahrheit für die jeweilige Indikatorfunktion. Externe Content-Plattform ist Quellenwahrheit für Published-/Live-Metadaten. Lokale Datenbank speichert den auditierbaren Botzustand, darf aber externe Wahrheit nach Restart nicht ungeprüft überschreiben.
