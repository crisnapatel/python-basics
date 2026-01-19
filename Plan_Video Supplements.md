## Plan: Manim Video Supplements for Python Basics Pages

**Design Principle**: Each page gets a 2–5 minute video that animates the key concept using the parachutist as the running example. Videos are "watch instead of read" supplements—not replacements.

---

## Why Videos?

| Benefit | Detail |
|---------|--------|
| **Lower barrier** | Students who skim text will watch a 3-min video |
| **Manim = perfect fit** | Equations morphing, code executing line-by-line, lists growing — all native Manim |
| **Reusable** | Videos can go on YouTube, be shared in WhatsApp groups, embedded in slides |
| **No JS dependencies** | Works everywhere, including mobile |
| **Parachutist story** | Animate the falling parachutist *visually* — velocity arrow growing, trajectory plotting |

---

## Video Structure Template

Each video follows a consistent format:

```
[0:00–0:15]  Hook — "What if you need to store 1000 velocities?"
[0:15–0:30]  Visual problem setup (parachutist context)
[0:30–2:30]  Core concept animation (Manim scenes)
[2:30–3:00]  Recap + "Try it yourself" prompt
[3:00–3:10]  End card — link to page, next topic
```

---

## Page-by-Page Video Plan

| Page | Video Title | Key Manim Scenes |
|------|-------------|------------------|
| `variables.md` | *"Variables: Naming Your Data"* | Memory boxes appearing, values updating as code runs, `v = v + dv` animation |
| `datatypes.md` | *"Types: Why 3 ≠ 3.0 in Python"* | Type labels morphing, `int` → `float` conversion, error when mixing types |
| `print.md` | *"See Your Results: print() and f-strings"* | Terminal output appearing character-by-character, format specifier breakdown |
| `data_structures.md` | *"Lists: Storing the Velocity History"* | List growing step-by-step during Euler loop, index highlighting, slice visualization |
| `control_flow/loops.md` | *"The Engine of Numerical Methods"* | Code block with moving highlight, variable table updating each iteration, velocity plot growing |
| `control_flow/if_else.md` | *"Decisions: When to Deploy the Parachute"* | Flowchart branching, condition evaluation animation |
| `functions.md` | *"Packaging Your Code"* | Inline code → function box, parameter arrows, return value flow |
| `errors.md` | *"Reading Tracebacks Like a Detective"* | Error message appearing, line highlight, fix animation |

---

## Technical Pipeline

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Write      │    │  Render     │    │  Generate   │    │  Combine    │
│  Manim      │ →  │  Manim      │ →  │  Audio      │ →  │  Video +    │
│  Scenes     │    │  (1080p)    │    │  (Coqui)    │    │  Audio      │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
                                                               ↓
                                                        ┌─────────────┐
                                                        │  Upload to  │
                                                        │  YouTube    │
                                                        └─────────────┘
```

**Environment**: Ubuntu (Manim + Coqui) → YouTube (NanoScaleModelling channel, dedicated playlist)

**Tools:**

- **Manim Community Edition** — animation (Ubuntu)
- **Coqui TTS (XTTS v2)** — AI voice cloning from script (Ubuntu, GPU recommended)
- **manim-voiceover** — syncs TTS audio directly to Manim scenes
- **FFmpeg** — combine video + audio, compress
- **YouTube** — NanoScaleModelling channel, "Python Basics" playlist

**Voice Cloning Setup (one-time):**

1. Record 30-second voice sample (clear speech, no background noise)
2. Install Coqui: `pip install TTS`
3. Generate audio: `tts --model_name tts_models/multilingual/multi-dataset/xtts_v2 --text "Script here" --speaker_wav voice_sample.wav --out_path voiceover.wav`

**Alternative**: iMovie on Mac for manual voiceover (slower but more control)

---

## Embedding in Jupyter Book

At the bottom of each page, use a collapsible admonition:

```markdown
```{admonition} 🎬 Prefer to Watch?
:class: dropdown tip

<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" 
  frameborder="0" allowfullscreen></iframe>

*This video covers the same content as the page above.*
```
```

---

## Phase 1: First 3 Videos

| Priority | Page | Why |
|----------|------|-----|
| 1 | `control_flow/loops.md` | Loops + Euler = the heart of the course; most visual payoff |
| 2 | `data_structures.md` | List indexing/slicing is confusing in text, obvious in animation |
| 3 | `variables.md` | Foundation; sets the visual language for later videos |

---

## Consistency Guidelines

- **Same parachutist parameters** in every video (`m=68.1`, `c=12.5`, `g=9.8`)
- **Same color scheme**: code = monospace white-on-dark, math = blue, parachutist = orange
- **Same voice** (you, or consistent TTS like ElevenLabs)
- **Same intro/outro** (3-second title card, end card with next topic)

---

## Effort Estimate

| Task | Time (per video) |
|------|------------------|
| Script + storyboard | 30 min |
| Manim scenes | 2–4 hrs (first few take longer) |
| Voiceover recording | 30 min |
| Edit + combine | 30 min |
| **Total** | ~4–6 hrs per video |

After 2–3 videos, you'll have reusable Manim components (parachutist, code blocks, variable tables) that speed up later videos.

---

## Reusable Manim Components to Build

| Component | Used In |
|-----------|---------|
| `ParachutistScene` — falling figure with velocity arrow | All videos |
| `CodeBlock` — syntax-highlighted code with line pointer | loops, functions, errors |
| `VariableTable` — updating `t`, `v`, `slope` display | loops, variables |
| `MemoryBox` — labeled box for variable visualization | variables, datatypes |
| `ListVisual` — array with index labels, slice highlighting | data_structures |
| `PlotBuilder` — velocity vs. time plot that grows | loops, numpy |

---

## Video Script Template

```markdown
## [Video Title] (`page.md`)

**Duration**: X min
**Learning Objective**: Student will understand _____.

### Script

| Time | Visual (Manim) | Voiceover |
|------|----------------|-----------|
| 0:00 | [Hook visual] | "What if..." |
| 0:15 | [Parachutist setup] | "Remember our falling parachutist..." |
| ... | ... | ... |

### Manim Scenes

1. `HookScene` — ...
2. `MainConceptScene` — ...
3. `RecapScene` — ...
```

---

## Next Actions

1. [ ] Record 30-second voice sample for Coqui cloning
2. [ ] Install Manim CE and Coqui TTS on Ubuntu
3. [ ] Test voice cloning with a sample sentence
4. [ ] Build reusable `ParachutistScene` component
5. [ ] Write script + storyboard for `loops.md` video
6. [ ] Render first video draft with AI voiceover
7. [ ] Create "Python Basics" playlist on NanoScaleModelling channel
8. [ ] Upload and embed in page
9. [ ] Gather feedback, iterate
