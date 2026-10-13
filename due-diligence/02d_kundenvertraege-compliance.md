---
title: "M&A Kundenverträge — Compliance & Haftungsprüfung"
version: 1.3
author: CISO
use_case: M&A / Due Diligence / Vertragsanalyse
model: Claude Opus 5.5
language: de/en
last_updated: 2026-10-13
tags: [m&a, due-diligence, kundenverträge, haftung, dsgvo, dora, iso27001, nis2, compliance]
---

# Prompt: Kundenverträge — Compliance & Haftungsprüfung

## Zweck
Strukturierte Analyse von Kundenverträgen eines Akquisitionskandidaten hinsichtlich
Datenschutz-, Security- und Compliance-Anforderungen sowie Haftungsrisiken.
Identifikation von vertraglichen Risiken, Lücken und Deal-relevanten Klauseln
im Kontext von DSGVO, DORA, ISO 27001, NIS2 und weiterer einschlägiger Regulatorik.

---

## System Prompt

```
Du bist ein erfahrener Rechtsanwalt und Compliance-Experte mit Spezialisierung auf
IT-, Datenschutz- und Technologieverträge im DACH-Raum. Du analysierst Kundenverträge
auf Compliance-Anforderungen, Haftungsklauseln und regulatorische Risiken im Kontext
von M&A Due Diligence. Du kennst DSGVO, DORA, ISO 27001, NIS2, BDSG, nDSG und weitere
einschlägige Regulatorik in der Tiefe. Deine Antworten sind präzise, risikobasiert
und auf C-Level-Kommunikation ausgerichtet.
Antworte auf Deutsch, ausser explizit anders angegeben.
```

---

## Prompt Template

```
Analysiere die folgenden Kundenverträge des Akquisitionskandidaten hinsichtlich
Datenschutz, Informationssicherheit, regulatorischer Compliance und Haftung:

**Projektname (im Bericht verwenden):** {{project_name}}
**Unternehmen (nur interne Referenz):** {{company_name}}
**Branche:** {{industry}}
**Anzahl analysierter Verträge:** {{contract_count}}
**Kundentypen:** {{customer_types}}
<!-- z.B. Finanzinstitute, Versicherungen, öffentliche Hand, KMU, Enterprise -->
**Anwendbares Recht:** {{applicable_law}}
<!-- z.B. Schweizer Recht, deutsches Recht, österreichisches Recht -->

**Vertragsinhalt:**
{{contract_content}}
<!-- Füge hier den Vertragstext oder eine Zusammenfassung der Verträge ein.
     Die im Datenraum verfügbaren Verträge ergeben sich aus Schritt 1
     (01_datenraum-matching.md) — dort als "Fertig" zugeordnete Vertragsdokumente. -->

---

### 1. Datenschutz & Auftragsverarbeitung (DSGVO / nDSG / BDSG)

Prüfe:
- [ ] Auftragsverarbeitungsvertrag (AVV/DPA) vorhanden und vollständig?
- [ ] Sind Verarbeitungszwecke, Datenkategorien und betroffene Personen klar definiert?
- [ ] Weisungsgebundenheit des Auftragnehmers geregelt?
- [ ] Subunternehmer-/Subprozessor-Klauseln: Zustimmungspflicht des Kunden?
- [ ] Pflichten bei Datenpannen: Meldepflicht an Kunden (Frist, Form, Inhalt)?
- [ ] Lösch- und Rückgabepflichten nach Vertragsende geregelt?
- [ ] Drittlandübermittlungen (z.B. USA) vertraglich abgesichert (SCC, etc.)?
- [ ] Datenschutz-Audits durch Kunden: Recht vorhanden? Aufwand geregelt?
- [ ] Change-of-Control-Klauseln bei Unternehmensübernahme bezüglich Datenschutz?

**Haftung Datenschutz:**
- [ ] Haftungsregelung bei Datenschutzverstössen (Schadensersatz nach Art. 82 DSGVO)?
- [ ] Haftungsobergrenze (Cap) für Datenschutzvorfälle definiert?
- [ ] Wer haftet gegenüber Aufsichtsbehörden und Betroffenen — Auftraggeber oder Auftragnehmer?
- [ ] Freistellungsklauseln (Indemnification) bei Bussen durch Datenschutzbehörden?

---

### 2. DORA — Digital Operational Resilience Act

*(Relevant wenn Kunden Finanzinstitute, Versicherungen oder Finanzmarktinfrastrukturen sind)*

Prüfe:
- [ ] Ist das Unternehmen als IKT-Drittdienstleister gemäss DORA eingestuft?
- [ ] Sind DORA-konforme Vertragsklauseln vorhanden (Art. 30 DORA)?

  Pflichtinhalte gemäss Art. 30 DORA:
  - [ ] Vollständige Beschreibung der erbrachten IKT-Dienstleistungen
  - [ ] Standorte der Datenverarbeitung und Datenspeicherung angegeben?
  - [ ] Zugänglichkeits-, Verfügbarkeits-, Integritäts- und Sicherheitsanforderungen definiert?
  - [ ] Regelungen zu IKT-Vorfallsmeldungen (Zeitrahmen, Format, Verantwortlichkeit)?
  - [ ] Business-Continuity-Anforderungen und Wiederherstellungsziele (RTO/RPO) vereinbart?
  - [ ] Auditrecht des Finanzunternehmens und der Aufsichtsbehörden verankert?
  - [ ] Unterstützungspflichten bei behördlichen Prüfungen?
  - [ ] Subunternehmer-Regelungen: Zustimmungspflicht, Weitergabe von DORA-Pflichten?
  - [ ] Exit-Strategie und Kündigungsrechte bei Compliance-Verstössen geregelt?
  - [ ] Recht auf Zugang zu Daten und Systemen im Notfall / bei Kündigung?

**Haftung DORA:**
- [ ] Haftung bei Nichteinhaltung von DORA-Anforderungen geregelt?
- [ ] Vertragsstrafen (Penalties) bei Verletzung von RTO/RPO oder Meldepflichten?
- [ ] Haftung bei Ausfall kritischer IKT-Dienste (Business Interruption)?

---

### 3. Informationssicherheit & ISO 27001 / SOC 2

Prüfe:
- [ ] Verpflichtung zur Einhaltung von Sicherheitsstandards (ISO 27001, SOC 2, TISAX) vertraglich vereinbart?
- [ ] Anforderungen an Zertifizierungen: Muss das Unternehmen zertifiziert sein / bleiben?
- [ ] Was passiert vertraglich wenn eine Zertifizierung wegfällt (Kündigungsrecht des Kunden)?
- [ ] Sicherheitsanforderungen an Subunternehmer/Subprozessoren geregelt?
- [ ] Penetrationstest-Pflichten oder Recht des Kunden auf eigene Sicherheitstests?
- [ ] Schwachstellenmanagement und Patch-Pflichten vertraglich definiert (Fristen)?
- [ ] Sicherheitsvorfallsmeldung an Kunden: Frist und Inhalt festgelegt?
- [ ] Mindestanforderungen an Verschlüsselung, Zugriffskontrolle, MFA?
- [ ] Anforderungen an Backup und Wiederherstellung vertraglich verankert?

**Haftung Informationssicherheit:**
- [ ] Haftung bei Sicherheitsvorfällen und Datenpannen beim Kunden (Folgeschäden)?
- [ ] Haftungsobergrenze (Cap): wie hoch, bezogen auf Jahresvertragswert oder absolut?
- [ ] Ausschluss von Folgeschäden (Consequential Damages)?
- [ ] Cyber-Versicherungspflicht vertraglich vorgeschrieben (Mindestdeckungssumme)?
- [ ] Freistellung (Indemnification) bei durch Sicherheitsvorfälle ausgelösten Drittschäden?

---

### 4. NIS2 — Netz- und Informationssicherheitsrichtlinie

*(Relevant wenn Kunden oder das Unternehmen selbst als wesentliche/wichtige Einrichtung eingestuft ist)*

Prüfe:
- [ ] NIS2-Einstufung des Unternehmens als Lieferant / Dienstleister berücksichtigt?
- [ ] Sicherheitsanforderungen gemäss NIS2 Art. 21 vertraglich verankert?
- [ ] Meldepflichten bei Vorfällen (24h Erstmeldung, 72h Folgemeldung) vertraglich geregelt?
- [ ] Supply-Chain-Sicherheitsanforderungen in Kundenverträgen verankert?
- [ ] Auditrechte der Kunden zur Überprüfung der NIS2-Compliance?

---

### 5. Allgemeine Haftungsstruktur & Vertragsrisiken

Prüfe:
- [ ] **Haftungsobergrenze (Liability Cap):** Wie hoch? (z.B. 1x / 2x Jahresgebühr, absoluter Betrag)
- [ ] **Unbegrenzte Haftung:** Gibt es Ausnahmen vom Cap? (z.B. Vorsatz, grobe Fahrlässigkeit, Datenschutzverstösse)
- [ ] **Gegenseitigkeit:** Gilt der Cap auch für Kundenforderungen oder nur für Anbieterleistungen?
- [ ] **Folgeschäden:** Sind entgangener Gewinn, Reputationsschäden und indirekte Schäden ausgeschlossen?
- [ ] **Vertragsstrafen (Penalties):** Gibt es SLA-Strafen (Service Credits)? Wie hoch und capped?
- [ ] **Gewährleistungen (Warranties):** Welche Zusicherungen werden zu Sicherheit/Compliance gemacht?
- [ ] **Freistellung (Indemnification):** Bei welchen Ereignissen muss das Unternehmen den Kunden freistellen?
- [ ] **Gerichtsstand und anwendbares Recht:** Welches Recht gilt, welches Gericht ist zuständig?
- [ ] **Change-of-Control:** Gibt es Kündigungsrechte des Kunden bei Unternehmensübernahme?
- [ ] **Laufzeit und Kündigung:** Mindestlaufzeiten, Kündigungsfristen, ausserordentliche Kündigung bei Compliance-Verletzungen?

---

### 6. Branchenspezifische Anforderungen

Prüfe je nach Kundentyp:
- [ ] **Finanzsektor:** FINMA-Rundschreiben (CH), MaRisk / BAIT (DE), BaFin-Anforderungen, DORA
- [ ] **Gesundheitswesen:** HIPAA (USA-Kunden), MedTech-Regulatorik, Patientendatenschutz
- [ ] **Öffentliche Hand:** Spezifische Datenschutz- und Sicherheitsanforderungen für Behörden
- [ ] **Kritische Infrastruktur:** KRITIS-Anforderungen (DE), NIS2-verschärfte Pflichten
- [ ] **Weitere:** {{regulatory_requirements}}

---

### 7. Change-of-Control & M&A-spezifische Risiken

Prüfe:
- [ ] Haben Kunden ein Sonderkündigungsrecht bei Unternehmensübernahme (Change of Control)?
- [ ] Müssen Kunden der Vertragsübertragung auf den Käufer explizit zustimmen?
- [ ] Gibt es Preisanpassungsrechte des Kunden nach einer Übernahme?
- [ ] Sind Compliance-Zertifizierungen (ISO 27001, SOC 2) an den bisherigen Inhaber geknüpft?
- [ ] Müssen Datenschutzvereinbarungen nach Closing neu abgeschlossen werden?

---

### Vertraulichkeitsregeln

1. **Projektname statt Firmenname:** Verwende im Bericht ausschliesslich
   {{project_name}}. Der echte Firmenname darf nicht erscheinen.
2. **Funktionen statt Namen:** Personen nur mit ihrer Funktion benennen,
   keine Personennamen.
3. **Kundennamen:** Kunden des Targets nur pseudonymisiert nennen
   (z.B. "Kunde A — Finanzinstitut", "Kunde B — Versicherung"), ausser
   der Name ist für die Risikobewertung zwingend erforderlich.

---

### Gewünschter Output

Erstelle einen strukturierten Vertragsanalyse-Bericht mit:

1. **Executive Summary** (max. 1 Seite — C-Level geeignet)

2. **Vertrags-Compliance Maturity Rating** — Bewertung 1–5 pro Bereich plus Gesamtwert.
   Skala: 1 = Kritisch / 2 = Unzureichend / 3 = Grundlegend / 4 = Gut / 5 = Sehr gut

   | Bereich | Rating (1–5) | Begründung |
   |---|---|---|
   | Datenschutz & Auftragsverarbeitung | [1–5] | [1 Satz] |
   | DORA-Konformität (falls anwendbar) | [1–5] | [1 Satz] |
   | Informationssicherheit & Zertifizierungen | [1–5] | [1 Satz] |
   | NIS2-Konformität (falls anwendbar) | [1–5] | [1 Satz] |
   | Haftungsstruktur & Risikoverteilung | [1–5] | [1 Satz] |
   | Change-of-Control-Absicherung | [1–5] | [1 Satz] |
   | **Gesamt Vertrags-Maturity** | **[1–5]** | **[1 Satz Gesamtbewertung]** |

   Dieses Rating wird im Master-DD-Bericht (`03_master-dd-bericht.md`) in der
   Maturity-Übersicht als Zeile "Kundenverträge" übernommen.
   Nicht anwendbare Bereiche (z.B. DORA ohne Finanzkunden) als "n/a" kennzeichnen
   und aus der Gesamtbewertung ausklammern.

3. **Haftungsmatrix:** Tabellarische Übersicht aller identifizierten Haftungsrisiken mit Höhe und Wahrscheinlichkeit
4. **Compliance-Gap-Analyse:** Welche regulatorischen Anforderungen sind vertraglich nicht oder unzureichend abgedeckt?
5. **Risk-Register** (Kritikalität: Critical / High / Medium / Low)
6. **Red Flags** (Deal-Breaker oder Punkte für Kaufpreisanpassung / Warranties im SPA)
7. **Empfehlungen:** Vertragsanpassungen die nach Closing prioritär vorgenommen werden sollten
8. **Offene Punkte:** Verträge oder Klauseln die weiterer Prüfung bedürfen

Format: Tabellarisch wo sinnvoll, Sprache: Deutsch
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{project_name}}` | Interner Projektname — wird im Bericht verwendet | Projekt Alpha |
| `{{company_name}}` | Echter Firmenname — nur interne Referenz, **nicht** im Bericht | Musterfirma AG |
| `{{industry}}` | Branche | Software / Fintech / Gesundheit |
| `{{contract_count}}` | Anzahl analysierter Verträge | 12 Kundenverträge |
| `{{customer_types}}` | Art der Kunden | Banken, Versicherungen, KMU |
| `{{applicable_law}}` | Anwendbares Vertragsrecht | Schweizer Recht / deutsches Recht |
| `{{contract_content}}` | Vertragstext oder Zusammenfassung | Vertragstext einfügen |
| `{{regulatory_requirements}}` | Weitere Branchenregulatorik | FINMA, BaFin, HIPAA |

---

## Ergänzende Prompts

### Follow-up: Haftungsvergleich über mehrere Verträge
```
Vergleiche die Haftungsklauseln aus den analysierten Kundenverträgen von {{company_name}}.
Erstelle eine Matrix: Welche Verträge haben die höchsten Haftungsrisiken?
Wo gibt es uneinheitliche Regelungen die nach Closing harmonisiert werden müssen?
```

### Follow-up: DORA-Lückenanalyse
```
Fokussiere auf die DORA-Compliance der Kundenverträge von {{company_name}}.
Welche Pflichtinhalte gemäss Art. 30 DORA fehlen in den Verträgen?
Erstelle eine priorisierte Liste der notwendigen Vertragsanpassungen mit Musterformulierungen.
```

### Follow-up: Change-of-Control-Risiken
```
Analysiere alle Change-of-Control-Klauseln in den Kundenverträgen von {{company_name}}.
Welche Kunden könnten die Übernahme zum Anlass nehmen den Vertrag zu kündigen oder neu zu verhandeln?
Bewerte das Umsatzrisiko und empfehle eine Kundenkommunikationsstrategie.
```

### Follow-up: SPA-Warranties
```
Basierend auf den identifizierten Compliance-Lücken in den Kundenverträgen von {{company_name}}:
Welche Garantien (Warranties) und Freistellungen (Indemnities) sollten im SPA verankert werden?
Formuliere konkrete Warranty-Texte für die kritischsten Punkte.
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung — DSGVO, DORA, ISO 27001, NIS2, Haftung, Change-of-Control | 2026-05-20 | CISO |
| 1.1 | Vertrags-Compliance Maturity Rating (1–5) im Output ergänzt — wird vom Master-DD-Bericht benötigt | 2026-09-03 | CISO |
| 1.2 | Vertraulichkeitsregeln ergänzt (Projektname statt Firmenname, Funktionen statt Namen, Kundennamen pseudonymisiert); Verweis auf Schritt 1 bei `{{contract_content}}` | 2026-09-03 | CISO |
| 1.3 | Zielmodell auf Claude Opus 5.5 umgestellt | 2026-10-13 | CISO |
