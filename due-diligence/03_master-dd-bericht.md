---
title: "M&A Master DD Bericht"
version: 1.4
author: CISO
use_case: M&A / Due Diligence / Konsolidierter Bericht
model: Claude Opus 5.5
language: de
last_updated: 2026-10-13
tags: [m&a, due-diligence, master-bericht, konsolidierung, risk-register, spa]
---

# Prompt: M&A Master DD Bericht

## Zweck
Konsolidierung der Einzelberichte aus IT-, Security-, Datenschutz- und Kundenvertrags-Due-Diligence
zu einem strukturierten Master-DD-Bericht. Dient als Grundlage für C-Level-Präsentation,
SPA-Verhandlungen und Post-Closing-Integration.

---

## System Prompt

```
Du bist ein erfahrener M&A Due-Diligence-Berater mit Fokus auf IT, Security und Datenschutz
in der DACH-Region. Du konsolidierst Einzelberichte aus verschiedenen DD-Bereichen zu einem
strukturierten Master-Bericht für C-Level-Kommunikation und SPA-Verhandlungen.
Deine Analyse ist präzise, risikobasiert und handlungsorientiert.
Antworte ausschliesslich auf Deutsch.
```

---

## Prompt Template

```
Erstelle einen konsolidierten Master-DD-Bericht basierend auf den folgenden Einzelberichten:

**Projekt:** {{project_name}}
**Entitäten:** {{entities}}
<!-- Anonymisiert, z.B. "Holding AG / Operating GmbH" — keine echten Firmennamen -->
**Bereiche:** IT · Security · Datenschutz · Kundenverträge
**Erstellt durch:** {{author}}
<!-- Funktion, kein Personenname — z.B. CISO -->
**Stand:** {{date}}

---

### Vertraulichkeitsregeln (gelten für den gesamten Bericht)

1. **Projektname statt Firmenname:** Verwende ausschliesslich {{project_name}}.
   Echte Firmennamen dürfen im Bericht nicht erscheinen — auch nicht in
   Überschriften, Fusszeilen oder Deckblatt.
2. **Funktionen statt Namen:** Personen ausschliesslich mit ihrer Funktion
   benennen (z.B. "IT-Leiter", "CISO"). Keine Personennamen.

### Konsolidierungsregel

Findings, die in mehreren Einzelberichten zum gleichen Sachverhalt vorkommen
(z.B. fehlender BCP in IT und Security), im konsolidierten Risk Register
(Abschnitt 6) und bei den Red Flags (Abschnitt 7) nur einmal führen — mit der
höchsten genannten Kritikalität und allen betroffenen Bereichen in der Spalte
"Bereich" (z.B. "IT / Security"). In den Bereichs-Abschnitten 2–5 bleiben sie
beim jeweiligen Bereich stehen.

---

### Eingabe: Einzelberichte

**IT Due Diligence Bericht:**
{{it_report}}

**Security Due Diligence Bericht:**
{{security_report}}

**Datenschutz Due Diligence Bericht:**
{{datenschutz_report}}

**Kundenverträge & Compliance Bericht:**
{{contracts_report}}

---

Erstelle den Master-DD-Bericht exakt in folgender Struktur:

---

## DECKBLATT

**DUE DILIGENCE — MASTER-BERICHT**
Projekt: {{project_name}}
Entitäten: {{entities}}
Bereiche: IT · Security · Datenschutz · Kundenverträge
Erstellt durch: {{author}}
Stand: {{date}} | Vertraulich — Nur für interne Verwendung

---

## KPI-ÜBERSICHT

| Analysierte Berichte | Kritische Risiken | High Risiken | Gesamt-Maturity |
|---|---|---|---|
| [Anzahl] | [Anzahl Critical] | [Anzahl High] | [Bewertung 1–5] |

---

## 1. Executive Summary

### Gesamteinschätzung
[2–3 Sätze Gesamtbewertung des Deals aus DD-Perspektive]

**Deal-Einschätzung:** [PROCEED / PROCEED WITH CONDITIONS / HIGH RISK]
[Kurze Begründung der Empfehlung]

### 1.1 Maturity-Übersicht nach Bereich

| Bereich | Maturity (1–5) | Kernbefund |
|---|---|---|
| IT-Infrastruktur | [1–5] | [1 Satz] |
| Cybersecurity | [1–5] | [1 Satz] |
| Datenschutz | [1–5] | [1 Satz] |
| Kundenverträge | [1–5] | [1 Satz] |

Maturity-Skala: 1 = Kritisch / 2 = Unzureichend / 3 = Grundlegend / 4 = Gut / 5 = Sehr gut

### 1.2 Top 5 Critical Findings

| # | Bereich | Finding |
|---|---|---|
| 1 | [Bereich] | [Kurzbeschreibung des kritischsten Findings] |
| 2 | [Bereich] | [Kurzbeschreibung] |
| 3 | [Bereich] | [Kurzbeschreibung] |
| 4 | [Bereich] | [Kurzbeschreibung] |
| 5 | [Bereich] | [Kurzbeschreibung] |

---

## 2. IT Due Diligence

**Scope:** IT-Infrastruktur, Netzwerk, Lizenzen, Business Continuity, Vendor Risk

### 2.1 Kernbefunde
[3–5 Bullet Points mit den wichtigsten Befunden aus dem IT-Bericht]

### 2.2 Risk Register IT (Auszug)

| Ref | Bereich | Befund | Level |
|---|---|---|---|
| IT-01 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| IT-02 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| [weitere relevante Findings] | | | |

---

## 3. Security Due Diligence

**Scope:** Security Governance, IAM, Monitoring, Incident Response, PenTests, Cloud Security

### 3.1 Kernbefunde
[3–5 Bullet Points mit den wichtigsten Befunden aus dem Security-Bericht]

### 3.2 Security Maturity Rating

| Bereich | Rating (1–5) | Begründung |
|---|---|---|
| Security Governance | [1–5] | [1 Satz] |
| Zertifizierungen & Frameworks | [1–5] | [1 Satz] |
| Technische Architektur | [1–5] | [1 Satz] |
| Identity & Access Management | [1–5] | [1 Satz] |
| Security Operations & Monitoring | [1–5] | [1 Satz] |
| Incident Response & BCP | [1–5] | [1 Satz] |
| Penetration Testing | [1–5] | [1 Satz] |
| Cloud Security | [1–5] | [1 Satz] |
| Compliance & Regulatorik | [1–5] | [1 Satz] |
| **Gesamt Security Maturity** | **[1–5]** | **[1 Satz Gesamtbewertung]** |

---

## 4. Datenschutz Due Diligence

**Scope:** DSGVO / nDSG / BDSG, DPO, VVT, AVVs, Betroffenenrechte, Datenpannen

### 4.1 Kernbefunde
[3–5 Bullet Points mit den wichtigsten Befunden aus dem Datenschutz-Bericht]

### 4.2 Risk Register Datenschutz (Auszug)

| Ref | Bereich | Befund | Level |
|---|---|---|---|
| DS-01 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| DS-02 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| [weitere relevante Findings] | | | |

---

## 5. Kundenverträge & Compliance

**Scope:** DSGVO-Vertragsklauseln, DORA, ISO 27001, NIS2, Haftung, Change-of-Control

### 5.1 Kernbefunde
[3–5 Bullet Points mit den wichtigsten Befunden aus dem Kundenvertrags-Bericht]

### 5.2 Risk Register Kundenverträge (Auszug)

| Ref | Bereich | Befund | Level |
|---|---|---|---|
| KV-01 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| KV-02 | [Unterbereich] | [Befund] | Critical / High / Medium / Low |
| [weitere relevante Findings] | | | |

---

## 6. Konsolidiertes Risk Register

Alle Findings bereichsübergreifend, nach Kritikalität sortiert (Critical zuerst):

| Ref | Bereich | Entität | Beschreibung | Level | SPA-Relevanz |
|---|---|---|---|---|---|
| [Ref] | [IT/Security/DS/KV] | [Entität] | [Befund] | Critical | Ja / Nein |
| [Ref] | [Bereich] | [Entität] | [Befund] | High | Ja / Nein |
| [Ref] | [Bereich] | [Entität] | [Befund] | Medium | Nein |
| [weitere Findings] | | | | | |

---

## 7. Red Flags & SPA-Relevanz

Findings mit direkter Auswirkung auf Kaufpreis, Warranties oder Closing-Bedingungen:

| # | Red Flag | Begründung | SPA-Mechanismus | Bereich |
|---|---|---|---|---|
| 1 | [Red Flag] | [Warum Deal-relevant] | Kaufpreisanpassung / Warranty / Condition Precedent | [Bereich] |
| 2 | [Red Flag] | [Begründung] | [Mechanismus] | [Bereich] |
| [weitere Red Flags] | | | | |

---

## 8. Konsolidierte Empfehlungen

### 8.1 Sofortmassnahmen (Pre-Closing / 0–90 Tage)

| # | Massnahme | Prio | Beschreibung |
|---|---|---|---|
| 1 | [Massnahme] | Critical | [Was genau zu tun ist, wer verantwortlich] |
| 2 | [Massnahme] | High | [Beschreibung] |
| [weitere] | | | |

### 8.2 Post-Closing Integration (90–365 Tage)

| # | Massnahme | Horizont | Beschreibung |
|---|---|---|---|
| 1 | [Massnahme] | 90–180 Tage | [Beschreibung] |
| 2 | [Massnahme] | 180–365 Tage | [Beschreibung] |
| [weitere] | | | |

---

## 9. Offene Punkte — Fehlende Unterlagen

Informationen die für eine vollständige DD-Bewertung noch fehlen:

| # | Bereich | Fehlende Information | Priorität | Quelle |
|---|---|---|---|---|
| 1 | [Bereich] | [Was fehlt] | Critical / High / Medium | Verkäufer / VDR / Dritte |
| 2 | [Bereich] | [Was fehlt] | [Priorität] | [Quelle] |
| [weitere] | | | | |

---

**Hinweis zur Analyse:** Dieser Master-Bericht basiert auf den Einzelberichten der vier
DD-Bereiche sowie den im VDR verfügbaren Unterlagen. Offene Punkte in Abschnitt 9
sind vor Closing zu klären. Die Bewertungen basieren auf den zum Zeitpunkt der Analyse
vorliegenden Informationen.
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{project_name}}` | Interner Projektname — wird im Bericht verwendet | Projekt Alpha |
| `{{entities}}` | Rechtliche Entitäten (anonymisiert, z.B. "Holding" / "OpCo") | Holding AG / Operating GmbH |
| `{{author}}` | Ersteller des Berichts (Funktion, kein Name) | CISO |
| `{{date}}` | Stand des Berichts | Juni 2026 |
| `{{it_report}}` | Output aus IT DD Prompt | Bericht einfügen |
| `{{security_report}}` | Output aus Security DD Prompt | Bericht einfügen |
| `{{datenschutz_report}}` | Output aus Datenschutz DD Prompt | Bericht einfügen |
| `{{contracts_report}}` | Output aus Kundenvertrags-Prompt | Bericht einfügen |

---

## Anwendung — Schritt für Schritt

### Schritt 1 — Einzelberichte erstellen
Führe die vier DD-Prompts aus und speichere die Outputs:
1. `02a_it-due-diligence.md` → IT-Bericht
2. `02b_security-due-diligence.md` → Security-Bericht
3. `02c_datenschutz-due-diligence.md` → Datenschutz-Bericht
4. `02d_kundenvertraege-compliance.md` → Kundenvertrags-Bericht

Voraussetzung: Der Datenraum wurde vorgängig mit `01_datenraum-matching.md` aufbereitet.

### Schritt 2 — Master-Prompt befüllen
Füge die vier Berichte in die entsprechenden `{{platzhalter}}` ein.

### Schritt 3 — Master-Bericht generieren
Übergib den vollständigen Prompt an Claude Opus 5.5.

### Schritt 4 — Bericht verwenden
Der Output kann direkt als:
- Word-Dokument (strukturiert kopieren)
- Basis für C-Level-Präsentation
- Grundlage für SPA-Warranty-Verhandlungen
verwendet werden.

---

## Ergänzende Prompts

### Follow-up: Executive Briefing (1 Seite)
```
Erstelle basierend auf dem Master-DD-Bericht zu {{project_name}} ein
Executive Briefing auf einer Seite für das Board / Investment Committee.
Inhalt: Deal-Empfehlung, Top 3 Risiken, Top 3 Chancen, nächste Schritte.
Keine Tabellen — Fliesstext, max. 400 Wörter.
```

### Follow-up: SPA-Warranty-Liste
```
Leite aus dem konsolidierten Risk Register und den Red Flags des Master-DD-Berichts
zu {{project_name}} eine strukturierte Liste von Warranties und Indemnities ab,
die im SPA verankert werden sollten.
Format: Warranty-Text (DE), Bereich, Kritikalität, empfohlener Mechanismus.
```

### Follow-up: 100-Tage-Plan
```
Erstelle basierend auf Abschnitt 8 des Master-DD-Berichts zu {{project_name}}
einen detaillierten 100-Tage-Integrationsplan für IT, Security und Datenschutz.
Format: Wochenweise Meilensteine, Verantwortlichkeiten, Abhängigkeiten.
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung — Struktur basierend auf bestehendem Master-DD-Bericht | 2026-06-23 | CISO |
| 1.1 | Verweise auf Einzelberichte korrigiert (neue Dateinamen 02a–02d), Hinweis auf Schritt 1 ergänzt | 2026-09-03 | CISO |
| 1.2 | Vertraulichkeitsregeln ergänzt; `{{company_name}}` durch `{{project_name}}` ersetzt; echte Firmennamen aus Platzhalter-Beispielen entfernt | 2026-09-03 | CISO |
| 1.3 | Konsolidierungsregel für bereichsübergreifende Findings ergänzt | 2026-10-13 | CISO |
| 1.4 | Zielmodell auf Claude Opus 5.5 umgestellt | 2026-10-13 | CISO |
