# CalmTyping

![CalmTyping](calmtyping-logo.svg)

A minimalist, ad-free touch typing trainer for Finnish and English.

- Finger hints  
- Mac keyboard layout support  
- Modular lessons  
- Long practice texts  
- Planned code drills for developers  

No login, no tracking, no backend. Just open the page and start typing.

---

## Features

### Distraction-free UI
Dark, minimalist interface designed for focused practice sessions.

### Free lesson order
You can open any exercise at any time. There is no forced progression or locking.

### Segment-based practice
Every exercise is split into short segments. You type one segment at a time.

- If you type a segment perfectly, CalmTyping auto-advances to the next segment.  
- If you reach the end of the segment, you can press **Space** or **Enter** to move forward even with mistakes.

### Finger hints
A compact line-art hand diagram shows which finger to use for the next character.

- letters → recommended finger  
- space → both thumbs  
- uppercase → main finger + opposite-hand Shift pinky  
- line break → right pinky (Enter)

### Layout awareness
Optimised for **Finnish Mac keyboard layout**.  
English practice uses the same mapping for now, but more layouts will be added later.

### Long practice texts
Calm, essay-like texts in Finnish and English.  
Designed for rhythm and attention, not raw speed.  
These use the full alphabet/symbol set and are meant for practice after you already know all keys (they remain freely accessible).

---

## Lesson Structure

Lessons are stored as data in `index.html` inside a `lessons` array.

Each lesson follows this format (shown here as indented code to avoid formatting issues):

    {
      id: "fi-l1-intro",
      group: "Lesson 1 – Home Row (FI)",
      category: "Introduction",   // "Introduction" | "Technique" | "Word practice" | "Long practice"
      language: "fi",              // "fi" or "en"
      label: "Home row – basic patterns",
      tag: "L1",                   // short label for UI
      fingerHints: true,           // show finger guidance
      segments: [
        "asdf asdf asdf asdf",
        "jklö jklö jklö jklö"
      ]
    }

---

## Categories

- **Introduction** – first exposure to new keys, simple patterns  
- **Technique** – drills focusing on transitions and rhythm  
- **Word practice** – simple “almost words” using available letters  
- **Long practice** – calm, paragraph-style training segments  

A separate **Code drills** category will be added later for programming-focused exercises.

---

## Letter Progression

Lessons must only use characters that have been introduced.

Current lessons (see `index.html` → `lessons` for the latest):

- L1: a s d f j k l ö (plus space)
- L2: add r u
- L3: add t y
- L4: add h n
- L5: add i o
- L6: add p m
- L7: add ä å
- L8: add e v
- L9: add g b
- L10: introduce SHIFT usage (capitals)
- L11: add punctuation , . ; :
- L12: add c w
- L13: add x z q

New lessons keep adding a few characters at a time while mixing earlier ones to reinforce previous keys.

---

## How Typing Works

There is no text input field.  
Once the page has focus, typing begins immediately.

### Segment behaviour

- Each exercise is split into short segments.
- You type one segment at a time.
- Characters are rendered as:
  - green = correct
  - red with underline = incorrect
  - highlighted = current cursor position

### Keys and controls

- **Backspace**  
  Removes the last typed character in the current segment.

- **Escape**  
  Resets the exercise back to the first segment and clears statistics.

- **Space or Enter**  
  - moves to the next segment if the current one is complete  
  - moves to the next exercise if the final segment is done  

### Statistics

The stats box shows:

    characters typed
    errors
    accuracy (percentage)
    elapsed time (seconds)
    estimated speed (WPM)

These reset when you enter a new exercise.


---

## Running CalmTyping Locally

Everything is contained in a single file: index.html  
No build step or dependencies are required.

To run locally:

1. Clone the repository.

       git clone https://github.com/YOUR_USERNAME/CalmTyping.git
       cd CalmTyping

2. Open index.html directly in your browser  
   —or—

3. Start a small local server and visit http://localhost:8000/

       python3 -m http.server 8000

---

## GitHub Pages

CalmTyping can be published directly through GitHub Pages.

Steps:

1. Push the repository to GitHub.
2. Open the repository settings.
3. Go to "Pages".
4. Select:
       Branch: main
       Folder: / (root)
5. Save.

Your site will appear at:

    https://YOUR_USERNAME.github.io/CalmTyping/

---

## Roadmap (High-Level)

- More Finnish lessons with controlled letter introduction
- English practice drills
- Additional long texts in both languages
- Code drills:
  - brackets, braces, quotes, semicolon patterns
  - indentation practice
  - language-specific snippets (Python, JavaScript/TypeScript, Go, C, Kotlin, Java)
- Layout variants:
  - English (US) Mac layout
  - possibly Nordic PC layout
- Optional progress tracking using localStorage

---

## Code & syntax practice (planned)

CalmTyping will also include an optional *syntax track* for people who write code and want to practice typical programming symbols calmly, with proper finger hints and Mac Finnish layout support.

The idea is:

- Base lessons (L1–L13) teach all letters, numbers (later), and basic punctuation.
- Syntax lessons (S1–S5) focus on programming-related symbols and operator patterns.
- Code drills reuse those symbols in realistic snippets from Python, JavaScript/TypeScript, Go, C/Java/Kotlin and similar languages.

### Goals for the syntax track

- Make it natural to type common code symbols without thinking.
- Respect Mac Finnish keyboard specifics (especially `{ } [ ]` on Alt-combinations).
- Keep the CalmTyping style: slow, low-pressure, segment-based, no gamified stress.
- Allow language-specific code drills later without needing to reteach the symbols.

### Planned syntax lessons (S1–S5)

These lessons are *symbol-first* and language-agnostic. They can be done after the current letter/punctuation lessons. (Numbers arrive later in the main track.)

#### S1 – Basic punctuation for code

Focus: characters that already appear in prose, but are fundamental in code:

- `,` comma  
- `.` dot  
- `;` semicolon  
- `:` colon  
- `_` underscore  
- `-` minus  
- `+` plus  
- `*` asterisk  
- `/` slash  

Content:

- Simple symbol patterns (`;; :: __ ++ --`)  
- Short pseudo-identifiers and function names (`do_stuff()`, `sum_total`, etc.)  
- Calm Finnish/English phrases that gradually include these symbols.

#### S2 – Parentheses & brackets

Focus on all three types of brackets and their Mac Finnish key combinations:

- `(` `)` – normal parentheses (Shift + 8 / 9)
- `[` `]` – square brackets (Alt + 8 / 9)
- `{` `}` – curly braces (Shift + Alt + 8 / 9)

Content:

- Drills that isolate each pair: `() [] {}`  
- Nested patterns: `(a[b{c}])`, `func(x[0])`, etc.  
- Small pseudo-code phrases that emphasise structure rather than realism.

#### S3 – Comparison & boolean operators

Focus:

- `=` `==` `!=`
- `<` `>` `<=` `>=`
- `!` (not)
- `&&` (and)
- `||` (or)

Content:

- Symbol sequences like `== != <= >=` typed in rhythm.
- Simple condition-like snippets: `if (x == 0)`, `while (a && !b)`  
- Calm pseudo-conditions in both Finnish and English text segments.

#### S4 – Strings & comments

Focus:

- `'` single quote
- `"` double quote
- `` ` `` backtick (JS/TS templates)
- `#` (Python-style comment)
- `//` and `/* */` (C/Java/JS-style comments)

Content:

- Quoted words and short strings: `"hello"`, `'nimi'`, `` `template` ``  
- Comment lines: `# todo: calm down`, `// note: slow typing`  
- Tiny “code diary” snippets that feel like real comments.

#### S5 – Arrows, bitwise and misc. symbols

Focus:

- `->` arrow (Go, Rust, C-style pseudo)
- `=>` fat arrow (JS/TS lambdas)
- `&` and `|` (bitwise / logical)
- `^` (xor)
- `@` (annotations, decorators)
- `$` (shell, JS templates)
- `~` (tilde, less common but present)

Content:

- Arrow-heavy patterns: `x -> y`, `value => result`.
- Short pseudo-function headers with `@decorator`-style lines.
- Simple imagined shell / config fragments with `$` and `~`.

### Code drills (planned after syntax lessons)

Once the syntax lessons exist, the plan is to add *code-focused tracks* that reuse them:

- **Python track**  
  - `def`/`class` blocks, `if/elif/else`, loops (`for`, `while`)  
  - f-strings and simple list comprehensions  
  - Calm examples with clear spacing and predictable patterns.

- **JavaScript / TypeScript track**  
  - Arrow functions (`const fn = () => {}`)  
  - Objects and arrays: `{ key: value }`, `[item1, item2]`  
  - Basic async/await and simple “config object” patterns.

- **Go / C / Java / Kotlin track**  
  - `func`/`void`/`int`-style declarations  
  - Curly-brace blocks and `if`/`for` structures  
  - Very small, focused snippets that prioritise typing feel over language correctness.

Each track will follow the same CalmTyping principles:

- segmented practice (8–12 segments per drill)
- no login, no timers, no distractions
- clear visual finger hints for each new symbol
- Finnish and English text variants where it makes sense.


---


## License

MIT License. See `LICENSE` for details.
