# 01 – Produktvision und Scope

Status: `VERBINDLICH` für den technischen Unterbau; Strategiequelle `OFFEN` bis DMS 03 eingefroren ist.

## Produktziel

Dieses Repository beschreibt einen eigenständigen **Bastian-Keller-/TradeMania-/Bitbull-Trading-Bot**. Der Bot soll den künftig bereitgestellten Originalindikator deterministisch auswerten, Bastian-Keller-Lives und offizielle Updates nach klaren Regeln als Kontext verarbeiten, historische Daten reproduzierbar backtesten, Paper-/Live-Orders verwalten und sämtliche Entscheidungen auditierbar anzeigen.

Der technische Unterbau wird nicht unnötig neu erfunden. Bewährte generische Komponenten aus dem bereits existierenden Bot dürfen nach dem Strategie-Freeze gezielt übernommen werden.

## Erfolgsbild

Ein fachkundiger Dritter kann später:

- erklären, wann Indikator oder Bastian-Quelle ein handelbares Signal erzeugt;
- Botreaktionen mit Originalindikator und gelabelten Referenz-Lives vergleichen;
- denselben Backtest reproduzieren;
- jede Order auf Signal, Quelle, Zeit, Konfiguration und Bot-Version zurückführen;
- Daten-/Source-Ausfälle erkennen;
- nach Neustart ohne Doppelorder fortsetzen;
- nachvollziehen, warum eine Order ausgeführt, blockiert oder verworfen wurde.

## Enthalten

- zehn Binance-Spot-Paare gegen USDT: BTC, ETH, BNB, SOL, XRP, ADA, LINK, AVAX, DOT, DOGE;
- Paper/Live-Baseline 240 USDT gemeinsamer Cashpool, drei Slots à 80 USDT;
- Backtest-Baseline zehn isolierte Tests à 250 USDT sowie Einzeltest à 250 USDT;
- mindestens drei vollständige Jahre historische Daten plus Warm-up;
- Startup-/Datenprüfung und täglicher Audit;
- UI-Zeiträume Heute, 1W, 1M, 1J, 3J;
- Paper als Pflichtstufe vor Live;
- Audit, Metriken, Alerts, Backup und Recovery;
- Originalindikator als technische Strategiequelle;
- Bastian Keller als primäre menschliche Strategiequelle;
- 24/7-Quellenmonitoring, ohne alte Inhalte zeitlich unbegrenzt weiterwirken zu lassen.

## Noch offen

Bis Originalindikator und rechtmäßig zugängliche Member-/Live-Quellen vorliegen, bleiben offen:

- exakter Indikatorname, Version, Publisher und Inputs;
- Signal-Timeframe/Multi-Timeframe-Verhalten;
- Kauf-/Verkaufs-/Trend-/Filterlogik;
- Bar-Close/Intrabar/Repainting;
- Warm-up und Initialzustand;
- Alerts und Overlays;
- Entry-/Exit-/Reentry-/TP-/SL-/Trailing-Regeln;
- Slotpriorisierung;
- ob Bastian selbst Entries auslösen darf oder nur bestätigt/blockiert;
- Freshness und Quellenpriorität bei Konflikten.

## Nicht enthalten

- erfundene Indikatorlogik;
- Gewinn- oder Renditeversprechen;
- Futures, Margin, Leverage oder Short ohne neue Freigabe;
- Martingale/Grid/DCA/Pyramiding ohne belegte Strategieanforderung;
- automatisches Folgen beliebiger Mentoren oder Community-Mitglieder;
- Umgehung von Plattformzugriffen, Bezahlschranken oder Schutzmaßnahmen;
- API-Schlüssel mit Auszahlungsrecht.

## Betriebsmodi

1. `BACKTEST`
2. `PAPER`
3. `LIVE_DISABLED`
4. `LIVE`

Sicherer Standard nach Installation, Restore oder ungeklärter Synchronisation ist `LIVE_DISABLED`.

## Vier Signalebenen

- `INDICATOR_SIGNAL`: technischer Originalindikatorzustand;
- `BASTIAN_CONTEXT`: Marktmeinung/Szenario ohne unmittelbaren Auftrag;
- `BASTIAN_ACTIONABLE_SIGNAL`: eindeutig strukturierte, aktuelle Entry-/Exit-/Manage-Aussage;
- `EXECUTION_INTENT`: erst nach Risk-, Kapital-, Freshness- und Plausibilitätsprüfung.

24/7 bedeutet kontinuierliche Markt- und Quellenüberwachung, nicht permanente Handelstätigkeit.