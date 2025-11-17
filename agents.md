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
