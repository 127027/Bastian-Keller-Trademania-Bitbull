# 21 – GitHub-Zusammenarbeit

## Repository

- Remote: `https://github.com/127027/Bastian-Keller-Trademania-Bitbull`
- Hauptzweig: `main`
- Projektkennung: `BTK`

Dieses Repository ist die alleinige GitHub-Wahrheit für den Bastian-Keller-/TradeMania-/Bitbull-Bot. Andere Trading-Projekte werden nicht in dieses Repository gemischt.

## Arbeitsweise

1. DMS zuerst;
2. echter Indikator → DMS 03 und Entscheidungslog vervollständigen;
3. `BTK-INDICATOR-SPEC-1.0` einfrieren;
4. erst danach bewährte technische Bot-Komponenten gezielt übernehmen/anpassen;
5. kleine nachvollziehbare Commits;
6. Änderungen an Strategie, Kapital, Execution oder Live-Gates besonders prüfen;
7. keine Secrets oder fremden/proprietären Sources ohne Rechte.

## Zielstruktur

```text
README.md
DMS/
strategy/
backtests/
config/
src/
tests/
.gitignore
```

Keine Parallel-App oder zweite Engine nur für einzelne BTK-Quellen, wenn dieselbe generische Engine Indicator-, Bastian-Context-, Backtest-, Paper- und Live-Pfade sauber abbilden kann.

## Quellen der Wahrheit

- `DMS/` = fachlicher Sollzustand;
- `DMS/03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md` = normative Strategie nach Freeze;
- Originalindikator/Settings/Referenzen = externe Evidenz;
- Config-/Codecommit = Build;
- Backtestmanifest = Code-/Config-/Daten-/Quellenhash.

## Branchregeln

`main` bleibt die freigegebene Projektlinie. Für größere Änderungen können kurzlebige Arbeitsbranches wie `gpt/<thema>` oder `codex/<thema>` verwendet werden. Sie sind Mittel zur Zusammenarbeit, keine zweite Produktspezifikation. Vor Merge müssen DMS, Tests und Artefakte konsistent sein.

## Commit-Konvention

```text
docs(btk): prepare indicator evidence schema
docs(btk-strategy): freeze BTK indicator v1 signals
test(btk-parity): add ETH reference bars
fix(btk-strategy): align close-bar signal timing
```

## Geheimnisse und geschützte Dateien

Niemals committen:

- Binance Keys/Secrets;
- persönliche Login-/Invite-Tokens;
- `.env` mit echten Werten;
- Account-/Saldoexporte mit Identifikatoren;
- private Backups;
- fremden/proprietären Pine-/Indikator-Source ohne Freigabe;
- vollständige geschützte Member-Transkripte oder Medien.

Wenn Material nur privat analysiert werden darf, kommen ausschließlich eigene technische Spezifikationen, Metadaten, Hashes und rechtmäßig erzeugte Referenzwerte nach Git.
