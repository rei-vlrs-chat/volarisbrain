---
title: "M&A Security Due Diligence"
version: 2.3
author: CISO
use_case: M&A / Due Diligence
model: Claude Opus 5.5
language: de/en
last_updated: 2026-10-13
tags: [m&a, due-diligence, security, cyber, ciso, dach]
---

# Prompt: M&A Security Due Diligence Assessment

## Zweck
Strukturierte Bewertung der Cybersecurity-Posture und des Security-Reifegrads
eines Akquisitionskandidaten. Identifikation von Cyber-Risiken, technischen Schulden
und Sicherheitslücken im Kontext von Unternehmensübernahmen.

---

## System Prompt

```
Du bist ein erfahrener Cybersecurity-Experte und CISO-Berater mit Fokus auf M&A Due Diligence
in der DACH-Region. Du analysierst Security-Architekturen, Reifegradmodelle, Incident-Historien
und Cyber-Risiken im Kontext von Unternehmensübernahmen. Du kennst aktuelle Bedrohungslagen,
gängige Frameworks (ISO 27001, NIST CSF, CIS Controls) und regulatorische Anforderungen
(NIS2, DORA, TISAX). Deine Antworten sind präzise, risikobasiert und auf C-Level-Kommunikation
ausgerichtet. Antworte auf Deutsch, ausser explizit anders angegeben.
```

---

## Prompt Template

```
Führe eine Security Due Diligence für folgenden Akquisitionskandidaten durch:

**Projektname (im Bericht verwenden):** {{project_name}}
**Unternehmen (nur interne Referenz):** {{company_name}}
**Branche:** {{industry}}
**Unternehmensgrösse:** {{company_size}} Mitarbeitende
**Standorte:** {{locations}}
**Deal-Typ:** {{deal_type}}
<!-- z.B. Full Acquisition / Majority Stake / Asset Deal -->
**Zeitrahmen Closing:** {{closing_date}}
**Kritische Assets / Geschäftsgeheimnisse:** {{critical_assets}}
<!-- z.B. IP, Kundendatenbank, Produktionssysteme, Quellcode -->

**Verfügbare Unterlagen:** {{available_docs}}
<!-- Aus Schritt 1 (01_datenraum-matching.md): die als "Fertig" zugeordneten
     Dokumente aus dem Datenraum. Zusätzlich: was ausserhalb des VDR vorliegt.
     z.B. ISMS-Dokumentation, Policies, ISO-Zertifikat, PenTest-Report -->

---

### 1. Security Governance & Organisation

Analysiere und bewerte:
- [ ] Person / Funktion verantwortlich für Informationssicherheit vorhanden? (CISO, ISB, etc. — Rolle, Reporting-Linie)
- [ ] Security-Strategie und -Roadmap dokumentiert
- [ ] Information Security Management System (ISMS) etabliert
- [ ] IT- und Datensicherheitsrichtlinien — formell, veröffentlicht, aktuell?
- [ ] Security Policies Teil des Mitarbeiter-Onboardings (überprüft und bestätigt)?
- [ ] Security-Budget (absolut und als % des IT-Budgets)
- [ ] Security Awareness Training — LMS vorhanden, Häufigkeit, Abdeckung, Nachweise
- [ ] Board-Level Reporting zu Cyber-Risiken

---

### 2. Zertifizierungen & Frameworks

- [ ] ISO 27001 (Zertifiziert? Scope? Letzte Auditdaten? Nächste Überwachungsaudit?)
- [ ] SOC 2 Type I / Type II (Aktueller Report vorhanden?)
- [ ] TISAX (relevant für Automotive-Zulieferer)
- [ ] BSI IT-Grundschutz (relevante Behörden/KRITIS-Umgebungen)
- [ ] CIS Controls Implementierungsgrad (Level 1 / 2 / 3)
- [ ] NIST CSF Reifegrad (Identify / Protect / Detect / Respond / Recover)
- [ ] Compliance-Auditing und -Monitoring: aktueller Ansatz zur regelmässigen Überprüfung
- [ ] Branchenspezifisch: {{certifications_required}}
<!-- z.B. PCI-DSS, HIPAA, DORA, NIS2, SSAE16/18 -->

---

### 3. Technische Security-Architektur & Physische Sicherheit

- [ ] Netzwerksegmentierung und Perimeter-Schutz (Firewall, WAF, IDS/IPS)
- [ ] Zero-Trust-Ansatz oder klassisches Perimeter-Modell?
- [ ] Endpoint Detection & Response (EDR/XDR) — Abdeckungsgrad (% der Endpoints), Version, Renewal-Datum
- [ ] E-Mail-Security (Anti-Phishing, DMARC/DKIM/SPF konfiguriert?)
- [ ] Multi-Faktor-Authentifizierung (MFA) — welche IT-Dienste erfordern MFA?
- [ ] Privileged Access Management (PAM)
- [ ] Patch-Management (interne Systeme): Methode, Abdeckung, Patch-Frequenz
- [ ] Patch-Management (kundenorientierte gehostete Infrastruktur): Methode, Abdeckung, Frequenz
- [ ] Vulnerability-Management: Scanner vorhanden, Häufigkeit, Remediation-SLAs
- [ ] Serverräume physisch gesichert und getrennt? (abgeschlossen / Zutrittskontrolle)

---

### 4. Identity & Access Management (IAM)

- [ ] Identity Provider (AD, Azure AD, Okta etc.) und Qualität
- [ ] Authentifizierung/Autorisierung im Produkt (RBAC, OAuth, SAML, etc.)
- [ ] Regelmässige Access Reviews / Rezertifizierungen
- [ ] Offboarding-Prozesse für ausscheidende Mitarbeitende
- [ ] Service Accounts und non-human Identities inventarisiert
- [ ] Anzahl privilegierter Accounts — nachvollziehbar und minimiert?
- [ ] Single Sign-On (SSO) Abdeckung
- [ ] Verschlüsselung (at rest / in transit) im Einsatz?

---

### 5. Security Operations & Monitoring

- [ ] SIEM vorhanden? (Produkt, Abdeckungsgrad, Alerting-Qualität)
- [ ] Security Operations Center (SOC) — intern / extern / MSSP
- [ ] Log-Management (Aufbewahrungsdauer, Vollständigkeit)
- [ ] Threat Detection Capabilities (Use Cases, MITRE ATT&CK Coverage)
- [ ] 24/7 Monitoring oder nur Geschäftszeiten?
- [ ] Threat Intelligence genutzt?
- [ ] Mean Time to Detect (MTTD) / Mean Time to Respond (MTTR) bekannt?

---

### 6. Incident Response & Business Continuity

<!-- BIA und BCP werden in der IT-DD (02a, Abschnitt 2) geprüft. Hier nur, ob
     IRP und DRP auf die dort identifizierten kritischen Funktionen abgestimmt sind. -->
- [ ] IRP und DRP auf die kritischen Funktionen aus BIA/BCP abgestimmt?
- [ ] Incident Response Plan (IRP) vorhanden, getestet, aktuell?
- [ ] Letzte IRP-Übung / Tabletop Exercise (Datum, Ergebnisse)
- [ ] Ransomware-Playbook vorhanden?
- [ ] Disaster Recovery Plan (DRP) — RTO / RPO definiert und technisch erreichbar?
- [ ] Offline-Backups vorhanden (immutable, air-gapped)?
- [ ] Kommunikationsplan für Sicherheitsvorfälle (intern / extern / Behörden)
- [ ] Meldepflichten bei Sicherheitsvorfällen — Prozesse etabliert?

---

### 7. Penetration Testing & Schwachstellenmanagement

- [ ] Penetration Test Produkt/Kundenlösung: letzter Test (Datum, Scope, Ergebnisse)?
- [ ] Vulnerability Scan Produkt/Kundenlösung: letzter Scan (Datum, letzte 3 Monate)?
- [ ] Vulnerability Scan interne Systeme/Netzwerke/Endpoints (Datum, Ergebnisse)?
- [ ] Interne Sicherheitsbewertungen durchgeführt und dokumentiert?
- [ ] Externe Sicherheitsbewertungen durchgeführt? (Dritte, Kunden)
- [ ] Red Team Exercises / Adversary Simulation durchgeführt?
- [ ] Bug Bounty Programm vorhanden?
- [ ] Responsible Disclosure Policy publiziert?
- [ ] Offene kritische / high Findings aus letzten Audits und deren Remediation-Status

---

### 8. Secure Software Development & Quellcodeschutz

- [ ] Secure Software Development Lifecycle (Secure SDLC) implementiert? Prozessdokumente vorhanden?
- [ ] Security-Checks im Entwicklungsprozess: SAST / DAST / Dependency Scanning integriert?
- [ ] Quellcode-Schutz: Wie wird der Produktquellcode gesichert (Backup)?
- [ ] Quellcode-Recovery: Wann wurden Wiederherstellungsverfahren zuletzt erfolgreich getestet?
- [ ] Quellcode-Escrow: Sind Kopien aller unterstützten Versionen bei einem unabhängigen Treuhänder hinterlegt?
- [ ] Endbenutzerschulungen zu Secure Development vorhanden?

---

### 9. Cloud Security

- [ ] Cloud-Provider und genutzte Services (AWS / Azure / GCP / Multi-Cloud)
- [ ] Cloud Security Posture Management (CSPM) im Einsatz?
- [ ] IAM in der Cloud — Least Privilege, keine Root-Keys in aktiver Verwendung
- [ ] Öffentlich exponierte Storage Buckets / Datenbanken geprüft?
- [ ] Container Security (Kubernetes, Docker) — Härtung, Runtime-Security
- [ ] CI/CD Pipeline Security (DevSecOps, SAST/DAST integriert?)

---

### 10. Cyber-Vorfall-Historie & Exposure

- [ ] Bekannte Sicherheitsvorfälle / Datenpannen der letzten 3 Jahre (Ransomware, APT, etc.)
- [ ] Darknet-Exposure (gestohlene Credentials, Datensätze in Darknet-Foren)
- [ ] Öffentlich bekannte CVEs in eingesetzter Software — ungepatchte Systeme
- [ ] Phishing-Angriffe — Häufigkeit, Erfolgsrate
- [ ] Supply-Chain-Angriffe oder kompromittierte Drittanbieter

---

### 11. Datenschutz & Datenverantwortung (Security-Perspektive)

- [ ] Hält das Unternehmen Kundendaten vor? Hosting: eigenes RZ / Azure / AWS / GCP?
- [ ] Enthält das Produkt personenbezogene Daten (PII) oder besondere Kategorien (Gesundheit, Religion, etc.)?
- [ ] PCI-DSS: Werden Zahlungskarten verarbeitet? Ist die Lösung PCI-DSS-konform?
<!-- Data Retention Policy, BAAs und Privacy Notice werden in der
     Datenschutz-DD (02c) geprüft. -->


---

### 12. Compliance & Integrität

- [ ] Anti-Korruptions-Compliance: Richtlinien, Guidelines und Schulungsmaterialien vorhanden?
- [ ] Dokumentation bekannter Beschwerden oder Vorfälle bezüglich Verstössen gegen Antikorruptionsgesetze
- [ ] ABC-Sheet (Anti-Bribery & Corruption) ausgefüllt?
- [ ] NIS2-Pflichten: Ist das Unternehmen ein wesentlicher / wichtiger Betreiber?
- [ ] DORA-Anforderungen (relevant für Finanzsektor)
- [ ] KRITIS-Einstufung?
- [ ] Branchenspezifische Security-Anforderungen: {{regulatory_requirements}}

---

### 13. Cyber-Versicherung

- [ ] Cyber-Versicherung vorhanden? (Deckungssumme, Ausschlüsse, Sublimits)
- [ ] Deckung aktuell genug? (Ransomware, Business Interruption, 3rd Party Liability)

---

### Vertraulichkeitsregeln

1. **Projektname statt Firmenname:** Verwende im Bericht ausschliesslich
   {{project_name}}. Der echte Firmenname darf nicht erscheinen.
2. **Funktionen statt Namen:** Personen nur mit ihrer Funktion benennen
   (z.B. "CISO", "IT-Leiter"), keine Personennamen.

---

### Gewünschter Output

Erstelle einen strukturierten Security-Due-Diligence-Bericht mit:

1. **Executive Summary** (max. 1 Seite, C-Level geeignet)
2. **Security Maturity Rating** — Bewertung 1–5 pro Bereich plus Gesamtwert.
   Skala: 1 = Kritisch / 2 = Unzureichend / 3 = Grundlegend / 4 = Gut / 5 = Sehr gut

   | Bereich | Abschnitte | Rating (1–5) | Begründung |
   |---|---|---|---|
   | Security Governance | 1 | [1–5] | [1 Satz] |
   | Zertifizierungen & Frameworks | 2 | [1–5] | [1 Satz] |
   | Technische Architektur | 3, 8 | [1–5] | [1 Satz] |
   | Identity & Access Management | 4 | [1–5] | [1 Satz] |
   | Security Operations & Monitoring | 5 | [1–5] | [1 Satz] |
   | Incident Response & BCP | 6, 10, 13 | [1–5] | [1 Satz] |
   | Penetration Testing | 7 | [1–5] | [1 Satz] |
   | Cloud Security | 9 | [1–5] | [1 Satz] |
   | Compliance & Regulatorik | 11, 12 | [1–5] | [1 Satz] |
   | **Gesamt Security Maturity** | | **[1–5]** | **[1 Satz Gesamtbewertung]** |

   Diese Tabelle wird im Master-DD-Bericht (`03_master-dd-bericht.md`) als
   Abschnitt 3.2 übernommen, der Gesamtwert in der Maturity-Übersicht als
   Zeile "Cybersecurity".

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
| `{{critical_assets}}` | Schützenswerte Assets | Quellcode, Kundendaten, IP |
| `{{available_docs}}` | Vorliegende Unterlagen | ISO-Zertifikat, PenTest-Report |
| `{{certifications_required}}` | Erwartete Zertifizierungen | ISO 27001, SOC 2, TISAX |
| `{{regulatory_requirements}}` | Branchenregulatorik | NIS2, DORA, FINMA |

---

## Ergänzende Prompts

### Follow-up: Tiefenanalyse eines Bereichs
```
Basierend auf dem Security-DD-Bericht zu {{company_name}}:
Führe eine vertiefte Analyse des Bereichs [{{focus_area}}] durch.
Fokus auf: konkrete Risikoquantifizierung und Massnahmenempfehlungen mit Zeitplan.
```

### Follow-up: Kaufpreisrelevanz
```
Bewerte die identifizierten Security-Risiken aus dem Due-Diligence-Bericht zu {{company_name}}
hinsichtlich ihrer Kaufpreisrelevanz. Welche Punkte rechtfertigen einen Abschlag
oder sollten als Conditions Precedent / Warranties im SPA verankert werden?
```

### Follow-up: Rapid Assessment (bei eingeschränktem Zugang)
```
Wir haben nur eingeschränkten Zugang zu Unterlagen für {{company_name}}.
Verfügbar sind lediglich: {{available_docs}}.
Erstelle ein Security-Risk-Assessment auf Basis der verfügbaren Informationen
und liste klar auf, welche zusätzlichen Informationen zwingend benötigt werden.
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung | 2026-05-20 | CISO |
| 2.0 | Erweitert um BIA, physische Sicherheit, Quellcode-Escrow, Patch-Management Hosted, PCI-DSS, Data Retention, BAAs, Anti-Korruption basierend auf realer DD-Anforderungsliste (Sektion 9) | 2026-05-20 | CISO |
| 2.1 | Vertraulichkeitsregeln ergänzt (Projektname statt Firmenname, Funktionen statt Namen); Verweis auf Schritt 1 bei `{{available_docs}}` | 2026-09-03 | CISO |
| 2.2 | Security Maturity Rating als Tabelle mit den 9 Bereichen des Master-DD-Berichts und Zuordnung der 13 Abschnitte; BIA/BCP an IT-DD (02a), Data Retention/BAAs/Privacy Notice an Datenschutz-DD (02c) abgegeben | 2026-10-13 | CISO |
| 2.3 | Zielmodell auf Claude Opus 5.5 umgestellt | 2026-10-13 | CISO |
