# 23 – Ordnerstruktur und einziger Einstiegspunkt

## Prinzip

Das Projekt erhält **einen Bot und einen technischen Haupteinstieg**.

- menschlicher Einstieg: `/README.md`
- technischer Einstieg nach Codeübernahme: `/src/main.py` bzw. ein einziges freigegebenes Hauptkommando
- Backtest/Paper/Live/UI bleiben Modi desselben Programms
- Indicator- und Bastian-Content-Schicht werden als klar getrennte Strategiequellen in dieselbe Strategy-/Execution-Kette integriert
- Source Discovery, Capture, Parser, Conditional Watcher und Fusion sind Komponenten desselben Bots, keine zweite App.

## Zielstruktur

```text
Bastian-Keller-Trademania-Bitbull/
├── README.md
├── .gitignore
├── DMS/
│   ├── 00_DOKUMENTENLENKUNG_UND_START.md
│   ├── ...
│   ├── 03_STRATEGIE_BITBULL_TRADEMANIA_BASTIAN_KELLER.md
│   └── 23_ORDNERSTRUKTUR_UND_EINSTIEGSPUNKT.md
├── strategy/
│   ├── source_material/
│   │   └── README.md              # nur eigene/rechtekonforme Quellenhinweise
│   ├── btk/
│   │   ├── indicator_spec/        # eigene technische Spezifikation/Referenzwerte
│   │   └── source_rules/          # eigene Source-/Freshness-/Fusion-Regeln
│   └── pine/                      # nur bei Veröffentlichungsrecht
├── backtests/
│   └── btk-v1/
│       ├── runs/
│       ├── reports/
│       ├── trades/
│       ├── data_quality/
│       └── source_replay/         # eigene Replay-Manifeste/Labels, keine geschützten Rohmedien
├── config/
│   └── examples/
├── src/
│   └── main.py
└── tests/
    └── fixtures/
        └── source_events/         # synthetische/eigene oder rechtekonforme Fixtures
```

Nicht jeder optionale Ordner muss sofort angelegt werden. Er wird erst erstellt, wenn die entsprechende Verantwortung tatsächlich implementiert wird.

## Runtimedaten

Runtimedaten bleiben außerhalb versionierter Projektartefakte bzw. in ignorierten Laufzeitpfaden:

```text
runtime/                   # gitignored
  source_cache/
  sessions/
  transcripts_private/
  pending_conditions/
  temporary_media/
```

Private Transkripte, Sessiontokens, Cookies, geschützte Medien und Zugangsdaten sind **niemals** Bestandteil des öffentlichen Git-Baums.

## Strategiequellen

Vor Codeumbau wird geprüft, welche technischen Komponenten bereits geeignete Plätze bieten für:

- Original-/Source-Material;
- rechtmäßig veröffentlichbare Referenzquellen;
- Indicator-Golden-/Evidence-Fixtures;
- Source-/Session-Metadaten;
- Parser-/Validation-Regeln;
- Pending-Condition-Fixtures;
- Source-Replay-Manifeste.

Neue Ordner werden nur angelegt, wenn eine bestehende Verantwortung nicht reicht und DMS 23 vorher aktualisiert wurde.

## Source-Material-Regel

`strategy/source_material/` ist **kein Ablageort für vollständige geschützte TradeMania-Inhalte**.

Dort dürfen nur liegen:

- eigene Notizen/Spezifikationen;
- öffentliche URLs/Metadaten;
- Hashes/Referenz-IDs;
- rechtmäßig veröffentlichbare Screenshots/Referenzwerte;
- vom Eigentümer ausdrücklich freigegebene eigene Artefakte.

Geschützte Rohtranskripte/Medien bleiben lokal/privat und werden nur über IDs/Hashes referenziert.

## Keine Parallelstruktur

Nicht anlegen:

- zusätzliche zweite Bot-Hauptdatei nur für Bastian;
- separate Execution-Engine pro Quelle;
- separate Datenbank ohne fachlichen Grund;
- kopierte UI nur für eine Quelle;
- lose Reports im Root;
- Secrets, private Downloads oder proprietären Source im öffentlichen Repo;
- separaten „Live-Bastian-Bot“ neben dem Indicator-Bot.

Die Zielarchitektur ist **ein BTK-Bot** mit mehreren klar getrennten Input-/Strategiequellen und einem gemeinsamen Risk-/Execution-Core.

## Backtest-/Replay-Versionierung

BTK-Runs werden unter einer eindeutigen BTK-Version geführt. Methodikänderungen erzeugen eine neue Version; Wiederholungen derselben Methodik erhalten neue Run-IDs und überschreiben keine alten Nachweise.

Source-Replays benötigen zusätzlich Source-Evidence-/Label-/Parser-/Session-Policy-Version.

## Neue Datei/Ordner – Pflichtprüfung

1. Gibt es bereits die passende Verantwortung?
2. Kann eine bestehende Datei/Komponente erweitert werden?
3. Erzeugt die Änderung einen zweiten Einstieg oder eine parallele Engine?
4. Muss das Artefakt überhaupt in Git?
5. Enthält es fremden Source, geschützten Memberinhalt oder Secrets?
6. Ist das Artefakt für Indicator-Parity, Source-Replay, Paper oder Betrieb reproduzierbar notwendig?

Minimaler, integrierter Umbau hat Vorrang.
