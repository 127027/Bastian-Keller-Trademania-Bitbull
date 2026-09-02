# 08 – UI/UX-Spezifikation

## Grundsätze

- deutsche Oberfläche;
- Modus und System-/Source-Health jederzeit sichtbar;
- keine Gewinnversprechen;
- keine versteckte Strategieänderung über UI;
- pro Order nachvollziehbare Quelle und Entscheidungskette;
- Roh-Capture/Parser/Context/Actionable/Intent klar getrennt darstellen.

## Navigation

1. Übersicht
2. Chart
3. Positionen/Orders
4. Bastian/Quellen
5. Pending Conditions
6. Backtests/Replays/Vergleich
7. Datenqualität
8. System/Logs
9. Einstellungen
10. Dokumentation

## Dashboard

Pro Coin mindestens:

- Kurs;
- aktueller Indikatorzustand;
- letzter gültiger Bastian-Kontext;
- offene Pending Condition soweit vorhanden;
- Position;
- unrealisiertes PnL;
- letzter Signal-/Orderzeitpunkt;
- Health.

Global:

- Modus;
- Equity/Cash/belegte Slots;
- Tages-PnL/Drawdown;
- Market Data Health;
- Indicator Health;
- Source Discovery/Capture/Parser Health;
- aktuelle Bastian-Session(s);
- Source-/E2E-Latenz;
- Not-Aus.

## Chart

Zeiträume:

- Heute
- 1 Woche
- 1 Monat
- 1 Jahr
- 3 Jahre

Darstellung nach DMS 03:

- Candles;
- Originalindikator-Overlays/Marker soweit reproduzierbar;
- Bastian-Ereignismarker getrennt von Indikatorsignalen;
- Pending-Condition-Zone/Trigger/Expiry soweit sinnvoll;
- Order-/Fillmarker;
- Position und Entry;
- provisorische Bars sichtbar markieren.

Strategiefremde Overlays werden nicht angezeigt.

## Bastian-/Source-Ansicht

Zeigt ausschließlich auditierbare Metadaten und eigene abgeleitete Zusammenfassungen:

- Source/Origin und allowgelistete Source-ID;
- Session-ID/Status `SCHEDULED|LIVE|ENDED|REPLAY|STALE|UNAVAILABLE|UNKNOWN`;
- Published-/Received-/Spoken-Time;
- Sprecher;
- Asset;
- Klassifikation (`CONTEXT`, `WATCH`, `ENTRY`, `EXIT`, `REDUCE`, `INVALIDATION`, `TARGET`, `RISK`, `UNKNOWN`);
- Bedingung und Condition-State;
- Freshness/Expiry;
- Capture-/Parser-/Validationstatus;
- Capture-/Parser-/End-to-End-Latenz;
- Supersede-/Konfliktreferenz;
- daraus entstandene oder blockierte Aktion und Blockgrund.

Geschützte Volltranskripte/Medien gehören nicht in die öffentliche UI, sofern Rechte das nicht erlauben.

## Pending-Conditions-Ansicht

Pro Condition:

- Ursprungsevent;
- Asset;
- Bedingung/Operator/Zone;
- Aktion bei Erfüllung;
- aktueller Zustand `PENDING|MET|INVALIDATED|EXPIRED`;
- Freshness/Expiry;
- letzte Marktprüfung;
- aktuelle Konflikt-/Revisionslage;
- Grund, falls blockiert.

Der Nutzer darf eine Pending Condition sehen, aber nicht über die UI still ihre Strategieparameter verändern.

## Backtest-/Replay-/Vergleichs-UI

Start-/Ansichtsmodi:

- alle 10 Coins ×250 USDT;
- einzelner Coin ×250 USDT;
- optional 240/3×80 Portfolio-Spiegel;
- Indicator-Parity;
- Bastian-Source-Replay;
- Fusions-Replay;
- fairer Referenzbot-Vergleich.

Vor Start zeigt die UI Strategieversion, Config, Datenzeitraum, Kostenmodell und Source-/Golden-Version.

Beim Vergleich sind Daten-/Kosten-/Kapital-/Paper-Basis und Abweichungen sichtbar. Pflichtmetriken mindestens Netto-PnL, Netto-PnL/Tag, Drawdown, Profit Factor soweit stabil, Kosten, Kapitalnutzung, technische Ausfälle und Latenz.

## Einstellungen

Strategierelevante Werte sind nach Freeze versioniert. Änderungen invalidieren abhängige Backtests/Replays. Live-relevante Änderungen benötigen bewusste Bestätigung und Audit.

Source-Allowlist, Capture-Modus, Freshness, Konflikt-/Revisionsregel und Latenzgrenzen dürfen nicht still außerhalb der DMS/Config-Version geändert werden.

## Bedienungssicherheit

`LIVE` darf optisch nicht mit `PAPER` verwechselbar sein. Not-Aus, Source-Ausfall, Capture-/Parserfehler, Datenlücke, Reconciliation-Fehler, abgelaufene Kontexte und globale Halt-Zustände müssen prominent sichtbar sein.
