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
| BTK-R-007 | fremde/alte strategiespezifische Logik bleibt unbemerkt im BTK-Codepfad | M | H | Repository-Trennung, Tests, Code-Audit | korrigieren, Runs invalidieren | Engineering |
| BTK-R-008 | Look-ahead im Backtest/Source-Replay | M | H | chronologischer Replay, Fillsemantik, Review | Runs invalidieren | QA |
| BTK-R-009 | Datenlücke erzeugt falsches Signal oder falschen Conditional-Trigger | M | H | Data-Quality/Gap-Fill | Symbol/Condition pausieren | Daten |
| BTK-R-010 | Gebühren/Slippage unterschätzt | H | H | Baseline/Stress/Paper | Freigabe neu bewerten | Backtest |
| BTK-R-011 | Overfitting auf Zielprofit | H | H | Baseline zuerst; Holdout; Suchlog | Variante verwerfen | Strategie |
| BTK-R-012 | Doppelorder nach Timeout/Restart | M | H | Idempotency/Reconciliation | Live halt | Execution |
| BTK-R-013 | Fremdorder/manueller Kontoeingriff | M | H | eigener Account | Live halt | Betreiber |
| BTK-R-014 | API-Key kompromittiert | N/M | H | Least Privilege/IP/Secret-Store | sperren/rotieren | Security |
| BTK-R-015 | Pair delistet/pausiert | M | H | Statusaudit | Coin pausieren | Daten/Betreiber |
| BTK-R-016 | Marktfeed/Rate-Limit-Ausfall | H | M/H | Backoff/Watchdog/REST | Entries/Conditions pausieren | Plattform |
| BTK-R-017 | falsche Zeit/Zeitzone | N/M | H | UTC/NTP | halt | Plattform |
| BTK-R-018 | DB-Korruption/Speicher voll | N/M | H | Integrity/Backup | halt/restore | Betrieb |
| BTK-R-019 | UI zeigt stale Wert/Kontext als live | M | H | Freshness/Badge | warnen/pausieren | UI/Daten |
| BTK-R-020 | Paper/Live verwechselt | N/M | H | Banner/Bestätigung/getrennte Keys | Not-Aus | UI/Betreiber |
| BTK-R-021 | Zielrendite als Garantie verstanden | M | H | Reportwarnungen | Kommunikation korrigieren | Produkt |
| BTK-R-022 | ungeprüfte Slotpriorität übernommen | M | H | DMS 03 + simultane Signaltests | Ranking entfernen/neu entscheiden | Strategie |
| BTK-R-023 | 10×250 mit 240 Paperkapital verwechselt | M | H | getrennte Modi/Ledger | Run invalidieren | QA/UI |
| BTK-R-024 | Bot wird unnötig strukturell umgebaut | M | M/H | Minimaländerungsregel | Refactor zurücknehmen | Engineering |
| BTK-R-025 | Vergleichsbot erhält andere Daten/Kosten/Kapitalbasis | M | H | Vergleichsmanifest + gleiche Hashes | Vergleich invalidieren | QA |
| BTK-R-026 | Zwischenstands-Tuning verfälscht A/B-Vergleich | M | H | Parameterfreeze vor Vergleich | Vergleich neu starten | Strategie/QA |
| BTK-R-027 | öffentlich erster gefundener Indikator wird vorschnell als Ziel ausgewählt | M | H | vollständiges Public-/Member-Inventar + Auswahlmatrix | Auswahl zurücksetzen | Strategie |
| BTK-R-028 | unnötiges Indicator-Stacking erzeugt Overfitting/Redundanz | H | H | minimaler Stack + Ablation/Forward-Paper | Zusatzindikator entfernen | Strategie/QA |

## Indicator-/Daten-/Tool-Risiken

| ID | Risiko | Eintritt | Auswirkung | Prävention/Erkennung | Reaktion | Owner |
|---|---|---:|---:|---|---|---|
| BTK-R-045 | geschützter PVSRA-Source wird aus öffentlicher Beschreibung als vollständig bekannte Formel behandelt | H | H | Black-Box-Parität, keine unbewiesenen Interna | Spec korrigieren/Runs stale | Strategie/QA |
| BTK-R-046 | Chartpreis und PVSRA-Volumen stammen in Referenz und Bot aus unterschiedlichen Providern | M/H | H | explizites Indicator-Source-Mapping + Mapping-Hash | Signale pausieren/Runs invalidieren | Daten |
| BTK-R-047 | Volume Override wird im Backtest anders behandelt als in TradingView/Paper | M | H | Cross-Exchange-Override-Fixtures | Run invalidieren | Daten/QA |
| BTK-R-048 | Spot-, Perpetual- oder Futures-Volumen werden still verwechselt | M | H | `market_type` je Source verpflichtend | Strategie pausieren | Daten |
| BTK-R-049 | Session-Zeitzone/DST erzeugt andere WIL-/Session-Levels | M | H | Sessiontimezone/DST-Freeze + Tests | Referenzen neu erzeugen | Daten/QA |
| BTK-R-050 | POC-/Footprint-Wert wird aus OHLCV angenähert und fälschlich als Originalwert behandelt | H | H | exakter Provider/Resolution oder `BLACK_BOX_EXTERNAL` | Komponente aus Signalpfad nehmen | Strategie/Daten |
| BTK-R-051 | TradeMania-Member-Indikator ändert Version ohne klare Versionsanzeige | M | H | regelmäßige Settings-/Screenshot-/Golden-Hashes | neue Version aufnehmen, Runs stale | Strategie/QA |
| BTK-R-052 | Marketingbegriff „KI-basiert/selbstlernend“ wird als reproduzierbare technische Eigenschaft übernommen | M | H | nur beobachtbare/versionierbare Funktion spezifizieren | Claim verwerfen | Produkt/Strategie |
| BTK-R-053 | `/bots`-Tool ist für Futures/andere Börse/anderen Tradingstil gedacht und wird fälschlich auf Binance Spot übertragen | M | H | Bot-Inventar: Markt, Exchange, Ordertyp, Risiko prüfen | Kandidat verwerfen | Strategie |
| BTK-R-054 | proprietäres Tool lässt sich nicht rechtmäßig oder reproduzierbar automatisieren | M | H | Rechte-/Alert-/API-/Black-Box-Prüfung vor Auswahl | nicht signalrelevant verwenden | Security/Strategie |
| BTK-R-055 | MACD/RSI/POC wird nur wegen öffentlichem Lernmaterial in V1 aufgenommen, obwohl Bastian es aktuell nicht nutzt | M | M/H | aktuelle Live-Evidence + Ablation | Zusatztool entfernen | Strategie |

## Source-/Sprach-/Live-Risiken

| ID | Risiko | Eintritt | Auswirkung | Prävention/Erkennung | Reaktion | Owner |
|---|---|---:|---:|---|---|---|
| BTK-R-029 | Hypothese wird als Order missverstanden | M | H | Actionable-Schema + Pflichtfelder | `NO_TRADE` | Strategy/QA |
| BTK-R-030 | Replay/altes Video wird als live verarbeitet | M | H | Sessionstatus + Published/Received + Freshness | Event blockieren | Source |
| BTK-R-031 | anderer Mentor wird Bastian zugeschrieben | M | H | Speaker-/Source-Allowlist | Event blockieren | Source |
| BTK-R-032 | Bastian revidiert Aussage nach wenigen Minuten | H | H | versionierter Kontext + Supersede-Regel | älteren Kontext invalidieren | Strategy |
| BTK-R-033 | Audio/Caption falsch transkribiert | M | H | Capture-/Parser-Tests + kein Trade bei kritischer Unsicherheit | `NO_TRADE` | Source/QA |
| BTK-R-034 | Fake-/Impersonation-Kanal liefert Signal | M | H | ausschließlich allowgelistete offizielle Source-/Channel-IDs | Source sperren | Security/Source |
| BTK-R-035 | Live-Latenz macht Entry wirtschaftlich unbrauchbar | M | H | Latenzmessung + Preisabweichungs-/Freshness-Guard | Event blockieren | Strategy/Execution |
| BTK-R-036 | Community-/Schulungsinhalt wird unzulässig öffentlich gespiegelt | N/M | H | private Speicherung, nur Hash/Metadaten in Public Git | entfernen/Incident | Security |
| BTK-R-037 | Marketingkalender ändert sich, Bot wartet auf falschen Zeitpunkt | H | M/H | dynamische Session Discovery statt hart codiertem Plan | Source-Health warnen | Source |
| BTK-R-038 | konditionale Aussage triggert auf falschem Marktwert/Timeframe | M | H | Condition-Schema + Market-Feed-Test | Condition invalidieren | Strategy/Data |
| BTK-R-039 | Pending Condition läuft nach Expiry weiter | M | H | Expiry-Watchdog + Tests | Condition blockieren | Strategy |
| BTK-R-040 | Restart reaktiviert alte Pending Condition | M | H | Freshness/Reconciliation beim Restore | nicht reaktivieren | Operations |
| BTK-R-041 | Streamende wird fälschlich als Exit oder Kontextverlängerung interpretiert | M | H | DMS-03-Regel + Session-State-Test | `NO_ACTION`/Incident | Strategy |
| BTK-R-042 | Source-Ausfall führt zu stiller Nutzung alter Aussage | M | H | Source Health + Context Expiry | Source-Layer pausieren | Operations |
| BTK-R-043 | automatische Zusammenfassung fügt nicht gesagte Details hinzu | M | H | Rohreferenz + strukturierte Pflichtfelder + Referenztest | Event verwerfen | Parser/QA |
| BTK-R-044 | mehrere Assets/Szenarien in einem Satz werden falsch verbunden | M | H | Segmentation + Multi-Asset-Fixtures | Event auf UNKNOWN | Parser/QA |

## Reviewtakt

- nach jeder Kandidateninventar-/Zielstack-Änderung;
- nach Erhalt/Update des finalen Indikators;
- nach Freischaltung neuer Bastian-/TradeMania-Quellen;
- vor jedem Gate;
- nach Incident oder Strategieänderung;
- im Livebetrieb mindestens monatlich.
