# 13 – Konfiguration und Schemata

## Grundsätze

- Schema validiert und versioniert;
- unbekannte Felder sind Fehler;
- Einheiten im Feldnamen oder Schema eindeutig;
- Secrets nur als Referenz auf Secret-Store;
- Strategie-, Config-, Daten- und Quellenhashes in Runs/Entscheidungen;
- DMS 03 ist für strategiespezifische Werte maßgeblich;
- keine signalaktive Source- oder Indicator-Konfiguration mit `OFFEN`-Pflichtfeldern.

## Baseline-Konfiguration

```yaml
project:
  id: btk
  repository: 127027/Bastian-Keller-Trademania-Bitbull

environment: paper

exchange:
  execution_venue: binance_spot
  quote_asset: USDT

markets:
  - BTCUSDT
  - ETHUSDT
  - BNBUSDT
  - SOLUSDT
  - XRPUSDT
  - ADAUSDT
  - LINKUSDT
  - AVAXUSDT
  - DOTUSDT
  - DOGEUSDT

candidate_inventory:
  version: UNFROZEN
  public_inventory_complete: false
  member_inventory_complete: false
  reviewed_sources:
    tradingview_bitbull: true
    trademania_indicator_masterclass: false
    trademania_strategy_indicator_masterclass: false
    trademania_discord: false
    trademania_bots: false
  strongest_public_candidate: trademania_pvsra
  selected_target_stack: OFFEN
  selection_evidence_version: OFFEN

strategy:
  id: btk_indicator
  version: UNFROZEN
  selected_indicator_or_stack: OFFEN
  indicator_version: OFFEN
  timeframe: OFFEN
  fusion_model: OFFEN
  trade_on_open_bar: false
  slot_priority: OFFEN

indicator_data_sources:
  chart_price_provider: OFFEN
  chart_symbol_mapping: OFFEN
  volume_provider: OFFEN
  volume_symbol_mapping: OFFEN
  volume_override_enabled: OFFEN
  volume_override_provider: OFFEN
  volume_override_symbol: OFFEN
  market_type: OFFEN              # spot | perpetual | futures | other
  session_timezone: OFFEN
  session_dst_policy: OFFEN
  footprint_required: OFFEN
  footprint_provider: OFFEN
  footprint_resolution: OFFEN
  poc_mode: OFFEN
  external_black_box_components: []

bastian_sources:
  primary_speaker: Bastian Keller
  other_mentors_allowed: false
  source_allowlist_version: UNFROZEN
  dynamic_schedule_discovery: true
  freshness_policy: OFFEN
  conflict_policy: OFFEN
  revision_policy: OFFEN
  max_end_to_end_latency_ms: OFFEN
  no_trade_on_critical_uncertainty: true

  sources:
    youtube_live:
      enabled: false
      official_channel_id: OFFEN
      capture_mode: OFFEN
      live_detection_mode: OFFEN
    youtube_updates:
      enabled: false
      official_channel_id: OFFEN
      capture_mode: OFFEN
    telegram:
      enabled: false
      official_channel_id: OFFEN
      capture_mode: OFFEN
    trademania_discord:
      enabled: false
      source_id: OFFEN
      capture_mode: OFFEN
    trademania_member_content:
      enabled: false
      source_id: OFFEN
      capture_mode: OFFEN

source_pipeline:
  session_states: [scheduled, live, ended, replay, stale, unavailable, unknown]
  actionable_required_fields:
    - speaker
    - asset
    - action_or_condition
    - freshness
    - source_status
  raw_transcript_is_actionable: false
  parser_confidence_alone_is_actionable: false
  conditional_watcher_enabled: false
  capture_latency_limit_ms: OFFEN
  parser_latency_limit_ms: OFFEN
  source_stale_seconds: OFFEN

capital:
  shared_cash_usdt: 240
  max_slots: 3
  slot_target_usdt: 80
  auto_compounding: false

backtest:
  primary_years: 3
  isolated_start_cash_usdt: 250
  all_ten: true
  optional_portfolio_mirror: true
  fee_bps_per_side: 10
  spread_bps_per_side: 2
  slippage_bps_per_side: 3
  stress_spread_bps_per_side: 10
  stress_slippage_bps_per_side: 20
  source_replay_required: true
  indicator_data_source_parity_required: true
  fair_reference_comparison: true

data:
  daily_audit_utc: "00:05"
  stream_stale_seconds: 90
  final_bar_late_seconds: 120

execution:
  live_enabled: false
  order_type_baseline: market
  pre_submit_price_deviation_bps: 25
  unknown_after_seconds: 10
  partial_review_after_seconds: 30

risk:
  allow_short: false
  allow_margin: false
  allow_futures: false
  max_daily_loss_pct: 5
  max_drawdown_pct: 20

operations:
  paper_soak_min_days: 30
  paper_soak_min_closed_bars_per_symbol: OFFEN_BY_STRATEGY_TIMEFRAME
  paper_soak_min_completed_trades: 20
  paper_soak_max_days_if_trade_count_low: 90
  telegram_p1_p2_required: true

ui:
  language: de
  ranges: [today, 1w, 1m, 1y, 3y]
```

Die verbindliche Mindestzahl geschlossener Strategiebars für den Paper-Soak wird erst beim Strategie-Freeze aus dem tatsächlich verwendeten BTK-Timeframe und der 30-Tage-Mindestdauer abgeleitet.

## Kandidateninventar-Schema

Pro ernsthaftem Indikator-/Bot-Kandidaten mindestens:

- `candidate_id`;
- exakter Name;
- Provider/Publisher;
- Version/Stand;
- öffentliche/member Quelle;
- Zweck/Tradingstil;
- Märkte/Timeframes;
- aktuelle Bastian-Nutzung mit Evidence;
- Settings/Defaults;
- Signale/Levels/Overlays;
- Alerts/Webhooks/Exports;
- Repainting-/Reload-Status;
- benötigte Datenprovider;
- Rechte-/Zugriffsstatus;
- ETH-Eignung;
- Automations-/Backtestbarkeit;
- Redundanz gegenüber anderen Kandidaten;
- Auswahlstatus `REJECTED|RESEARCH|SHORTLIST|SELECTED`;
- Begründung.

## Indicator-Data-Source-Schema

Die spätere Strategie-Konfiguration muss für jede signalrelevante Funktion explizit festlegen, welche Daten sie verwendet. Besonders bei PVSRA darf ein Volume Override nicht implizit bleiben.

Pflichtfelder, soweit relevant:

- Preis-/Chartprovider und Symbol;
- Volumenprovider und Symbol;
- Cross-Exchange-/Volume-Override;
- Spot/Perpetual/Futures-Typ;
- Sessiontimezone/DST;
- Footprint-/POC-Provider;
- Footprint-Auflösung;
- Aggregationsregeln;
- Black-Box-Komponenten;
- Mapping-/Evidence-Hash.

Wenn ein benötigter POC-/Footprint-Wert nicht exakt reproduzierbar ist, muss er als `BLACK_BOX_EXTERNAL`/`NOT_REPRODUCIBLE` markiert oder aus dem signalrelevanten V1-Pfad entfernt werden. Eine OHLCV-Näherung darf nicht als exakt identisch konfiguriert werden.

## Source-Allowlist-Schema

Jede signalrelevante Quelle benötigt mindestens:

- eindeutige Provider-/Channel-/Source-ID;
- URL oder private Referenz;
- Quellenklasse;
- `speaker_scope`;
- zulässige Capture-Methode;
- Live-/Replay-Erkennung;
- Freshness-/Latenzgrenze;
- Rechte-/Zugriffsstatus;
- Aktivierungsstatus;
- Config-/Evidence-Hash.

Eine URL allein reicht nicht zur Allowlist, wenn die Quelle durch Channel-/Account-ID sicherer identifiziert werden kann.

## Signal-/Decision-Snapshot

Jeder Strategy-Snapshot enthält mindestens:

- strategy version/hash;
- selected target stack + inventory version;
- config hash;
- symbol/timeframe/bar time;
- indicator reference/state;
- indicator data-source mapping/version;
- source-session/event IDs;
- Bastian classification/freshness;
- pending-condition state soweit vorhanden;
- capture/parser/validation versions;
- source/capture/parser/end-to-end latency;
- fusion rule version;
- decision/action/block reason.

## Backtest-/Replay-Manifest

Pflichtfelder:

- Run-ID;
- Commit-SHA;
- Strategieversion/hash;
- Kandidateninventar-/Auswahlversion;
- Config hash;
- Datenhash/Zeitraum;
- Indicator-Data-Source-Mapping/Hash;
- Source-Evidence-/Label-Version;
- Session-/Replay-Policy-Version;
- Kostenmodell;
- Kapitalmodell;
- erzeugte Artefakte;
- Validierungsstatus.

## Validierung

Konfiguration ist ungültig, wenn beispielsweise:

- `LIVE` ohne Live-Freigabe gesetzt wird;
- Slotnotional × Slots den Cashpool unzulässig überschreitet;
- eine nicht eingefrorene Strategie signalaktiv geschaltet wird;
- kein finaler Zielstack ausgewählt wurde;
- ein signalrelevanter Indicator-Provider/Override/Footprint-Pfad noch `OFFEN` ist;
- Backtest/Paper/Live unterschiedliche Indicator-Source-Mappings verwenden, ohne dies ausdrücklich als nicht-paritätisch zu markieren;
- Bastian-Source-Trading ohne Freshness-/Konflikt-/Revisionsregel aktiviert werden soll;
- eine signalaktive Quelle keine Allowlist-ID oder keinen dokumentierten Capture-Pfad besitzt;
- `raw_transcript_is_actionable=true` gesetzt würde;
- Conditional-Watcher aktiv ist, obwohl Trigger-/Expiry-/Invalidation-Regeln noch offen sind;
- eine erforderliche Latenzgrenze noch `OFFEN` ist;
- `paper_soak_min_closed_bars_per_symbol` vor Strategie-Freeze willkürlich auf einen fremden Timeframe festgesetzt wird.
