# 05 – Marktdaten und Aktualisierung

Status: `VERBINDLICH` für die Datenplattform; tatsächlicher Strategie-Timeframe, indikatorabhängige Datenquellen und Source-Capture-Details bleiben bis DMS-03-Freeze teilweise `OFFEN`.

## Börsendaten

Primäre Handels-/Execution-Basis ist Binance Spot. Gespeichert werden pro Symbol/Timeframe mindestens Open-/Close-Time UTC, OHLC, Volumen, `closed/provisional`, Datenquelle, Abrufzeit und Import-Batch-ID. Preise und Mengen werden decimal-sicher verarbeitet.

## Indikator-Datenquellen sind separat zu erfassen

Der endgültige Zielindikator darf **nicht automatisch** so behandelt werden, als nutze jede Berechnung dieselbe Börsenquelle wie die spätere Orderausführung.

Vor Strategie-Freeze werden je Indikatorfunktion getrennt dokumentiert:

- Chart-/Preisquelle;
- Volumen-/Tick-Volumenquelle;
- mögliche Cross-Exchange-/Volume-Overrides;
- Spot vs Futures/Perpetual als Datenbasis;
- Sessionkalender/Zeitzone/DST;
- Footprint-/POC-Datenquelle und Auflösung, falls benötigt;
- externe Zusatzdaten;
- Timeframe und Aggregationsmethode;
- Symbolmapping zwischen Provider und Binance Spot.

Der öffentlich verifizierte Kandidat `Trademania - PVSRA Indicator` beschreibt ausdrücklich die Möglichkeit, z. B. einen Chart einer Börse zu betrachten und für PVSRA-/Vector-Candles das Volumen einer anderen Börse wie Binance zu verwenden. Falls dieser Kandidat ausgewählt wird, muss das tatsächlich bei Bastian verwendete Source-Mapping als Einstellung/Evidence erfasst werden.

Der öffentliche PVSRA-Kandidat beschreibt außerdem POC-Informationen aus einer Footprint-Berechnung. Es wird **nicht** angenommen, dass diese Werte aus normalen 1h-OHLCV-Daten exakt rekonstruierbar sind. Falls die erforderliche POC-/Footprint-Logik oder Datenbasis nicht rechtmäßig/exakt reproduzierbar ist, wird sie als Black-Box-/externe Referenz behandelt oder aus dem signalrelevanten V1-Pfad ausgeschlossen – niemals angenähert und als exakt ausgegeben.

## Strategie-Timeframe

Es wird kein Timeframe aus einem anderen System automatisch übernommen. Die Datenplattform muss die für den final ausgewählten Indikator/Stack benötigten Timeframes nach DMS 03 vollständig unterstützen. UI-Zeiträume sind keine Trading-Timeframes.

## Historie

Für den reproduzierbaren Indicator-/Marktdatenpfad:

- mindestens drei vollständige Jahre vor Backtestende;
- zusätzlicher Warm-up gemäß DMS 03;
- jede relevante Datenquelle und jedes Symbolmapping je Import festhalten;
- Providerwechsel oder geändertes Source-Mapping erzeugt neuen Datensatzstand.

Für Bastian-Content gilt **keine erfundene Drei-Jahres-Pflicht**. Source-Replay nutzt ausschließlich tatsächlich vorhandene, zeitlich belastbare Evidence. Fehlende historische Live-/Update-Inhalte werden nicht synthetisch ergänzt.

## Startup-Sequenz

1. Konfiguration/Schema validieren.
2. Systemuhr/UTC prüfen.
3. DB-Integrität prüfen.
4. Börsenmetadaten/Filter für alle zehn Paare laden.
5. alle für den eingefrorenen Indikator benötigten Preis-/Volumen-/Zusatzprovider und Source-Mappings laden.
6. Zeitraum, Duplikate, Lücken und OHLC-Konsistenz prüfen.
7. falls separate Volumen-/Footprint-/Sessiondaten erforderlich sind, deren Frische und Mapping separat prüfen.
8. fehlende Bereiche paginiert nachladen.
9. offene Kerze als `provisional` markieren.
10. finale Bars freigeben.
11. nach Strategie-Freeze Indikatorzustand/Warm-up rekonstruieren.
12. Paper/Live: Orders, Fills, Positionen, Salden abgleichen.
13. Source-Allowlist und Source-Adapter-Konfiguration laden.
14. bekannte Source-Sessions/Pending Conditions auf Freshness/Expiry/Revisionslage prüfen.
15. Source Discovery/Capture/Parser-Health prüfen.
16. erst bei gesundem Zustand und bestandenen Gates signalaktive Verarbeitung freigeben.

Historische Signale und verspätete Source-Events werden beim Start nicht als rückwirkende Live-Orders nachgesendet.

## Laufende Marktaktualisierung

- Stream/WebSocket für benötigte Klines/Feeds;
- REST-Fallback und Gap-Recovery;
- finale Bar genau einmal verarbeiten;
- Reconnect mit Backoff/Jitter;
- 90 s ohne erwartetes Streamupdate -> `DEGRADED`;
- erwartete finale Strategiebar >120 s verspätet -> Symbol pausieren/recovern;
- indikatorrelevante Zusatzfeeds erhalten eigene Health-/Freshness-Prüfung.

Intrabar-Handel bleibt deaktiviert, bis DMS 03 ihn ausdrücklich und reproduzierbar verlangt.

## Täglicher Audit

Um **00:05 UTC**:

- alle zehn Paare prüfen;
- fehlende abgeschlossene Bars nachladen;
- Duplikate/Raster/OHLC/Frische validieren;
- indikatorabhängige Zusatzprovider/Source-Mappings prüfen;
- Symbolstatus und Börsenfilter aktualisieren;
- Datenqualitätsreport schreiben;
- abhängige Backtests bei historischen Korrekturen oder geändertem Source-Mapping `STALE` markieren.

Keine synthetischen Kerzen oder angenäherten Indikator-Zusatzdaten ohne ausdrücklich dokumentierte, fachlich freigegebene Methodik.

## Content-/Source-Datenstrom

Neben Marktdaten verarbeitet das System freigegebene Bastian-/TradeMania-Quellenereignisse. Contentzeit und Börsenzeit bleiben getrennte Zeitachsen.

### Source Session

Mindestens:

- `session_id`;
- Origin/Provider;
- eindeutige Source-/Channel-ID;
- URL/private reference;
- Status `SCHEDULED|LIVE|ENDED|REPLAY|STALE|UNAVAILABLE|UNKNOWN`;
- angekündigte/erkannte Start-/Endzeit UTC;
- allowlist version;
- capture mode/version;
- source health.

### Source Event

Mindestens:

- immutable `source_event_id`;
- `session_id`;
- Origin und Source-ID/URL/private Referenz;
- Published-Time;
- Received-Time;
- Spoken-Time oder Streamoffset soweit bestimmbar;
- Live/Replay/Update-Status;
- Sprecher;
- Assetbezug;
- Aussageklasse;
- Bedingung/Zone soweit relevant;
- Content-Hash/private Referenz;
- Capture-/Parser-/Validation-Version und Status;
- Freshness deadline;
- Revision/Supersede-/Conflict-Referenz;
- gemessene Source-/Capture-/Parser-Latenz.

Roh-Capture und strukturierte Strategieentscheidung werden getrennt persistiert.

## Source Discovery und Terminfindung

Der Bot darf keinen Wochenplan als ewige Strategie-Wahrheit hardcoden. Öffentliche Terminankündigungen und Plattform-Metadaten werden über allowgelistete offizielle Quellen dynamisch beobachtet, soweit technisch/rechtlich zulässig. Aktuell recherchierte Routinen in DMS 22 sind nur Erwartungsfenster.

Wenn ein angekündigter Stream nicht startet oder technisch nicht auswertbar ist:

- entstehen keine synthetischen Aussagen;
- Source-/Capture-Layer wird `DEGRADED`;
- stale Kontexte werden nicht still verlängert;
- Drittzusammenfassungen ersetzen die Originalquelle nicht.

## Pending Conditions und Marktfeed

Konditionale Bastian-Aussagen werden erst nach DMS-03-Freeze als `PENDING_CONDITION` gegen den dafür eingefrorenen Marktfeed geprüft. Ein Trigger ist nur zulässig, wenn:

- verwendeter Marktfeed gesund ist;
- Symbol/Timeframe/Operator/Zone eindeutig sind;
- Condition noch frisch und nicht invalidiert ist;
- keine neuere Bastian-Revision entgegensteht;
- die Fusionsregel den Trigger zulässt.

Ein Daten-Gap oder stale Feed darf keine Condition blind erfüllen.

## Zeitwahrheit

Börsenzeit, Indikator-Providerzeit, Source-Published-Time, Received-Time und Spoken-Time werden niemals gleichgesetzt. Für chronologische Replays und Live-Entscheidungen darf nur Information verwendet werden, die zum jeweiligen Entscheidungszeitpunkt bereits tatsächlich verfügbar war.
