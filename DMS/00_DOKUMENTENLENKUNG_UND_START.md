# 00 – Dokumentenlenkung und Start

## Zweck

Dieses DMS ist die maßgebliche Produktspezifikation für den eigenständigen **Bitbull / TradeMania / Bastian Keller** Trading-Bot.

Der strategieneutrale technische Projekt-Unterbau ist bereits als Ausgangsbasis in dieses Repository gespiegelt. Botarchitektur, Datenhaltung, Backtestprinzipien, Paper-/Live-Trennung, Kapitalmodell, Orderzustände, Sicherheitsmechanismen, UI-Grundsätze, Recovery, Audit und Tests werden wiederverwendet, soweit sie strategiespezifisch neutral sind und die neue Strategie keine fachlich zwingende Abweichung erfordert.

Dieses DMS ist aktuell eine **vorbereitete Spezifikation**. Es darf noch keine konkrete Bastian-Keller-Indikatorlogik oder Sprachregel erfinden. Erst nach rechtmäßigem Erhalt des tatsächlichen Indikators, seiner Einstellungen und geeigneter Live-/Update-Referenzen wird Dokument 03 vollständig geschlossen und die Strategieversion eingefroren.

## Repositorybasis

- Repository: `127027/Bastian-Keller-Trademania-Bitbull`
- Hauptzweig: `main`
- fachliche Projektkennung: `BTK`
- Strategie-Freeze: `BTK-INDICATOR-SPEC-1.0` erst nach vollständiger Evidenz

Dieses Repository ist die eigenständige Wahrheit für das Bastian-Keller-/TradeMania-/Bitbull-System. Keine frühere oder fremde Strategiespezifikation gilt hier automatisch.

## Geltungsbereich

Die Dokumentation deckt ab:

- Erfassung und exakte Spezifikation des neuen Indikators;
- 24/7-Erkennung und Verarbeitung freigegebener offizieller Bastian-Keller-Live-/Update-Quellen;
- Source-Session-Lifecycle: angekündigt, live, beendet, Replay, stale;
- technisch/rechtlich zulässige Erfassung über verfügbare offizielle Metadaten, Untertitel, Transkripte, APIs oder andere freigegebene Wege;
- Sprecher-, Asset-, Aussage-, Freshness-, Revisions- und Konfliktprüfung;
- konditionale Aussagen als wartende Regeln, die erst bei bestätigter Marktbedingung auslösen dürfen;
- Fusion von Indikator und Bastian-Kontext nach genau einer eingefrorenen Regel;
- zehn Kryptowährungspaare auf Binance Spot;
- Einzel- und Portfoliobacktests mit klaren Annahmen;
- Marktdatenbeschaffung, Lückenprüfung und tägliche Aktualisierung;
- Order-, Kapital- und Sicherheitsregeln;
- Live-/Paper-UI mit Heute, 1 Woche, 1 Monat, 1 Jahr und 3 Jahre;
- Architektur, Datenmodell, Betrieb, Wiederanlauf, Monitoring und Recovery;
- Tests, Abnahme und Nachvollziehbarkeit;
- späteren kontrollierten Umbau des Botcodes erst nach Strategie-Freeze;
- fairen späteren Vergleich mit einem separat betriebenen Referenzbot unter identischen Bedingungen.

## Rangfolge der Quellen

Bei Widerspruch gilt:

1. schriftlich vom Eigentümer freigegebene Entscheidung im Entscheidungslog;
2. die eingefrorene normative Strategie in Dokument 03;
3. DMS-Dokumente mit Status `VERBINDLICH`;
4. rechtmäßig verfügbarer Originalindikator, Einstellungen, Alertdefinitionen und ggf. Quellcode/Hash als Referenzquelle;
5. vom Eigentümer bereitgestellte Screenshots, Exporte und reproduzierbare Referenzbeobachtungen;
6. offizielle Inhalte von Bitbull/TradeMania/Bastian Keller, z. B. Dokumentation, öffentliche oder rechtmäßig zugängliche Schulungsunterlagen, Videos, Livestreams und Marktupdates;
7. sonstige Kommentare, Beispiele und Interpretationen.

Öffentliche Videos oder Live-Aussagen sind Forschungs- und Strategiereferenzen, aber keine stille Erlaubnis, fehlende technische Details zu erfinden.

## Dokumentstatus

| Status | Bedeutung |
|---|---|
| VERBINDLICH | freigegebene Soll-Vorgabe |
| ANNAHME | Arbeitsannahme, die bestätigt oder ersetzt werden muss |
| OFFEN | Entscheidung oder Quelle fehlt |
| NACHWEIS AUSSTEHEND | Vorgabe ist definiert, aber noch nicht durch Artefakt/Test belegt |
| VERWORFEN | darf nicht implementiert werden |

Aktueller Paketstatus: **BTK-DMS PREPARED / STRATEGIE OFFEN**.

Die BTK-Projektstruktur ist vorbereitet. Die neue Indikator- und Bastian-Live-Strategie ist noch nicht eingefroren, weil Originalindikator und vollständige Source-Evidence noch fehlen. Deshalb dürfen noch kein signalaktiver BTK-Paper-/Live-Betrieb und keine Performanceaussage daraus abgeleitet werden.

## Dokumentenkarte

| Datei | Inhalt |
|---|---|
| `01_PRODUKTVISION_SCOPE.md` | Ziel, Grenzen und Nutzerrollen |
| `02_VERBINDLICHE_ANFORDERUNGEN.md` | funktionale und nichtfunktionale Anforderungen |
| `03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` | normative Strategieaufnahme, Live-Source-Pipeline und spätere Signaldefinition |
| `04_MARKT_KAPITAL_RISIKO.md` | Märkte, Kapital und Schutzregeln |
| `05_MARKTDATEN_UND_AKTUALISIERUNG.md` | Daten, Lücken, Startup und Update |
| `06_BACKTEST_UND_VALIDIERUNG.md` | Signalparität, Source-Replay, Backtest, Kosten und Vergleich |
| `07_AUSFUEHRUNG_ORDERS.md` | Signal-zu-Order-Lebenszyklus |
| `08_UI_UX_SPEZIFIKATION.md` | Screens, Charts, Source-Status und Bedienregeln |
| `09_SYSTEMARCHITEKTUR_DATENMODELL.md` | Komponenten, Zustände und persistente Daten |
| `10_BETRIEB_MONITORING_RECOVERY.md` | 24/7-Betrieb, Source-Monitoring, Logs, Backup, Störungen |
| `11_SICHERHEIT_COMPLIANCE.md` | Schlüssel, Rechte, Audit und Quellenrechte |
| `12_TESTS_ABNAHMEKRITERIEN.md` | Testpyramide und Freigabegates |
| `13_KONFIGURATION_UND_SCHEMATA.md` | Konfigurationsfelder und Validierung |
| `14_BUILD_PLAN_UND_DEFINITION_OF_DONE.md` | Umsetzungsreihenfolge |
| `15_TRACEABILITY_MATRIX.md` | Anforderung → Test → Artefakt |
| `16_ENTSCHEIDUNGSLOG_UND_OFFENE_PUNKTE.md` | zentrale Beschlüsse und offene Strategiefragen |
| `17_GLOSSAR.md` | eindeutige Begriffe |
| `18_BACKTEST_STATUS_UND_ERGEBNISFORMAT.md` | Ist-Stand und Ergebnisformat |
| `19_RISIKOREGISTER.md` | fachliche, technische und betriebliche Restrisiken |
| `20_BETRIEBSRUNBOOK.md` | Bedien- und Störungsabläufe |
| `21_GITHUB_ZUSAMMENARBEIT.md` | Repository-, Branch-, Review- und Merge-Regeln |
| `22_QUELLEN_UND_BINANCE_PRUEFUNG.md` | Quellenkatalog, öffentliche TradeMania-Basis und Börsenprüfung |
| `23_ORDNERSTRUKTUR_UND_EINSTIEGSPUNKT.md` | Projektstruktur und technischer Einstieg |

## Änderungsprozess

1. Jede fachliche Änderung erhält eine `BTK-DEC-xxx`-ID.
2. Betroffene Anforderungen und Tests werden aktualisiert.
3. Sobald die neue Strategie eingefroren ist, erhöht jede Änderung an ihrer Logik die Strategieversion und invalidiert betroffene Backtests/Replays.
4. Ein Backtest/Replay nennt immer Code-/Buildversion, Strategiehash, Konfigurationshash, Datenhash, Source-Evidence-Version und Kostenmodell.
5. Nur bestätigte Strategieelemente dürfen implementiert werden.
6. Erst wenn Dokument 03 keine kritische Strategiefrage mehr auf `OFFEN` enthält, beginnt der signalaktive Codeumbau.

## Nichtverhandelbare Wahrheitsregeln

- Keine erfundenen Indikatorformeln oder Parameter.
- Keine erfundenen Bastian-Aussagen oder Bedeutungen.
- Keine erfundenen Backtestwerte.
- Keine Ergebnisgarantie oder Renditezusage.
- Kein Look-ahead oder stilles Repainting.
- Keine heimliche Optimierung auf Wunschprofit.
- Keine Order aus einem unsicheren, mehrdeutigen oder nicht ausreichend frischen Source-Ereignis.
- Kein Replay oder altes Video wird als aktuelles Live-Signal behandelt.
- Ein blockierter Trade muss mit Ursache protokolliert werden.
- Der neue Indikator wird erst implementiert, wenn seine beobachtbare und/oder technische Signaldefinition reproduzierbar dokumentiert ist.

## Bastian-Keller-Quellenmodell

Diese Variante ist fachlich nicht nur ein Indikatorwechsel. Sie bildet eine **Bastian-Keller-Strategiequelle** ab, bestehend aus:

1. dem rechtmäßig bereitgestellten TradeMania-/Bastian-Keller-Indikator;
2. offiziellen Aussagen von Bastian Keller in Live-Tradings, Marktupdates und freigegebenen Community-/Member-Inhalten;
3. daraus reproduzierbar abgeleiteten, versionierten Handelsregeln.

Der Bot darf eine Aussage nicht deshalb handeln, weil sie lediglich positiv oder negativ klingt. Eine sprachliche Aussage wird erst zu einem `BASTIAN_ACTIONABLE_SIGNAL`, wenn Sprecher, Instrument, Aktion/Bedingung, zeitlicher Kontext und Freshness eindeutig genug sind und die in DMS 03 definierten Validierungsregeln erfüllen.

**Primärperson ist Bastian Keller.** Aussagen anderer TradeMania-Mentoren werden nicht automatisch als Bastian-Signal behandelt. Eine spätere Erweiterung benötigt eine eigene Entscheidung.

Der Bot läuft 24/7. Marktfeed, Quellenmonitoring und Indikator laufen unabhängig davon, ob Bastian gerade live ist. Neue Bastian-Aussagen können den aktuell gültigen Strategiekontext aktualisieren oder ersetzen. Wie lange ein Kontext gilt und ob er Indikatorsignale bestätigt, blockiert, ersetzt oder selbst Orders auslösen darf, wird nach Beobachtung der echten Inhalte in DMS 03 verbindlich festgelegt.

## Verbindlicher Echtzeitpfad nach Strategie-Freeze

Nach Freigabe muss jede Bastian-Reaktion diese Reihenfolge durchlaufen:

1. erlaubte offizielle Quelle/Session erkennen;
2. Live/Update/Replay-Status und Zeit erfassen;
3. Bastian als Sprecher validieren;
4. Inhalt über den zulässigen Capture-Pfad erfassen;
5. Asset, Aussageklasse, Richtung/Aktion, Preis/Zone und Bedingung strukturieren;
6. Unsicherheit, Freshness und widersprechende neuere Aussagen prüfen;
7. konditionale Regeln gegebenenfalls als `PENDING_CONDITION` weiterbeobachten;
8. Fusionsregel mit Indikator anwenden;
9. Risk-, Capital-, Exchange- und Price-Deviation-Gates prüfen;
10. erst danach `EXECUTION_INTENT` erzeugen und vollständig auditieren.

Kein Rohtranskript, keine automatische Zusammenfassung und kein einzelner Confidence-Wert ist allein eine Orderautorität.
