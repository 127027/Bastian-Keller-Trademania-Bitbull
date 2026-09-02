# 17 – Glossar

| Begriff | Verbindliche Bedeutung |
|---|---|
| BTK | Arbeitskürzel für Bitbull / TradeMania / Bastian-Keller-Bot |
| Originalindikator | der vom Eigentümer rechtmäßig bereitgestellte konkrete TradeMania-/Bastian-Keller-Indikator |
| Strategie-Spec | eingefrorene technische Definition in DMS 03 |
| Referenzparität | Übereinstimmung der Botstrategie mit freigegebenen Original-/Golden-Beobachtungen |
| Black-Box-Parität | Parität gegen beobachtbare Signale/Outputs ohne einsehbaren Sourcecode |
| Source Evidence | Screenshot, Settings, Alert, Export, Hash oder dokumentierte offizielle Erklärung/Source-Session als Beleg |
| Bar/Kerze | OHLCV-Datensatz eines Timeframes |
| geschlossene Kerze | finalisierte Kerze |
| vorläufige Kerze | laufende Kerze |
| Signal | deterministische Strategieausgabe gemäß eingefrorener BTK-Spec |
| Strategie-Zustand | vom neuen Indikator/Fusionsmodell definierter persistenter oder punktueller Zustand |
| Order-Intent | interner, nach allen Gates prüfbarer Wunsch, eine Order zu erzeugen |
| Order | an Paper-/Börsenadapter übermittelte Anweisung |
| Fill | vollständige/teilweise Ausführung |
| Position | aus Fills/Beständen abgeleitete offene Assetmenge |
| Long-only | kaufen und später verkaufen, kein Leerverkauf |
| Pyramiding | mehrfacher Einstieg/Vergrößerung derselben Position |
| isolierter Backtesttopf | 250-USDT-Simulationskonto eines Coins |
| gemeinsamer Paper-Cashpool | 240-USDT-Modellkonto für zunächst 3×80 Slots |
| Positionsslot | einer von maximal drei gleichzeitig belegbaren BTK-Positionsplätzen in der V1-Baseline |
| Backtest | historische Simulation ohne echte Börsenorder |
| Source Replay | chronologische Wiederholung gelabelter Source-Ereignisse mit ihren damaligen Zeit-/Freshness-/Revisionsinformationen |
| Paper | laufende Simulation mit realen Marktdaten und – soweit freigegeben – realen Source-Ereignissen |
| Live | echte Börsenorders |
| Warm-up | historische Daten vor erster handelbarer Auswertung |
| Look-ahead | Nutzung zukünftiger Information |
| Repainting | nachträgliche Änderung eines zuvor sichtbaren/angenommenen historischen Indikatorzustands oder Signals |
| Slippage | Differenz Referenz- zu Fillpreis |
| Spread | Bid-/Ask-Differenz |
| Drawdown | Equity-Rückgang von vorherigem Hoch |
| PnL | Gewinn/Verlust; netto nach Kosten |
| Mark-to-market | Bewertung offener Position ohne erfundenen Verkauf |
| Reconciliation | Abgleich lokalen Zustands mit externer Ausführungs-/Quellenwahrheit |
| Idempotenz | Wiederholung erzeugt keine zweite Wirkung |
| stale | definierte Frischegrenze überschritten |
| Datenrevision | nachträgliche Provideränderung historischer Daten |
| Run-Manifest | vollständige Metadaten eines reproduzierbaren Backtest-/Replaylaufs |
| Not-Aus | Sperre neuer Entries; Liquidation separat |
| UTC | interne Standardzeitzone |

## Bastian-/Source-Begriffe

| Begriff | Bedeutung |
|---|---|
| TradeMania | offizielle Ausbildungs-/Community-Marke um Bastian Keller und weitere Trader/Mentoren |
| Bitbull | Bastians etablierter Kanal-/Markenbezug für Marktanalysen/Tradinginhalte |
| Source Allowlist | versionierte Liste eindeutig freigegebener offizieller Channel-/Account-/Source-IDs |
| Source Session | zusammengehörige Live-/Update-/Replay-Sitzung einer offiziellen Quelle |
| Session State | `SCHEDULED`, `LIVE`, `ENDED`, `REPLAY`, `STALE`, `UNAVAILABLE` oder `UNKNOWN` |
| Capture | technisch/rechtlich zulässige Erfassung von Source-Metadaten/Inhalt für die interne Verarbeitung |
| Capture Result | erfasster Roh-/Zwischenstand; ausdrücklich noch keine Handelsentscheidung |
| Bastian Statement | strukturierte Aussage, die Bastian als Sprecher zugeordnet wurde; noch nicht automatisch handelbar |
| Bastian Context | aktuelle Markt-/Szenarioaussage ohne automatisch handelbaren Auftrag |
| Bastian Actionable Signal | nach DMS 03 validierte, hinreichend eindeutige und frische Bastian-Aussage |
| Source Event | immutable zeitgestempeltes Ereignis aus offizieller Bastian-/TradeMania-Quelle |
| Freshness | Zeitraum, in dem eine Aussage/Condition noch als aktuell gelten darf |
| Expiry | Zeitpunkt, ab dem Kontext/Condition nicht mehr neu auslösen darf |
| Revision | neuere Aussage, die eine ältere Aussage ändert, einschränkt oder invalidiert |
| Supersede | dokumentierte Beziehung, dass ein neueres Event einen älteren Kontext nach Regel ersetzt |
| Pending Condition | konditionale Bastian-Aussage, deren Marktbedingung noch nicht erfüllt ist |
| Conditional Watcher | Komponente, die Pending Conditions gegen gültige Marktdaten, Freshness und Revisionen prüft |
| Fusion Mode | festgelegte Priorität/Verknüpfung zwischen Indikator und Bastian-Aussagen |
| Source Latency | Zeit von Quelle/Veröffentlichung bis Empfang/Capture |
| End-to-End-Latenz | Zeit vom relevanten Source-Zeitpunkt bis zur validierten Entscheidung bzw. Orderabsicht |
| `NO_TRADE` | sicherer Ausgang, wenn Pflichtinformation, Freshness, Source-Health oder Eindeutigkeit nicht ausreicht |
