# CalmTyping – Agent Guidelines

This document defines how coding assistants (including Codex CLI) should work on the CalmTyping project.  
The goal is to keep the project simple, consistent, and easy to evolve.

CalmTyping is a minimalist, ad-free touch typing trainer built with:

- a single HTML file (index.html)
- pure JavaScript
- pure CSS (embedded or inline)
- no frameworks
- no build step
- no backend

Agents must follow the principles below when modifying or extending the code.

---

## 1. Project Structure

The entire application lives in:

    index.html

This file contains:

    - HTML layout
    - CSS styles
    - JavaScript logic
    - lesson data (the lessons[] array)
    - UI text definitions
    - finger layout and mapping data
    - SVG-based hand diagrams

Do not introduce additional files unless explicitly approved by the user.

---

## 2. Code Philosophy

CalmTyping is intentionally minimal:

    - No TypeScript
    - No React / Vue / Svelte
    - No npm packages
    - No Webpack / Vite / Parcel
    - No external libraries except optionally small SVG icons
    - No backend or user accounts
    - No analytics

The app must continue to run when the user opens index.html directly in a browser.

Agents must not introduce unnecessary complexity.

---

## 3. Lessons (Core Data Structure)

Lessons are plain JavaScript objects stored inside a lessons[] array.

A lesson looks like this:

    {
      id: "fi-l1-intro",
      group: "Lesson 1 – Home Row (FI)",
      category: "Introduction",   // one of: Introduction, Technique, Word practice, Long practice
      language: "fi",              // fi or en
      label: "Home row – basic patterns",
      tag: "L1",                   // short marker shown in the UI
      fingerHints: true,           // enable finger guide for this lesson
      segments: [
        "asdf asdf asdf asdf",
        "jklö jklö jklö jklö"
      ]
    }

Rules for agents:

1. Never break or reuse lesson IDs.  
2. When adding new lessons:
       - 6 to 10 segments is ideal.
       - each segment should be short (1–3 lines).
3. Lessons must use only characters introduced so far in the progression.
4. fingerHints should be set consistently:
       - true for most lessons
       - false only if explicitly requested

---

## 4. Lesson Categories

CalmTyping uses four functional categories:

    Introduction   – new key introductions and simple patterns
    Technique      – drills focusing on transitions, rhythm and accuracy
    Word practice  – “almost words” or short patterns
    Long practice  – calm, narrative-style text split into segments (these may use the full alphabet/symbols; they are intended for advanced practice but remain freely accessible)

Future category:

    Code drills    – programming-related exercises (planned)

Agents should not create new categories without the user’s approval.

---

## 5. Allowed Characters and Progression

Typing lessons must follow a strict rule:

    Do not use a character before it has been introduced.

Currently:

    Lesson 1 (FI):
      allowed: a s d f j k l ö
      plus space

Later lessons will introduce:

    - top/bottom row letters
    - ä and c (later in the progression)
    - punctuation and symbols
    - coding syntax characters for code drills

If an agent adds characters prematurely, this must be corrected.

### Capital Letters, Acronyms, and Mixed Case (after L10)

After the SHIFT / capital letters lesson (L10), uppercase use becomes normal practice.

- Allowed from L10 onward: capitalized words (e.g. `Pause`), acronyms (e.g. `API`, `HTML`), and mixed-case identifiers like camelCase (`runTask`, `saveState`) or PascalCase (`WorkManager`, `MainTask`), plus short identifiers (`wrkMgr`, `cfgVal`).
- All letters must already be introduced in earlier lessons.
- Capitalization must be meaningful (names, acronyms, identifiers), not random noise.
- Avoid all-caps blocks; capitals should appear naturally and gradually.
- Applies to word practice, long practice, and syntax/code-oriented lessons.

---

## 6. Typing Engine Logic

The typing system is segment-based.

Important behaviours:

### Segment handling

1. If the user types the segment perfectly:
       → auto-advance to the next segment.

2. If the user reaches the end of the segment (typed.length >= segment.length):
       → pressing Space or Enter advances even with mistakes.

3. On the final segment:
       → segment completion sets exerciseCompleted = true  
       → pressing Space or Enter moves to the next lesson.

Agents must not change these behaviours unless explicitly instructed.

---

## 7. Finger Guide System

Finger hints are determined by:

    - fingerLayouts.fi
    - fingerLayouts.en
    - keyMap objects inside each layout

The keyMap maps characters to:

    leftPinky
    leftRing
    leftMiddle
    leftIndex
    rightIndex
    rightMiddle
    rightRing
    rightPinky
    leftThumb
    rightThumb

And special rules:

- space → both thumbs
- uppercase → main finger + opposite-hand Shift pinky
- line break → right pinky (Enter key)

Agents updating key maps must ensure:

    - The mapping matches the physical layout (Finnish Mac is the reference)
    - No new characters appear in exercises unless mapped

---

## 8. UI Text and Language

CalmTyping supports two UI languages:

    Finnish (fi)
    English (en)

Lessons themselves can be either language (language field on lesson objects).

When modifying UI texts:

- maintain the calm, focused tone
- avoid overly long sentences
- ensure translations preserve meaning

---

## 9. Visual Design Principles

CalmTyping follows these design rules:

    - dark background (#111)
    - light text (#eaeaea)
    - soft borders and small shadows
    - rounded corners
    - minimal color palette
    - no flashing animations
    - no complex gradients
    - simple, clean layout

Agents may adjust layout or styling **only if**:

- changes improve clarity or usability
- maintain consistent aesthetic
- code remains entirely in index.html

---

## 10. Safe Refactoring Guidelines

Agents may:

- extract helpers into small JS functions
- improve code readability
- split CSS into sections inside <style> tags
- reorganise the lessons array
- add comments for clarity

Agents must not:

- split code into modules unless requested
- add build systems or package managers
- introduce state management libraries
- use Canvas/WebGL unless explicitly asked
- add complex animations that distract from typing

---

## 11. Code Drills (Future Work)

Planned features:

    - parentheses, brackets and braces
    - quotes (“ ' " ”)
    - semicolons, colons, commas and operators
    - indentation and tabs
    - small code snippets in Python, JS/TS, Go, C, Java, Kotlin

When implemented, code drills should:

- be their own top-level lesson group
- not break the basic typing flow
- introduce characters in logical order
- avoid advanced syntax until basic symbols are introduced

---

## 12. When Generating New Lessons

Agents must:

1. Ensure 6–10 segments per exercise.
2. Vary patterns to avoid repetitive “sala kala” style loops.
3. Keep text calm, focused and free of slang.
4. Maintain difficulty balance (not too easy, not too chaotic).
5. When adding Finnish content:
       - keep segments pronounceable if possible
6. When adding English content:
       - keep vocabulary simple and neutral
7. For long practice texts:
       - aim for calm, meditative pacing
       - right-size segments to match the user’s breathing and typing rhythm

---

## 13. Adding New Features

If asked to add a feature, agents must:

1. Propose a minimal version first.
2. Explain any UI or layout implications.
3. Avoid breaking existing behaviour.
4. Keep code inside index.html unless the user explicitly wants files split.

If in doubt, **ask the user for confirmation** before implementing a large change.

---

## 14. Summary

CalmTyping should remain:

    - lightweight
    - calm
    - minimalistic
    - educational
    - layout-accurate
    - data-driven

Agents should preserve the personality of the project:

    "A calm space to practice typing, without distractions or noise."

All changes must support this vision.

## Generating Lesson Text for CalmTyping (Universal Instructions for All Lessons)

This project uses lesson-by-lesson character progression. When generating any text segments (Finnish or pseudo-English) for any lesson, follow the rules below. These rules apply to all word practice, technique drills, and long text segments.

---

### 1. Use only the characters that have been introduced up to that lesson

Every lesson in CalmTyping unlocks a specific set of characters. When generating content:

    - Only use characters that the user has already learned.
    - Never include letters or symbols that come from future lessons.
    - The allowed character set will either be provided in the request or can be inferred from previous lessons.

Examples:
    If lesson includes only: a s d f j k l ö r u
        → Do NOT use e, t, h, i, m, n, v, o, c, p, y, etc.
    If the lesson has later unlocked ä or å:
        → You may use ä and/or å occasionally in the generated text.

These constraints are essential and must be respected strictly.

---

### 2. Style depends on the lesson language (“fi” or “en”)

#### If the lesson is FI (Finnish practice):
Generate playful, readable, almost-Finnish words or short sentences.  
They may be silly, surprising or lightly slangy, but must follow the allowed characters.

Good examples:
    saara rullaa kuraa auralla
    kalja kallaa ja darra rullaa auraa
    ura kulkee kuralla ja laura surraa

---

#### If the lesson is EN (English practice):
Generate pseudo-English: words and mini-sentences that look like English,  
but are constructed using only the allowed characters.

You may:
    - Replace “o” with “ö” if ö is allowed.
    - Replace “a” with “ä” if ä is allowed.
    - Rarely use å if å is allowed.
    - Invent names (aura, laura, lura, löra, röra, etc.).
    - Create English-like rhythm even if the words are not real.

Examples:
    löad röad lura aura rull lura
    a lura rull aura löad along a röad
    laura rälls a löad aura röad

---

### 3. Avoid repetitive syllable-noise (no “ruru ruru rurr”)

CalmTyping is meant to feel engaging. Do NOT generate content such as:

    ruru ruru ruru
    lala ruru lara
    urur urur urr

Instead, generate:
    - Phrases
    - Mini sentences
    - Funny pseudo-Finnish or pseudo-English expressions
    - Rhythmic but meaningful-looking text

Users should enjoy typing the segments; they must not look like random syllable spam.

---

### 4. Emphasize the newly learned letters of the lesson

Each new lesson introduces one or more characters.  
Segments should use these frequently but naturally.

Example (Lesson 2 introduces r and u):
    Good:  rull aura kura rura löad rull
    Good:  a lura rull aura löad along a röad
    Bad:   ruru ruru rurr rurr (too repetitive, not meaningful)

---

### 5. Segment format

Each segment must:
    - Be a single line of text.
    - Be ready to paste into a JavaScript segments array.
    - Contain 1–3 small phrases or one short sentence.
    - Respect all character constraints.

Example of valid output:

    "löad röad lura aura rull lura",
    "rura löra rull aura löad rura",
    "kalja kallaa ja darra rullaa auraa",
    "a lura rull aura löad along a röad",

When the user requests N segments, return exactly N segments in this format.

---

### 6. Maintain the tone of CalmTyping

All generated text should feel:

    - Calm
    - Playful
    - Lightly humorous
    - Non-stressful
    - Not offensive, political or heavy
    - Suitable for long typing flow

The purpose is to keep the user in a relaxed, enjoyable typing rhythm.

---

### 7. Summary

When generating CalmTyping lesson content:

    - Strictly follow the allowed character set of the current lesson.
    - Choose style based on language: playful Finnish or pseudo-English.
    - Use ö, ä, å only if they are allowed at that stage.
    - Prefer meaningful, fun phrases over random syllables.
    - Emphasize the lesson’s new characters.
    - Output clean JavaScript-string segments, one per line.

These instructions apply to all lessons (L1–L10), in both languages, for both short and long practice segments.
