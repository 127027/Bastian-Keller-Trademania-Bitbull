# 12 – Tests und Abnahmekriterien

## Testebenen

1. Unit-Tests
2. Kandidateninventar-/Auswahlreview
3. Indicator-Parity/Golden-/Black-Box-Tests
4. Indicator-Data-Source-Parity-Tests
5. Source-Discovery-/Session-Tests
6. Capture-/Transcript-/Parser-/Classification-Tests
7. Strategy-/Fusion-/Conditional-Watcher-Tests
8. Backtest-/Source-Replay-Tests
9. Execution-/Failure-Tests
10. Integration-/Restart-/Recovery-Tests
11. Paper-Soak/Abnahme
12. fairer Referenzbot-Vergleich

## Kandidateninventar-/Auswahltests

Vor Freeze muss nachgewiesen sein:

- öffentlich verfügbare TradeMania-/Bitbull-Indikatoren wurden inventarisiert;
- rechtmäßig sichtbare Member-Kandidaten aus Indicator Masterclass, Strategie-Indikator Masterclass, Discord und `trademania.app/bots` wurden geprüft;
- PVSRA wurde nicht allein wegen seiner öffentlichen Verfügbarkeit automatisch ausgewählt;
- pro ernsthaftem Kandidaten sind aktuelle Bastian-Nutzung, ETH-Eignung, Determinismus, Repainting, Automation/Alerts, Datenbedarf, Rechte und Backtestbarkeit bewertet;
- zusätzliche MACD-/POC-/RSI-Komponenten werden nur übernommen, wenn sie gegenüber dem Zielstack einen belegten, nicht redundanten Nutzen haben;
- die finale Auswahl ist vor Performanceoptimierung dokumentiert und versioniert.

## Kritische Strategietests

- Originalindikatorzustand entspricht Botzustand bzw. dokumentierter Black-Box-Referenz;
- Bar-Close/Intrabar/Repaint-Verhalten stimmt;
- Entry/Exit/Context/Reentry/Pyramiding entspricht DMS 03;
- simultane Signale werden deterministisch behandelt;
- keine historische Marker-/Level-Verschiebung wird als frühere Information benutzt.

## Indicator-Data-Source-Parity

Für jeden signalrelevanten Indikatorbestandteil muss geprüft werden:

- Preis-/Chartprovider entspricht der eingefrorenen Konfiguration;
- Volumenprovider entspricht der eingefrorenen Konfiguration;
- ein Cross-Exchange-/PVSRA-Volume-Override wird in Golden-Test, Backtest, Paper und Live identisch abgebildet;
- Spot-/Perpetual-/Futures-Daten werden nicht still verwechselt;
- Session-Zeitzone und DST stimmen;
- benötigte Footprint-/POC-Auflösung und Provider sind reproduzierbar oder ausdrücklich `BLACK_BOX_EXTERNAL`;
- ein nicht exakt rekonstruierbarer POC-/Footprint-Wert wird nicht durch OHLCV-Näherung als exakt ausgegeben;
- Provider-/Mappingwechsel invalidiert betroffene Golden-Artefakte und Backtests.

Für `Trademania - PVSRA Indicator` ist dieser Testblock zwingend, falls er Zielstack wird, weil die öffentliche Beschreibung einen separaten Volumen-Override und POC-/Footprint-Funktionen vorsieht.

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
- gleicher Run mit gleichen Hashes und identischem Indicator-Source-Mapping liefert identisches Ergebnis;
- 10×250, Einzeltest und optional 240/3×80 funktionieren;
- Source-Replay respektiert Published-/Received-/Spoken-Time, Sessionstatus, Revisionen und Expiry;
- Kandidaten-/Zielstack-Auswahl wird nicht nachträglich anhand des Testfensters umgeschrieben;
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
- finaler Indikator/Stack und Version sichtbar;
- signalrelevante Indicator-Provider/Overrides diagnostizierbar;
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

Der Vergleich ist nur gültig, wenn beide Systeme denselben Zeitraum und – soweit fachlich möglich – dieselben Marktdaten, Gebühren-/Slippageannahmen, Kapitalregeln und Paper-Zeiträume verwenden. Während des Vergleichs werden keine Parameter oder der Zielstack aufgrund des Zwischenstands nachoptimiert.

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

- Kandidateninventar ausreichend vollständig;
- finaler Zielindikator/minimaler Stack begründet ausgewählt;
- keine kritische Strategiefrage offen;
- Originalindikator/Settings/Referenzen vorhanden;
- Preis-/Volumen-/Session-/POC-/Zusatzdaten-Mapping eingefroren;
- Bastian-Quellen, Capture-Pfade, Sessionstatus, Freshness, Revisionen und Fusionsmodell eingefroren;
- Conditional-Watcher-Regeln und Latenzgrenzen definiert;
- Traceability vollständig.

### Gate B – Backtest/Replay

- Indicator-Parität bestanden;
- Indicator-Data-Source-Parität bestanden bzw. unvermeidbare Black-Box-Anteile ausdrücklich markiert;
- Bastian-Source-Replay bestanden;
- Datenqualität grün;
- Kostenmodell korrekt;
- alle Pflichtläufe reproduzierbar.

### Gate C – Paper Ready

- Execution-/Recoverytests bestanden;
- Source-/Market-/Indicator-/Capture-/Parser-Health funktioniert;
- Secrets/Alerts/Backups eingerichtet;
- keine kritische Source-Unsicherheit ohne `NO_TRADE`-Fallback.

### Gate D – Live Ready

- Paper-Soak bestanden;
- Restore getestet;
- Livekonto Least Privilege;
- Betreiberfreigabe bewusst erfolgt.

`BTK-DMS PREPARED` bedeutet nur: die Dokumentstruktur ist implementierbar vorbereitet. Es bedeutet nicht, dass Bot, Backtest, Paper oder Live bereits freigegeben sind.
