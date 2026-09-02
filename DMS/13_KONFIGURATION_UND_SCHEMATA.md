# 13 – Konfiguration und Schemata

## Grundsätze

- Schema validiert und versioniert;
- unbekannte Felder sind Fehler;
- Einheiten im Feldnamen oder Schema eindeutig;
- Secrets nur als Referenz auf Secret-Store;
- Strategie-, Config-, Daten- und Quellenhashes in Runs/Entscheidungen;
- DMS 03 ist für strategiespezifische Werte maßgeblich;
- keine signalaktive Source-Konfiguration mit `OFFEN`-Pflichtfeldern.

## Baseline-Konfiguration

```yaml
project:
  id: btk
  repository: 127027/Bastian-Keller-Trademania-Bitbull

environment: paper

exchange:
  venue: binance_spot
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

strategy:
  id: btk_indicator
  version: UNFROZEN
  indicator_name: OFFEN
  indicator_version: OFFEN
  timeframe: OFFEN
  fusion_model: OFFEN
  trade_on_open_bar: false
  slot_priority: OFFEN

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
  conditional_watcher_enabled: false  # erst nach Strategie-Freeze
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
  paper_soak_reference_bars_if_1h: 720
  paper_soak_min_completed_trades: 20
  paper_soak_max_days_if_trade_count_low: 90
  telegram_p1_p2_required: true

ui:
  language: de
  ranges: [today, 1w, 1m, 1y, 3y]
```

`paper_soak_reference_bars_if_1h: 720` ist ausschließlich eine Rechenreferenz für einen möglichen 1h-Timeframe. Der verbindliche Wert wird erst beim Strategie-Freeze aus dem tatsächlich verwendeten BTK-Timeframe abgeleitet.

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
- config hash;
- symbol/timeframe/bar time;
- indicator reference/state;
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
- Config hash;
- Datenhash/Zeitraum;
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
- Bastian-Source-Trading ohne Freshness-/Konflikt-/Revisionsregel aktiviert werden soll;
- eine signalaktive Quelle keine Allowlist-ID oder keinen dokumentierten Capture-Pfad besitzt;
- `raw_transcript_is_actionable=true` gesetzt würde;
- Conditional-Watcher aktiv ist, obwohl Trigger-/Expiry-/Invalidation-Regeln noch offen sind;
- eine erforderliche Latenzgrenze noch `OFFEN` ist;
- `paper_soak_min_closed_bars_per_symbol` vor Strategie-Freeze willkürlich auf einen fremden Timeframe festgesetzt wird.
