---
name: create-concept-notes
description: >-
  Recap a study or Socratic session into a clear concept note (or two) under
  `knowledge/` in Sivaram's Obsidian vault, written from a cc-export transcript.
  This is the breadth companion to `/create-mental-model`: where that captures
  one deep aha, this captures the spread of what a session worked through and
  explains it plainly. Use whenever the user says `/create-concept-notes`, "recap
  this session", "write a concept note from this transcript", "capture what we
  covered", or finishes a `/study` session and wants the discussion written up.
  Reach for this on session transcripts even when the user does not say the words
  "concept note". Do NOT use for a single reducible aha (that is
  `/create-mental-model`), for meeting or conference logs (`log/`), blog drafts
  (`writing/`), or reading clippings (`clippings/`).
---

# Create Concept Notes

Turn a study-session transcript into a clear write-up of the concept(s) it covered. A Socratic session usually orbits one concept, gets an overview, and brushes a few adjacent ideas without going deep on all of them. This note captures that: the recap and the explanation in one. It is the kind of note you reread weeks later to reload what a session gave you.

This is the **breadth** sibling of `/create-mental-model`. That skill captures one reducible aha, deeply, through a stuck-point arc. This one captures the **spread** of a session and explains each piece clearly enough to stand on its own. When a session produced both a sharp aha and a broader recap, the two skills split the work: the aha becomes a mental-model note, this note covers the rest and links to it.

## Input

The skill reads a **cc-export transcript file** (a `.md` in `~/Notes/log/`, the output of `cc-export <topic>` at the end of a `/study` session). The user gives a path. The transcript has the learner's turns blockquoted under `User:` and the tutor's turns under `Claude:`, exchanges separated by `---`.

Pasted text also works, whether it is the full transcript or just a summary, when the user has no file path. If neither is given, ask for the transcript path.

A transcript tells you two things: *what* the session covered (the topics and the order they came up) and *how the learner engaged* (which questions they asked, where they got stuck, what example made it click). Both feed the note. The second is what keeps it in the learner's voice rather than a textbook's.

## Workflow

### Step 1: Read and scope

Read the transcript end to end. Identify the concept(s) the session actually worked through, not every term that flew by. Most sessions are **one note**: a single concept with its adjacent ideas folded in.

Split into two or three notes only when the session genuinely covered distinct, non-adjacent topics that each deserve their own page. Be conservative. Adjacent ideas (a concept and the trick that proves it, a primitive and its failure case) belong together. When in doubt, keep it as one note. A split that scatters a single line of reasoning across pages is worse than one slightly longer note.

While reading, watch for an **aha candidate**: a moment where the learner was stuck and a reframing dissolved it, the kind of thing `/create-mental-model` exists to capture. Note it for the confirm step. Do not write it up here yet.

Also harvest the **learner's own phrasings of core ideas** while reading: a side note, a proof annotation, a summary in their words ("the important property is realizing P(U <= F(x)) = F(x), the core of this proof"). When the note explains that idea, use their line, verbatim or rephrased into a clearer sentence that loses none of the meaning. Their wording of a key insight beats a freshly composed explanation, because it is the understanding the note exists to preserve. Do this by default, without waiting to be asked.

### Step 2: Confirm

One combined exchange before writing, always. Run it even when a kickoff prompt or contract file already supplies an approved structure (the preview catches drift between the contract and what the transcript actually holds), and even when the input is pasted text rather than a file. Present, in a single message:

1. **Source summary**: a few bullets on what the session covered: the topics worked through, the concepts discussed, where the learner got stuck, and what made it click. This doubles as proof the skill read the source right.
2. **The plan**: one note, or a conservative split, with a one-line title for each.
3. **Structure preview**: for each planned note, its sections in order, one line per section on what it holds. List each proposed diagram as its own line (which section, what the figure shows) so it can be vetoed before any writing happens.
4. **Frontmatter**: each note's filename slug, tags, sources, and related wikilinks.
5. **Aha candidates**: if Step 1 found one, ask whether to promote it. "The part where you got stuck on X and then saw Y looks like its own mental-model note. Want me to hand that to `/create-mental-model`, or just cover it briefly here?" If they say promote, default to finishing this concept note first with a `[[link]]` to the aha note (the wikilink is fine before that note exists), then run `/create-mental-model` on the aha. Reverse the order only if they ask. If they say it is not a deep enough aha to deserve its own note, fold a short version into the concept note instead.
6. **Links**: if mental-model notes already exist from this session, plan to `[[wikilink]]` them rather than re-explaining their content. The learner usually knows. If unsure, grep `~/Notes/knowledge/` for `type: mental-model` notes that match the session's topic by filename or tag.

Then stop and wait. The learner will tweak or approve. After tweaks, acknowledge them in one line and start writing, do not re-present the full outline. In an autonomous or non-interactive run, make these calls yourself on the most reasonable reading, state the summary and structure compactly, and proceed.

### Step 3: Write

Write the note(s). Save to `~/Notes/knowledge/<slug>.md`, where `<slug>` is a kebab-case description of the concept. Soft length target: **600 to 1200 words** per note. If a single note would run well past that, treat it as a signal to re-check Step 1's split test. The cause is usually two distinct topics, not verbose writing, so split rather than trim.

Before writing, read `writing-principles.md` for the general craft rules (plain English, lead with the point, scannable prose, structure fits content) and `voice-calibration.md` for the target voice, then invoke the `obsidian:obsidian-markdown` skill so wikilinks, callouts, LaTeX, and frontmatter render correctly. The writing rules live in `writing-principles.md` and the two sections below (**Voice** and **Structure**). They are the heart of this skill, read them.

### Step 4: Verify

Run the note through the `humanizer` skill as a **detection-only pass**. It flags AI-tone markers. Rewrite only the flagged spots in the learner's voice, leave everything else. Do not relaunder the whole note.

Then a quick structural self-check: does the note reduce to its stated concept(s)? Does every section earn its place? Is the English plain (see the rule below)? Are existing aha notes linked rather than duplicated?

Then a completeness check: spawn a subagent (`model: "sonnet"`) that re-reads the transcript and the finished note(s) and returns any learner realizations, aha moments, or tutor-confirmed observations the notes missed. Fold in the ones that matter, ignore the rest.

Optional visual: if a concept is genuinely spatial or structural (a distribution, a protocol's round order, a geometric symmetry), spawn an agent to make one Excalidraw diagram via `obsidian-visual-skills:excalidraw-diagram`, save to `~/Notes/assets/`, and embed it with `![[filename]]`. Skip it for pure algebra or definitions. A diagram that does not carry understanding is clutter.

## Voice

The target is **60% Sivaram's own voice, 40% Brilliant-wiki / 3Blue1Brown clarity**. Personal recap voice carries the note, clean explainer structure carries the technical core. See `voice-calibration.md` for worked examples of both sides and how they mix.

The 60% (personal): first person where it helps, questions as natural entry points ("So can we just convert the shares?"), direct landings ("That's all this is.", "This doesn't solve the problem."), numbers that ground every claim, honest asides. This is the register of `/create-mental-model`. The note should read like the learner explaining the session to themselves, not like an encyclopedia entry.

The 40% (clarity): the moves that make Brilliant and 3Blue1Brown easy to follow. Functional definition plus a concrete instance in the opening. Name the action before the term. Surface the confusion the reader is about to have. A short mantra that compresses the idea. Use these to keep the explanation clear, not to flatten the voice out of it.

### The plain-English rule

Keep the English **simple, clear, and easy to read**. This is the single most important rule, and the thing the old version of this skill got wrong. The full rule (keep technical terms exact, cut fancy English, clear beats impressive) is general and lives in `writing-principles.md`. Read it. The swap table of specific word replacements is in `voice-calibration.md`.

## Structure

**There is no fixed template, and that is deliberate.** The strongest notes in this vault each have a structure that fits their own content: an attack note runs Setup, Attack, Why, Fix. A contrast note runs TL;DR, the principle, two parallel halves, a mnemonic. Forcing every session into one skeleton (Overview, Details, Summary) produces worse notes, because the structure of a good note is part of its argument. Let the content choose the shape.

What helps without caging is a **soft set of elements** to consider, not a form to fill. Reach for the ones the session calls for, in whatever order fits:

- an **orienting opener**: a one-line statement of the concept, or the question the session started from, often a `> [!info]` callout or a TL;DR line.
- the **walk-through**: the concept(s) explained clearly, in the order that builds understanding, which is often not the order the session covered them.
- **the move that made it click**: the example or reframe that landed, in the learner's voice.
- **links out**: `[[wikilinks]]` to any aha notes from the session and related vault notes, instead of re-explaining them.
- **what stayed shaky**: the open threads, the thing to re-test next session. Genuinely useful in a recap, and most notes should end on one.

The research signal behind this: notes that ramble tend to lack any opener or any sense of what was unresolved. Notes that are good tend to have a clear anchor and content-shaped sections. So nudge toward an anchor and an open-threads line, and otherwise let the concept dictate the rest. The general layout rules (no walls of text, no bullet piles, bullets only for parallel items) live in `writing-principles.md`.

## Boundary with create-mental-model

Keep these straight, it is the distinction the old skill blurred:

| | `/create-mental-model` | `/create-concept-notes` |
|---|---|---|
| Captures | one reducible aha | the spread of a session |
| Depth | deep, one insight | broad, clear on each piece |
| Shape | stuck-point arc | content-shaped recap |
| `type:` | `mental-model` | `concept` |

When a session has both, this note covers the breadth and **links to** the aha note for the depth, it does not duplicate the explanation. The confirm step (Step 2) is where you catch an aha worth promoting and hand it off.

## Frontmatter and saving

Save to `~/Notes/knowledge/<slug>.md` with:

```yaml
---
type: concept
status: done
tags: []
created: <today's date, YYYY-MM-DD>
sources: []
related: []
---
```

Fill `tags` with broad themes only (`#cryptography`, `#frost`, `#secp256k1`), `sources` with the transcript path or any references discussed, `related` with `[[wikilinks]]` to connected notes (including any mental-model note from this session). Do not invent new frontmatter fields, the vault schema is fixed.

## What makes a note fail

- **Generic / AI-ish voice.** The top reason the old skill went unused. If it reads like a textbook or a press release, it failed. Plain words, personal voice.
- **Forced into a template.** Sections that exist because a skeleton demanded them, not because the content needed them.
- **Topic tour.** A list of everything mentioned, with no through-line. Cover what the session worked through, not its full vocabulary.
- **Duplicating an aha note.** Re-explaining what a linked mental-model note already covers. Link, do not repeat.
- **Coverage over clarity.** Trying to be complete instead of clear. A note that explains three things well beats one that name-drops eight.

## Sibling skills

- `obsidian:obsidian-markdown`: Step 3, for correct wikilink, callout, LaTeX, and frontmatter syntax.
- `humanizer`: Step 4, detection pass for AI-tone.
- `obsidian-visual-skills:excalidraw-diagram`: Step 4, optional, only when a visual carries understanding.
- `/create-mental-model`: the handoff target when Step 2 finds an aha worth its own note.

`voice-calibration.md` and `sample-notes.md` sit next to this file. Read the first before writing. The second shows real vault notes and why their structures work. The `references/` folder holds Brilliant and 3Blue1Brown exemplars for the clarity 40%, scan them when a concept's explanation needs a model to follow.
