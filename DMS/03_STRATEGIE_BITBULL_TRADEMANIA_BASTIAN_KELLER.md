# 03 – Normative Strategie: Bitbull / TradeMania / Bastian Keller

Status: `OFFEN / VORBEREITET`.

Vorgesehene erste eingefrorene Strategieversion: `BTK-INDICATOR-SPEC-1.0`.

## Zweck

Dieses Dokument wird die **einzige normative technische Referenz** für die BTK-Strategie. Bis der tatsächliche Zielindikator, seine Einstellungen und ausreichend reale Bastian-Referenzen vorliegen, enthält es bewusst Aufnahme-, Prüf-, Auswahl- und Freeze-Regeln statt erfundener Formeln.

Keine Strategie aus einem anderen Projekt darf als Ersatz dienen.

# A0 – Kandidateninventar und Auswahl vor Strategie-Freeze

Vor der Auswahl des Zielindikators werden **alle tatsächlich verfügbaren TradeMania-/Bitbull-Kandidaten** inventarisiert. Das betrifft öffentliche TradingView-Scripts ebenso wie rechtmäßig zugängliche Indicator-Masterclass-, Discord- und `trademania.app/bots`-Inhalte.

## Öffentlich verifizierter Kandidat 1

`TM-CAND-001 = Trademania - PVSRA Indicator`

Öffentlich verifiziert:

- Plattform: TradingView;
- Publisher: `BitbullTrading`;
- Script: `https://www.tradingview.com/script/mIsU8J9c/`;
- Source: protected/closed source;
- öffentlich als über alle Timeframes nutzbar beschrieben;
- Funktionsblöcke: PVSRA/Vector-Candles, Imbalance-Zonen, Sessions, EMAs, Pivot-/M-Levels, Vorperiodenlevels, ADR/AWR, Daily Open, POC, WIL und Lite Mode.

Dies ist ein **Kandidat**, noch keine freigegebene BTK-Strategie. Die öffentliche Beschreibung zeigt umfangreiche Analyse-/Kontextfunktionen, aber keinen vollständigen deterministischen Entry-/Exit-Automaten. Eine persönliche Urheberschaft durch Bastian Keller wird nicht behauptet; verifiziert ist die Veröffentlichung über den `BitbullTrading`-Account.

## Weitere öffentlich belegte Werkzeuge

- MACD: öffentlich von Bitbull Education erklärt und in der PVSRA-Beschreibung als mögliche Momentum-/Trendbestätigung erwähnt;
- POC/VRVP/VPVR: öffentlich in Bitbull-Education-Material verwendet; POC ist im PVSRA-Kandidaten integriert;
- RSI: öffentlich von Bitbull Education erklärt;
- TradeMania Indicator Masterclass: offiziell angekündigte eigene Indikatoren, einzelne Namen öffentlich nicht vollständig aufgelistet;
- Strategie-Indikator Masterclass: offiziell angekündigte weitere Profi-/KI-basierte Tools, technische Details öffentlich nicht belegt.

Diese Punkte sind **noch keine V1-Pflichtindikatoren**.

## Member-Inventar

Der Eigentümer hat Zugang zu:

- TradeMania Discord / Live-/Memberbereich;
- `https://trademania.app/bots`;
- weiteren nach Registrierung sichtbaren Indicator-/Academy-Bereichen.

Vor Auswahl werden daraus pro Tool mindestens Name, Version, Publisher, Zweck, unterstützte Märkte, Timeframes, Settings, Alerts/Webhooks, Signal-/Leveltypen, Repainting, Automationsgrad, Rechte und aktuelle Nutzung durch Bastian erfasst.

Geschützte Rohinhalte werden nicht öffentlich gespiegelt.

## Auswahlregel

V1 verwendet **nicht automatisch mehrere Indikatoren**. Gewählt wird der kleinste reproduzierbare Stack, der Bastians aktuelle Entscheidungsweise auf ETH und den übrigen Startmärkten tatsächlich abbildet.

Gewichtung:

1. wiederholte aktuelle Nutzung durch Bastian;
2. ETH-Eignung;
3. reproduzierbare Zustände/Levels/Signale;
4. Repainting-/Reload-Verhalten;
5. Alerts/Webhooks oder belastbare Black-Box-Parität;
6. historische Backtestbarkeit ohne Look-ahead;
7. Live-Latenz;
8. rechtmäßige Nutzbarkeit;
9. geringer redundanter Indikator-Stack;
10. stabiles Forward-Paper-Verhalten.

Marketingaussagen oder ein einzelner guter Screenshot entscheiden nicht über die Auswahl.

# A – Finalen Originalindikator aufnehmen

Nach Auswahl werden, soweit rechtmäßig zugänglich, dokumentiert:

1. exakter Indikatorname;
2. Plattform und Publisher-/Accountname;
3. Zugriffsart und Datum;
4. sichtbare Version/Änderungsdatum;
5. komplette Einstellungsmaske;
6. alle Defaultparameter und Auswahlwerte;
7. Alertnamen und Alertbedingungen;
8. reproduzierbare Kauf-/Verkaufs-/Neutralbeispiele mit Symbol, Timeframe und UTC-Zeit;
9. bei rechtmäßig einsehbarem Source: Hash, Version und private/rechtekonforme Ablage;
10. zugehörige offizielle Schulungs-/Live-Aussagen mit Datum und Kontext.

## Identität

| Feld | Wert |
|---|---|
| Kandidateninventar | DMS 22 |
| derzeit stärkster öffentlicher Kandidat | `Trademania - PVSRA Indicator` |
| finaler Zielindikator | OFFEN |
| Plattform | OFFEN bis Auswahl |
| Publisher | OFFEN bis Auswahl |
| Version/Build | OFFEN |
| Strategie-ID | `btk_indicator` vorläufig |
| Strategieversion | `BTK-INDICATOR-SPEC-1.0` erst nach Freeze |
| Repainting-Status | UNKNOWN |

## Inputs

Jeder sichtbare Input wird mit Typ, Default, Einheit, erlaubten Werten und Signalrelevanz erfasst. Es werden **keine** Defaults aus ähnlichen Indikatoren übernommen.

# B – Timeframe, Daten und Repainting

Vor Implementierung muss geklärt sein:

- zulässiger Signal-Timeframe;
- interne Multi-Timeframe-Abfragen;
- verwendete Preisquellen;
- Volumen-/Zusatzdaten;
- Warm-up;
- Datenlückenverhalten;
- Intrabar vs. Bar-Close;
- Verhalten nach Reload;
- historische Marker-Verschiebungen;
- Pivot-/Zukunftsbestätigung.

Bis zum Abschluss gilt: `trade_on_open_bar=FORBIDDEN`, sofern nicht ausdrücklich anders belegt.

# C – Signal- und Positionsabbildung

Die Tabelle wird erst anhand des final ausgewählten Indikators geschlossen:

| Originalereignis | Botzustand vorher | Botaktion | Gültigkeit | Status |
|---|---|---|---|---|
| Kaufsignal/Long-Condition | flat | OFFEN | OFFEN | OFFEN |
| Kaufsignal/Long-Condition | long | OFFEN | OFFEN | OFFEN |
| Verkaufssignal/Exit-Condition | long | OFFEN | OFFEN | OFFEN |
| Verkaufssignal/Exit-Condition | flat | OFFEN | OFFEN | OFFEN |
| Kontext-/Levelereignis ohne Entry | beliebig | OFFEN | OFFEN | OFFEN |
| kein Signal | beliebig | OFFEN | OFFEN | OFFEN |

Explizit zu klären:

- ob der Zielindikator überhaupt diskrete Buy/Sell-Signale liefert oder primär Kontext/Levels;
- ein Einstieg pro Trend oder wiederholte Entries;
- Pyramiding/Reentry;
- Gegensignal als Exit;
- Stop-Loss/Take-Profit/Trailing;
- Teilverkäufe;
- Zeitexit;
- Bestätigungsfilter;
- Nachholen verpasster Signale;
- Neustart mitten in einem Trend.

# D – Simultane Signale und drei Slots

Wenn mehr als drei gültige Entries gleichzeitig vorliegen, braucht V1 eine deterministische Priorität. Zulässige Quellen sind z. B. ein Indikator-Score, definierte Signalstärke, explizite Bastian-Priorität oder eine vor dem Backtest festgelegte neutrale Regel. Keine fremde Priorisierungslogik wird ungeprüft übernommen.

# E – Golden-/Referenzverfahren

Je Referenzbar werden mindestens gespeichert:

- Symbol und Timeframe;
- UTC-Barzeit;
- OHLCV;
- sichtbare/ableitbare Indikatorwerte;
- Originalzustand und Marker/Levels;
- Alertzustand soweit vorhanden;
- Screenshot-/Export-/Source-Referenz;
- Bot-Sollzustand.

Ziel ist eine ausreichend starke, reproduzierbare Paritätsbasis, vorzugsweise mindestens 1.000 aufeinanderfolgende Bars je Referenzmarkt, soweit die Indikatorplattform dies praktisch erlaubt.

Bei einem geschützten Script wie `TM-CAND-001` gilt: beobachtbare Black-Box-Parität ist zulässig; intern unbekannte Formeln dürfen nicht als sicher bekannt dargestellt werden.

# F – Bastian-Keller-Live-/Content-Schicht

## Quellenklassen

| Origin | Bedeutung | Unmittelbar handelbar? |
|---|---|---|
| `BTK_INDICATOR` | final ausgewählter Originalindikator/Stack | erst nach Freeze |
| `BASTIAN_YOUTUBE_LIVE` | aktuelle Live-Aussage von Bastian | nur validiert |
| `BASTIAN_YOUTUBE_UPDATE` | veröffentlichtes Marktupdate | nur innerhalb Freshness |
| `BASTIAN_TELEGRAM` | offizieller Kanal/Ankündigung/Markthinweis | nur nach eingefrorener Regel |
| `TRADEMANIA_DISCORD_BASTIAN` | rechtmäßig zugänglicher Bastian-/Memberinhalt | nur nach eingefrorener Regel |
| `TRADEMANIA_MEMBER_CONTENT_BASTIAN` | sonstiger rechtmäßig zugänglicher Bastian-Inhalt | nur nach eingefrorener Regel |
| `TRADEMANIA_BOT_CATALOG` | `/bots`-Katalog/Toolinfo | nie direkt handelbar ohne eigene Strategieentscheidung |
| `TRADEMANIA_OTHER_MENTOR` | anderer Mentor | nein, bis ausdrücklich freigegeben |

## Session-Lifecycle

Jede überwachte Quelle/Sendung hat mindestens einen der Zustände:

`SCHEDULED -> LIVE -> ENDED -> REPLAY`

Zusätzlich möglich: `STALE`, `UNAVAILABLE`, `UNKNOWN`.

Ein öffentlich beobachtetes Wochen-/Uhrzeitmuster ist **kein harter Strategiezeitplan**. Offizielle Ankündigungen und tatsächlicher Live-Status werden dynamisch erkannt, soweit die jeweilige Plattform dies technisch/rechtlich zulässt.

## Capture-Pfad

Für jede Quellenklasse wird vor signalaktivem Betrieb explizit dokumentiert:

- welche offizielle URL/ID allowgelistet ist;
- wie Live/Replay erkannt wird;
- welche Erfassungsmethode zulässig ist;
- ob offizielle Untertitel/Transkripte/Metadaten/API verfügbar sind;
- ob eine lokale Speech-to-Text-Verarbeitung überhaupt erforderlich und zulässig ist;
- erwartete Capture-Latenz und Ausfallverhalten;
- wie Content-Hash/private Referenz erzeugt wird.

Der Bot darf keine Bezahlschranke, Zugriffskontrolle oder technische Schutzmaßnahme umgehen.

## Struktur eines Bastian-Ereignisses

```text
source_event_id
session_id
origin
source_url_or_private_ref
session_state
published_at_utc
received_at_utc
spoken_at_utc_or_offset
speaker = Bastian Keller
asset_symbols[]
statement_class = CONTEXT | WATCH | ENTRY | EXIT | REDUCE | INVALIDATION | TARGET | RISK | UNKNOWN
side = LONG | SHORT | FLAT | UNKNOWN
price_or_zone
condition
condition_state = NONE | PENDING | MET | INVALIDATED | EXPIRED
horizon
freshness_deadline
capture_confidence
parser_confidence
content_hash_or_private_ref
derived_summary
decision_rule_version
supersedes_event_id
```

Rohtranskripte und geschützte Schulungsinhalte bleiben außerhalb des öffentlichen Repositories.

## Verbindliche Echtzeit-Reaktionspipeline

Nach Freeze läuft eine neue Bastian-Aussage nur über diese Kette:

1. **Source Discovery:** allowgelistete offizielle Quelle bzw. Session erkennen.
2. **Session Validation:** `LIVE`, `UPDATE`, `REPLAY` und Zeitkontext feststellen.
3. **Capture:** Inhalt über den dokumentierten zulässigen Weg erfassen.
4. **Speaker Validation:** Bastian Keller als Sprecher bestätigen.
5. **Segmentation:** relevante Aussage zeitlich isolieren; Zuschauer-/Mentorensätze trennen.
6. **Structuring:** Asset, Aussageklasse, Aktion/Richtung, Preis/Zone, Bedingung, Horizont extrahieren.
7. **Validation:** Pflichtfelder, Unsicherheit, Freshness, Revisionen und Konflikte prüfen.
8. **Conditional Watch:** bei „wenn X, dann Y“ zunächst `PENDING_CONDITION`; Marktbedingung separat beobachten.
9. **Fusion:** eingefrorene Beziehung zwischen Bastian und finalem Indikator-Stack anwenden.
10. **Risk/Capital/Exchange Guard:** Kapital, Slots, Börsenfilter, Preisabweichung und Systemhealth prüfen.
11. **Execution Intent:** erst jetzt darf ein Order-Intent entstehen.
12. **Audit:** Rohreferenz, strukturierte Aussage, Entscheidung, Blockgrund, Latenzen und Orderbezug speichern.

## Wann eine Aussage NICHT gehandelt wird

Keine automatische Order bei:

- reinem Szenario „wenn … dann …“, solange die Bedingung nicht erfüllt ist;
- historischer Trade-Beschreibung;
- Zuschauerfrage;
- Kommentar über fremden Trade/anderen Mentor;
- bloßer Watch-Zone;
- mehreren Alternativen ohne eindeutige Priorität;
- Aussage, die später im selben Stream revidiert wurde;
- verspätetem Replay ohne aktuelle Gültigkeit;
- unklarem Asset;
- unklarer Aktion;
- kritisch unsicherem Capture/Transkript/Parser-Ergebnis;
- Source-Ausfall oder Sprecherunsicherheit;
- fehlender Freshness-/Konfliktregel.

## `BASTIAN_ACTIONABLE_SIGNAL`

Ein Bastian-Signal benötigt mindestens:

1. Bastian eindeutig als Sprecher;
2. eindeutig identifizierbares Asset;
3. eindeutige Aktion oder deterministisch prüfbare Bedingung;
4. gültigen Zeitkontext/Freshness;
5. keine aktuellere widersprechende Aussage;
6. gültigen Session-/Source-Status;
7. bestandene Capture-/Parser-Validierung;
8. bestandene Risiko-, Kapital-, Exchange- und Source-Health-Guards.

Ein Rohtranskript, eine automatische Zusammenfassung oder ein einzelner Confidence-Wert ist **nie allein** ein handelbares Signal.

# G – Konditionale Aussagen

Aussagen wie „wenn ETH über X kommt, dann Long“ erzeugen **keine sofortige Order**. Sie werden als versionierte `PENDING_CONDITION` gespeichert.

Vor Auslösung müssen definiert und erfüllt sein:

- Asset;
- Bedingung und Operator;
- Preis/Zone/Timeframe soweit erforderlich;
- Aktion nach Bedingung;
- Freshness/Expiry;
- Invalidation;
- Marktfeed-Quelle;
- Konfliktfreiheit mit neueren Bastian-Aussagen;
- Fusionsregel mit dem finalen Indikator-Stack.

Nach Expiry oder Invalidation wird die Regel nicht reaktiviert, außer ein neues Source-Ereignis erzeugt sie erneut.

# H – Revisionen und Meinungswechsel

Eine spätere Aussage überschreibt die Historie nicht. Sie erzeugt ein neues Source-Ereignis mit `supersedes_event_id` oder einer anderen eingefrorenen Konfliktbeziehung.

Zu prüfen sind insbesondere:

- „Setup ist invalidiert“;
- „ich bin doch nicht mehr bullish/bearish“;
- neue Entry-Zone;
- Stop/Target wird verschoben;
- Teilgewinn/Positionsreduktion;
- Wechsel von Intraday- zu Swing-Horizont.

Nur die nach DMS 03 gültige aktuelle Kontextversion darf neue Entscheidungen beeinflussen.

# I – Indikator + Bastian: Fusionsmodell

Die endgültige Priorität wird erst nach echten Beispielen eingefroren. Zu prüfen sind:

- `INDICATOR_PRIMARY`: Indikator handelt, Bastian bestätigt/blockiert/managt;
- `BASTIAN_PRIMARY`: Bastian primär, Indikator als Timing/Bestätigung;
- `DUAL_CONFIRMATION`: Entry nur bei Übereinstimmung;
- `SOURCE_SPECIFIC`: Bastian darf nur bestimmte Aktionen überschreiben.

Genau **ein** Modell wird für V1 freigegeben. Die Auswahl erfolgt nicht nur nach höchstem historischen PnL, sondern nach Referenztreue, Robustheit und Forward-Paper-Verhalten.

# J – Freshness, Konflikte und Latenz

Jeder Bastian-Kontext erhält eine explizite Lebensdauer. Bis echte Beispiele ausgewertet sind, bleibt `freshness_deadline=OFFEN`; alte Aussagen dürfen nicht still weiterwirken.

Für jede Quellenklasse werden vor signalaktivem Paper/Live festgelegt:

- Source-Priorität;
- maximale Source-/Capture-/Parser-/End-to-End-Latenz;
- Freshness-Regel;
- Verhalten bei Sessionende;
- Verhalten bei Source-Ausfall;
- Verhalten bei verspäteter Zustellung;
- Konfliktregel mit neueren Aussagen und dem Indikator.

Die Latenz wird pro Event gemessen. Ein wirtschaftlich veralteter Entry darf trotz formal korrekter Aussage blockiert werden.

# K – Paper-/Replay-Pflicht für Bastian-Inhalte

Vor Live müssen mindestens getestet werden:

- Live-Start und Streamende;
- expliziter Entry;
- konditionaler Entry;
- expliziter Exit;
- Teilreduktion/Gewinne sichern;
- Zielzone;
- Invalidation/Stop;
- Meinungswechsel im Live;
- mehrere Coins nacheinander;
- Aussage ohne Preisangabe;
- Zuschauerfrage/anderer Mentor;
- falsches oder unvollständiges Transkript;
- verspätetes Video/Replay;
- Source-Abbruch und Reconnect;
- widersprüchliche Quellen;
- Expiry einer Pending Condition.

# Freeze-Kriterien für `BTK-INDICATOR-SPEC-1.0`

Freeze erst wenn:

- öffentliches + Member-Indikator-/Bot-Inventar geprüft;
- finaler Zielindikator bzw. minimaler Zielstack bewusst ausgewählt;
- aktuelle Nutzung durch Bastian ausreichend belegt;
- Indikatoridentität und Version eindeutig;
- Inputs/Defaults vollständig;
- Timeframe/Datenabhängigkeiten geklärt;
- Signal-/Entry-/Exit-/Pyramiding-Regeln eindeutig;
- Repainting/Bar-Close geprüft;
- Slotpriorität geklärt;
- Referenzfälle reproduzierbar;
- Bastian-Quellen und Speaker-Regel definiert;
- Capture-Pfad je signalrelevanter Quelle dokumentiert;
- Session-Lifecycle definiert;
- Freshness/Konflikt-/Revisionsregel definiert;
- Conditional-Watcher-Regeln definiert;
- maximal zulässige Latenzen festgelegt;
- genau ein Fusionsmodell freigegeben;
- keine kritische Strategiefrage mehr `OFFEN` ist.

Erst danach darf signalaktiver Strategiecode umgesetzt werden.
