# 01 – Produktvision und Scope

Status: `VERBINDLICH` für den technischen Unterbau; konkrete Strategiequelle bleibt bis zum DMS-03-Freeze teilweise `OFFEN`.

## Produktziel

Dieses Repository beschreibt einen eigenständigen **Bastian-Keller-/TradeMania-/Bitbull-Trading-Bot**. Der Bot soll einen bewusst ausgewählten, rechtmäßig zugänglichen TradeMania-/Bitbull-Indikator bzw. minimalen Indikatorstack deterministisch auswerten und eindeutige, aktuelle Aussagen von Bastian Keller aus freigegebenen offiziellen Live-/Update-Quellen nach genau dokumentierten Regeln in Handelskontext bzw. handelbare Strategieereignisse überführen.

Der technische Unterbau wird nicht unnötig neu erfunden. Bewährte generische Komponenten dürfen gezielt wiederverwendet werden, wenn sie strategiespezifisch neutral sind. Die neue Source-/Live-Schicht wird nur dort ergänzt, wo der bestehende Unterbau diese Verantwortung noch nicht besitzt.

## Aktueller Indikatorstatus

Öffentlich verifiziert ist derzeit der Kandidat **`Trademania - PVSRA Indicator`** des TradingView-Publishers `BitbullTrading`. Er bietet laut öffentlicher Beschreibung u. a. PVSRA-/Vector-Candles, Imbalance-Zonen, EMAs, Pivots/M-Levels, POC, WIL, Sessions, ADR/AWR und Vorperiodenlevels.

Dieser Kandidat ist **noch nicht automatisch der Zielindikator**. Vor dem Strategie-Freeze werden zusätzlich die nach Registrierung verfügbaren TradeMania Indicator-/Strategie-Indicator-Masterclasses, Discord-Inhalte und `trademania.app/bots` inventarisiert. V1 soll den kleinsten reproduzierbaren Stack verwenden, den Bastian aktuell tatsächlich nutzt und der für ETH/Startuniversum sinnvoll ist.

## Erfolgsbild

Ein fachkundiger Dritter kann später:

- erklären, warum genau der ausgewählte Indikator/Stack gewählt wurde;
- erklären, wann der Originalindikator ein Signal, Level oder nur Kontext erzeugt;
- erklären, wann eine Bastian-Aussage nur Kontext, eine Pending Condition oder ein handelbares Signal ist;
- nachvollziehen, wie Live/Replay, Sprecher, Asset, Bedingung, Freshness, Revision und Latenz geprüft wurden;
- Botreaktionen mit Originalindikator und gelabelten Referenz-Lives vergleichen;
- denselben Indicator-Backtest und denselben Source-Replay reproduzieren;
- jede Order auf Signal, Source-Event, Zeit, Fusion, Risk-/Capital-Gate, Konfiguration und Bot-Version zurückführen;
- Daten-/Source-/Capture-/Parser-Ausfälle erkennen;
- nach Neustart ohne Doppelorder und ohne blind reaktivierte alte Pending Conditions fortsetzen;
- nachvollziehen, warum eine Order ausgeführt, blockiert oder verworfen wurde.

## Enthalten

- zehn Binance-Spot-Paare gegen USDT: BTC, ETH, BNB, SOL, XRP, ADA, LINK, AVAX, DOT, DOGE;
- Paper/Live-Baseline 240 USDT gemeinsamer Cashpool, drei Slots à 80 USDT;
- Backtest-Baseline zehn isolierte Tests à 250 USDT sowie Einzeltest à 250 USDT;
- mindestens drei vollständige Jahre Marktdaten plus Warm-up für den reproduzierbaren Indicator-/Marktpfad;
- Bastian-Source-Replay ausschließlich für tatsächlich vorhandene, zeitlich belastbare Evidence;
- Startup-/Datenprüfung und täglicher Audit;
- UI-Zeiträume Heute, 1W, 1M, 1J, 3J;
- 24/7-Paper als Pflichtstufe vor Live;
- Audit, Metriken, Alerts, Backup und Recovery;
- Kandidateninventar und begründete Zielindikator-Auswahl;
- final ausgewählter Originalindikator als technische Strategiequelle;
- Bastian Keller als primäre menschliche Strategiequelle;
- Source-Allowlist und dynamische Live-/Update-Erkennung;
- technisch/rechtlich zulässigen Capture-Pfad je Quelle;
- Speaker-/Asset-/Statement-Validierung;
- Freshness, Revision/Supersede und Konfliktbehandlung;
- `PENDING_CONDITION` für konditionale Aussagen;
- genau ein später eingefrorenes Fusionsmodell zwischen Indikator und Bastian-Kontext;
- Messung von Source-, Capture-, Parser- und End-to-End-Latenz;
- späteren fairen Vergleich mit dem separat betriebenen Referenzbot.

## Noch offen

Bis Member-Inventar, finaler Zielindikator und rechtmäßig zugängliche Live-Quellen vollständig geprüft sind, bleiben insbesondere offen:

- finaler Indikator/Stack, Version, Publisher und Inputs;
- welche PVSRA-Funktionen Bastian aktuell wirklich entscheidungsrelevant nutzt;
- welche zusätzlichen Member-Indikatoren/Bots tatsächlich relevant sind;
- Signal-Timeframe/Multi-Timeframe-Verhalten;
- Kauf-/Verkaufs-/Trend-/Level-/Filterlogik;
- Bar-Close/Intrabar/Repainting;
- Warm-up und Initialzustand;
- Alerts und Overlays;
- Entry-/Exit-/Reentry-/TP-/SL-/Trailing-Regeln;
- Slotpriorisierung;
- exakte offizielle Source-/Channel-IDs;
- Capture-Methode je Quelle;
- Mindestqualität/Pflichtfelder für Capture und Parser;
- Sprechererkennung in Multi-Person-Lives;
- ob Bastian selbst Entries auslösen darf oder nur bestätigt/blockiert/managt;
- Regeln für konditionale Aussagen;
- Freshness, Revision, Source-Priorität und Konflikte;
- maximal zulässige Reaktionslatenz;
- Verhalten bei Streamende/Source-Ausfall;
- genaues Fusionsmodell.

## Nicht enthalten

- erfundene Indikatorlogik;
- erfundene oder aus dem Kontext gerissene Bastian-Aussagen;
- blindes Stapeln von MACD/RSI/POC oder anderen Tools ohne aktuelle Bastian-Evidence;
- Gewinn- oder Renditeversprechen;
- Futures, Margin, Leverage oder Short ohne neue Freigabe;
- Martingale/Grid/DCA/Pyramiding ohne belegte Strategieanforderung;
- automatisches Folgen beliebiger Mentoren oder Community-Mitglieder;
- Drittzusammenfassungen als Ersatz für ausgefallene Bastian-Quellen;
- Umgehung von Plattformzugriffen, Bezahlschranken oder Schutzmaßnahmen;
- API-Schlüssel mit Auszahlungsrecht.

## Betriebsmodi

1. `BACKTEST`
2. `SOURCE_REPLAY`
3. `PAPER`
4. `LIVE_DISABLED`
5. `LIVE`

Sicherer Standard nach Installation, Restore oder ungeklärter Synchronisation ist `LIVE_DISABLED`.

## Strategieebenen

- `INDICATOR_SIGNAL`: technischer Zustand/Signal/Level des final ausgewählten Indikators;
- `BASTIAN_STATEMENT`: strukturierte Aussage, noch nicht automatisch handelbar;
- `BASTIAN_CONTEXT`: gültiger Markt-/Szenariokontext;
- `PENDING_CONDITION`: konditionale Aussage, die auf bestätigte Marktbedingung wartet;
- `BASTIAN_ACTIONABLE_SIGNAL`: nach DMS 03 validierte, ausreichend eindeutige und frische Aussage;
- `STRATEGY_DECISION`: Ergebnis des eingefrorenen Fusionsmodells;
- `EXECUTION_INTENT`: erst nach Risk-, Kapital-, Exchange-, Freshness- und Health-Prüfung.

24/7 bedeutet kontinuierliche Markt-, Indikator- und Quellenüberwachung, nicht permanente Handelstätigkeit.
