# 03 – Normative Strategie: Bitbull / TradeMania / Bastian Keller

Status: `OFFEN / VORBEREITET`.

Vorgesehene erste eingefrorene Strategieversion: `BTK-INDICATOR-SPEC-1.0`.

## Zweck

Dieses Dokument wird die **einzige normative technische Referenz** für die BTK-Strategie. Bis der tatsächliche Indikator, seine Einstellungen und ausreichend reale Bastian-Referenzen vorliegen, enthält es bewusst Aufnahme-, Prüf- und Freeze-Regeln statt erfundener Formeln.

Keine Strategie aus einem anderen Projekt darf als Ersatz dienen.

## A – Originalindikator aufnehmen

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

### Identität

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

### Inputs

Jeder sichtbare Input wird mit Typ, Default, Einheit, erlaubten Werten und Signalrelevanz erfasst. Es werden **keine** Defaults aus ähnlichen Indikatoren übernommen.

## B – Timeframe, Daten und Repainting

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

## C – Signal- und Positionsabbildung

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

## D – Simultane Signale und drei Slots

Wenn mehr als drei gültige Entries gleichzeitig vorliegen, braucht V1 eine deterministische Priorität. Zulässige Quellen sind z. B. ein Indikator-Score, definierte Signalstärke oder eine vor dem Backtest festgelegte neutrale Regel. Fremde Priorisierungsregeln werden nicht ungeprüft übernommen.

## E – Golden-/Referenzverfahren

Je Referenzbar werden mindestens gespeichert:

- Symbol und Timeframe;
- UTC-Barzeit;
- OHLCV;
- sichtbare/ableitbare Indikatorwerte;
- Originalzustand und Marker;
- Alertzustand soweit vorhanden;
- Screenshot-/Export-/Source-Referenz;
- Bot-Sollzustand.

Ziel ist eine ausreichend starke, reproduzierbare Paritätsbasis, vorzugsweise mindestens 1.000 aufeinanderfolgende Bars je Referenzmarkt.

# F – Bastian-Keller-Live-/Content-Schicht

## Quellenklassen

| Origin | Bedeutung | Unmittelbar handelbar? |
|---|---|---|
| `BTK_INDICATOR` | Originalindikator | erst nach Freeze |
| `BASTIAN_YOUTUBE_LIVE` | aktuelle Live-Aussage von Bastian | nur validiert |
| `BASTIAN_YOUTUBE_UPDATE` | veröffentlichtes Marktupdate | nur innerhalb Freshness |
| `BASTIAN_TELEGRAM` | offizieller Kanal/Ankündigung/Markthinweis | nur nach Regel |
| `TRADEMANIA_MEMBER_CONTENT_BASTIAN` | rechtmäßig zugänglicher Bastian-Inhalt | nur nach Regel |
| `TRADEMANIA_OTHER_MENTOR` | anderer Mentor | nein, bis ausdrücklich freigegeben |

## Struktur eines Bastian-Ereignisses

```text
source_event_id
origin
source_url_or_private_ref
published_at_utc
received_at_utc
spoken_at_utc_or_offset
speaker = Bastian Keller
asset_symbols[]
statement_class = CONTEXT | WATCH | ENTRY | EXIT | REDUCE | INVALIDATION | TARGET | RISK | UNKNOWN
side = LONG | SHORT | FLAT | UNKNOWN
price_or_zone
condition
horizon
freshness_deadline
confidence
content_hash_or_private_ref
derived_summary
decision_rule_version
```

Rohtranskripte und geschützte Schulungsinhalte bleiben außerhalb des öffentlichen Repositories.

## Wann eine Aussage NICHT gehandelt wird

Keine automatische Order bei:

- reinem Szenario „wenn … dann …“, solange die Bedingung nicht erfüllt ist;
- historischer Trade-Beschreibung;
- Zuschauerfrage;
- Kommentar über fremden Trade/anderen Mentor;
- bloßer Watch-Zone;
- mehreren Alternativen ohne Priorität;
- Aussage, die später im selben Stream revidiert wurde;
- verspätetem Replay ohne aktuelle Gültigkeit.

## `BASTIAN_ACTIONABLE_SIGNAL`

Ein Bastian-Signal benötigt mindestens:

1. Bastian eindeutig als Sprecher;
2. eindeutig identifizierbares Asset;
3. eindeutige Aktion oder deterministisch prüfbare Bedingung;
4. gültigen Zeitkontext/Freshness;
5. keine aktuellere widersprechende Aussage;
6. bestandene Risiko-, Kapital-, Exchange- und Source-Health-Guards.

## G – Indikator + Bastian: Fusionsmodell

Die endgültige Priorität wird erst nach echten Beispielen eingefroren. Zu prüfen sind:

- `INDICATOR_PRIMARY`: Indikator handelt, Bastian bestätigt/blockiert/managed;
- `BASTIAN_PRIMARY`: Bastian primär, Indikator als Timing/Bestätigung;
- `DUAL_CONFIRMATION`: Entry nur bei Übereinstimmung;
- `SOURCE_SPECIFIC`: Bastian darf nur bestimmte Aktionen überschreiben.

Genau **ein** Modell wird nach Replay/Paper-Vergleich für V1 freigegeben.

## H – Freshness und Konflikte

Jeder Bastian-Kontext erhält eine explizite Lebensdauer. Bis echte Beispiele ausgewertet sind, bleibt `freshness_deadline=OFFEN`; alte Aussagen dürfen nicht still weiterwirken.

Bei Konflikten wird nach einer noch festzulegenden Quellenpriorität und Aktualität entschieden. Die Regel muss deterministisch sein und im Audit protokolliert werden.

## I – Reaktionszeit

Der Bot soll offizielle Live-/Update-Inhalte so zeitnah wie technisch und rechtlich möglich erkennen. Die maximal zulässige End-to-End-Latenz wird nach Prüfung der verfügbaren Schnittstellen, Untertitel und Content-Typen festgelegt. Keine Umgehung von Zugriffsschutz wird vorausgesetzt.

## J – Paper-/Replay-Pflicht für Bastian-Inhalte

Vor Live müssen mindestens getestet werden:

- expliziter Entry;
- konditionaler Entry;
- expliziter Exit;
- Teilreduktion/Gewinne sichern;
- Zielzone;
- Invalidation/Stop;
- Meinungswechsel im Live;
- mehrere Coins nacheinander;
- Aussage ohne Preisangabe;
- verspätetes Video/Replay;
- widersprüchliche Quellen.

## Freeze-Kriterien für `BTK-INDICATOR-SPEC-1.0`

Freeze erst wenn:

- Indikatoridentität und Version eindeutig;
- Inputs/Defaults vollständig;
- Timeframe/Datenabhängigkeiten geklärt;
- Signal-/Entry-/Exit-/Pyramiding-Regeln eindeutig;
- Repainting/Bar-Close geprüft;
- Slotpriorität geklärt;
- Referenzfälle reproduzierbar;
- Bastian-Quellen und Speaker-Regel definiert;
- Freshness/Konfliktregel definiert;
- genau ein Fusionsmodell freigegeben;
- keine kritische Strategiefrage mehr `OFFEN` ist.

Erst danach darf Strategiecode umgesetzt werden.