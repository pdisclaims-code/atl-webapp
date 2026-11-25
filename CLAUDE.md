# CLAUDE.md – Spielregeln für die Zusammenarbeit

Projekt: ATL-Webapp im Modul Applications Engineering

## 1. Rollen
- **Patrick** gibt die Ziele vor, gibt Schritte frei und prüft das Ergebnis.
  Er schreibt selbst keinen Code und keine Konfiguration.
- **Claude** entwickelt und richtet alles ein: Code, Konfiguration, Dockerfiles,
  docker compose, GitHub Actions, Cloudflare Tunnel.

## 2. Arbeitsweise
- Vor jedem Schritt kurz erklären, was ich vorhabe und warum.
- Grössere Vorhaben (mehrere Dateien, neue Komponenten, Änderungen an
  Infrastruktur oder Deployment) zuerst als Plan vorlegen und auf Freigabe warten.
- Nach einem Schritt kurz sagen, was gemacht wurde und wie man es prüfen kann.
- Unklarheiten nachfragen statt raten.

## 3. Sicherheit
- **Niemals** Passwörter, Tokens, API-Keys oder andere Secrets in Dateien
  schreiben, die ins Git-Repository kommen.
- Secrets gehören in eine lokale `.env` (steht in `.gitignore`) bzw. in
  GitHub Secrets. Im Repository liegt höchstens eine `.env.example` mit Platzhaltern.
- Vor jedem Commit prüfen, dass keine Secrets enthalten sind.
- **Nie `git push` ohne Patricks ausdrückliche Freigabe.**
- Auch Commits nur nach Freigabe.

## 4. Ziel der App
- Öffentlich via HTTPS erreichbar.
- Anzeige:
  `Hallo von Patrick – Besucher Nr. [aus DB] – DB: verbunden – Version: [Commit-Hash]`
  - Besucherzähler wird in der Datenbank gespeichert und bei jedem Aufruf erhöht.
  - Commit-Hash wird beim Bauen des Images eingesetzt.

## 5. Vorgaben
- Läuft lokal auf Patricks MacBook (Apple Silicon, arm64).
- App und Datenbank in getrennten Containern, gestartet mit `docker compose`.
- Code liegt auf GitHub.
- Das Image wird mit GitHub Actions gebaut.
- Die abgegebene Version muss bei einer Drittperson ohne Anpassungen starten.
  Das Image wird deshalb für `linux/amd64` und `linux/arm64` gebaut.
- Veröffentlicht wird über Cloudflare Tunnel.
- Ausser der KI darf nichts etwas kosten. Es werden nur Gratis-Angebote genutzt.

## 6. Muss-Punkte
- Daten überstehen einen Neustart der Container (persistentes Volume).
- Keine Secrets im Repository oder in der Git-History.
- Healthcheck für die App und die Datenbank.
- Ein Push auf `main` bringt die neue Version ohne Handarbeit live.

## 7. Sprache
- Antworten auf Deutsch, Schweizer Rechtschreibung (ss statt ß).
