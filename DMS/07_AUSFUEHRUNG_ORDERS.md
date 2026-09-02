# 07 – Ausführung und Orders

## Grundkette

`Signal/Source Event -> Validation -> Risk/Capital Guards -> Order Intent -> Börsenorder -> Fill(s) -> Position/Ledger`.

Keine Quelle darf die Schutz- und Reconciliation-Schicht umgehen.

## Order-Baseline

- Binance Spot;
- Long-only in V1, solange DMS 03 nichts anderes ausdrücklich freigibt;
- Marktorder als technische Baseline;
- Paper/Live Zielnotional 80 USDT je Slot;
- Sell schließt die nach DMS 03 freigegebene Menge;
- >25 bp Preisabweichung vor Submit blockiert den Entry.

## Zustände

`INTENT_CREATED -> BLOCKED | SUBMITTING -> SUBMITTED -> PARTIALLY_FILLED | FILLED | CANCELED | REJECTED | UNKNOWN`.

Jeder Fill wird einzeln persistiert. Restmengen/Dust bleiben sichtbar.

## Idempotency

Ein Intent erhält einen deterministischen Idempotency-Key aus Strategieversion, Symbol, Signal-/Source-ID und Aktion. Derselbe fachliche Impuls darf nach Restart/Retry nicht unbemerkt eine zweite Order erzeugen.

## Unsichere Orders

- nach 10 s ohne eindeutigen Submit-Status -> `UNKNOWN`;
- keine Ersatzorder senden;
- Börsenstatus/ClientOrderId/Trades abgleichen;
- Teilfill-Rest nach 30 s explizit klären/canceln, nicht blind neu ordern;
- starke Ausführungsabweichung (>25 bp gegenüber Pre-Submit-Referenz) als P2 melden.

## Restart/Reconciliation

Lokale DB ist nicht die Ausführungswahrheit. Nach Neustart werden offene Orders, Fills, Salden und Positionen mit der Börse abgeglichen, bevor neue Intents zugelassen werden.

Manuelle Trades im Bot-Konto sind nicht vorgesehen.

## Paper

Paper verwendet dieselbe Daten-, Strategy-, Source-, Slot-, Risk- und Intentlogik wie Live. Nur der Execution-Adapter wird simuliert. Kosten, Rundung und realistische Latenz bleiben Teil der Simulation.

## Bastian-Quelle

Ein `BASTIAN_ACTIONABLE_SIGNAL` ist noch keine Order. Erst nach Freshness-, Konflikt-, Indikator-/Fusions-, Kapital- und Risiko-Validierung darf daraus ein `EXECUTION_INTENT` entstehen. Jede Transformation wird auditiert.