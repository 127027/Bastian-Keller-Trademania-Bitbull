# 12 – Tests und Abnahmekriterien

## Testebenen

1. Unit-Tests
2. Indicator-Parity/Golden-Tests
3. Bastian-Source-Parser-/Classification-Tests
4. Strategy-/Fusion-Tests
5. Backtest-/Replay-Tests
6. Execution-/Failure-Tests
7. Integration-/Restart-/Recovery-Tests
8. Paper-Soak/Abnahme

## Kritische Strategietests

- Originalindikatorzustand entspricht Botzustand;
- Bar-Close/Intrabar/Repaint-Verhalten stimmt;
- Entry/Exit/Reentry/Pyramiding entspricht DMS 03;
- simultane Signale werden deterministisch behandelt;
- keine historische Marker-Verschiebung wird als frühere Information benutzt.

## Kritische Bastian-Tests

- Bastian als Sprecher korrekt erkannt;
- Zuschauerfragen/andere Mentoren werden nicht als Bastian-Signal gehandelt;
- historische Beschreibungen werden nicht als aktuelle Entries klassifiziert;
- konditionale Aussagen warten auf ihre Bedingung;
- Freshness läuft deterministisch ab;
- spätere Revision invalidiert älteren Kontext;
- Replay wird nicht als Live missverstanden;
- mehrere Assets im selben Live bleiben sauber getrennt;
- verspäteter Empfang erzeugt keinen rückwirkenden Trade;
- Konflikte zwischen Quellen folgen exakt der eingefrorenen Priorität.

## Daten-/Backtesttests

- Lücken/Duplikate/OHLC-Verletzungen werden erkannt;
- keine synthetische Zukunftsinformation;
- Kosten, Tick/Step/MinNotional stimmen;
- gleicher Run mit gleichen Hashes liefert identisches Ergebnis;
- 10×250, Einzeltest und optional 240/3×80 funktionieren;
- Manifest und Datenqualitätsreport vollständig.

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
- Not-Aus.

## UI-/Betriebstests

- PAPER/LIVE eindeutig sichtbar;
- Markt- und Source-Health getrennt;
- Bastian-Ereignisse mit Zeit/Freshness nachvollziehbar;
- Today/1W/1M/1J/3J korrekt;
- Backup/Restore getestet;
- Telegram P1/P2 getestet.

## Nichtfunktionale Ziele

- normale UI-/Read-API p95 <= 2 s;
- Verarbeitung finaler Strategiebars für alle zehn Symbole <= 60 s, sofern DMS 03 keine engere Latenz verlangt;
- kontrollierter Cancel von Import/Backtest <= 5 s bestätigt;
- 3-Jahres-Chart p95 <= 3 s;
- Betriebslogs standardmäßig <=90 Tage, sofern rechtliche/operative Gründe nichts anderes verlangen.

## Gates

### Gate A – DMS/Strategie

- keine kritische Strategiefrage offen;
- Originalindikator/Settings/Referenzen vorhanden;
- Bastian-Quellen/Freshness/Fusionsmodell eingefroren;
- Traceability vollständig.

### Gate B – Backtest/Replay

- Parität bestanden;
- Datenqualität grün;
- Kostenmodell korrekt;
- alle Pflichtläufe reproduzierbar.

### Gate C – Paper Ready

- Execution-/Recoverytests bestanden;
- Source-/Market-Health funktioniert;
- Secrets/Alerts/Backups eingerichtet.

### Gate D – Live Ready

- Paper-Soak bestanden;
- Restore getestet;
- Livekonto Least Privilege;
- Betreiberfreigabe bewusst erfolgt.

`BTK-DMS PREPARED` bedeutet nur: die Dokumentstruktur ist implementierbar vorbereitet. Es bedeutet nicht, dass Bot, Backtest, Paper oder Live bereits freigegeben sind.