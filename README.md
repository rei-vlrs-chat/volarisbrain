# Volarisbrain

Arbeitsrepository für Volaris-bezogene Arbeit mit Claude Code.

## Inhalt

### `due-diligence/` — Prompt-Vorlagen für die IT-, Security- und Datenschutz-DD

Vorlagen mit Platzhaltern (`{{...}}`) für einen DD-Workflow in vier Schritten:

| Schritt | Datei | Ergebnis |
|---|---|---|
| 1 | `01_datenraum-matching.md` | Zuordnung VDR-Dokumente zur DD-Anforderungsliste, GAP-Liste |
| 2 | `02a_it-due-diligence.md` | IT-DD-Bericht mit IT Maturity Rating |
| 2 | `02b_security-due-diligence.md` | Security-DD-Bericht mit Security Maturity Rating |
| 2 | `02c_datenschutz-due-diligence.md` | Datenschutz-DD-Bericht mit Datenschutz Maturity Rating |
| 2 | `02d_kundenvertraege-compliance.md` | Vertragsanalyse mit Vertrags-Maturity Rating |
| 3 | `03_master-dd-bericht.md` | Konsolidierter Master-DD-Bericht |
| 4 | `04_expert-session-agenda.md` | Verkäufer-Agenda, interne Agenda, Pre-Session Checklist |

Die Maturity Ratings aus Schritt 2 fliessen in die Maturity-Übersicht des Master-Berichts.

Zielmodell ist Claude Opus 5.5. Das Feld `effort` im Frontmatter jeder Vorlage ist die
empfohlene Effort-Stufe bei API-Nutzung (`output_config.effort`); ohne Angabe arbeitet
Opus 5.5 mit `medium`.

## Hinweise

- GitHub-Konto: `rei-vlrs-chat`
- Nur Vorlagen einchecken. Keine Echtfalldaten, Firmennamen hinter Deal-Codenamen,
  Personendaten, VDR-Auszüge, ausgefüllte Prompts, Berichte oder Zugangsdaten.
- Ausgefüllte Prompts und Ergebnisse bleiben ausserhalb des Repositorys.
