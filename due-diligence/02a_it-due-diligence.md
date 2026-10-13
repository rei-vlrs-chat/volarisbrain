---
title: "M&A IT Due Diligence"
version: 2.4
author: CISO
use_case: M&A / Due Diligence
model: Claude Opus 5.5
language: de/en
last_updated: 2026-10-13
tags: [m&a, due-diligence, it-infrastruktur, ciso, dach]
---

# Prompt: M&A IT Due Diligence Assessment

## Zweck
Strukturierte Analyse der IT-Landschaft und Integrationsrisiken eines Akquisitionskandidaten.
Dient als Grundlage für die Risikobewertung und Integrationsplanung im M&A-Prozess.

---

## System Prompt

```
Du bist ein erfahrener IT-Berater mit Fokus auf M&A Due Diligence in der DACH-Region.
Du analysierst IT-Infrastrukturen, technische Schulden und Integrationsrisiken im Kontext
von Unternehmensübernahmen. Deine Antworten sind präzise, risikobasiert und auf
C-Level-Kommunikation ausgerichtet.
Antworte auf Deutsch, ausser explizit anders angegeben.
```

---

## Prompt Template

```
Führe eine IT Due Diligence für folgenden Akquisitionskandidaten durch:

**Projektname (im Bericht verwenden):** {{project_name}}
**Unternehmen (nur interne Referenz):** {{company_name}}
**Branche:** {{industry}}
**Unternehmensgrösse:** {{company_size}} Mitarbeitende
**Standorte:** {{locations}}
**Deal-Typ:** {{deal_type}}
<!-- z.B. Full Acquisition / Majority Stake / Asset Deal -->
**Zeitrahmen Closing:** {{closing_date}}
**Muttergesellschaft vorhanden:** {{parent_company}}
<!-- Ja / Nein — relevant für Infrastruktur-Abhängigkeiten -->
**Branchenregulatorik:** {{regulatory_requirements}}
<!-- z.B. FINMA, NIS2, DORA, KRITIS — bestimmt Anforderungen an Verfügbarkeit,
     Ausfallsicherheit und Nachweispflichten der IT-Infrastruktur -->

**Verfügbare Unterlagen:** {{available_docs}}
<!-- Aus Schritt 1 (01_datenraum-matching.md): die als "Fertig" zugeordneten
     Dokumente aus dem Datenraum. Zusätzlich: was ausserhalb des VDR vorliegt. -->

---

### 1. IT-Infrastruktur & Netzwerk

Analysiere und bewerte:
- [ ] On-Premise vs. Cloud-Anteil (AWS / Azure / GCP / Private Cloud)
- [ ] Netzwerk-Architektur und Segmentierung (Netzwerktyp: MPLS, IPSEC, etc.)
- [ ] Internetverbindung und Bandbreite pro Bürostandort
- [ ] Verbindung zur Muttergesellschaft oder anderen Entitäten (VPN, WAN) — muss bei Übernahme ersetzt werden?
- [ ] Gibt es eine separate Entität, die Infrastruktur oder Services bereitstellt?
- [ ] Active Directory Domain (alle Büros im gleichen AD? Mit anderen Unternehmen geteilt?)
- [ ] E-Mail-Plattform (Produkt + Version, z.B. MS Exchange 2019 / M365)
- [ ] E-Mail-Domäne(n) — mit anderen Unternehmen geteilt?
- [ ] E-Mail-Server: lokal / zentral bei Muttergesellschaft / Cloud
- [ ] Extern gehostete Applikationen (bei Muttergesellschaft oder Cloud)
- [ ] Öffentliche IP-Adressen inventarisiert?
- [ ] End-of-Life / nicht patchbare Systeme identifiziert und quantifiziert
- [ ] Computerhardware: geleast oder gekauft? Leasingbedingungen und Exit-Klauseln?
- [ ] Anteil veralteter Hardware (Laptops, Server, Netzwerkgeräte) — Ersatzbedarf in 12 Monaten?
- [ ] File-Sharing- und Intranet-Systeme vorhanden?
- [ ] ERP/CRM-Systeme und Lizenzmodelle
- [ ] Backup- und Recovery-Konzepte (RTO/RPO definiert und getestet?)

---

### 2. Business Continuity & Resilienz

- [ ] Business Impact Assessment (BIA) durchgeführt? Kritische Funktionen in den Bereichen Software-Support, Betrieb und Finanzen identifiziert?
- [ ] Business Continuity Plan (BCP) vorhanden? Wann zuletzt überprüft und getestet?

---

### 3. Software, Lizenzen & Cloud-Abonnements

- [ ] Vollständige Softwarelizenzliste (Produkt, Version, Anzahl, Verlängerungsdatum)
- [ ] Lizenz-Compliance: Sind ausreichend Lizenzen für alle genutzten Tools vorhanden?
- [ ] Cloud-Abonnement-Liste (z.B. M365 E3 / 100 User / Jahresabo, Renewal-Datum)
- [ ] Microsoft-Partnership-Berechtigungen genutzt? IUR-Schlüssel (Internal Use Rights) eingelöst?
- [ ] Lizenzvereinbarungen: lokal oder Teil einer Gruppenvereinbarung mit Muttergesellschaft?
- [ ] Change-of-Control-Klauseln in Lizenzverträgen identifiziert?
- [ ] Entwicklungstools im Einsatz (Jira, Confluence, GitHub, Azure DevOps, etc.)
- [ ] Open-Source-Software: vollständige Liste pro Softwaremodul, Lizenzarten geprüft?

---

### 4. Vendor & Third-Party Risk

- [ ] Kritische IT-Dienstleister und Abhängigkeiten
- [ ] MSP/MSSP-Verträge (Laufzeit, SLAs, Exit-Klauseln)
- [ ] Cloud-Provider-Verträge und Datenverarbeitungsvereinbarungen
- [ ] Drittanbieter-Lizenzkonformität (Oracle, Microsoft, etc.)

---

### 5. IT-Personal & Organisation

- [ ] IT-Organisationsstruktur und Schlüsselpersonen
- [ ] Key-Person-Dependency-Risiken
- [ ] Outsourcing-Anteil und Nearshore/Offshore-Modelle
- [ ] IT-Budget (Capex/Opex, IT-Spend als % des Umsatzes)

---

### 6. Integrationsrisiken

Bewerte auf Basis der obigen Erkenntnisse:
- [ ] Integrationsaufwand (Low / Medium / High / Very High)
- [ ] Geschätzte Integrationskosten (IT-Migration, Harmonisierung)
- [ ] Abhängigkeiten von Muttergesellschaft — was muss nach Closing ersetzt werden?
- [ ] Inkompatible Systeme oder Standards
- [ ] Tag-1-Readiness (kann das Unternehmen eigenständig operieren?)
- [ ] Synergien vs. Risiken

---

### Vertraulichkeitsregeln

1. **Projektname statt Firmenname:** Verwende im Bericht ausschliesslich
   {{project_name}}. Der echte Firmenname darf nicht erscheinen.
2. **Funktionen statt Namen:** Personen nur mit ihrer Funktion benennen
   (z.B. "IT-Leiter"), keine Personennamen.

---

### Gewünschter Output

Erstelle einen strukturierten Due-Diligence-Bericht mit:

1. **Executive Summary** (max. 1 Seite, C-Level geeignet)

2. **IT Maturity Rating** — Bewertung 1–5 pro Bereich plus Gesamtwert.
   Skala: 1 = Kritisch / 2 = Unzureichend / 3 = Grundlegend / 4 = Gut / 5 = Sehr gut

   | Bereich | Rating (1–5) | Begründung |
   |---|---|---|
   | IT-Infrastruktur & Netzwerk | [1–5] | [1 Satz] |
   | Business Continuity & Resilienz | [1–5] | [1 Satz] |
   | Software, Lizenzen & Cloud | [1–5] | [1 Satz] |
   | Vendor & Third-Party Risk | [1–5] | [1 Satz] |
   | IT-Personal & Organisation | [1–5] | [1 Satz] |
   | **Gesamt IT Maturity** | **[1–5]** | **[1 Satz Gesamtbewertung]** |

   Dieses Rating wird im Master-DD-Bericht (`03_master-dd-bericht.md`) in der
   Maturity-Übersicht als Zeile "IT-Infrastruktur" übernommen.

3. **Risk-Register** (Kritikalität: Critical / High / Medium / Low)
4. **Red Flags** (Deal-Breaker oder Punkte für Kaufpreisanpassung)
5. **Empfehlungen** (sofortige Massnahmen vs. Post-Closing-Integrationsplan)
6. **Offene Punkte** (fehlende Informationen, weiterer Abklärungsbedarf)

Format: Tabellarisch wo sinnvoll, Sprache: Deutsch
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{project_name}}` | Interner Projektname — wird im Bericht verwendet | Projekt Alpha |
| `{{company_name}}` | Echter Firmenname — nur interne Referenz, **nicht** im Bericht | Musterfirma AG |
| `{{industry}}` | Branche | Software / Fintech / Industrie |
| `{{company_size}}` | Mitarbeiterzahl | 250 |
| `{{locations}}` | Standorte | Zürich, München, Wien |
| `{{deal_type}}` | Art der Transaktion | Full Acquisition |
| `{{closing_date}}` | Geplanter Abschluss | Q3 2026 |
| `{{parent_company}}` | Muttergesellschaft vorhanden? | Ja / Nein |
| `{{available_docs}}` | Vorliegende Unterlagen | IT-Inventar, ISO-Zertifikat |
| `{{regulatory_requirements}}` | Branchenregulatorik | FINMA, NIS2 |

---

## Ergänzende Prompts

### Follow-up: Tiefenanalyse eines Bereichs
```
Basierend auf dem IT-DD-Bericht zu {{company_name}}:
Führe eine vertiefte Analyse des Bereichs [{{focus_area}}] durch.
Fokus auf: konkrete Risikoquantifizierung und Massnahmenempfehlungen mit Zeitplan.
```

### Follow-up: Kaufpreisrelevanz
```
Bewerte die identifizierten IT-Risiken aus dem Due-Diligence-Bericht zu {{company_name}}
hinsichtlich ihrer Kaufpreisrelevanz. Welche Punkte rechtfertigen einen Abschlag
oder sollten als Conditions Precedent im SPA verankert werden?
```

### Follow-up: Integrationsplanung
```
Erstelle basierend auf dem IT-DD-Bericht zu {{company_name}} einen detaillierten
IT-Integrationsplan für die ersten 100 Tage nach Closing.
Priorisiere: Infrastruktur-Separation von Muttergesellschaft, kritische Systemmigration
und Quick Wins. Berücksichtige Tag-1-Readiness und Ressourcenverfügbarkeit.
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung | 2025-05-12 | CISO |
| 2.0 | Erweitert basierend auf DD-Anforderungsliste (Sektionen 9 & 10) | 2026-05-20 | CISO |
| 2.1 | Section 10 (Produkt, R&D, Tech Debt, IT Costs) entfernt — nur Section 9 relevant | 2026-05-20 | CISO |
| 2.2 | IT Maturity Rating (1–5) im Output ergänzt — wird vom Master-DD-Bericht benötigt | 2026-09-03 | CISO |
| 2.3 | Vertraulichkeitsregeln ergänzt (Projektname statt Firmenname, Funktionen statt Namen); `{{regulatory_requirements}}` im Template aktiviert; Verweis auf Schritt 1 bei `{{available_docs}}` | 2026-09-03 | CISO |
| 2.4 | Zielmodell auf Claude Opus 5.5 umgestellt | 2026-10-13 | CISO |
