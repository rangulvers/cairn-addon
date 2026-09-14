# Cairn

Haushalts-Inventar als Home-Assistant-Add-on. Cairn katalogisiert, was im Haus
steht — Geräte, Werkzeug, Kisten, Garantien, Verleih — und übernimmt die Geräte
dafür direkt aus Home Assistant.

## Installation

1. Einstellungen → Add-ons → Add-on Store
2. Oben rechts das Dreipunkt-Menü → Repositories
3. `https://github.com/rangulvers/cairn-addon` hinzufügen
4. Cairn installieren und starten
5. "Web UI öffnen" oder das Cairn-Symbol in der Seitenleiste

Es gibt nichts zu konfigurieren. Keine URL, kein Token.

## Geräte übernehmen

Mehr → Home Assistant → Geräte importieren.

Die Liste ist in drei Gruppen geteilt:

- **Empfohlen** — echte Hardware mit eigener Kennung (Seriennummer, MAC,
  Zigbee-Adresse). Vorausgewählt.
- **Vielleicht** — Telefone, Teilgeräte wie Optimierer hinter einem
  Wechselrichter, reine Anwesenheits-Einträge.
- **Ausgeblendet** — Add-ons, Dienste, Gruppen, virtuelle Geräte.

Name, Kategorie und Raum lassen sich vor dem Import je Gerät ändern. Bereiche
aus Home Assistant, die es in Cairn noch nicht gibt, können als Räume angelegt
werden — die Häkchen dafür stehen oben auf der Seite.

Importierte Gegenstände bleiben mit ihrem HA-Gerät verknüpft. "Synchronisieren"
aktualisiert Firmware und Bereich, meldet neue Geräte und markiert Geräte, die
Home Assistant nicht mehr kennt.

## Benutzer und Rechte

Cairn übernimmt die Anmeldung von Home Assistant. Wer das Panel öffnen darf,
ist in Cairn angemeldet — kein zweiter Login, kein PIN. Beim ersten Besuch legt
Cairn für die Person automatisch ein Profil an.

Alle, die das Panel öffnen können, haben vollen Zugriff. Wer das nicht möchte,
beschränkt in Home Assistant, wer das Add-on-Panel sieht.

## Daten und Backup

Alle Daten liegen im `/data`-Verzeichnis des Add-ons: die SQLite-Datenbank und
die hochgeladenen Fotos. Home-Assistant-Backups schließen dieses Verzeichnis
ein, ein HA-Backup sichert also auch das Inventar.

## Optionen

| Option | Bedeutung |
|---|---|
| `log_level` | Ausführlichkeit der Add-on-Logs. Standard `info`. |

## Fehlersuche

**Panel bleibt leer.** Seite neu laden (Strg+Shift+R). Wenn es danach bleibt:
Add-on-Log ansehen und einen Fehlerbericht mit dem Log-Auszug öffnen.

**Keine Geräte in der Liste.** Im Add-on-Log nach `supervisor_token_missing`
suchen. Tritt das auf, das Add-on neu starten — der Supervisor erneuert den
Token bei jedem Start.

**Import zeigt nichts an.** Home Assistant kennt dann keine Geräte mit eigener
Kennung. Integrationen ohne Geräteregistrierung (reine Template-Sensoren, viele
YAML-Integrationen) tauchen absichtlich nicht auf.

**Nach einem Update fehlen Daten.** Sollte nicht passieren — `/data` bleibt über
Updates erhalten. Falls doch: HA-Backup vor dem Update wiederherstellen und
einen Fehlerbericht öffnen.

## Quellcode

Die Anwendung liegt in <https://github.com/rangulvers/attic>. Dieses Repository
enthält nur die Add-on-Verpackung; die Images kommen fertig gebaut aus der
GitHub Container Registry.
