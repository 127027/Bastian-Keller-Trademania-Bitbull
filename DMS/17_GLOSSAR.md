# 17 – Glossar

| Begriff | Verbindliche Bedeutung |
|---|---|
| BTK | Arbeitskürzel für Bitbull / TradeMania / Bastian-Keller-Variante |
| Originalindikator | der vom Eigentümer später rechtmäßig bereitgestellte konkrete Indikator |
| Strategie-Spec | eingefrorene technische Definition in DMS 03 |
| Referenzparität | Übereinstimmung der Botstrategie mit freigegebenen Original-/Golden-Beobachtungen |
| Black-Box-Parität | Parität gegen beobachtbare Signale/Outputs ohne einsehbaren Sourcecode |
| Source Evidence | Screenshot, Settings, Alert, Export, Hash oder dokumentierte offizielle Erklärung als Beleg |
| Bar/Kerze | OHLCV-Datensatz eines Timeframes |
| geschlossene Kerze | finalisierte Kerze |
| vorläufige Kerze | laufende Kerze |
| Signal | deterministische Strategieausgabe gemäß eingefrorener BTK-Spec |
| Strategie-Zustand | vom neuen Indikator definierter persistenter oder punktueller Zustand; Bezeichnungen noch offen |
| Order-Intent | interner, prüfbarer Wunsch, eine Order zu erzeugen |
| Order | an Paper-/Börsenadapter übermittelte Anweisung |
| Fill | vollständige/teilweise Ausführung |
| Position | aus Fills/Beständen abgeleitete offene Assetmenge |
| Long-only | kaufen und später verkaufen, kein Leerverkauf |
| Pyramiding | mehrfacher Einstieg/Vergrößerung derselben Position |
| isolierter Backtesttopf | 250-USDT-Simulationskonto eines Coins |
| gemeinsamer Paper-Cashpool | 240-USDT-Modellkonto für zunächst 3×80 Slots |
| Positionsslot | maximal eine gleichzeitig belegte Coinposition im geerbten Basismodell |
| Backtest | historische Simulation ohne echte Börsenorder |
| Paper | laufende Simulation mit realen Marktdaten |
| Live | echte Börsenorders |
| Warm-up | historische Daten vor erster handelbarer Auswertung |
| Look-ahead | Nutzung zukünftiger Information |
| Repainting | nachträgliche Änderung eines zuvor sichtbaren/angenommenen historischen Indikatorzustands oder Signals |
| Slippage | Differenz Referenz- zu Fillpreis |
| Spread | Bid-/Ask-Differenz |
| Drawdown | Equity-Rückgang von vorherigem Hoch |
| PnL | Gewinn/Verlust; netto nach Kosten |
| Mark-to-market | Bewertung offener Position ohne erfundenen Verkauf |
| Reconciliation | Abgleich lokalen Zustands mit Börse |
| Idempotenz | Wiederholung erzeugt keine zweite Wirkung |
| stale | Frischegrenze überschritten |
| Datenrevision | nachträgliche Provideränderung historischer Daten |
| Run-Manifest | vollständige Metadaten eines reproduzierbaren Backtestlaufs |
| Not-Aus | Sperre neuer Entries; Liquidation separat |
| UTC | interne Standardzeitzone |

## Zusätzliche Begriffe

| Begriff | Bedeutung |
|---|---|
| TradeMania | aktuelle offizielle Ausbildungs-/Community-Marke um Bastian Keller/Bitbull |
| Bastian Context | aktuelle Markt-/Szenarioaussage ohne automatisch handelbaren Auftrag |
| Bastian Actionable Signal | nach DMS 03 validierte, hinreichend eindeutige Bastian-Aussage |
| Source Event | zeitgestempeltes Ereignis aus offizieller Bastian-/TradeMania-Quelle |
| Freshness | Zeitraum, in dem eine Aussage noch als aktuell/handelbar gelten darf |
| Fusion Mode | festgelegte Priorität/Verknüpfung zwischen Indikator und Bastian-Aussagen |
