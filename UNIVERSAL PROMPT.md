# GP System Blueprint (Universal)
## Super-MD Strategy + Claude Sonnet Thinking Prompt (No Web, No External Sources)

This document defines a reusable, topic-agnostic system for GP (Geschichte & Politik):
- Convert class material into ONE “Super-MD” context file that is fast to search and hard to misread.
- Use a strict Claude prompt that forces: correct routing → minimal answers → high exam scoring.
- Works for any GP topic (Staatskunde CH, Demokratie, Föderalismus, Kalter Krieg, EU, UNO, Menschenrechte, Parteienlandschaft, etc.).

Important: Use this system for study/practice and any explicitly allowed open-book scenarios. Do not use it to break exam rules.

---

# 1) Pilot Test Results (System Performance Snapshot)

## Test Setup (Pilot)
- Input: photos of a printed mock test paper displayed on a laptop (multiple shots per page).
- Model/Tool: 7cal backend + Claude Sonnet Thinking using one Super-MD as context and a strict prompt.
- Constraint: No internet. Only the provided Super-MD context.
- Result: Each sub-answer generated in ~4–6 seconds.

## Observed Output Quality (Pilot)
- Accuracy: high for definitions, R/F with brief justification, Swiss civics concepts, and Majorz arithmetic.
- Style: short, school-level German, no fluff, no meta explanations.
- Consistency: stable across question types (definition → R/F → explanation → calculation).

## Why it worked
- One source of truth (single Super-MD) reduced “missing file” failures.
- Router tokens (QT / T / X) reduced drift and improved relevance.
- Hard output limits prevented overlong “AI essays”.

---

# 2) System Goals (High ROI)

Primary goal:
- Maximum exam points per minute of work.

Secondary goals:
- Minimal cognitive load.
- Stable performance under time pressure.
- Consistent “teacher-accepted” output format (short, structured, normal student writing).

Non-goals:
- No “fancy” writing.
- No academic essays.
- No external web knowledge unless explicitly allowed (default: NOT allowed).

---

# 3) System Architecture Overview

This system has 3 layers:

## Layer A — Super-MD (single context file)
One large markdown file containing:
- Quick Router (keywords → tokens)
- Question-Type templates (QT-*)
- Topic blocks (T-*)
- Extras: traps, R/F catalog, standard justifications, math schemas (X-*)

## Layer B — Claude Prompt (strict control)
A single prompt that forces:
- Read only the Super-MD link
- Route to the right token
- Output minimal answer, no fluff
- Handle missing info safely (1 clarification line OR 1 minimal assumption)

## Layer C — Calibration Loop
You test the system with 5–10 mock questions per topic and patch:
- Router keywords
- Templates
- Traps (common point-loss mistakes)

---

# 4) Super-MD Design Spec (Universal)

## 4.1 Token System (mandatory)
Use these token prefixes everywhere:

- QT-  = question-type templates (answer schemas)
- T-   = topic blocks (content)
- X-   = extras (traps, catalogs, standard answers, checklists)

Example tokens (universal):
- QT-DEF, QT-WHY, QT-RF, QT-COMP, QT-CLASS, QT-FILL
- QT-MATH (generic), plus topic-specific math templates if needed:
  - QT-MATH-PROP (seat allocation), QT-MATH-PERC (percent), QT-MATH-GRAPH (reading graphs)
- X-TRAPS, X-RF-CATALOG, X-CHECKLIST, X-TERMS

Topic tokens (examples, replace per topic):
- T-CH-STAAT, T-DIREKTE-DEMOKRATIE, T-EU, T-UNO, T-KALTER-KRIEG, T-MENSCHENRECHTE, T-PARTEIEN, T-WIRTSCHAFT, etc.

## 4.2 File Order (chronological for fast routing)
The Super-MD must start with what the model needs first:

1) QUICK ROUTER (keyword mapping)
2) MICRO INDEX (10-second map)
3) WORKFLOW (6-step algorithm)
4) ANSWER STYLE RULES (hard limits)
5) QT- templates (question-type schemas)
6) Teacher patterns / exam blueprint (if known)
7) Topic blocks (T-*) in likely exam frequency order
8) X- extras (traps, R/F catalog, standard justifications, checklists)
9) Glossary / terms

## 4.3 Router Rules (what makes it “fast + accurate”)
The Router must:
- map common question verbs to QT tokens
- map domain keywords to T tokens
- include “pitfall jump links” (X-TRAPS) for high-risk topics

Router example (universal pattern):
- “Definieren / Erklären / Was bedeutet” → QT-DEF
- “Begründen / Warum / Weshalb” → QT-WHY
- “Richtig/Falsch” → QT-RF + X-RF-CATALOG
- “Vergleichen / Unterschied” → QT-COMP
- “Ordnen Sie zu / Bestimmen Sie” → QT-CLASS
- “Tabelle / Übersicht ergänzen” → QT-FILL
- “Berechnen / Auswerten / Diagramm” → QT-MATH / QT-GRAPH (as needed)

## 4.4 Topic Block Micro-Structure (repeatable)
Every topic block must follow the same internal pattern:

- Definition (1–2 lines)
- Key points (3–8 bullets)
- Typical exam questions (2–6 bullets)
- Common traps (2–6 bullets)
- Mini examples (optional, 2–4 lines)

Consistency is the performance hack.

---

# 5) Claude Sonnet Thinking Prompt (Universal, 6/6)

## 5.1 Prompt Requirements
- No internet use.
- Only the Super-MD raw link is allowed context.
- Output must be direct answers only.
- No markdown, no LaTeX, no code blocks in the final answer (unless you explicitly allow it).

## 5.2 Copy-Paste Prompt Template (fill placeholders)

Paste this into Claude/7cal as the SYSTEM/USER prompt (depending on your tool).  
Replace:
- [RAW_SUPER_MD_LINK]
- optionally [LANGUAGE] (default German)
- optionally [SCHOOL_LEVEL] (default Sek II)

---

### PROMPT (Plain Text inside markdown for your project)

ROLE: GP (Geschichte & Politik) Lern- und Prüfungsassistent auf Niveau Sek II. Antworte kurz, punktesicher, in normalem Schuldeutsch. KEIN FLUFF. KEIN META-TALK.

SOURCE (ONLY): [RAW_SUPER_MD_LINK]
WICHTIG: Nutze ausschließlich den Inhalt aus SOURCE. Keine Websuche. Kein externes Wissen. Wenn etwas nicht im SOURCE steht, frage kurz nach oder formuliere eine minimale Annahme.

HARD OUTPUT RULES:
1) Gib nur die Antwort. Keine Einleitung, kein Schluss, keine Erklärungen über Vorgehen.
2) Sprache: Deutsch, Sek-II-Niveau, klar und knapp.
3) Format:
   - Bei Teilaufgaben: antworte exakt mit "a) ...", "b) ...", "c) ...".
   - Definition: 1–3 Sätze.
   - Begründung/Warum: genau 2 Gründe (2–4 kurze Sätze ODER 2–4 Stichpunkte).
   - Richtig/Falsch: "Aussage: richtig/falsch." + 1–2 Sätze Begründung.
   - Vergleich: A vs B als Stichpunkte + 1 Satz Fazit.
   - Tabelle/Lücken: nur die geforderten Begriffe/Zahlen, keine Sätze, wenn eindeutig.
   - Rechnen: 3–7 kurze Zeilen Rechenweg + 1 klare Ergebniszeile.
4) Kein Markdown (**fett**), kein LaTeX, keine Codeblöcke.

DYNAMIC WORKFLOW (DO THIS SILENTLY):
Step 1: Frage lesen und (a/b/c) erkennen.
Step 2: Fragetyp bestimmen: DEF / WHY / RF / COMP / CLASS / FILL / MATH / GRAPH.
Step 3: Im SOURCE zuerst QUICK ROUTER nutzen, dann die Tokens:
        - QT-* für Antwortschema
        - T-* für Inhalt
        - X-* für Fallen/Kataloge/Checklisten
Step 4: Antwort strikt nach QT-Schablone schreiben und nur Infos aus dem passenden T-Block verwenden.
Step 5: Final Check (still):
        - Alle Teilfragen beantwortet?
        - Fachbegriffe korrekt?
        - Keine unnötigen Extras?

MISSING INFO HANDLING:
- Wenn entscheidende Angaben fehlen oder die Aufgabe mehrdeutig ist:
  - Stelle genau 1 kurze Rückfrage (eine Zeile).
- Wenn Rückfrage nicht möglich:
  - Nenne 1 minimale Annahme ("Annahme: ...") und löse danach kurz weiter.
- Niemals Zahlen/Fakten erfinden, die nicht im SOURCE stehen.

GOAL:
Maximale Punkte bei minimalem Text. Stabil, relevant, sauber.

---

# 6) Calibration Loop (How to keep it 6/6)

After building a new topic Super-MD:
1) Generate 5–10 mock questions that match the teacher’s style.
2) Run them through Claude with the prompt above.
3) Score each answer on:
   - correctness (0/1)
   - format (0/1)
   - relevance (0/1)
   - brevity (0/1)
4) Patch the Super-MD:
   - Add router keywords that were missed.
   - Add/adjust a QT template if the model wrote too long.
   - Add traps if it confused two concepts.
5) Repeat once. Stop. Over-optimizing wastes time.

---

# 7) Universal Best Practices (High ROI)

- Keep the Super-MD as a “map + templates + minimal facts”, not a textbook.
- Add “X-TRAPS” early and keep it short (point-loss prevention is peak ROI).
- For any topic with calculations/graphs:
  - create a dedicated QT-MATH-* or QT-GRAPH schema
  - include 2–3 miniature worked examples (tiny, not essays)
- Always prioritize:
  - correctness > style
  - relevance > completeness
  - short > fancy

---

# 8) Minimal Universal Super-MD Skeleton (for new topics)

Use this when you create a new Super-MD from scratch:

# QUICK ROUTER
# MICRO INDEX
# WORKFLOW
# ANSWER STYLE RULES
# QT-TEMPLATES
## QT-DEF
## QT-WHY
## QT-RF
## QT-COMP
## QT-CLASS
## QT-FILL
## QT-MATH (if needed)
## QT-GRAPH (if needed)
# TEACHER PATTERNS / EXAM BLUEPRINT (optional)
# TOPIC BLOCKS (T-*)
## T-[TOPIC_1]
## T-[TOPIC_2]
...
# X-EXTRAS
## X-TRAPS
## X-RF-CATALOG (if relevant)
## X-CHECKLIST
# GLOSSARY

---

End of document.
