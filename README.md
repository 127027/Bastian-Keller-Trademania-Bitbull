# Bastian Keller / TradeMania / Bitbull – Trading-Bot

Dieses Repository ist die **eigenständige Projektbasis** für den Bastian-Keller-/TradeMania-/Bitbull-Trading-Bot.

## Zielbild

Der Bot soll 24/7 laufen und zwei Strategiequellen zusammenführen:

1. den rechtmäßig bereitgestellten TradeMania-/Bastian-Keller-Indikator;
2. eindeutige, aktuelle Aussagen von **Bastian Keller** aus freigegebenen offiziellen Live-/Update-Quellen.

Eine Aussage von Bastian wird niemals allein deshalb gehandelt, weil sie positiv oder negativ klingt. Der vollständige Pfad lautet:

`Quelle erkennen -> Live/Update erfassen -> Sprecher/Asset/Aussage strukturieren -> Freshness/Konflikt prüfen -> ggf. Bedingung beobachten -> mit Indikator/Fusionsregel auswerten -> Risk/Capital Guard -> Order Intent -> Börsenorder -> Audit`

Replays, alte Videos, Zuschauerfragen, Aussagen anderer Mentoren und mehrdeutige/unsichere Transkripte dürfen keine unbeabsichtigte Order auslösen.

## Fachliche Wahrheit

Die normative Wahrheit liegt in `DMS/`. Solange der echte Indikator, seine Einstellungen und die nach Registrierung zulässigen Member-/Live-Quellen noch nicht vollständig untersucht wurden, bleiben Formeln, Parameter, Signaldefinition, Source-Priorität, Freshness, Reaktionslatenz und das Fusionsmodell ausdrücklich `OFFEN`. Es werden keine Regeln erfunden.

Die offizielle TradeMania-Seite `https://www.trademania.io/about` ist als öffentliche Quelle dokumentiert. Bastian Keller ist die primäre menschliche Strategiequelle dieses Projekts; andere TradeMania-Mentoren werden nicht automatisch gehandelt.

## Aktueller Stand

Der komplette derzeit verfügbare **strategieneutrale Projekt-Unterbau** ist als Ausgangsbasis gespiegelt: `.gitignore`, Backtest-, Config-, Strategy-, `src/`- und `tests/`-Struktur. Strategiespezifisches Material anderer Bots wurde bewusst nicht übernommen.

Der technische Ausgangsstand enthält derzeit noch keinen implementierten Botcode in `src/`. Deshalb gibt es aktuell noch keinen BTK-Bot zu starten. Sobald Indikator und Bastian-Regeln fachlich geschlossen sind, werden vorhandene generische Bot-Komponenten gezielt übernommen bzw. angepasst – ohne unnötigen Strukturumbau.

## Arbeitsreihenfolge

1. DMS und öffentliche Quellen vollständig vorbereiten.
2. Nach Registrierung Originalindikator, Version, Settings, Alerts und zulässige Member-Quellen erfassen.
3. Mehrere reale Bastian-Lives/Updates beobachten und Source-Ereignisse mit Zeit, Sprecher, Asset, Aussageklasse, Bedingungen, Revisionen und Freshness labeln.
4. Technisch/rechtlich zulässigen Echtzeitpfad bestimmen: z. B. offizielle Untertitel/Transkript/API oder andere freigegebene Erfassungsmethode. Keine Umgehung von Zugriffsschutz.
5. Live-Reaktionspipeline testen: Streamstart, Capture, Parser, Unsicherheit, konditionale Aussagen, Meinungswechsel, Streamende und Source-Ausfall.
6. `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` vollständig schließen und `BTK-INDICATOR-SPEC-1.0` einfrieren.
7. Strategiespezifischen Botcode minimal auf BTK/TradeMania/Bastian anpassen.
8. Indicator-Parity, Bastian-Source-Replay, Backtests und 24/7-Paper durchführen.
9. Unter identischen Daten-, Kosten-, Kapital- und Paper-Bedingungen gegen den separat betriebenen Referenzbot vergleichen.
10. Live erst nach separatem Freigabegate.

## Vergleichsziel

Der spätere Vergleich entscheidet nicht allein nach Bruttogewinn. Beide Bots werden unter derselben Markt-, Kosten-, Kapital- und Zeitbasis beurteilt nach **Netto-PnL, Netto-PnL/Tag, Drawdown, Profit Factor, Kosten, Kapitalnutzung, Stabilität, Source-/Execution-Latenz und technischer Zuverlässigkeit**.

## Grundsatz

Dieses Repository ist **kein umbenannter Alt-Bot**. Es besitzt eine eigene fachliche Wahrheit für **Bastian Keller / TradeMania / Bitbull**. Wiederverwendet werden nur strategiespezifisch neutrale technische Komponenten. Jede Handelsregel muss aus dem neuen Indikator, bestätigter Bastian-Evidence oder einer ausdrücklich freigegebenen BTK-Entscheidung stammen.
