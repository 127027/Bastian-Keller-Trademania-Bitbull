# 19 – Risikoregister

Bewertung: Eintritt `N/M/H`, Auswirkung `N/M/H`.

| ID | Risiko | Eintritt | Auswirkung | Prävention/Erkennung | Reaktion | Owner |
|---|---|---:|---:|---|---|---|
| BTK-R-001 | neuer Indikator wird vor Erhalt/Analyse falsch rekonstruiert | H | H | DMS 03 offen halten; keine Erfindungen | Codeumbau stoppen | Strategie |
| BTK-R-002 | falsche Indikatorversion/Settings analysiert | M | H | Identität, Screenshots, Hashes | Evidence neu aufnehmen | Strategie |
| BTK-R-003 | Black-Box-Verhalten wird fälschlich als Formelgewissheit dargestellt | M | H | Beweisstärke kennzeichnen | Aussage korrigieren | Strategie/QA |
| BTK-R-004 | Repainting/Intrabar-Verhalten übersehen | M/H | H | Open-Bar/Reload/Alert-Tests | Strategie nicht freigeben | Strategie/QA |
| BTK-R-005 | Schulungsaussage wird als technische Signalregel missverstanden | M | H | Quelle/Kontext + Referenztest | DMS korrigieren | Produkt/Strategie |
| BTK-R-006 | fremder proprietärer Source wird öffentlich committed | M | H | Rechteprüfung/Secret-Scan | entfernen, Rechte/Incident klären | Security |
| BTK-R-007 | alte strategiespezifische Logik bleibt unbemerkt im BTK-Codepfad | M | H | Repository-Trennung, Tests, Code-Audit | korrigieren, Backtests invalidieren | Engineering |
| BTK-R-008 | Look-ahead im Backtest | M | H | Replay, Fillsemantik, Review | Runs invalidieren | QA |
| BTK-R-009 | Datenlücke erzeugt falsches Signal | M | H | Data-Quality/Gap-Fill | Symbol pausieren | Daten |
| BTK-R-010 | Gebühren/Slippage unterschätzt | H | H | Baseline/Stress/Paper | Freigabe neu bewerten | Backtest |
| BTK-R-011 | Overfitting auf Zielprofit | H | H | Baseline zuerst; Holdout; Suchlog | Variante verwerfen | Strategie |
| BTK-R-012 | Doppelorder nach Timeout/Restart | M | H | Idempotency/Reconciliation | Live halt | Execution |
| BTK-R-013 | Fremdorder/manueller Kontoeingriff | M | H | eigener Account | Live halt | Betreiber |
| BTK-R-014 | API-Key kompromittiert | N/M | H | Least Privilege/IP/Secret-Store | sperren/rotieren | Security |
| BTK-R-015 | Pair delistet/pausiert | M | H | Statusaudit | Coin pausieren | Daten/Betreiber |
| BTK-R-016 | Feed/Rate-Limit-Ausfall | H | M/H | Backoff/Watchdog/REST | Entries pausieren | Plattform |
| BTK-R-017 | falsche Zeit/Zeitzone | N/M | H | UTC/NTP | halt | Plattform |
| BTK-R-018 | DB-Korruption/Speicher voll | N/M | H | Integrity/Backup | halt/restore | Betrieb |
| BTK-R-019 | UI zeigt stale Wert als live | M | H | Freshness/Badge | warnen/pausieren | UI/Daten |
| BTK-R-020 | Paper/Live verwechselt | N/M | H | Banner/Bestätigung/getrennte Keys | Not-Aus | UI/Betreiber |
| BTK-R-021 | Zielrendite als Garantie verstanden | M | H | Reportwarnungen | Kommunikation korrigieren | Produkt |
| BTK-R-022 | altes Slotranking ungeprüft übernommen | M | H | DMS 03 + simultane Signaltests | Ranking entfernen/neu entscheiden | Strategie |
| BTK-R-023 | 10×250 mit 240 Paperkapital verwechselt | M | H | getrennte Modi/Ledger | Run invalidieren | QA/UI |
| BTK-R-024 | vorhandener Bot wird unnötig strukturell umgebaut | M | M/H | Minimaländerungsregel | Refactor zurücknehmen | Engineering |

## Reviewtakt

- nach Erhalt des Indikators;
- vor jedem Gate;
- nach Incident oder Strategieänderung;
- im Livebetrieb mindestens monatlich.

## Zusätzliche Source-/Sprachrisiken

| ID | Risiko | W | A | Prävention |
|---|---|---:|---:|---|
| BTK-R-029 | Hypothese wird als Order missverstanden | M | H | Actionable-Schema + deterministische Pflichtfelder |
| BTK-R-030 | Replay/altes Video wird als live verarbeitet | M | H | Published/Received/Live-Status + Freshness |
| BTK-R-031 | anderer Mentor wird Bastian zugeschrieben | M | H | Speaker-/Source-Allowlist |
| BTK-R-032 | Bastian revidiert Aussage nach wenigen Minuten | H | H | versionierter Kontext + neueste Aussage gewinnt nach Regel |
| BTK-R-033 | Audio/Caption falsch transkribiert | M | H | Confidence + Referenztests + kein Trade bei kritischer Unsicherheit |
| BTK-R-034 | Fake-/Impersonation-Kanal liefert Signal | M | H | ausschließlich verifizierte/allowgelistete Quellen |
| BTK-R-035 | Live-Latenz macht Entry wirtschaftlich unbrauchbar | M | H | Latenzmessung + Preisabweichungs-/Freshness-Guard |
| BTK-R-036 | Community-/Schulungsinhalt wird unzulässig öffentlich gespiegelt | L | H | private Speicherung, nur Hash/Metadaten in Public Git |
