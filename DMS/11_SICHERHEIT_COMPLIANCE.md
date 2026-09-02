# 11 – Sicherheit und Compliance

## Börsenkonto

- separates Bot-Konto/Subaccount;
- keine manuellen Trades im selben Konto;
- API nur Read + Spot-Trade;
- kein Withdrawal, Margin oder Futures;
- IP-Allowlist wenn verfügbar;
- getrennte Test-/Paper- und Live-Schlüssel.

## Secrets

Secrets gehören in OS-Credential-/Secret-Store, niemals in Git. `.env` mit echten Werten, Login-Cookies, Invite-Tokens, Sessiontokens und private Accountdaten werden nicht committed.

## Content-/Member-Rechte

Der Bot darf nur Quellen verwenden, auf die der Eigentümer rechtmäßig zugreifen darf. Keine Umgehung von Bezahlschranken, DRM, Login-Schutz oder Plattformbeschränkungen.

Nicht in das öffentliche Repository:

- fremder/proprietärer Indikator-Source ohne Veröffentlichungsrecht;
- vollständige geschützte Schulungsvideos;
- vollständige private Member-Transkripte;
- persönliche Zugangsdaten;
- private Downloadlinks/Tokens.

Zulässig sind eigene technische Spezifikationen, Metadaten, Hashes, abgeleitete Testfälle und rechtmäßig veröffentlichbare Referenzwerte.

## Lokale Oberfläche/API

Default: `localhost`. Schreibende Aktionen benötigen Auth/Bestätigung. Externe Freigabe ist kein V1-Default.

## Supply Chain

- Dependencies pinnen/locken;
- Hashes/Versionen dokumentieren;
- Security-Updates kontrolliert testen;
- keine zufälligen Skripte aus Communityquellen ungeprüft ausführen.

## Audit

Auditierbar sind mindestens:

- Strategie-/Configänderungen;
- Source-/Parser-Versionen;
- Moduswechsel;
- Live-Aktivierung;
- Orders/Fills;
- Blockgründe;
- Not-Aus;
- Reconciliation;
- Backups/Restore;
- Quellen- und Datenstörungen.

## Live-Gate Sicherheit

Vor Live müssen Least Privilege, Secret-Handling, Reconciliation, Idempotency, Not-Aus, Audit, Backup, Restore, Paper-Soak und Runbook praktisch getestet sein.