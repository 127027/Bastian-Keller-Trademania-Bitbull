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

Der Bot darf nur Quellen verwenden, auf die der Eigentümer rechtmäßig zugreifen darf. Keine Umgehung von Bezahlschranken, DRM, Login-Schutz, Plattformbeschränkungen oder technischen Schutzmaßnahmen.

Vor signalaktiver Nutzung einer Quelle wird dokumentiert:

- offizieller Provider/Channel/Account;
- Zugriffsart;
- erlaubte/technisch zulässige Capture-Methode;
- ob offizielle Metadaten, Untertitel, Transkript/API oder andere Wege verfügbar sind;
- ob lokale Verarbeitung von Audio/Text erforderlich und zulässig ist;
- Speicher-/Aufbewahrungsform;
- was öffentlich in Git referenziert werden darf.

Nicht in das öffentliche Repository:

- fremder/proprietärer Indikator-Source ohne Veröffentlichungsrecht;
- vollständige geschützte Schulungsvideos oder Streams;
- vollständige private Member-Transkripte;
- Audio-/Videorips geschützter Inhalte;
- persönliche Zugangsdaten;
- Cookies/Sessiontokens;
- private Downloadlinks/Tokens;
- personenbezogene Inhalte, die für die Strategie nicht erforderlich sind.

Zulässig sind eigene technische Spezifikationen, Metadaten, Hashes, abgeleitete Testfälle, eigene kurze Labels/Zusammenfassungen und rechtmäßig veröffentlichbare Referenzwerte.

## Source-Allowlist und Identität

Nur eindeutig verifizierte offizielle Source-/Channel-/Account-IDs dürfen signalrelevante Events liefern. Ähnlich benannte Fan-, Reupload-, Fake- oder Communitykanäle sind keine automatische Ersatzquelle.

Sprecheridentität und Source-Identität sind getrennte Prüfungen. Ein offizieller TradeMania-Livecall mit einem anderen Mentor ist nicht automatisch ein Bastian-Signal.

## Lokale Oberfläche/API

Default: `localhost`. Schreibende Aktionen benötigen Auth/Bestätigung. Externe Freigabe ist kein V1-Default.

## Supply Chain

- Dependencies pinnen/locken;
- Hashes/Versionen dokumentieren;
- Security-Updates kontrolliert testen;
- keine zufälligen Skripte aus Communityquellen ungeprüft ausführen;
- externe Parser-/STT-/Modelldienste nur nach Daten-/Rechteprüfung verwenden;
- keine sensiblen Member-Rohinhalte ungeprüft an externe Dienste übertragen.

## Audit

Auditierbar sind mindestens:

- Strategie-/Configänderungen;
- Source-Allowlist-/Capture-/Parser-Versionen;
- Source Sessions und Source Health;
- Moduswechsel;
- Live-Aktivierung;
- Orders/Fills;
- Blockgründe;
- Pending-Condition-Erstellung/Expiry/Invalidation;
- Revision/Supersede;
- Not-Aus;
- Reconciliation;
- Backups/Restore;
- Quellen- und Datenstörungen.

## Datenminimierung

Für den Tradingzweck werden nur die erforderlichen Source-Informationen langfristig gespeichert. Wo ein Hash, Eventlabel, Zeitstempel und eigene technische Zusammenfassung genügen, wird kein vollständiges Rohmedium in der Botdatenbank oder in Git dauerhaft gehalten.

## Live-Gate Sicherheit

Vor Live müssen praktisch getestet und dokumentiert sein:

- Least Privilege;
- Secret-Handling;
- Reconciliation/Idempotency;
- Not-Aus;
- Audit;
- Backup/Restore;
- Paper-Soak;
- Source-Allowlist;
- zulässige Capture-Pfade;
- `NO_TRADE` bei kritischer Unsicherheit;
- Freshness/Revision/Conditional-Watcher;
- Source-/Capture-/Parser-/E2E-Latenzgrenzen;
- Runbook.
