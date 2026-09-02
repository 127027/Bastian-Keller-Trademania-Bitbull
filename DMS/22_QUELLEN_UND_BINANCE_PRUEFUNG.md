# 22 – Quellen und Binance-Prüfung

## Zweck

Dieses Dokument trennt veränderliche externe Tatsachen von dauerhaften Produktentscheidungen und führt den Quellenkatalog für **Bastian Keller / TradeMania / Bitbull**.

## Binance

Primär: Binance Spot. Beim späteren Start werden Symbolstatus, Filter, Gebühren und API-Regeln aktuell abgefragt.

BTK-Startuniversum:

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

Ein dokumentierter Vorabcheck vom 31.08.2026 hatte für alle zehn Märkte `TRADING` und mindestens drei Jahre Binance-Historie festgestellt. Dieser historische Check ist **kein Ersatz** für den Runtime-Check.

## TradeMania / Bastian Keller – öffentliche Basis

Öffentlich verifizierte Basis, Stand 02.09.2026:

- Offizielle TradeMania-Seite: `https://www.trademania.io/about`.
- Bastian Keller wird dort als **Founder & CEO TradeMania** geführt.
- TradeMania beschreibt, dass Bastian unter dem Namen **Bitbull** tägliche Marktanalysen teilt und Live-Sessions mit Tradern durchführt.
- Die Plattform beschreibt tägliche Live-/Mentoring-/Marktupdate-Formate. Konkrete Zahlen und Wochenpläne sind Marketing-/Betriebsdaten und können sich ändern.
- Die offizielle Live-Call-Seite `https://www.trademania.io/live-call` beschreibt Live-Trading, Morgenmeetings, Marktanalysen, Setups, Entries/Exits, Risikologik und tägliche Updates.
- Die offizielle Community-Seite beschreibt Discord-Bereiche für Setups, Signale, Analysen, Entry-Zonen, Indikatoren, Daily Recaps und Live-Breakdowns.
- Die TradeMania-Registrierung beschreibt nach Freischaltung Zugang zu Discord, Indikatoren, Trading-Academy, Live-Setups, Signalen und Community-Kanälen.

Diese öffentlichen Angaben legitimieren **keine erfundene Handelsregel**. Sie begründen das Quellenmodell und die Recherche-/Monitoringrichtung.

# Verifiziertes Indikator-/Tool-Inventar

Die Auswahl des späteren Zielindikators erfolgt **erst nach vollständigem Inventar** aus öffentlichen und rechtmäßig zugänglichen Member-Quellen. Ein öffentlich gefundener Kandidat wird nicht allein aufgrund von Marketing oder Popularität zur Strategie erklärt.

## Kandidat TM-CAND-001 – `Trademania - PVSRA Indicator`

Öffentlich verifiziert auf TradingView:

- URL: `https://www.tradingview.com/script/mIsU8J9c/`
- Publisher: `BitbullTrading`
- TradingView-Profil: `https://www.tradingview.com/u/BitbullTrading/`
- öffentliches Profil zeigt derzeit genau ein veröffentlichtes Script;
- Script-Typ: Indicator;
- Source-Zugriff: `PROTECTED SOURCE SCRIPT` / closed source;
- öffentlich nutzbar auf TradingView, Source selbst nicht offen;
- veröffentlicht 07.10.2024, öffentliche Release Notes zuletzt 10.10.2024;
- laut öffentlicher Beschreibung für Forex, Krypto, Aktien und andere Assets sowie über alle Timeframes einsetzbar.

Öffentlich beschriebene Funktionsblöcke:

- PVSRA-/Vector-Candles;
- dynamische Imbalance-Zonen;
- Markt-Sessions mit High/Low;
- integrierte und frei konfigurierbare EMAs;
- Pivot Points inklusive M-/50%-Levels;
- Vortages-/Vorwochen-High/Low;
- ADR/AWR bzw. Average Ranges;
- Daily Open;
- High-/Low-POC für Wick und Candle Body;
- WIL / Weekly Interest Level aus der asiatischen Session;
- Lite Mode;
- Labels/Levels im Chart.

Öffentlich dokumentiert sind außerdem PVSRA-Volumen-/Vector-Candle-Kriterien mit erhöhtem Volumen sowie Hinweise auf Breakout-/Retrace-/Confirmation-Anwendung. Diese öffentliche Beschreibung reicht **nicht** aus, um die vollständige interne Logik des geschützten Scripts als exakt bekannt zu behaupten.

### Vorläufige Einordnung

`TM-CAND-001` ist derzeit der **stärkste öffentlich verifizierte TradeMania-/Bitbull-Kandidat**, weil Publisher, Produktname, Plattform und Funktionsumfang nachvollziehbar sind. Er ist **noch nicht** als BTK-Zielindikator freigegeben.

Besonders interessant für unseren ETH-Bot sind:

- PVSRA/Vector-Candles als Volumen-/Aktivitätskontext;
- Imbalance-Zonen;
- POC;
- 13/50/200/800-EMA-Kontext aus der öffentlichen Beschreibung;
- Session-High/Lows und WIL;
- ADR/AWR sowie Vorperiodenlevels;
- Kombination aus Level, Momentum und Bestätigung statt eines isolierten Buy/Sell-Pfeils.

Das spricht eher für einen **Analyse-/Kontextindikator** als für einen automatisch handelbaren Einzelsignal-Indikator. Ob und wie Bastian ihn aktuell selbst für Entries, Exits oder Management nutzt, muss durch echte aktuelle Evidence bestätigt werden.

## Öffentliche ergänzende Tools – noch keine BTK-Pflichtindikatoren

### TM-CAND-002 – MACD

- öffentlich von Bitbull Education als Momentum-/Trendwerkzeug erklärt;
- auch in der öffentlichen PVSRA-Beschreibung als mögliche zusätzliche Trend-/Momentum-Bestätigung empfohlen;
- generischer Indikator, kein exklusiver TradeMania-Source.

### TM-CAND-003 – POC / VRVP / VPVR / Volume Profile

- POC ist im öffentlichen PVSRA-Indikator integriert;
- Bitbull Education zeigt öffentlich POC-/Volume-Profile-Anwendung;
- interessant für Levels, Retests, Ziele und Liquiditäts-/Volumenkontext;
- noch keine eigenständige Entry-Regel.

### TM-CAND-004 – RSI

- öffentlich von Bitbull Education erklärt;
- generischer Momentum-/Overbought-/Oversold-Indikator;
- nur aufnehmen, wenn aktuelle Bastian-Evidence zeigt, dass RSI tatsächlich Bestandteil der Zielstrategie ist.

## Nicht öffentlich namentlich aufgeschlüsselte TradeMania-Angebote

### TM-CAND-005 – `TradeMania Indikator Masterclass`

Die offizielle TradeMania-Komplettausbildung beschreibt eine eigene Indikator-Masterclass mit exklusiv entwickelten, kostenfrei verfügbaren Indikatoren. Die einzelnen Indikatornamen und aktuellen Versionen sind öffentlich nicht vollständig aufgelistet.

### TM-CAND-006 – `Strategie-Indikator Masterclass`

Die offizielle Seite beschreibt zusätzlich eine Strategie-Indikator-Masterclass und bewirbt dort professionelle bzw. KI-basierte/selbstlernende Tools. Öffentliche Marketingbeschreibung ist **kein technischer Nachweis**. Namen, Versionen, Funktionsweise und Reproduzierbarkeit müssen im Memberbereich geprüft werden.

### TM-CAND-007 – `trademania.app/bots`

Der Eigentümer hat Zugang zu `https://trademania.app/bots`. Die Seite liegt hinter dem TradeMania-Account und ist über die öffentliche Recherche nicht inhaltlich einsehbar.

Status: `OWNER ACCESS CONFIRMED / CONTENT REVIEW OUTSTANDING`.

Vor Verwendung werden pro dort sichtbarem Bot/Tool dokumentiert:

- exakter Name;
- Anbieter/Publisher;
- Zweck;
- unterstützte Märkte/Exchanges;
- Timeframe/Tradingstil;
- Entry-/Exit-/Risk-Logik soweit sichtbar;
- Automationsgrad;
- API-/Webhook-/Alert-Möglichkeiten;
- Performanceangaben inklusive Zeitraum und Beweisart;
- Kosten/Zugriffsmodell;
- Rechte/Exportmöglichkeiten;
- Nutzen für unsere BTK-Strategie.

`/bots` wird **nicht** automatisch mit dem Zielindikator gleichgesetzt.

### TM-CAND-008 – TradeMania Discord / Member-Live-Bereich

Der Eigentümer ist im TradeMania-Discord registriert und hat einen konkreten Member-/Live-Kanal bereitgestellt. Der Kanalinhalt ist nicht öffentlich auswertbar und wird deshalb nicht als bereits geprüfte Evidence dargestellt.

Status: `OWNER ACCESS CONFIRMED / CONTENT REVIEW OUTSTANDING`.

Im privaten Review werden insbesondere gesucht:

- Indikatornamen und Setup-Anleitungen;
- aktuelle Bastian-Live-Termine/Ankündigungen;
- Bastian-spezifische Markt-/Coin-Analysen;
- Entry-/Exit-/Stop-/Target-/Invalidation-Sprache;
- Screenshots mit aktiven Indikatoren;
- Hinweise auf verwendete Timeframes;
- Alerts/Webhooks/TradingView-Namen;
- Replays und Recaps mit Zeitstempel.

Geschützte Rohinhalte werden nicht in das öffentliche Repository gespiegelt.

# Auswahlkriterien für den BTK-Zielstack

Wir wählen **nicht möglichst viele Indikatoren**, sondern den kleinsten reproduzierbaren Stack, der Bastians aktuelle Entscheidungsweise tatsächlich abbildet.

Bewertung pro Kandidat:

1. **Bastian-Nähe:** nutzt Bastian das Tool selbst aktuell und wiederholt?
2. **ETH-Eignung:** liefert es auf ETH robuste, nachvollziehbare Information?
3. **Determinismus:** sind Zustände/Levels/Signale eindeutig reproduzierbar?
4. **Repainting:** kann historisches Verhalten sauber geprüft werden?
5. **Automation:** gibt es Alerts, Webhooks, sichtbare Werte oder belastbare Black-Box-Parität?
6. **Backtestbarkeit:** kann die Logik ohne Look-ahead reproduziert werden?
7. **Latenz:** ist die Information für die Tradingart schnell genug erfassbar?
8. **Rechte/Zugriff:** kann sie rechtmäßig im Bot verwendet und getestet werden?
9. **Komplexität:** bringt ein zusätzlicher Indikator echten Mehrwert oder nur Redundanz?
10. **Forward-Paper:** verbessert er reale Paper-Ergebnisse stabil, nicht nur einen historischen Fit?

### Vorläufige Priorität

1. `Trademania - PVSRA Indicator` vollständig aufnehmen und gegen aktuelle Bastian-Lives prüfen.
2. Member-Inventar aus Indicator Masterclass, Strategie-Indikator Masterclass, Discord und `/bots` erfassen.
3. MACD/POC/RSI nur dann in V1 aufnehmen, wenn sie in Bastians tatsächlichem Entscheidungsprozess wiederholt eine klare Rolle spielen.
4. Erst danach Zielstack und Fusionsmodell einfrieren.

# Öffentliche Referenzen

- `https://www.trademania.io/about`
- `https://www.trademania.io/live-call`
- `https://www.trademania.io/community`
- `https://www.trademania.io/komplettausbildung`
- `https://www.trademania.io/getting-started-now`
- `https://trademania.app/register`
- `https://www.tradingview.com/u/BitbullTrading/`
- `https://www.tradingview.com/script/mIsU8J9c/`
- offizieller Bastian-/Bitbull-YouTube-Auftritt, konkrete Channel-ID vor signalaktiver Nutzung erneut verifizieren
- öffentlicher Bitbull-Telegram-Auftritt, konkrete Channel-ID vor signalaktiver Nutzung erneut verifizieren

# Beobachtete Zeitmuster – keine harte Strategie

TradeMania beschreibt Live-/Analyseformate Montag bis Samstag sowie mehrere Live-Tradings pro Woche. Öffentliche Seiten können sich bei der konkreten Anzahl unterscheiden oder geändert werden. Diese Angaben werden deshalb nur als **veränderliche Betriebsbeobachtung** behandelt.

Konsequenz:

- Source Discovery überwacht allowgelistete offizielle Quellen dynamisch;
- ein Zeitplan ist höchstens Erwartungsfenster für Health/Monitoring;
- tatsächlicher Sessionstatus (`LIVE`, `ENDED`, `REPLAY` usw.) ist maßgeblich;
- Änderungen an Marketing-/Wochenplänen erfordern keine Strategieänderung, solange die Source-Erkennung dynamisch bleibt.

# Evidence-Tabelle

| Evidence-ID | Quelle | Datum | Indikator-/Source-Version | Inhalt | Beweiskraft | Status |
|---|---|---|---|---|---|---|
| BTK-EV-001 | Zielindikator | – | – | finaler Originalindikator/Access | kritisch | OFFEN |
| BTK-EV-002 | Zielindikator | – | – | Settings-Snapshot | kritisch | OFFEN |
| BTK-EV-003 | Zielindikator | – | – | Signalreferenzen ETH | kritisch | OFFEN |
| BTK-EV-004 | Zielindikator | – | – | Alertdefinitionen | hoch | OFFEN |
| BTK-EV-005 | `trademania.io/about` | 02.09.2026 | Webstand | Bastian/TradeMania/Bitbull Rollenbeschreibung | ergänzend | VERIFIZIERT |
| BTK-EV-006 | `trademania.io/live-call` | 02.09.2026 | Webstand | Live-/Update-Angebot | ergänzend | VERIFIZIERT |
| BTK-EV-007 | echte Bastian-Live-Session | – | – | gelabelte Live-Evidence | kritisch Source-Modell | OFFEN |
| BTK-EV-008 | Capture-/Parser-Referenz | – | – | Echtzeit-Erfassung | kritisch Automation | OFFEN |
| BTK-EV-009 | TradingView `mIsU8J9c` | 02.09.2026 | öffentlich, Release Notes 10.10.2024 | `Trademania - PVSRA Indicator` | hoch für Kandidatenidentität | VERIFIZIERT |
| BTK-EV-010 | TradingView `BitbullTrading` | 02.09.2026 | Profilstand | Publisherprofil, aktuell 1 öffentliches Script | hoch | VERIFIZIERT |
| BTK-EV-011 | `trademania.io/komplettausbildung` | 02.09.2026 | Webstand | Indicator-/Strategie-Indicator-Masterclass | ergänzend | VERIFIZIERT |
| BTK-EV-012 | `trademania.app/register` | 02.09.2026 | Webstand | Registrierung verspricht Zugang zu Discord/Indikatoren/Live-Setups/Signalen | ergänzend | VERIFIZIERT |
| BTK-EV-013 | TradeMania Discord Memberbereich | 02.09.2026 | Owner-Zugang | konkrete Member-/Live-Evidence | kritisch | REVIEW AUSSTEHEND |
| BTK-EV-014 | `trademania.app/bots` | 02.09.2026 | Owner-Zugang | Bot-/Tool-Inventar | hoch | REVIEW AUSSTEHEND |

# Quellen-Allowlist vor signalaktivem Paper/Live

Für jede Quelle müssen vor Aktivierung dokumentiert sein:

- offizieller Provider;
- eindeutige Channel-/Account-/Source-ID;
- URL/private Referenz;
- Source-Klasse;
- Sprecher-Scope;
- Live-/Replay-Erkennung;
- zulässiger Capture-Pfad;
- Freshness-/Latenzgrenze;
- Rechte-/Zugriffsstatus;
- Evidence-/Config-Hash.

Eine ähnlich benannte Community-, Reupload- oder Fanquelle darf nicht automatisch aufgenommen werden.

# Quellenbewertung

## Kritisch

- final ausgewählter Originalindikator;
- vollständige Settings;
- reproduzierbare Signale/Alerts;
- echte gelabelte Bastian-Live-/Update-Ereignisse;
- Source-/Session-/Capture-Referenzen;
- rechtmäßig einsehbarer Source/Hash, falls vorhanden.

## Ergänzend

- offizielle Website;
- Videos/Livestreams/Seminare;
- schriftliche Erklärungen;
- öffentliche Terminankündigungen;
- Community-Hinweise als Recherchehinweis, nicht als Orderquelle.

Ergänzende Quellen dürfen keine widersprüchliche technische Regel über reproduzierbare Originalbeobachtung und eingefrorene DMS stellen.

# Rechte

- keine Zugangsdaten in Git;
- keine Umgehung von Zugriffsschutz/Paywalls/DRM/Schutzmaßnahmen;
- fremden Source nur veröffentlichen, wenn Rechte klar sind;
- sonst Hash + eigene Spezifikation + Referenzwerte;
- lange fremde Schulungs-/Memberinhalte nicht vollständig kopieren;
- private Transkripte/Medien außerhalb des öffentlichen Repositorys;
- persönliche Discord-/TradeMania-Sessiondaten bleiben privat.

# Repository

Remote: `127027/Bastian-Keller-Trademania-Bitbull`.

Dieses Repository enthält ausschließlich die BTK-/TradeMania-/Bastian-Keller-Projektwahrheit. Fremde Strategiespezifikationen werden nicht als aktive Quelle übernommen.
