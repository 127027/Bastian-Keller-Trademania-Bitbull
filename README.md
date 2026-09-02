# Bastian Keller / TradeMania / Bitbull – Trading-Bot

Dieses Repository ist die **eigenständige Projektbasis** für den Bastian-Keller-/TradeMania-/Bitbull-Trading-Bot.

## Zielbild

Der Bot soll 24/7 laufen und zwei Strategiequellen zusammenführen:

1. einen bewusst ausgewählten, rechtmäßig zugänglichen TradeMania-/Bitbull-Indikator bzw. minimalen Indikatorstack;
2. eindeutige, aktuelle Aussagen von **Bastian Keller** aus freigegebenen offiziellen Live-/Update-Quellen.

Eine Aussage von Bastian wird niemals allein deshalb gehandelt, weil sie positiv oder negativ klingt. Der vollständige Pfad lautet:

`Quelle erkennen -> Live/Update erfassen -> Sprecher/Asset/Aussage strukturieren -> Freshness/Konflikt prüfen -> ggf. Bedingung beobachten -> mit Indikator/Fusionsregel auswerten -> Risk/Capital Guard -> Order Intent -> Börsenorder -> Audit`

Replays, alte Videos, Zuschauerfragen, Aussagen anderer Mentoren und mehrdeutige/unsichere Transkripte dürfen keine unbeabsichtigte Order auslösen.

## Aktuell verifizierter Indikator-Kandidat

Öffentlich verifiziert ist der TradingView-Indikator **`Trademania - PVSRA Indicator`** des Publishers `BitbullTrading`.

Öffentlich beschriebene Bestandteile sind u. a.:

- PVSRA-/Vector-Candles;
- Imbalance-Zonen;
- Markt-Sessions und High/Lows;
- integrierte/konfigurierbare EMAs;
- Pivot- und M-/50%-Levels;
- POC;
- WIL;
- ADR/AWR und Vorperioden-High/Lows;
- Daily Open;
- Lite Mode.

Der Script-Source ist geschützt/closed source. Deshalb wird keine intern unbekannte Formel erfunden. Der Kandidat wird bei Bedarf über beobachtbare Referenzparität getestet.

**Wichtig:** PVSRA ist derzeit Kandidat Nr. 1, aber noch **nicht** automatisch der finale BTK-Indikator.

## Member-Inventar – jetzt verfügbar, noch auszuwerten

Der Eigentümer ist inzwischen bei TradeMania registriert und hat Zugang zu:

- TradeMania Discord / Live-/Memberbereichen;
- `https://trademania.app/bots`;
- Indicator-/Strategie-Indicator-Masterclass und weiteren freigeschalteten Inhalten, soweit im Account sichtbar.

Vor dem Strategie-Freeze wird dort ein vollständiges Inventar erstellt. Geschützte Member-Rohinhalte werden nicht in dieses öffentliche Repository kopiert; dokumentiert werden eigene Spezifikationen, Namen/Versionen, Settings, Hashes, erlaubte Referenzen und technische Erkenntnisse.

## Auswahlprinzip

Wir bauen **keinen Indikator-Weihnachtsbaum**. V1 bekommt den kleinsten reproduzierbaren Stack, den Bastian aktuell tatsächlich nutzt und der für ETH bzw. unser Startuniversum technisch sinnvoll ist.

Entscheidend sind:

- aktuelle Nutzung durch Bastian;
- ETH-Eignung;
- eindeutige/reproduzierbare Zustände oder Levels;
- Repainting-/Reload-Verhalten;
- Alerts/Webhooks/Black-Box-Parität;
- Backtestbarkeit;
- Live-Latenz;
- rechtmäßige Nutzung;
- zusätzlicher Mehrwert statt Redundanz;
- Forward-Paper-Ergebnis.

Öffentlich belegte Ergänzungen wie **MACD, POC/VRVP/VPVR und RSI** werden nur übernommen, wenn aktuelle Bastian-Evidence ihre konkrete Rolle bestätigt.

## Fachliche Wahrheit

Die normative Wahrheit liegt in `DMS/`. Solange Zielindikator, Settings und Member-/Live-Quellen noch nicht vollständig untersucht wurden, bleiben Formeln, Parameter, Signaldefinition, Source-Priorität, Freshness, Reaktionslatenz und das Fusionsmodell ausdrücklich `OFFEN`. Es werden keine Regeln erfunden.

Die öffentliche Quellen- und Kandidatenlage ist in `DMS/22_QUELLEN_UND_BINANCE_PRUEFUNG.md` dokumentiert. Die normative Auswahl-/Strategieaufnahme steht in `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md`.

Bastian Keller ist die primäre menschliche Strategiequelle dieses Projekts; andere TradeMania-Mentoren werden nicht automatisch gehandelt.

## Aktueller technischer Stand

Der komplette derzeit verfügbare **strategieneutrale Projekt-Unterbau** ist als Ausgangsbasis gespiegelt: `.gitignore`, Backtest-, Config-, Strategy-, `src/`- und `tests/`-Struktur. Strategiespezifisches Material anderer Bots wurde bewusst nicht übernommen.

Der technische Ausgangsstand enthält derzeit noch keinen implementierten BTK-Botcode in `src/`. Erst wenn Zielindikator und Bastian-Regeln fachlich geschlossen sind, werden vorhandene generische Bot-Komponenten gezielt übernommen bzw. angepasst – ohne unnötigen Strukturumbau.

## Arbeitsreihenfolge

1. DMS und öffentliche Quellen vollständig vorbereiten.
2. Öffentliches + Member-Indikator-/Bot-Inventar erstellen.
3. PVSRA und andere reale Kandidaten gegen aktuelle Bastian-Nutzung und ETH-Eignung prüfen.
4. Finalen Zielindikator/minimalen Stack bewusst auswählen.
5. Version, Settings, Alerts, Timeframes, Repainting und Referenzfälle vollständig aufnehmen.
6. Mehrere reale Bastian-Lives/Updates beobachten und Source-Ereignisse mit Zeit, Sprecher, Asset, Aussageklasse, Bedingungen, Revisionen und Freshness labeln.
7. Technisch/rechtlich zulässigen Echtzeitpfad bestimmen: z. B. offizielle Untertitel/Transkript/API oder andere freigegebene Erfassungsmethode. Keine Umgehung von Zugriffsschutz.
8. Live-Reaktionspipeline testen: Streamstart, Capture, Parser, Unsicherheit, konditionale Aussagen, Meinungswechsel, Streamende und Source-Ausfall.
9. `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` vollständig schließen und `BTK-INDICATOR-SPEC-1.0` einfrieren.
10. Strategiespezifischen Botcode minimal auf BTK/TradeMania/Bastian anpassen.
11. Indicator-Parity, Bastian-Source-Replay, Backtests und 24/7-Paper durchführen.
12. Unter identischen Daten-, Kosten-, Kapital- und Paper-Bedingungen gegen den separat betriebenen Referenzbot vergleichen.
13. Live erst nach separatem Freigabegate.

## Vergleichsziel

Der spätere Vergleich entscheidet nicht allein nach Bruttogewinn. Beide Bots werden unter derselben Markt-, Kosten-, Kapital- und Zeitbasis beurteilt nach **Netto-PnL, Netto-PnL/Tag, Drawdown, Profit Factor, Kosten, Kapitalnutzung, Stabilität, Source-/Execution-Latenz und technischer Zuverlässigkeit**.

## Grundsatz

Dieses Repository ist **kein umbenannter Alt-Bot**. Es besitzt eine eigene fachliche Wahrheit für **Bastian Keller / TradeMania / Bitbull**. Wiederverwendet werden nur strategiespezifisch neutrale technische Komponenten. Jede Handelsregel muss aus dem final ausgewählten Indikator, bestätigter Bastian-Evidence oder einer ausdrücklich freigegebenen BTK-Entscheidung stammen.
