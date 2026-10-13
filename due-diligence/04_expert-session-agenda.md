---
title: "M&A Expert Session — Agenda-Erstellung"
version: 2.6
author: CISO
use_case: M&A / Due Diligence / Expert Session
model: Claude Opus 5.5
effort: high
language: de
last_updated: 2026-10-13
tags: [m&a, due-diligence, expert-session, agenda, ciso, dach]
---

# Prompt: M&A Expert Session — Agenda-Erstellung

## Zweck

Erstellt auf Basis der abgeschlossenen DD-Einzelberichte (IT, Security, Datenschutz,
Kundenverträge) drei Dokumente für die Expert Session mit dem Target:

1. **Verkäufer-Agenda** — Hochrangige Übersicht der Themenblöcke ohne interne Fragen.
   Dient als Einladung / Orientierung für die Gegenseite (CEO, IT-Leiter, Rechtsabteilung).
   Varianten: 60, 90 oder 120 Minuten.

2. **Gesamt-Agenda (intern)** — Vollständige Agenda mit detaillierten Fragen, Kontext aus
   dem VDR, Risikoklassifikation und internen Hinweisen. Nur für das Volaris-Team.

3. **Pre-Session Checklist (intern)** — Was vor der Session vorbereitet werden muss:
   Dokumente, VDR-Auszüge, SPA-Passagen, interne Abstimmungen.

---

## System Prompt

```
Du bist ein erfahrener IT- und Security-Berater mit Fokus auf M&A Due Diligence
in der DACH-Region. Du analysierst Findings aus IT, Security, Datenschutz und
Kundenverträgen und strukturierst daraus gezielte Expert-Session-Agenden für
Unternehmensübernahmen. Deine Agenden sind präzise, risikobasiert und auf
C-Level-Kommunikation ausgerichtet.
Antworte auf Schweizer Hochdeutsch (immer «ss», nie Eszett), ausser {{session_language}} gibt eine andere Sprache vor.
```

---

## Prompt Template

```
Bevor du mit der Erstellung der Dokumente beginnst, stelle folgende Frage und warte
auf die Antwort:

"Wie lange soll die Expert Session dauern?

A) 60 Minuten — Erstkontakt, überschaubare Findings, kleineres Target
B) 90 Minuten — Standard: mehrere Entitäten, kritische Security- oder DORA-Findings
C) 120 Minuten — Umfangreiche DD: viele CRITICAL/HIGH-Findings, komplexe Struktur,
                  mehrere Entitäten mit eigener IT/Datenschutz-Verantwortung

Bitte wähle A, B oder C."

Erstelle nach der Antwort drei Dokumente für eine Expert Session im Rahmen der
Due Diligence für folgenden Akquisitionskandidaten:

**Projektname (intern):** {{project_name}}
**Unternehmen / Target:** {{company_name}}
**Branche:** {{industry}}
**Entitäten:** {{entities}}
<!-- z.B. "Holding AG + Operating GmbH" oder "Einzelgesellschaft" -->
**Anzahl Mitarbeitende (gesamt):** {{headcount}}
**Hauptstandort:** {{main_location}}
**Geplantes Closing-Datum:** {{closing_date}}
**Geplantes Session-Datum:** {{session_date}}
**Session-Sprache:** {{session_language}}
<!-- z.B. Deutsch / Englisch / Deutsch mit englischen Folien -->
**Session-Dauer:** gemäss gewählter Option (60 / 90 / 120 Minuten)
**Gesprächspartner (Gegenseite):** {{counterparts}}
<!-- Nur Funktionen / Jobbezeichnungen, keine Namen — z.B. CEO, IT-Leiter, CFO -->
**Volaris-Team:** {{volaris_team}}
<!-- Nur Funktionen / Jobbezeichnungen, keine Namen — z.B. M&A Manager, CISO, externer Berater -->

---

## Verfügbare DD-Findings

Füge hier die relevanten Erkenntnisse aus den Einzelberichten ein.
Nutze die folgende Struktur — je Bereich die Top-3 bis Top-5 Findings mit Risikoklasse.
Lasse einen Abschnitt leer (oder schreibe "keine"), wenn keine Findings für diesen
Bereich vorliegen — die entsprechenden Agendablöcke werden dann weggelassen.

### IT-Findings (aus IT-DD-Bericht)
{{it_findings}}
<!-- Beispiel:
- [CRITICAL] Kein BCP/DRP vorhanden
- [HIGH] EOL-Hardware im produktiven Betrieb (Server seit mehreren Jahren ohne Herstellersupport)
- [HIGH] Kein automatisiertes Patch-Management
- [MEDIUM] VPN-Policy seit Jahren nicht überarbeitet
-->

### Security-Findings (aus Security-DD-Bericht)
{{security_findings}}
<!-- Beispiel:
- [CRITICAL] Kein Penetrationstest in den letzten 24 Monaten
- [HIGH] CISO-Funktion nicht formal definiert
- [HIGH] Kein Schwachstellenmanagement-Prozess
- [HIGH] MFA intern nicht durchgängig implementiert
-->

### Datenschutz-Findings (aus Datenschutz-DD-Bericht)
{{datenschutz_findings}}
<!-- Beispiel:
- [HIGH] DSB-Rolle und CISO in Personalunion (Interessenkonflikt)
- [HIGH] Kein Art.-30-Verarbeitungsverzeichnis nachgewiesen
- [MEDIUM] Fehlende AVVs mit IT-Lieferanten
- [MEDIUM] Website: Google Analytics ohne DSGVO-Konformität
-->

### Regulatorik-Findings
{{regulatorik_findings}}
<!-- Beispiel:
- [CRITICAL] DORA-Compliance als ICT-Drittanbieter nicht nachgewiesen
- [HIGH] ISO 27001-Auditbericht fehlt im VDR
- [MEDIUM] NIS2-Status ungeklärt
-->

### Kundenvertrags-Findings (aus Vertrags-DD-Bericht)
{{vertrag_findings}}
<!-- Beispiel:
- [HIGH] Datenschutz-Verletzungsklauseln mit ausserordentlichem Kündigungsrecht
- [HIGH] Veraltete Verträge ohne aktuelle DSGVO-Klauseln
- [MEDIUM] Fehlende Haftungslimits in mehreren Verträgen
-->

### Offene VDR-Dokumente (GAP-Liste)
{{open_vdr_docs}}
<!-- Beispiel:
- Penetrationstest-Bericht (letzter verfügbarer)
- BCP/IRP — aktueller Stand
- ISO 27001-Auditbericht mit Findings
- DORA-Gap-Assessment oder Compliance-Nachweis
- Art.-30-Verarbeitungsverzeichnis
- AVV-Status der IT-Lieferanten
-->

---

## Ausgabe-Anforderungen

**Wichtige Regeln für alle drei Dokumente:**

1. **Projektname statt Firmenname:** Verwende in allen Dokumenten ausschliesslich
   den Projektnamen ({{project_name}}). Der echte Firmenname ({{company_name}}) darf
   in keinem der drei Ausgabe-Dokumente erscheinen — auch nicht in Überschriften,
   Fusszeilen oder Betreffzeilen.

2. **Funktionen statt Namen:** Nenne Teilnehmer beider Seiten ausschliesslich mit
   ihrer Funktion / Jobbezeichnung (z.B. "IT-Leiter", "CISO", "M&A Manager").
   Personennamen dürfen in keinem der drei Dokumente erscheinen.

3. **Adaptive Blöcke:** Lasse Agendablöcke weg, für die keine Findings vorliegen
   (leerer oder "keine"-Eintrag im entsprechenden Abschnitt). Passe die Zeitfenster
   der verbleibenden Blöcke proportional an, sodass die gewählte Gesamtdauer
   eingehalten wird.

---

### Dokument 1: Verkäufer-Agenda (für die Gegenseite)

Erstelle eine saubere, professionelle Agenda **ohne interne Fragen und ohne
interne Risikoklassifikationen**. Die Gegenseite soll die Themenblöcke kennen,
aber keine strategischen Hinweise auf unsere Bewertung erhalten.

**Inhalt je Themenblock:**
- Zeitfenster (TBD +X, berechnet ab Session-Datum {{session_date}})
- Blockname und Dauer
- Kurze, neutrale Beschreibung der Schwerpunkte (2–4 Stichpunkte)
- Kein Hinweis auf kritische Findings oder Risikoklassen

**Entitäten berücksichtigen:** Falls {{entities}} mehrere Gesellschaften umfasst,
weise in Block 2 explizit darauf hin, welche Entität für welche Themen
verantwortlich ist (z.B. "Abgrenzung IT-Betrieb Holding vs. Operating GmbH").

**Erstelle die Verkäufer-Agenda für die gewählte Dauer (nur Blöcke mit vorhandenen Findings):**

**Option A — 60 Minuten:**
- Block 1: Einführung (5 min)
- Block 2: Unternehmensstruktur & Entitäten (10 min)
- Block 3: IT-Infrastruktur (10 min)
- Block 4: Security — Kritische Themen (15 min)
- Block 5: Datenschutz (10 min)
- Block 6: Kundenverträge (5 min)
- Block 7: Nächste Schritte (5 min)

**Option B — 90 Minuten:**
- Block 1: Einführung (5 min)
- Block 2: Unternehmensstruktur & Entitäten (10 min)
- Block 3: IT-Infrastruktur & Architektur (15 min)
- Block 4: Security — Pentest, BCM (20 min)
- Block 5: Regulatorik & Compliance (15 min)
- Block 6: Datenschutz (10 min)
- Block 7: Kundenverträge (10 min)
- Block 8: Nächste Schritte (5 min)

**Option C — 120 Minuten:**
- Block 1: Einführung & Kontext (10 min)
- Block 2: Unternehmensstruktur & Entitäten (15 min)
- Block 3: IT-Infrastruktur & Technische Architektur (20 min)
- Block 4: Security — Pentest, BCM, CISO-Funktion (25 min)
- Block 5: Regulatorik & Compliance — DORA, ISO 27001, NIS2 (20 min)
- Block 6: Datenschutz & Datenverantwortung (15 min)
- Block 7: Kundenverträge & Haftungsrisiken (10 min)
- Block 8: Nächste Schritte (5 min)

**Ton:** Professionell, partnerschaftlich, kein Druck.
Hinweis am Ende: "Keine Präsentation erforderlich — strukturiertes Gespräch."
Closing-Hinweis: "Im Hinblick auf den angestrebten Abschluss bis {{closing_date}}
bitten wir um zeitnahe Rückmeldung zur Terminbestätigung."

---

### Dokument 2: Gesamt-Agenda (intern, mit Fragen)

Erstelle die vollständige interne Agenda mit allen Detailfragen.
Orientiere dich an der gewählten Session-Dauer (60 / 90 / 120 Minuten).
Lasse Blöcke ohne Findings vollständig weg.

**Inhalt je Themenblock:**
- Zeitfenster, Blockname, Dauer, Risikoklasse
- Kontext-Box: Kurze Zusammenfassung des relevanten VDR-Befunds
- Pro Unterabschnitt:
  - Risikoklasse als Label (⚠ CRITICAL / ▲ HIGH / ◆ MEDIUM)
  - VDR-Fundstelle oder Finding als Kontext (kursiv/eingerückt)
  - Konkrete Fragen (3–5 Fragen pro Unterabschnitt)
  - Dringlichkeitshinweis wo relevant: [INTERN] Closing {{closing_date}} — Klärung vor Signing erforderlich

**Struktur der Blöcke (nur wenn Findings vorhanden):**
- Block 1: Einführung & Kontext (Vorstellung, Einstiegsfrage: grösste Herausforderungen)
- Block 2: Unternehmensstruktur & Entitäten-Abgrenzung
  - Geschäftsmodell & Leistungsabgrenzung je Entität ({{entities}})
  - Verantwortlichkeiten & Governance (IT, CISO, DSB) je Entität
  - VDR-Dokumentenabdeckung je Entität — welche Dokumente gelten für welche Gesellschaft?
  - Datenhaltung & Systemverantwortung (Shared Services vs. eigenständig)
- Block 3: IT-Infrastruktur & Technische Architektur [aus IT-Findings]
  - Hardware & EOL-Systeme
  - Identity & Access Management / MFA
  - Endpoint Security & Netzwerk
  - Hosting & Betriebsmodell
- Block 4: Security — Kritische Themen [aus Security-Findings CRITICAL/HIGH]
  - Penetrationstest & Schwachstellenmanagement
  - Business Continuity & Incident Response
  - CISO-Funktion & Kontrolluniversum
- Block 5: Regulatorik & Compliance [aus Regulatorik-Findings]
  - DORA-Compliance-Status
  - ISO 27001 & Zertifizierungsstatus
  - NIS2 & weitere Regulatorik
- Block 6: Datenschutz & Datenverantwortung [aus Datenschutz-Findings]
  - Datenschutzorganisation (DSB, AVV, Verarbeitungsverzeichnis)
  - Offene Datenschutzrisiken (Website, US-Tools, Gerichtsverfahren)
- Block 7: Kundenverträge & Haftungsrisiken [aus Vertrags-Findings]
  - Haftungslimits & Klauselrisiken
  - Offene Vertragslücken & DORA-Anpassungen
- Block 8: Nächste Schritte (5 min)
  - Ausstehende VDR-Dokumente (aus GAP-Liste) — Frist: {{closing_date}}
  - Action Items & Timelines

**Wichtige Anforderungen:**
- Fragen sollen spezifisch auf die vorliegenden Findings eingehen, nicht generisch
- Wo ein VDR-Dokument oder ein Assessment als Quelle bekannt ist, dieses benennen
- Fragen so formulieren, dass die Gegenseite keine strategische Gegenposition aufbauen kann
- Interne Hinweise (z.B. "SPA-Mechanismus prüfen", "Risikoakzeptanz verlangen") als
  separate Notiz [INTERN] markieren und nicht in die Verkäufer-Agenda übernehmen

---

### Dokument 3: Pre-Session Checklist (intern)

Erstelle eine kompakte Checkliste mit allem, was das Volaris-Team vor der Session
am {{session_date}} vorbereiten muss. Unterteile nach Verantwortlichkeit.

**Struktur:**

**Bis 2 Werktage vor der Session:**
- VDR-Auszüge zu den CRITICAL/HIGH-Findings ausdrucken oder lokal speichern
- Relevante SPA-Passagen markieren (Warranties & Representations zu IT/Security/Datenschutz)
- Interne Abstimmung Volaris-Team: Welche Fragen sind Pflicht, welche optional?
- Verkäufer-Agenda an Gegenseite versenden (Funktionen: {{counterparts}})

**Am Tag der Session:**
- Interne Agenda (Dokument 2) ausgedruckt / auf Gerät verfügbar
- GAP-Liste griffbereit (ausstehende VDR-Dokumente)
- Protokollant bestimmt (wer nimmt Notizen?)
- Aufnahme / Transkript-Tool bereit (falls erlaubt)

**Weitere spezifische To-Dos basierend auf den vorliegenden Findings:**
[Generiere hier 4–6 finding-spezifische Vorbereitungspunkte, z.B.:
 "DORA-Nachweis nachfordern falls bis Session-Datum nicht im VDR",
 "Letzten verfügbaren Pentest-Bericht aus VDR X.X.X.X herunterladen"]

---

Erstelle alle drei Dokumente vollständig und strukturiert.
Nutze Markdown-Formatierung.
```

---

## Platzhalter-Referenz

| Platzhalter | Beschreibung | Beispiel |
|---|---|---|
| `{{project_name}}` | Interner Projektname — wird in allen Ausgabe-Dokumenten verwendet | Projekt Alpha |
| `{{company_name}}` | Echter Firmenname — nur intern als Referenz, erscheint **nicht** in der Ausgabe | Musterfirma AG |
| `{{industry}}` | Branche des Targets | Fintech / SaaS / Industrie |
| `{{entities}}` | Gesellschaftsstruktur | Holding AG + Operating GmbH |
| `{{headcount}}` | Gesamtanzahl Mitarbeitende | 45 |
| `{{main_location}}` | Hauptstandort | Zürich / Wien / München |
| `{{closing_date}}` | Angestrebtes Closing-Datum | Q3 2026 / 30.09.2026 |
| `{{session_date}}` | Geplantes Datum der Expert Session | 15.07.2026 |
| `{{session_language}}` | Sprache der Session | Deutsch / Englisch |
| `{{counterparts}}` | Funktionen der Gegenseite — **keine Namen** | CEO, IT-Leiter, CFO |
| `{{volaris_team}}` | Funktionen Volaris-Seite — **keine Namen** | M&A Manager, CISO, externer Berater |
| `{{it_findings}}` | Top-Findings IT-DD (mit Risikoklasse) | Siehe Beispiele im Template |
| `{{security_findings}}` | Top-Findings Security-DD | Siehe Beispiele im Template |
| `{{datenschutz_findings}}` | Top-Findings Datenschutz-DD | Siehe Beispiele im Template |
| `{{regulatorik_findings}}` | Regulatorische Findings | Siehe Beispiele im Template |
| `{{vertrag_findings}}` | Top-Findings Kundenvertrags-DD | Siehe Beispiele im Template |
| `{{open_vdr_docs}}` | Noch fehlende Dokumente im VDR | Siehe Beispiele im Template |

---

## Workflow-Integration

Dieser Prompt ist **Schritt 4** im DD-Workflow und baut auf den Ergebnissen
der vier Einzelberichte auf:

```
SCHRITT 1 — Datenraum aufbereiten
└── 01_datenraum-matching.md

        ↓

SCHRITT 2 — Einzelberichte erstellen
├── 02a_it-due-diligence.md
├── 02b_security-due-diligence.md
├── 02c_datenschutz-due-diligence.md
└── 02d_kundenvertraege-compliance.md

        ↓

SCHRITT 3 — Master-Bericht konsolidieren
└── 03_master-dd-bericht.md

        ↓

SCHRITT 4 — Expert Session vorbereiten         ← DIESER PROMPT
└── 04_expert-session-agenda.md
    Input:  Top-Findings aus den 4 Einzelberichten + GAP-Liste
    Output: Verkäufer-Agenda (60/90/120 min)
            Gesamt-Agenda mit Fragen (intern)
            Pre-Session Checklist (intern)
```

---

## Tipps zur Verwendung

**Findings priorisieren:** Verwende nur die Top-3 bis Top-5 Findings je Bereich.
Zu viele Inputs führen zu einer unstrukturierten Agenda. Die Findings sind in den
Einzelberichten mit Risikoklassen versehen — CRITICAL und HIGH zuerst.

**Leere Bereiche weglassen:** Wenn z.B. keine Kundenvertrags-Findings vorliegen,
schreibe "keine" in das Feld. Claude lässt den Block dann weg und verteilt die
Zeit auf die verbleibenden Blöcke.

**Fragen schärfen:** Die KI generiert zunächst generische Fragen. Follow-up:
> "Formuliere die Fragen für Block 3 konkreter — benenne das spezifische
> Dokument (VDR X.X.X.X) und die genaue Feststellung aus dem Assessment."

**Session-Dauer wählen:** Claude fragt beim Start automatisch. Faustregel:
60 Min für Erstkontakt / wenige Findings, 90 Min für Standard-DD mit mehreren
Entitäten oder DORA-Findings, 120 Min bei umfangreicher DD mit vielen CRITICAL/HIGH-
Findings oder komplexer Gesellschaftsstruktur.

**Interne vs. Externe Version:** Niemals die Gesamt-Agenda oder Pre-Session Checklist
an die Gegenseite weitergeben. Die Verkäufer-Agenda zeigt nur Themen, keine
Risikobewertungen.

**Versand der Verkäufer-Agenda:** Spätestens 5 Werktage vor der Session versenden,
damit die Gegenseite die richtigen Personen mobilisieren kann.

---

## Ergänzende Follow-up Prompts

### Follow-up 1: Fragen schärfen
```
Überarbeite die Fragen in Block {{block_number}} ({{block_name}}).
Nutze folgende konkrete VDR-Fundstellen und Assessment-Ergebnisse:

{{specific_findings}}

Formuliere 4–5 Fragen, die direkt auf diese Findings eingehen und
die Gegenseite zu konkreten Massnahmen und Timelines verpflichten.
```

### Follow-up 2: Action Items ableiten
```
Basierend auf den Antworten aus der Expert Session ({{meeting_summary}}),
erstelle eine priorisierte Action-Item-Liste:
- Verantwortliche (Gegenseite vs. Volaris)
- Frist (Zeitnah / Mittelfristig / Bis Closing {{closing_date}})
- Eskalation bei Nichterfüllung (SPA-Mechanismus / Preisanpassung)
```

### Follow-up 3: Protokoll strukturieren
```
Ich habe ein rohes Meeting-Transkript / Protokoll aus der Expert Session:
{{meeting_notes}}

Erstelle ein strukturiertes Protokoll in der Struktur der Gesamt-Agenda.
Ordne jede Antwort dem entsprechenden Agendapunkt zu.
Markiere:
- ✓ Vollständig beantwortet
- ◑ Teilweise beantwortet / Nachlieferung erbeten (mit Frist)
- ✗ Nicht besprochen / Offen
- 🆕 Neu-Finding: Erkenntnisse aus der Session, die nicht in den DD-Berichten
     standen — diese separat in einer Tabelle zusammenfassen mit Risikoklasse
     und empfohlenem Follow-up (Vertiefte Analyse / SPA-Mechanismus / Akzeptiert)
```

---

## Versionshistorie

| Version | Änderung | Datum | Autor |
|---|---|---|---|
| 1.0 | Initiale Erstellung — basierend auf einem realen DD-Projekt | 2026-06-23 | CISO |
| 2.0 | session_date / closing_date / session_language ergänzt; adaptive Block-Logik; Entitäten in Ausgabe; Pre-Session Checklist als Dokument 3; Follow-up 3 mit Neu-Finding-Marker | 2026-06-23 | CISO |
| 2.1 | Interaktive Dauer-Auswahl am Anfang (60 / 90 / 120 Min); 120-Min-Blockstruktur ergänzt | 2026-06-23 | CISO |
| 2.2 | Vertraulichkeitsregeln: Projektname statt Firmenname, Funktionen statt Namen in allen Ausgabe-Dokumenten | 2026-06-23 | CISO |
| 2.3 | Blockreihenfolge angepasst: IT-Infrastruktur vor Security, Nächste Schritte fix 5 min | 2026-06-23 | CISO |
| 2.4 | Echte Firmennamen aus Platzhalter-Beispielen und Versionshistorie entfernt | 2026-09-03 | CISO |
| 2.5 | Finding-Beispiele und VDR-Referenz neutralisiert; 120-Min-Variante in Zweck und Workflow ergänzt; Spalte Autor ergänzt | 2026-10-13 | CISO |
| 2.6 | Zielmodell auf Claude Opus 5.5 umgestellt; Schweizer Schreibweise in der Sprachvorgabe; Effort-Empfehlung im Frontmatter | 2026-10-13 | CISO |
