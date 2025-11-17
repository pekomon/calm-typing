# CalmTyping

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

## Letter Progression (Finnish)

The app should not use a character before it is introduced in the lesson progression.

### Lesson 1 – Home Row (FI)
Allowed characters:

    a s d f j k l ö
    (plus space)

Later lessons (not yet fully implemented) will introduce:

- more letters from other rows
- eventually the letters ä and c
- punctuation and special characters
- symbols needed for coding drills such as parentheses, braces, brackets, semicolons and operators

When adding new exercises, keep the characters consistent with what has been introduced so far.

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

## License

MIT License. See `LICENSE` for details.
