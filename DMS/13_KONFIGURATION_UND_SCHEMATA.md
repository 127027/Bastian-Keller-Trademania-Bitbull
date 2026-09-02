# 13 – Konfiguration und Schemata

## Grundsätze

- Schema validiert und versioniert;
- unbekannte Felder sind Fehler;
- Einheiten im Feldnamen oder Schema eindeutig;
- Secrets nur als Referenz auf Secret-Store;
- Strategie-, Config-, Daten- und Quellenhashes in Runs/Entscheidungen;
- DMS 03 ist für strategiespezifische Werte maßgeblich.

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

bastian_sources:
  primary_speaker: Bastian Keller
  youtube_live: OFFEN
  youtube_updates: OFFEN
  telegram: OFFEN
  trademania_member_content: OFFEN
  other_mentors_allowed: false
  freshness_policy: OFFEN
  conflict_policy: OFFEN

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
  paper_soak_min_closed_bars_per_symbol: 720
  paper_soak_min_completed_trades: 20
  paper_soak_max_days_if_trade_count_low: 90
  telegram_p1_p2_required: true

ui:
  language: de
  ranges: [today, 1w, 1m, 1y, 3y]
```

## Signal-/Decision-Snapshot

Jeder Strategy-Snapshot enthält mindestens:

- strategy version/hash;
- config hash;
- symbol/timeframe/bar time;
- indicator reference/state;
- source-event IDs;
- Bastian classification/freshness;
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
- Kostenmodell;
- Kapitalmodell;
- erzeugte Artefakte;
- Validierungsstatus.

## Validierung

Konfiguration ist ungültig, wenn beispielsweise `LIVE` ohne Live-Freigabe gesetzt wird, Slotnotional × Slots den Cashpool unzulässig überschreitet, eine nicht eingefrorene Strategie signalaktiv geschaltet wird oder Bastian-Source-Trading ohne Freshness-/Konfliktregel aktiviert werden soll.