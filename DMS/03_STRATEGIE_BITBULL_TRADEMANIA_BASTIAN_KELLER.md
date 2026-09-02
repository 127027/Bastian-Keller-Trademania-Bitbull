# 03 – Normative Strategie: Bitbull / TradeMania / Bastian Keller

Status: `OFFEN / VORBEREITET`.

Vorgesehene erste eingefrorene Strategieversion: `BTK-INDICATOR-SPEC-1.0`.

## Zweck

Dieses Dokument wird die **einzige normative technische Referenz** für die BTK-Strategie. Bis der tatsächliche Indikator, seine Einstellungen und ausreichend reale Bastian-Referenzen vorliegen, enthält es bewusst Aufnahme-, Prüf- und Freeze-Regeln statt erfundener Formeln.

Keine Strategie aus einem anderen Projekt darf als Ersatz dienen.

# A – Originalindikator aufnehmen

Nach Registrierung werden, soweit rechtmäßig zugänglich, dokumentiert:

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
| Arbeitstitel | Bitbull / TradeMania / Bastian Keller Indikator |
| exakter Produktname | OFFEN |
| Plattform | OFFEN |
| Publisher | OFFEN |
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

Die Tabelle wird erst anhand des echten Indikators geschlossen:

| Originalereignis | Botzustand vorher | Botaktion | Gültigkeit | Status |
|---|---|---|---|---|
| Kaufsignal | flat | OFFEN | OFFEN | OFFEN |
| Kaufsignal | long | OFFEN | OFFEN | OFFEN |
| Verkaufssignal | long | OFFEN | OFFEN | OFFEN |
| Verkaufssignal | flat | OFFEN | OFFEN | OFFEN |
| kein Signal | beliebig | OFFEN | OFFEN | OFFEN |

Explizit zu klären:

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
- Originalzustand und Marker;
- Alertzustand soweit vorhanden;
- Screenshot-/Export-/Source-Referenz;
- Bot-Sollzustand.

Ziel ist eine ausreichend starke, reproduzierbare Paritätsbasis, vorzugsweise mindestens 1.000 aufeinanderfolgende Bars je Referenzmarkt, soweit die Indikatorplattform dies praktisch erlaubt.

# F – Bastian-Keller-Live-/Content-Schicht

## Quellenklassen

| Origin | Bedeutung | Unmittelbar handelbar? |
|---|---|---|
| `BTK_INDICATOR` | Originalindikator | erst nach Freeze |
| `BASTIAN_YOUTUBE_LIVE` | aktuelle Live-Aussage von Bastian | nur validiert |
| `BASTIAN_YOUTUBE_UPDATE` | veröffentlichtes Marktupdate | nur innerhalb Freshness |
| `BASTIAN_TELEGRAM` | offizieller Kanal/Ankündigung/Markthinweis | nur nach eingefrorener Regel |
| `TRADEMANIA_MEMBER_CONTENT_BASTIAN` | rechtmäßig zugänglicher Bastian-Inhalt | nur nach eingefrorener Regel |
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
9. **Fusion:** eingefrorene Beziehung zwischen Bastian und Indikator anwenden.
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
- Fusionsregel mit dem Indikator.

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

- `INDICATOR_PRIMARY`: Indikator handelt, Bastian bestätigt/blockiert/managed;
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
