# Writing principles

> A near-identical copy of this file lives in the sibling `create-concept-notes` skill (the two install as independent symlinks, so each carries its own copy). Keep the general rules below roughly aligned across both. Intentional per-skill differences are fine and expected, since the two skills do different jobs.

General craft rules for any knowledge note in this vault. They cover clarity, structure, and layout. They are loose guidelines, not a template. This skill writes deep notes on a single aha, meant to be re-studied closely rather than skimmed, so never trade a re-derivable reasoning chain for maximal skimmability. The skill's own Voice and Structure sections add the rest.

## Plain English, full technicality

Keep the English **simple, clear, and easy to read**. This is the rule that matters most.

- **Keep technical terms exact.** Nonce, homomorphism, negligible, Lagrange coefficient, soft fork. Never dumb the domain down. The reader is a cryptography engineer.
- **Cut fancy English that is not the concept.** Words reaching for sophistication the author does not use, like "elegant", "leverage", or "crucially". Replace them with plain words or cut them. The full swap list, including connector words like "utilize" and "in order to", lives in `references/voice-calibration.md`.
- **Keep sentences short.** Aim for about 15 to 20 words, treat 25 as a soft cap, and split any sentence you have to read twice. A non-native reader decoding vocabulary, syntax, and math at once feels a long sentence harder than a native reader does.
- The test: every non-technical word should be one a tired reader understands at once. If a sentence sounds smart, suspect it. Clear beats impressive.

## Make the title specific

The title is the note's strongest retrieval cue, the line you scan in a file list or link to by name. Make it name the actual point, not just the topic: "Pedersen commitments: hiding and binding", not "Pedersen commitments". Keep it short and specific. Test it by hiding the body: the title alone should bring back what the note says. For a stuck-point note, a short motivated question does the same job, like "Why does flatline data inflate Strauss's C value?".

## Lead with the point

Open each section and each paragraph with its conclusion, then give the detail. A reader skimming only first sentences should still get the gist. This is what keeps a note navigable for a quick reread without flattening it for a deep study.

The cover test: hide everything after the first sentence of a section, and if the point is gone, move it up. The sharpest check for the whole note is to read only the title and the first sentence of each section. If you cannot rebuild the note's main points from those alone, the structure needs work.

## Write from understanding, verify against the source

The source is usually a conversation between you and an AI, where the understanding surfaces through back and forth. Those sentences are dialogue, not note prose, so you cannot lift them straight into the note. Read the source, grasp what it actually established, and write the note from that understanding in your own clear structure.

Faithful is the hard constraint. The note must be factually correct, it must capture the real insight the conversation reached, and it must not change or soften it. After drafting, check the note against the source: every claim, number, and definition matches, the key insights are the ones the conversation actually reached, and nothing important is missing.

## Add the why, show a concrete case

After a main claim, add one sentence on why it must be true, or what would break if it were false, even when it feels obvious. That one sentence is what makes a note teach instead of list. Show one concrete instance per key idea too, ideally before the abstract statement, since a worked example with real values is a second, independent way to recall the idea months later. This works at the level of a claim or a paragraph, not as a section you bolt on.

## Scannable prose, not a bullet pile

A note gets reread, sometimes skimmed, sometimes studied closely. The layout has to serve both. Two opposite failures, avoid both:

- **Wall of text.** One paragraph carrying five or six separate facts in a row, the kind of dense block the eye slides off. If a paragraph runs past about five sentences, or you cannot state its point in the first sentence, it is too dense. Break it up, and pull any genuine list of parallel facts out into bullets.
- **Bullet pile.** A reasoning chain chopped into bullets. Bullets drop the "because / so / which means" that carries an argument and leave fragments the reader has to reconnect. Keep reasoning, narrative, and every "why" in prose.

The line between them: bullets are for parallel, order-independent items the reader compares or returns to one at a time. Prose is for anything joined by logic or sequence. A two-to-four item list usually reads fine as a sentence with commas, and a longer list should stay around five items, split into named groups beyond that. Most of a strong note is prose with a few bold lead-ins and the odd short list, not a slide deck.

## Structure fits the content

There is no fixed template, and that is deliberate. The strongest notes each take the shape their content calls for, because the structure of a good note is part of its argument. Forcing every note into one skeleton produces worse notes. Let the content choose the shape, and reach for subheadings freely, since they are the highest-leverage way to make a note navigable.

## Link out, do not repeat

Use `[[wikilinks]]` to point at related notes and prior aha notes instead of re-explaining them. A note that links is more useful than a note that duplicates, and it keeps each note to one job.

## Clarity over coverage

A note that explains three things well beats one that name-drops eight. The idea underneath is atomicity: one idea per note. The moment a second distinct idea wants its own explanation, stop and start a new note linked with a `[[wikilink]]`. Cover what the note is actually about, in depth, and link the rest.

## Notation and symbols

Most notes here are crypto and math, so a few habits keep symbol-heavy prose readable.

- **Avoid starting a sentence with a symbol.** Use English words for quantifiers in prose (for all, there exists, implies), and keep the symbol forms inside displayed formulas. A sentence that opens with a symbol loses its grammatical subject and forces a reparse.
- **Give a symbol's role before its name.** Write "the blinding scalar that hides the private key, $r$", not "let $r$ be the nonce". It forces you to know what the symbol does, and it helps a reader who has been away from the material.
- **Introduce an ad-hoc symbol only when it earns its keep.** If a letter would appear just once or twice, write the phrase out instead. Lean on this for invented letters, and relax it for field-standard ones like $r$ for a nonce, $x$ for a secret key, or $G$ for a generator.
- **Proofs read as prose.** Introduce each variable with its type when it first appears, write complete sentences, end formulas with punctuation, and add a one-sentence plain restatement after a formal expression.
