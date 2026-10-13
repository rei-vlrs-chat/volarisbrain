---
title: "M&A DD Datenraum-Matching"
version: 1.5
author: CISO
use_case: M&A / Due Diligence / Datenraum-Analyse
model: Claude Opus 5.5
effort: medium
language: de/en
last_updated: 2026-10-13
tags: [m&a, due-diligence, datenraum, dataroom, gap-analysis, matching]
---

# Prompt: M&A DD Datenraum-Matching

## Zweck
Automatisiertes Durchsuchen eines Datenraums und Zuordnung der vorhandenen Dokumente
zu den Anforderungen der DD-Datenanforderungsliste (GAP_Analysis_Data_Request_List).
Ergebnis: Ausgabe im Format der Spalte "Matching Dataroom Document(s)" bereit zum
Einfügen in das Excel.

---

## System Prompt

```
Du bist ein erfahrener M&A Due-Diligence-Analyst. Du analysierst Dokumentenlisten aus
Datenräumen und ordnest Dokumente gezielt den Anforderungen einer DD-Datenanforderungsliste zu.
Du arbeitest präzise, erkennst relevante Dokumente auch bei abweichenden Bezeichnungen
und gibst deine Ergebnisse strukturiert im vorgegebenen Format aus.
Antworte auf Schweizer Hochdeutsch (immer «ss», nie Eszett), ausser explizit anders angegeben.
```

---

## Prompt Template

```
Du erhältst zwei Eingaben:

1. Eine Liste von Dokumenten aus dem Datenraum (mit Pfad/Referenz und Dateiname)
2. Eine Liste von DD-Anforderungen aus der GAP_Analysis_Data_Request_List

Deine Aufgabe: Ordne für jede DD-Anforderung die passenden Dokumente aus dem Datenraum zu.

---

### Eingabe 1: Datenraum-Dokumente

{{dataroom_documents}}

<!--
Füge hier die vollständige Dokumentenliste des Datenraums ein.

Zwei unterstützte Formate:

Format A — klassische Referenznummer:
  [2.2.3.1] 2022_Musterfirma AG_Annual report (pdf)
  [4.2.7.2.2] Musterfirma AG_IT security policy (pdf)

Format B — Ordnerstruktur als Referenz (z.B. VDR-Export):
  [9.2.1 Verfügen Sie über IT-Sicherheitsrichtlinien?] 143_Sicherheitsrichtlinien.docx
  [9.2.10 Schwachstellenscan / 9.2.10.1 Scan_2026-04] auto-results.html

Wichtig bei Format B: Der Ordnername ist ein semantisches Signal — nutze ihn als
primären Hinweis auf den Inhalt, auch wenn der Dateiname wenig aussagekräftig ist.

Dokumentenpakete (mehrere Dateien in einem Ordner, z.B. Vulnerability-Scan-Reports):
Als Gruppe angeben: [9.2.10.1] Vulnerability Assessment Suite (23 Dateien: ZAP, Trivy, Nuclei etc.)
-->

---

### Eingabe 2: DD-Anforderungen (Sektion {{section_number}})

{{dd_requirements}}

<!--
Füge hier die relevanten Zeilen aus der GAP_Analysis_Data_Request_List ein.
Format pro Zeile: [Ref] [Sub] Beschreibung (EN) | Beschreibung (DE)
Beispiel:
[9][b] Do you have formal and published IT/data security policies? | Verfügen Sie über formelle IT-/Datensicherheitsrichtlinien?
[9][b] Is multi-factor authentication (MFA) used? | Wird eine Multi-Faktor-Authentifizierung verwendet?
[10][b] Technical products overview | Technische Produktübersicht
-->

---

### Anweisungen

Für jede DD-Anforderung:

1. **Durchsuche** die Datenraum-Dokumentenliste nach passenden Dokumenten.
   Nutze dabei **sowohl den Dateinamen als auch den Ordnernamen** als Matching-Signal.

2. **Prüfe den Dokumenttyp** und unterscheide:
   - **Report/Nachweis:** Das Dokument enthält tatsächliche Ergebnisse (z.B. PenTest-Report mit Findings)
   - **Vertrag/Beauftragung:** Das Dokument belegt, dass etwas beauftragt wurde, aber noch kein Ergebnis vorliegt
   - **Verweis:** Das Dokument enthält nur einen Querverweis auf ein anderes Dokument (z.B. "Siehe 9.2.10")
   - **Nicht anwendbar:** Das Dokument ist explizit als "nicht anwendbar" markiert (z.B. xx_nicht-anwendbar.docx)

3. **Bestimme den Status** jeder Anforderung:

   | Status | Bedeutung |
   |--------|-----------|
   | **Fertig** | Passendes Dokument mit echtem Inhalt vorhanden (Konfidenz ≥ 85%) |
   | **Unvollständig** | Dokument vorhanden, aber nur Verweis / Beauftragung / Teilinformation — oder Konfidenz 70–84% |
   | **N/A** | Anforderung explizit als nicht anwendbar markiert |
   | **Missing** | Kein passendes Dokument im Datenraum (Konfidenz < 70%) |

4. **Vergib einen Konfidenz-Score** pro Zuordnung:
   - 🟢 **Hoch (85–100%):** Dokument trifft die Anforderung direkt und vollständig → Status **Fertig**
   - 🟡 **Mittel (70–84%):** Wahrscheinlich passend, aber Einschränkungen vorhanden → Status **Unvollständig**
   - 🔴 **Niedrig (<70%):** Nicht zuordnen → Status **Missing**

   Der Status folgt zwingend aus dem Konfidenz-Score. Ein Dokument mit 80% Konfidenz
   ist nie "Fertig", auch wenn es thematisch nahe liegt.

   **Besondere Regeln:**
   - Ordnername als semantisches Signal: Ordner `9.2.14 Antivirus` → direkt auf EDR-Anforderung matchen, auch wenn Dateiname generisch ist
   - Dokumentenpaket: Mehrere Dateien in einem Ordner (z.B. 23 Scan-Reports) → als Gruppe mit zusammenfassender Beschreibung zuordnen
   - Querverweise (z.B. "Siehe 9.2.10"): Status **Unvollständig**, Konfidenz max. 🟡 70% — nur wenn das referenzierte Dokument im VDR vorhanden ist
   - Beauftragung ohne Ergebnis (z.B. Vertrag für geplanten PenTest): Status **Unvollständig**, Konfidenz max. 🟡 75% — explizit vermerken, dass Ergebnis noch aussteht
   - "xx_nicht-anwendbar.docx" oder gleichwertig: Status **N/A** — kein Konfidenz-Score, kein Match

5. **Zuordnungsregeln:**

   ✅ **Zuordnen (Fertig) wenn — alle drei Punkte erfüllt:**
   - Der Dokument-/Ordnername weist direkt auf den gefragten Inhalt hin
   - Das Dokument enthält die geforderten Informationen mit hoher Wahrscheinlichkeit
   - Der Dokumenttyp passt eindeutig (Report, Policy, Zertifikat etc.)

   ⚠️ **Zuordnen (Unvollständig) wenn:**
   - Das Dokument nur einen Verweis auf ein anderes Dokument enthält
   - Ein Vertrag/Auftrag vorliegt, aber kein Ergebnis/Report
   - Das Dokument die Anforderung nur teilweise abdeckt
   - Die Zuordnung plausibel, aber nicht eindeutig ist (Konfidenz 70–84%)

   ❌ **Nicht zuordnen (Missing) wenn:**
   - Kein Dokument mit ausreichendem Bezug zur Anforderung existiert
   - Konfidenz < 70%
   - Dokument zwar thematisch verwandt, aber für diese spezifische Anforderung unpassend

---

### Gewünschter Output

Erstelle eine tabellarische Ausgabe — bereit zum Einfügen in das Excel:

| Ref | Sub | Anforderung (DE) | Status | Konfidenz | Matching Dataroom Document(s) | Hinweis |
|-----|-----|-----------------|--------|-----------|-------------------------------|---------|
| 9 | b | IT-Sicherheitsrichtlinien | Fertig | 🟢 95% | [4.2.7.2.2] Musterfirma_IT security policy (pdf) | Vollständige Policy vorhanden |
| 9 | b | Penetrationstest | Unvollständig | 🟡 75% | [9.2.9.1] PenTest_Anbieter_signed.pdf | Vertrag vorhanden, Test geplant — kein Ergebnis-Report im VDR |
| 9 | b | Interne Systeme Schwachstellenscan | N/A | — | [9.2.11.1] xx_nicht-anwendbar.docx | Nicht anwendbar (Cloud-hosted, keine eigene Infrastruktur) |
| 9 | b | MFA-Nutzung | Missing | — | — | — |

**Wichtig:** Lieber Missing oder Unvollständig als ein schlecht passendes Dokument als Fertig markieren.
Qualität der Zuordnung ist wichtiger als Vollständigkeit.

Zusätzlich am Ende:

- **Zusammenfassung:** Anzahl Fertig / Unvollständig / N/A / Missing — Match-Quote = Fertig / (Fertig + Unvollständig + Missing)
- **Offene Lücken (GAP-Liste):** Alle Missing-Anforderungen, priorisiert nach DD-Relevanz
- **Unvollständige Positionen:** Beauftragungen ohne Ergebnis und Querverweise — mit konkretem Nachforderungsbedarf
- **Nicht zugeordnete Dokumente:** VDR-Dokumente, die keiner Anforderung zugeordnet wurden
```

---

## Anwendungsbeispiel

### Schritt 1 — Datenraum-Export einfügen
Exportiere die Dokumentenliste aus dem Datenraum (z.B. als Textdatei, Ordnerstruktur oder
Dateiliste) und füge sie in `{{dataroom_documents}}` ein.

Tipp: Bei VDRs mit Ordnerstruktur-Nummerierung (z.B. 9.2.14 Antivirus / 9.2.14.1 Dateiname)
den vollen Pfad inkl. Ordnernamen einfügen — der Ordnername dient als semantisches Signal.

Tipp: Mehrere Dateien im gleichen Unterordner (z.B. 23 Scan-Reports) als Gruppe beschreiben:
`[9.2.10.1] Vulnerability Assessment Suite (23 Dateien: ZAP, Trivy, Nuclei, PHPCS, Gitleaks etc.)`

### Schritt 2 — DD-Anforderungen einfügen
Kopiere die relevanten Zeilen aus dem Excel (Spalten: Ref, Sub, Item EN, Item DE)
und füge sie in `{{dd_requirements}}` ein.

### Schritt 3 — Prompt ausführen
Übergib den vollständigen Prompt an Claude Opus 5.5.

### Schritt 4 — Ergebnis ins Excel übernehmen
Kopiere die Einträge direkt in die Spalte "Matching Dataroom Document(s)" der
GAP_Analysis_Data_Request_List und übertrage den Status in die Statusspalte.

---

## Ergänzende Prompts

### Follow-up: Nur fehlende Dokumente
```
Basierend auf dem Matching-Ergebnis für {{company_name}}:
Erstelle eine priorisierte Liste aller fehlenden Dokumente (Missing) aus Sektion {{section_number}}.
Gruppiere nach Kritikalität: welche Lücken sind Deal-Breaker, welche sind nachforderbar?
```

### Follow-up: Nachforderungsliste
```
Erstelle basierend auf den identifizierten Lücken im Datenraum von {{company_name}}
eine formelle Nachforderungsliste für den Verkäufer.
Berücksichtige: Missing UND Unvollständig (Beauftragungen ohne Ergebnis, reine Querverweise).
Format: nummerierte Liste mit klarer Beschreibung des fehlenden Dokuments auf Deutsch und Englisch,
Frist und Begründung warum das Dokument für die DD erforderlich ist.
```

### Follow-up: Status-Update nach neuen VDR-Uploads
```
Der Datenraum von {{company_name}} wurde aktualisiert. Neue Dokumente:
{{new_documents}}

Prüfe ob die neu hochgeladenen Dokumente offene Lücken (Missing) oder unvollständige
Positionen (Unvollständig) aus dem letzten Matching schliessen und aktualisiere den
Status entsprechend. Vermerke insbesondere ob bisher nur beauftragte Leistungen
(z.B. PenTest-Vertrag) nun als abgeschlossene Reports vorliegen.
```

### Follow-up: Bewertung der Unvollständig-Positionen
```
Analysiere alle als "Unvollständig" markierten Anforderungen im Matching-Ergebnis
für {{company_name}}.
Unterscheide:
1. Querverweise ohne Substanz → Nachforderung erforderlich
2. Beauftragungen ohne Ergebnis → Timeline und Ergebnis nachfordern
3. Teilweise abgedeckt → Was fehlt konkret?
Erstelle eine priorisierte Nachforderungsliste.
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{company_name}}` | Name des Targets | Musterfirma AG |
| `{{section_number}}` | Relevante Sektion(en) | 9 / 9a / 9b / alle |
| `{{dataroom_documents}}` | Vollständige Datenraum-Dokumentenliste | Siehe Schritt 1 |
| `{{dd_requirements}}` | Anforderungszeilen aus dem Excel | Siehe Schritt 2 |
| `{{new_documents}}` | Neu hochgeladene Dokumente | [9.2.9.1] PenTest-Report (pdf) |

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung | 2026-05-20 | CISO |
| 1.1 | Konfidenz-Schwellenwert ergänzt — nur Matches ≥ 70% werden zugeordnet | 2026-05-20 | CISO |
| 1.2 | Erweiterungen basierend auf praktischer Anwendung in einem realen DD-Projekt: Status N/A und Unvollständig ergänzt; Ordnernamen als semantisches Matching-Signal; Dokumentenpakete als Gruppe; Unterscheidung Report vs. Beauftragung; Querverweise-Regel; Hinweis-Spalte im Output; Follow-up für Unvollständig-Positionen | 2026-06-02 | CISO |
| 1.3 | Konfidenz-Schwelle für Status "Fertig" von 70% auf 85% angehoben; 70–84% ergibt neu "Unvollständig"; Status folgt zwingend aus dem Score; Firmenname aus Versionshistorie entfernt | 2026-09-03 | CISO |
| 1.4 | Ordnername im Format-B-Beispiel neutralisiert | 2026-10-13 | CISO |
| 1.5 | Zielmodell auf Claude Opus 5.5 umgestellt; Schweizer Schreibweise in der Sprachvorgabe; Effort-Empfehlung im Frontmatter | 2026-10-13 | CISO |
