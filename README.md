# Bastian Keller / TradeMania / Bitbull – Trading-Bot

Dieses Repository ist die **eigenständige Projektbasis** für den Bastian-Keller-/TradeMania-/Bitbull-Trading-Bot.

Ziel ist ein 24/7-System, das den rechtmäßig bereitgestellten TradeMania-/Bastian-Keller-Indikator auswertet und – nach separater Validierung – eindeutige, aktuelle Aussagen von Bastian Keller aus offiziellen Live-/Update-Quellen in strukturierte Handelsentscheidungen einbeziehen kann.

Die normative Wahrheit liegt in `DMS/`. Solange der echte Indikator und die zulässigen Member-/Live-Evidenzen fehlen, bleiben Formeln, Parameter, Signaldefinition, Freshness und die Fusion mit Bastian-Aussagen ausdrücklich `OFFEN`. Es werden keine Regeln erfunden.

## Aktueller Stand

Der komplette derzeit verfügbare **strategieneutrale Projekt-Unterbau** wurde als Ausgangsbasis gespiegelt: `.gitignore`, Backtest-, Config-, Strategy-, `src/`- und `tests/`-Struktur. Strategiespezifisches Material anderer Bots wurde bewusst nicht übernommen.

Der derzeitige technische Ausgangsstand enthält noch keinen implementierten Botcode in `src/`; deshalb gibt es aktuell auch in diesem Repository noch keinen BTK-Botcode zu starten. Sobald der echte Indikator und die Bastian-Regeln fachlich geschlossen sind, wird der vorhandene/weiterentwickelte neutrale Bot-Unterbau gezielt übernommen bzw. angepasst, ohne unnötigen Strukturumbau.

## Arbeitsreihenfolge

1. DMS vollständig vorbereiten und öffentliche Quellen dokumentieren.
2. Nach Registrierung Indikator, Settings, Alerts und zulässige Member-Quellen erfassen.
3. Mehrere reale Bastian-Lives/Updates manuell labeln und die Entscheidungslogik ableiten.
4. `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` vollständig schließen und `BTK-INDICATOR-SPEC-1.0` einfrieren.
5. Den strategiespezifischen Botcode minimal auf BTK/TradeMania/Bastian anpassen.
6. Referenz-/Source-Replay, Backtests und 24/7-Paper durchführen.
7. Unter identischen Daten-, Kosten-, Kapital- und Paper-Bedingungen gegen den separat betriebenen Referenzbot vergleichen.
8. Live erst nach separatem Freigabegate.

## Grundsatz

Dieses Repository ist kein umbenannter Alt-Bot. Es besitzt eine eigene fachliche Wahrheit für **Bastian Keller / TradeMania / Bitbull**. Bestehende technische Komponenten dürfen wiederverwendet werden, sofern sie strategiespezifisch neutral sind und den DMS entsprechen.

Der spätere Vergleich entscheidet nicht allein nach Bruttogewinn, sondern nach **Netto-PnL, Netto-PnL/Tag, Drawdown, Stabilität, Kosten, Kapitalnutzung und technischer Zuverlässigkeit**.
