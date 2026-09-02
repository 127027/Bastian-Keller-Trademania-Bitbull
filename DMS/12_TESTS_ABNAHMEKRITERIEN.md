# 12 – Tests und Abnahmekriterien

## Testebenen

1. Unit-Tests
2. Indicator-Parity/Golden-Tests
3. Source-Discovery-/Session-Tests
4. Capture-/Transcript-/Parser-/Classification-Tests
5. Strategy-/Fusion-/Conditional-Watcher-Tests
6. Backtest-/Source-Replay-Tests
7. Execution-/Failure-Tests
8. Integration-/Restart-/Recovery-Tests
9. Paper-Soak/Abnahme
10. fairer Referenzbot-Vergleich

## Kritische Strategietests

- Originalindikatorzustand entspricht Botzustand;
- Bar-Close/Intrabar/Repaint-Verhalten stimmt;
- Entry/Exit/Reentry/Pyramiding entspricht DMS 03;
- simultane Signale werden deterministisch behandelt;
- keine historische Marker-Verschiebung wird als frühere Information benutzt.

## Kritische Source-/Session-Tests

- nur allowgelistete offizielle Quellen werden verarbeitet;
- angekündigt/live/beendet/replay/stale/unavailable werden korrekt unterschieden;
- dynamisch geänderter Livetermin wird erkannt, ohne dauerhaft hart codierten Kalender;
- Replay oder verspätetes Update wird nicht als aktueller Livestream behandelt;
- Source-Abbruch und Reconnect erzeugen keine doppelten Events;
- Streamende verlängert Kontext oder Pending Conditions nicht still.

## Kritische Bastian-/Parser-Tests

- Bastian als Sprecher korrekt erkannt;
- Zuschauerfragen/andere Mentoren werden nicht als Bastian-Signal gehandelt;
- historische Beschreibungen werden nicht als aktuelle Entries klassifiziert;
- Asset, Richtung/Aktion, Preis/Zone, Bedingung und Horizont werden gemäß DMS 03 strukturiert;
- unvollständiges/falsches Transkript führt bei kritischer Unsicherheit zu `NO_TRADE`;
- ein Confidence-Wert allein erzeugt keine Order;
- konditionale Aussagen erzeugen `PENDING_CONDITION` und warten auf ihre Bedingung;
- Freshness läuft deterministisch ab;
- spätere Revision invalidiert/ersetzt älteren Kontext nach eingefrorener Regel;
- mehrere Assets im selben Live bleiben sauber getrennt;
- verspäteter Empfang erzeugt keinen rückwirkenden Trade;
- Konflikte zwischen Quellen folgen exakt der eingefrorenen Priorität.

## Conditional-Watcher-Tests

Mindestens:

- Bedingung noch nicht erfüllt -> keine Order;
- Bedingung erfüllt innerhalb Freshness -> regelkonformer Fusions-/Risk-Pfad;
- Bedingung erfüllt nach Expiry -> keine Order;
- neue Bastian-Invalidierung vor Trigger -> Condition invalidiert;
- Marktfeed stale -> Condition darf nicht blind triggern;
- Restart -> Pending Condition wird nur nach Freshness-/State-Reconciliation weitergeführt.

## Daten-/Backtest-/Replaytests

- Lücken/Duplikate/OHLC-Verletzungen werden erkannt;
- keine synthetische Zukunftsinformation;
- Kosten, Tick/Step/MinNotional stimmen;
- gleicher Run mit gleichen Hashes liefert identisches Ergebnis;
- 10×250, Einzeltest und optional 240/3×80 funktionieren;
- Source-Replay respektiert Published-/Received-/Spoken-Time, Sessionstatus, Revisionen und Expiry;
- Manifest und Datenqualitäts-/Source-Evidence-Report vollständig.

## Executiontests

- Idempotency;
- Reject;
- Timeout -> `UNKNOWN` ohne Doppelorder;
- Teilfill;
- Netzwerkabbruch;
- Restart/Reconciliation;
- Preisabweichung >25 bp;
- Tagesverlustpause;
- Drawdown-Halt;
- Not-Aus;
- kein `order_intent` direkt aus Rohtranskript/Parserausgabe ohne Fusion-/Risk-Gates.

## UI-/Betriebstests

- PAPER/LIVE eindeutig sichtbar;
- Markt-, Indicator-, Discovery-, Capture-, Parser- und Execution-Health getrennt;
- Bastian-Ereignisse mit Zeit/Freshness nachvollziehbar;
- Sessionstatus und Pending Conditions sichtbar;
- Source-/Capture-/Parser-/End-to-End-Latenzen nachvollziehbar;
- Today/1W/1M/1J/3J korrekt;
- Backup/Restore getestet;
- Telegram P1/P2 getestet.

## Nichtfunktionale Ziele

- normale UI-/Read-API p95 <= 2 s;
- Verarbeitung finaler Strategiebars für alle zehn Symbole <= 60 s, sofern DMS 03 keine engere Latenz verlangt;
- Source-End-to-End-Latenz: Grenzwert bleibt `OFFEN`, bis reale Capture-Technik und Tradinghorizont bekannt sind; danach verbindlich in DMS 03/13;
- kontrollierter Cancel von Import/Backtest <= 5 s bestätigt;
- 3-Jahres-Chart p95 <= 3 s;
- Betriebslogs standardmäßig <=90 Tage, sofern rechtliche/operative Gründe nichts anderes verlangen.

## Fairer Bot-gegen-Bot-Vergleich

Der Vergleich ist nur gültig, wenn beide Systeme denselben Zeitraum und – soweit fachlich möglich – dieselben Marktdaten, Gebühren-/Slippageannahmen, Kapitalregeln und Paper-Zeiträume verwenden. Während des Vergleichs werden keine Parameter aufgrund des Zwischenstands nachoptimiert.

Pflichtmetriken:

- Netto-PnL und Netto-PnL/Tag;
- Max Drawdown;
- Tradezahl/Exposure;
- Profit Factor soweit statistisch sinnvoll;
- Gebühren/Slippage;
- Kapitalnutzung;
- technische Ausfälle;
- Source-/Execution-Latenz;
- blockierte/verpasste Signale;
- Reproduzierbarkeit.

## Gates

### Gate A – DMS/Strategie

- keine kritische Strategiefrage offen;
- Originalindikator/Settings/Referenzen vorhanden;
- Bastian-Quellen, Capture-Pfade, Sessionstatus, Freshness, Revisionen und Fusionsmodell eingefroren;
- Conditional-Watcher-Regeln und Latenzgrenzen definiert;
- Traceability vollständig.

### Gate B – Backtest/Replay

- Indicator-Parität bestanden;
- Bastian-Source-Replay bestanden;
- Datenqualität grün;
- Kostenmodell korrekt;
- alle Pflichtläufe reproduzierbar.

### Gate C – Paper Ready

- Execution-/Recoverytests bestanden;
- Source-/Market-/Capture-/Parser-Health funktioniert;
- Secrets/Alerts/Backups eingerichtet;
- keine kritische Source-Unsicherheit ohne `NO_TRADE`-Fallback.

### Gate D – Live Ready

- Paper-Soak bestanden;
- Restore getestet;
- Livekonto Least Privilege;
- Betreiberfreigabe bewusst erfolgt.

`BTK-DMS PREPARED` bedeutet nur: die Dokumentstruktur ist implementierbar vorbereitet. Es bedeutet nicht, dass Bot, Backtest, Paper oder Live bereits freigegeben sind.
