# 23 – Ordnerstruktur und einziger Einstiegspunkt

## Prinzip

Das Projekt erhält **einen Bot und einen technischen Haupteinstieg**.

- menschlicher Einstieg: `/README.md`
- technischer Einstieg nach Codeübernahme: `/src/main.py` bzw. ein einziges freigegebenes Hauptkommando
- Backtest/Paper/Live/UI bleiben Modi desselben Programms
- Indicator- und Bastian-Content-Schicht werden als klar getrennte Strategiequellen in dieselbe Engine integriert.

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
│   └── pine/            # nur bei Veröffentlichungsrecht
├── backtests/
│   └── btk-v1/
├── config/
│   └── examples/
├── src/
│   └── main.py
└── tests/
```

Runtimedaten bleiben außerhalb versionierter Projektartefakte bzw. in ignorierten Laufzeitpfaden.

## Strategiequellen

Vor Codeumbau wird geprüft, welche übernommenen technischen Komponenten bereits geeignete Plätze für:

- Original-/Source-Material;
- rechtmäßig veröffentlichbare Referenzquellen;
- Golden-/Evidence-Fixtures;
- Bastian-Source-Metadaten

bieten. Neue Ordner werden nur angelegt, wenn eine bestehende Verantwortung nicht reicht und DMS 23 vorher aktualisiert wurde.

## Keine Parallelstruktur

Nicht anlegen:

- zusätzliche zweite Bot-Hauptdatei nur für Bastian;
- separate Execution-Engine pro Quelle;
- separate Datenbank ohne fachlichen Grund;
- kopierte UI nur für eine Quelle;
- lose Reports im Root;
- Secrets, private Downloads oder proprietären Source im öffentlichen Repo.

## Backtestversionierung

BTK-Runs werden unter einer eindeutigen BTK-Version geführt. Methodikänderungen erzeugen eine neue Version; Wiederholungen derselben Methodik erhalten neue Run-IDs und überschreiben keine alten Nachweise.

## Neue Datei/Ordner – Pflichtprüfung

1. Gibt es bereits die passende Verantwortung?
2. Kann eine bestehende Datei/Komponente erweitert werden?
3. Erzeugt die Änderung einen zweiten Einstieg oder eine parallele Engine?
4. Muss das Artefakt überhaupt in Git?
5. Enthält es fremden Source oder Secrets?

Minimaler, integrierter Umbau hat Vorrang.

## Zusätzliche BTK-Artefakte

Nur bei Bedarf:

```text
strategy/
  btk/
    indicator_spec/
    source_rules/

runtime/                 # gitignored
  btk_source_cache/
  transcripts_private/

backtests/
  btk-v1/
    runs/
    reports/
```

Private Transkripte, Sessiontokens und geschützte Medien sind **niemals** Bestandteil des öffentlichen Git-Baums.
