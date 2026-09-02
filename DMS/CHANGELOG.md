# BTK-DMS-Changelog

## 0.1.0-prep – 02.09.2026

- eigenständiges Repository `127027/Bastian-Keller-Trademania-Bitbull` als Projektziel festgelegt;
- bewährte technische Baseline als spätere Übernahmequelle festgehalten, ohne eine fremde Strategiespezifikation zu übernehmen;
- vollständigen DMS-Satz auf die neue Bitbull-/TradeMania-/Bastian-Keller-Variante vorbereitet;
- bewährte Bot-Infrastruktur als geerbt beibehalten: zehn Binance-USDT-Spot-Paare, 240-USDT-Paper/Live mit 3×80 Slots, 10×250-USDT-Backtest, Daten-, Execution-, Risk-, UI-, Audit-, Recovery- und Security-Grundsätze;
- alle alten strategiespezifischen Annahmen aus der neuen normativen Strategie entfernt;
- neues `03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` als vollständige Quellen-/Evidence-/Signalaufnahme vorbereitet;
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
- alte strategiespezifische Begriffe aus UI-/Datenmodelltexten weiter neutralisiert;
- DMS-first-Reihenfolge beibehalten: Indikator + Bastian-Evidence schließen, dann erst Bot-Unterbau übernehmen.
