# Zwischenstand: Methodischer Status & Übergang zur Literaturrecherche

## Aktueller Stand des Projekts

Im Rahmen des CSLI-Projekts wurden die experimentellen Grundlagen erfolgreich etabliert:

### 1. Testkatalog & Bedingungen (Step 02)
- Ein fixer, eingefrorener Katalog aus **12 realistischen Testszenarien** wurde definiert.
- Ziel ist die **vergleichbare Untersuchung von Kontextstabilität** unter kontrollierten Bedingungen.
- Tests und Bedingungen sind seit Step 02 **nicht mehr veränderbar**.

### 2. Execution Pipeline (Step 06 – Phase A)
- Eine vollständig generalisierte Test-Pipeline wurde implementiert:
  - client-agnostisch
  - reproduzierbare Runs (`run_index`)
  - deterministische Logging-Struktur
- Textbasierte Tests (z. B. T01) konnten erfolgreich über CompanyGPT (506.ai) ausgeführt werden.
- Die Pipeline ist **stabil, getestet und einsatzbereit**.

### 3. Plattformbefund: Multimodaler Input bei CompanyGPT
- CompanyGPT verarbeitet multimodale Inputs **nicht nativ** im LLM-Kontext.
- Medien (Image / Audio / Video) werden:
  - entweder in **Data Collections** hochgeladen und dort vorverarbeitet
  - oder (bei Audio/Video) **transkribiert**, bevor ein LLM-Call erfolgt
- Das LLM erhält **keine Originaldateien**, sondern ausschließlich **textuelle Repräsentationen**.

Dieser Befund ist **keine Limitation der Pipeline**, sondern eine **architektonische Designentscheidung der Plattform**.

---

## Identifiziertes Kernproblem

### Problemstellung

> **Die Transformation multimodaler Inputs in textuellen Kontext erfolgt außerhalb der direkten Kontrolle des Context-Engineering-Systems.**

Konkret bedeutet das:

- Bei plattformseitiger Transkription (z. B. durch 506.ai):
  - ist der erzeugte Text **nicht transparent spezifiziert**
  - kann nicht versioniert oder eingefroren werden
  - unterliegt potenzieller Veränderung ohne explizite Kontrolle
- Dadurch entsteht **Kontextinstabilität vor dem eigentlichen LLM-Prompt**, die nicht dem CSLI-Mechanismus zugerechnet werden kann.

Für ein Projekt mit dem Fokus **Context-Stable LLM Integration** ist dies methodisch kritisch.

---

## Abgrenzung der Forschungsfrage

Diese Arbeit untersucht **nicht**:

- native multimodale Modelle vs. textbasierte Modelle
- Bild-, Audio- oder Videoverständnis als solches

Stattdessen lautet die präzise Forschungsfrage:

> **Wo sollte die multimodale → textuelle Kontexttransformation stattfinden, um maximale Kontextstabilität, Reproduzierbarkeit und Kontrollierbarkeit zu gewährleisten?**

Diese Frage liegt im Bereich **Context Engineering**, nicht Modellarchitektur.

---

## Übergang zur Literaturrecherche

Die Literaturrecherche dient nicht der Suche nach „besseren Modellen“, sondern der **theoretischen Fundierung einer architektonischen Designentscheidung**.

### Ziel der Literaturrecherche

> *Welche Strategien zur Kontextkonstruktion gelten in der Forschung als geeignet, um Stabilität, Kontrolle und Reproduzierbarkeit in LLM-basierten Systemen zu gewährleisten?*

---

## Zentrale Suchachsen für die Literaturrecherche

### 1. Context Engineering & Prompt Construction
Fokus auf:
- explizite Kontextkonstruktion
- Prompt Engineering als Systemdesign
- kontrollierbare Kontextfenster

**Suchbegriffe:**
- `context engineering large language models`
- `explicit context representation LLM`
- `prompt construction reproducibility`

---

### 2. Pipeline-basierte Multimodalverarbeitung
Relevant sind Arbeiten zu:
- Multimodalität als **Vorverarbeitung**
- Audio/Video → Text → Reasoning

**Suchbegriffe:**
- `speech-to-text preprocessing language models`
- `multimodal pipeline architecture NLP`
- `transcription-based reasoning systems`

---

### 3. Reproduzierbarkeit & Stabilität in LLM-Systemen
Hier liegt die methodische Begründung.

Fokus auf:
- nicht-deterministische Effekte
- versteckte Varianzquellen außerhalb des Modells
- Evaluationsprobleme in LLM-Pipelines

**Suchbegriffe:**
- `reproducibility challenges large language models`
- `evaluation stability LLM pipelines`
- `hidden variables LLM systems`

---

### 4. Explainability & Auditability
Besonders relevant für Mobile Support / Field Applications.

Fokus auf:
- Nachvollziehbarkeit von Entscheidungen
- Auditierbarkeit von Vorverarbeitungsschritten

**Suchbegriffe:**
- `explainable AI preprocessing pipelines`
- `auditability AI decision support systems`

---

## Erwartetes Ergebnis der Literaturrecherche

Es wird erwartet, dass die Literatur zeigt:

- Explizite, textbasierte Kontextrepräsentationen:
  - erhöhen Reproduzierbarkeit
  - reduzieren implizite Varianz
  - verbessern Debuggability
- Plattforminterne Vorverarbeitung wird häufig als:
  - Black Box
  - Quelle versteckter Bias
  - methodische Schwäche diskutiert

Daraus folgt, dass **externe Kontextkonstruktion** keine ad-hoc-Entscheidung ist,
sondern **theoretisch fundiert** begründet werden kann.

---

## Übergang zur eigenen Designentscheidung

Auf Basis der Literaturrecherche kann die folgende Designentscheidung getroffen werden:

> *All multimodal-to-text transformations are deliberately externalized to maintain full control over context construction, enabling a stable and reproducible evaluation of context engineering mechanisms.*

Diese Entscheidung ist:
- methodisch sauber
- theoretisch begründet
- praktisch relevant

---

## Status

- Execution Pipeline: **fertiggestellt**
- Plattformverhalten: **analysiert**
- Methodisches Kernproblem: **identifiziert**
- Nächster Schritt: **gezielte Literaturrecherche zur Kontextkonstruktion**
