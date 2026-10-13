---
title: "M&A Datenschutz Due Diligence"
version: 2.4
author: CISO
use_case: M&A / Due Diligence
model: Claude Opus 5.5
effort: high
language: de/en
last_updated: 2026-10-13
tags: [m&a, due-diligence, datenschutz, dsgvo, ndsg, dach]
---

# Prompt: M&A Datenschutz Due Diligence Assessment

## Zweck
Strukturierte Analyse der Datenschutz-Compliance eines Akquisitionskandidaten.
Bewertet DSGVO-, nDSG- und BDSG-Konformität sowie Datenschutzrisiken im M&A-Prozess.

---

## System Prompt

```
Du bist ein erfahrener Datenschutzberater und Rechtsexperte mit Fokus auf M&A Due Diligence
in der DACH-Region. Du analysierst Datenschutz-Compliance, regulatorische Risiken und
organisatorische Datenschutzstrukturen im Kontext von Unternehmensübernahmen.
Du kennst DSGVO, nDSG (Schweiz), BDSG (Deutschland) und DSG (Österreich) in der Tiefe.
Deine Antworten sind präzise, risikobasiert und auf C-Level-Kommunikation ausgerichtet.
Antworte auf Schweizer Hochdeutsch (immer «ss», nie Eszett), ausser explizit anders angegeben.
```

---

## Prompt Template

```
Führe eine Datenschutz Due Diligence für folgenden Akquisitionskandidaten durch:

**Projektname (im Bericht verwenden):** {{project_name}}
**Unternehmen (nur interne Referenz):** {{company_name}}
**Branche:** {{industry}}
**Unternehmensgrösse:** {{company_size}} Mitarbeitende
**Standorte / Länder:** {{locations}}
**Deal-Typ:** {{deal_type}}
<!-- z.B. Full Acquisition / Majority Stake / Asset Deal -->
**Zeitrahmen Closing:** {{closing_date}}
**Anwendbares Recht:** {{applicable_law}}
<!-- z.B. DSGVO + nDSG / DSGVO + BDSG / DSGVO + DSG -->

**Verfügbare Unterlagen:** {{available_docs}}
<!-- Aus Schritt 1 (01_datenraum-matching.md): die als "Fertig" zugeordneten
     Dokumente aus dem Datenraum. Zusätzlich: was ausserhalb des VDR vorliegt.
     z.B. Datenschutzrichtlinie, DSB-Bestellungsurkunde, VVT, AVVs -->

---

### 1. Datenschutzorganisation & Governance

Analysiere und bewerte:
- [ ] Datenschutzbeauftragter (DSB/DPO) vorhanden? (intern / extern / keiner)
- [ ] Qualifikation und Unabhängigkeit des DSB
- [ ] Datenschutz-Management-System (DSMS) etabliert?
- [ ] Datenschutz-Richtlinien — formell veröffentlicht, aktuell, nachweislich kommuniziert?
- [ ] Datenschutz by Design / by Default in der Produktentwicklung
- [ ] Datenschutz-Schulungen: werden diese im Onboarding durchgeführt? Frequenz, LMS, Nachweise?
- [ ] Regelmässige Überprüfung und Überwachung der Compliance (Auditing-Ansatz)

---

### 2. Verarbeitungsverzeichnis & Rechtsgrundlagen

- [ ] Verzeichnis der Verarbeitungstätigkeiten (VVT) vorhanden und aktuell?
- [ ] Rechtsgrundlagen für alle wesentlichen Verarbeitungen dokumentiert
- [ ] Einwilligungsmanagement (Consent) — Prozesse und Dokumentation
- [ ] Zweckbindung und Datensparsamkeit überprüft
- [ ] Besondere Kategorien personenbezogener Daten (Art. 9 DSGVO) identifiziert
  - Enthält das Produkt PII oder besondere Kategorien (Gesundheit, Religion, sexuelle Orientierung)?
- [ ] Datenschutz-Folgenabschätzungen (DSFA/DPIA) durchgeführt wo erforderlich
- [ ] HIPAA-Risikoanalysen der letzten 2–3 Jahre vorhanden (falls anwendbar)?

---

### 3. Betroffenenrechte & Transparenz

- [ ] Prozesse für Auskunfts-, Löschungs-, Berichtigungs- und Widerspruchsrecht
- [ ] Nachweisbare Einhaltung von Fristen (30 Tage)
- [ ] Datenschutzhinweise / Privacy Notices aktuell, vollständig und für Betroffene zugänglich?
- [ ] Notice of Privacy Practices publiziert (falls anwendbar, z.B. HIPAA-Umfeld)?
- [ ] Cookie-Consent und Online-Tracking rechtskonform?
- [ ] Dokumentation erledigter Betroffenenanfragen

---

### 4. Auftragsverarbeitung & Drittländer

- [ ] AVV-Verträge (Auftragsverarbeitungsverträge) mit allen relevanten Dienstleistern
- [ ] Business Associate Agreements (BAAs) mit Auftragnehmern / Kunden vorhanden?
- [ ] Vollständigkeit und Aktualität der AVVs / BAAs
- [ ] Drittlandübermittlungen identifiziert (USA, Indien, etc.)
- [ ] Geeignete Garantien vorhanden (SCC, Adequacy Decision, BCR)
- [ ] Transfer Impact Assessments (TIA) durchgeführt?
- [ ] Cloud-Dienste und SaaS-Anbieter geprüft (Kundendaten-Hosting: Azure / AWS / GCP / eigenes RZ?)

---

### 5. Technische und organisatorische Massnahmen (TOMs)

- [ ] TOMs dokumentiert und dem Stand der Technik entsprechend
- [ ] Zugriffskontrolle und Berechtigungsmanagement
- [ ] Verschlüsselung (at rest / in transit)
- [ ] Pseudonymisierung / Anonymisierung wo möglich angewandt
- [ ] Löschkonzept und Löschfristen implementiert (Data Retention Policy vorhanden?)
- [ ] Datensicherung und Wiederherstellbarkeit

---

### 6. Datenpannen & Behördenverfahren

- [ ] Datenpannen der letzten 3 Jahre (Art. 33/34 DSGVO Meldungen)
- [ ] Meldungen an Aufsichtsbehörden dokumentiert
- [ ] Laufende oder abgeschlossene Behördenverfahren / Beschwerden
- [ ] Verhängte Bussgelder (DSGVO, nDSG, BDSG)
- [ ] Zivilrechtliche Klagen mit Datenschutzbezug
- [ ] Verfahren zur Behandlung von Sicherheitsvorfällen mit Datenschutzbezug vorhanden?

---

### 7. Länderspezifische & regulatorische Anforderungen (DACH)

- [ ] **Schweiz (nDSG):** Datenschutzberater, Bekanntgaben ins Ausland, Profiling, Datenschutz-Folgenabschätzung
- [ ] **Deutschland (BDSG):** Betriebsrat-Mitbestimmung bei Beschäftigtendaten, § 26 BDSG
- [ ] **Österreich (DSG):** Nationale Besonderheiten, Datenschutzbehörde
<!-- PCI-DSS wird in der Security-DD (02b, Abschnitt 11) geprüft. -->
- [ ] **HIPAA:** Sind HIPAA-Anforderungen anwendbar? Risikoanalysen (letzte 2–3 Jahre) und Management-Pläne vorhanden?
- [ ] Branchenspezifische Anforderungen: {{regulatory_requirements}}
<!-- z.B. FINMA-Rundschreiben, ePrivacy, MedTech-Regulatorik, DORA -->

---

### 8. M&A-spezifische Datenschutzrisiken

- [ ] Datenweitergabe im Rahmen des DD-Prozesses selbst (Data Room — rechtskonforme Grundlage?)
- [ ] Change-of-Control und Einwilligungserfordernisse bei Kundendaten
- [ ] Mitarbeiterdaten und Betriebsübergang (Unterrichtungspflichten)
- [ ] Weitergabe von Kundenstammdaten — ist Einwilligung oder Interessenabwägung ausreichend?
- [ ] Post-Closing: Datenmigration und Datenisolation bis Closing

---

### Belegregel

1. Stütze jeden Befund und jedes Rating auf die vorliegenden Unterlagen und nenne
   die Fundstelle (VDR-Referenz, Dokumentname oder Vertragsklausel).
2. Was die Unterlagen nicht belegen, kennzeichne als Annahme oder führe es unter
   "Offene Punkte". Ergänze keine Zahlen, Daten, Zertifikate oder Ereignisse, die
   nicht in den Unterlagen stehen.
3. Fehlen für einen Bereich die Unterlagen, vergib kein Rating, sondern "n/b"
   (nicht bewertbar), und nenne, was fehlt.

---

### Vertraulichkeitsregeln

1. **Projektname statt Firmenname:** Verwende im Bericht ausschliesslich
   {{project_name}}. Der echte Firmenname darf nicht erscheinen.
2. **Funktionen statt Namen:** Personen nur mit ihrer Funktion benennen
   (z.B. "DSB", "IT-Leiter"), keine Personennamen — das gilt auch für
   den Datenschutzbeauftragten.

---

### Gewünschter Output

Erstelle einen strukturierten Datenschutz-Due-Diligence-Bericht mit:

1. **Executive Summary** (max. 1 Seite, C-Level geeignet)

2. **Datenschutz Maturity Rating** — Bewertung 1–5 pro Bereich plus Gesamtwert.
   Skala: 1 = Kritisch / 2 = Unzureichend / 3 = Grundlegend / 4 = Gut / 5 = Sehr gut

   | Bereich | Rating (1–5) | Begründung |
   |---|---|---|
   | Datenschutzorganisation & Governance | [1–5] | [1 Satz] |
   | Verarbeitungsverzeichnis & Rechtsgrundlagen | [1–5] | [1 Satz] |
   | Betroffenenrechte & Transparenz | [1–5] | [1 Satz] |
   | Auftragsverarbeitung & Drittländer | [1–5] | [1 Satz] |
   | Technische & organisatorische Massnahmen | [1–5] | [1 Satz] |
   | Datenpannen & Behördenverfahren | [1–5] | [1 Satz] |
   | **Gesamt Datenschutz Maturity** | **[1–5]** | **[1 Satz Gesamtbewertung]** |

   Dieses Rating wird im Master-DD-Bericht (`03_master-dd-bericht.md`) in der
   Maturity-Übersicht als Zeile "Datenschutz" übernommen.

3. **Risk-Register** (Kritikalität: Critical / High / Medium / Low)
4. **Red Flags** (Deal-Breaker oder Punkte für Kaufpreisanpassung)
5. **Empfehlungen** (sofortige Massnahmen vs. Post-Closing-Massnahmen)
6. **Offene Punkte** (fehlende Informationen, weiterer Abklärungsbedarf)

Format: Tabellarisch wo sinnvoll, Sprache: Deutsch
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{project_name}}` | Interner Projektname — wird im Bericht verwendet | Projekt Alpha |
| `{{company_name}}` | Echter Firmenname — nur interne Referenz, **nicht** im Bericht | Musterfirma AG |
| `{{industry}}` | Branche | Software / Fintech / Gesundheit |
| `{{company_size}}` | Mitarbeiterzahl | 250 |
| `{{locations}}` | Standorte / Länder | Zürich, München, Wien |
| `{{deal_type}}` | Art der Transaktion | Full Acquisition |
| `{{closing_date}}` | Geplanter Abschluss | Q3 2026 |
| `{{applicable_law}}` | Anwendbares Datenschutzrecht | DSGVO + nDSG |
| `{{available_docs}}` | Vorliegende Unterlagen | VVT, Datenschutzrichtlinie, AVVs |
| `{{regulatory_requirements}}` | Branchenregulatorik | FINMA, ePrivacy |

---

## Ergänzende Prompts

### Follow-up: Tiefenanalyse eines Bereichs
```
Basierend auf dem Datenschutz-DD-Bericht zu {{company_name}}:
Führe eine vertiefte Analyse des Bereichs [{{focus_area}}] durch.
Fokus auf: konkrete Risikoquantifizierung und Massnahmenempfehlungen mit Zeitplan.
```

### Follow-up: Kaufpreisrelevanz
```
Bewerte die identifizierten Datenschutzrisiken aus dem Due-Diligence-Bericht zu {{company_name}}
hinsichtlich ihrer Kaufpreisrelevanz. Welche Punkte rechtfertigen einen Abschlag
oder sollten als Conditions Precedent / Warranties im SPA verankert werden?
```

### Follow-up: Post-Closing Massnahmenplan
```
Erstelle basierend auf dem Datenschutz-DD-Bericht zu {{company_name}} einen priorisierten
100-Tage-Plan zur Behebung der identifizierten Datenschutzmängel nach Closing.
Berücksichtige: Ressourcen, regulatorische Fristen und Integrationsaufwand.
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung | 2026-05-20 | CISO |
| 2.0 | Erweitert um PII im Produkt, HIPAA, BAAs, Privacy Notice, PCI-DSS, Data Retention, Compliance-Auditing basierend auf realer DD-Anforderungsliste (Sektion 9) | 2026-05-20 | CISO |
| 2.1 | Datenschutz Maturity Rating (1–5) im Output ergänzt — wird vom Master-DD-Bericht benötigt | 2026-09-03 | CISO |
| 2.2 | Vertraulichkeitsregeln ergänzt (Projektname statt Firmenname, Funktionen statt Namen — auch für den DSB); Verweis auf Schritt 1 bei `{{available_docs}}` | 2026-09-03 | CISO |
| 2.3 | PCI-DSS an Security-DD (02b) abgegeben | 2026-10-13 | CISO |
| 2.4 | Zielmodell auf Claude Opus 5.5 umgestellt; Schweizer Schreibweise in der Sprachvorgabe; Belegregel ergänzt; Effort-Empfehlung im Frontmatter | 2026-10-13 | CISO |
