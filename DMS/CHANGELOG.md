# BTK-DMS-Changelog

## 0.1.0-prep – 02.09.2026

- eigenständiges Repository `127027/Bastian-Keller-Trademania-Bitbull` als Projektziel festgelegt;
- strategieneutrale technische Baseline als Wiederverwendungsbasis festgehalten, ohne eine fremde Strategiespezifikation zu übernehmen;
- vollständigen DMS-Satz auf die neue Bitbull-/TradeMania-/Bastian-Keller-Variante vorbereitet;
- technische Baseline beschlossen: zehn Binance-USDT-Spot-Paare, 240-USDT-Paper/Live mit 3×80 Slots, 10×250-USDT-Backtest, Daten-, Execution-, Risk-, UI-, Audit-, Recovery- und Security-Grundsätze;
- alle fremden strategiespezifischen Annahmen aus der neuen normativen Strategie entfernt;
- neues `03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` als Quellen-/Evidence-/Signalaufnahme vorbereitet;
- konkrete neue Indikatorformel, Inputs, Signal-Timeframe, Entry-/Exit-Regeln, Repainting und Slotpriorität absichtlich `OFFEN`, bis der Originalindikator vorliegt;
- Codeumbau explizit hinter DMS-Freeze und Referenzparität gestellt;
- keine BTK-Performancewerte und keine Strategieeigenschaften erfunden.

## 0.2.0-prep – 02.09.2026

- offizielle Schreibweise `TradeMania` übernommen;
- Ziel von reinem Indikatorwechsel auf **Bastian-Keller-Strategiequelle = Indikator + Live-/Update-Aussagen** erweitert;
- öffentliche TradeMania-/Bitbull-Routinen und Quellen dokumentiert;
- `BASTIAN_CONTEXT` und `BASTIAN_ACTIONABLE_SIGNAL` eingeführt;
- Source-Freshness, Live-vs-Replay, Speaker-Allowlist und Konfliktbehandlung spezifiziert;
- Source-Replay/Forward-Paper als notwendige Validierung ergänzt;
- Datenschutz-/Copyright-Grenze für Member-Inhalte und Transkripte festgelegt;
- Live-Aussagen dürfen niemals ohne deterministischen Validation Gate direkt Orders erzeugen.

## 0.3.0-prep – 02.09.2026

- Projekt von einer Arbeitsbranch-Idee auf ein **eigenständiges GitHub-Repository** umgestellt;
- Repository-Wahrheit auf `127027/Bastian-Keller-Trademania-Bitbull` geändert;
- Branch-/Remote-Verweise auf andere Trading-Projekte aus der BTK-DMS entfernt;
- DMS 21 und 23 für eigenständige Repository-, Branch- und Ordnerregeln neu gefasst;
- strategiefremde Begriffe aus UI-/Datenmodelltexten neutralisiert;
- DMS-first-Reihenfolge beibehalten: Indikator + Bastian-Evidence schließen, dann signalaktiven Botcode anpassen.

## 0.4.0-prep – 02.09.2026 – Vollaudit

- beide vorhandenen `README.md` vollständig auf den Bastian-Keller-/TradeMania-/Bitbull-Plan ausgerichtet;
- Legacy-Audit auf fremde Indikatornamen/Formeln/Strategie-Specs durchgeführt;
- verbindliche Echtzeitpipeline ergänzt: Source Discovery -> Session Validation -> Capture -> Speaker Validation -> Structuring -> Freshness/Conflict -> Conditional Watch -> Fusion -> Risk/Capital -> Execution Intent -> Audit;
- Source-Allowlist und dynamische Livestream-/Update-Erkennung ergänzt; keine hart codierten Marketingzeiten als Strategie-Wahrheit;
- Capture-Pfad je Quelle als offener, vor Paper/Live zu klärender Punkt aufgenommen (offizielle Untertitel/Transkript/API/lokale STT nur soweit zulässig);
- Rohtranskript/automatische Zusammenfassung/Confidence ausdrücklich als nicht allein orderautorisierend definiert;
- `PENDING_CONDITION`, Expiry, Invalidation, Revision/Supersede und Restart-Reconciliation vollständig spezifiziert;
- Source-/Capture-/Parser-/End-to-End-Latenz als Mess- und Blockierkriterium aufgenommen;
- Architektur, Monitoring, UI, Config, Tests, Runbook, Risiken und Glossar auf die 24/7-Bastian-Source-Schicht synchronisiert;
- Traceability-Matrix vollständig gegen die aktuellen IDs in DMS 02 neu ausgerichtet;
- fairen späteren Referenzbot-Vergleich mit gleicher Daten-, Kosten-, Kapital- und Forward-Paper-Basis verbindlich gemacht;
- öffentliche TradeMania-About-/Live-Call-Quellen im Quellenkatalog verankert;
- weiterhin keine erfundene Indikatorlogik, keine erfundene Bastian-Performance und keine Live-Freigabe vor Strategie-Freeze.
