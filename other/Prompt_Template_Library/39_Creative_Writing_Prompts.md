# Creative Writing Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-39

---

## 01. Overview

Creative Writing prompting is a domain-specific technique for generating fiction, poetry, and other imaginative written work. Unlike informational content writing, creative writing prompts benefit from specifying craft elements that shape the actual creative execution: genre and its conventions, point of view, narrative voice, pacing, and the emotional or thematic core the piece should serve — details that determine not just what happens in a story but how it's told, which is often where creative writing succeeds or falls flat.

## 02. Purpose

- Produce creative work with a genuinely distinct voice and craft, not generic template fiction.
- Match genre conventions appropriately while leaving room for originality within them.
- Support both short, self-contained pieces and larger structured works (chapters, story arcs).
- Balance creative freedom with the specific constraints/direction the writer actually wants.

## 03. Use Cases

- Short story and flash fiction writing
- Poetry (structured forms and free verse)
- Character and world-building development
- Dialogue writing
- Story outlining and plot development
- Genre fiction (mystery, sci-fi, fantasy, romance, horror)
- Creative writing exercises and prompts for practice

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — noted for strong creative writing performance)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Creative` · `Fiction & Poetry`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Premise/subject**: What the piece is about
- **Form**: Short story, poem, dialogue, character sketch, etc.

## 08. Optional Inputs

- Genre and its conventions
- Point of view (first person, third limited, omniscient)
- Tone/mood
- Length
- Thematic core or emotional arc
- Specific craft constraints (a poetic form, a narrative structure)
- Character details (if character-focused)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{premise_subject}}` | Yes |
| `{{form}}` | Yes |
| `{{genre}}` | No |
| `{{point_of_view}}` | No |
| `{{tone_mood}}` | No |
| `{{length}}` | No |
| `{{thematic_core}}` | No |
| `{{craft_constraints}}` | No |

## 10. Prompt Template

```text
Write a piece of creative writing based on the following.

PREMISE/SUBJECT:
{{premise_subject}}

FORM:
{{form}}

GENRE:
{{genre}}

POINT OF VIEW:
{{point_of_view}}

TONE/MOOD:
{{tone_mood}}

LENGTH:
{{length}}

THEMATIC CORE (what this piece is really about, beneath the surface plot):
{{thematic_core}}

CRAFT CONSTRAINTS:
{{craft_constraints}}

INSTRUCTIONS:
- Prioritize a genuine, specific voice over generic genre-typical phrasing
  — favor concrete, sensory detail over abstract description.
- Let the thematic core inform choices (what to show, what to leave
  unsaid) rather than stating the theme explicitly within the piece.
- Honor genre conventions where they serve the piece, but don't feel
  bound to cliché versions of them.
- Match the specified point of view consistently throughout.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{premise_subject}}` | The core idea/situation | "A lighthouse keeper receives a letter from someone who claims to be their future self" |
| `{{form}}` | The type of piece | "Short story" |
| `{{genre}}` | Genre and its conventions | "Literary fiction with a subtle magical realism element" |
| `{{point_of_view}}` | Narrative perspective | "First person, present tense" |
| `{{tone_mood}}` | Overall feeling | "Quiet, melancholic, with a thread of hope" |
| `{{length}}` | Target length | "800-1000 words" |
| `{{thematic_core}}` | The underlying meaning | "About the fear of becoming who you're afraid you'll become, and choosing otherwise" |
| `{{craft_constraints}}` | Specific structural requirements | "Must end on a line of dialogue, not narration" |

## 12. Example Input

```text
PREMISE: A lighthouse keeper receives a letter claiming to be from their
future self, warning them about a choice they haven't made yet
FORM: Short story
GENRE: Literary fiction, subtle magical realism
POV: First person, present tense
TONE: Quiet, melancholic, thread of hope
LENGTH: 800-1000 words
THEME: Fear of becoming who you're afraid you'll become, and choosing
otherwise
CRAFT CONSTRAINT: End on a line of dialogue
```

## 13. Example Output

```text
[A full 800-1000 word short story would be generated here, written in
first person present tense, opening with a concrete sensory image (the
lighthouse, the letter's arrival), developing the central tension between
the keeper and the warning letter, allowing the theme of self-determination
versus fated identity to emerge through the keeper's specific choices and
observations rather than stated directly, maintaining the melancholic-but-
hopeful tone throughout, and ending precisely on a line of dialogue per the
craft constraint.]
```

*(Note: Full story output omitted here for brevity in this template
reference; in actual use, the complete generated piece would appear.)*

## 14. Customization Guide

- **State thematic core separately from plot premise**: The premise is what happens; the theme is what it means — providing both explicitly helps the model make purposeful craft choices rather than just narrating events.
- **Specify point of view and tense together**: "First person" alone leaves tense ambiguous (past vs. present), which meaningfully affects narrative immediacy — state both.
- **Use genre labels as a starting point, not a cage**: Naming a genre helps establish conventions and reader expectations, but explicitly inviting departure from cliché versions of those conventions often produces more interesting work.
- **Add specific craft constraints for practice/exercise purposes**: Constraints like "no dialogue," "must be exactly 100 words," or "second person throughout" are valuable creative writing exercises that push past default patterns.

## 15. Output Format Options

- Prose (narrative formatting)
- Verse (line breaks preserved for poetry)
- Script/dialogue format
- Structured outline (for longer works, plot/chapter breakdown)

## 16. Best Practices

- Provide both the surface premise and the underlying thematic core — this produces writing with purposeful craft choices rather than plot-only narration.
- Specify point of view and tense together for narrative consistency.
- Invite departure from generic genre convention rather than only naming the genre, to avoid cliché-heavy output.
- For poetry, specify the form explicitly (sonnet, haiku, free verse) since formal constraints meaningfully shape the writing process and result.

## 17. Common Mistakes

- Providing only a plot premise without any thematic direction, resulting in competent but hollow event-narration.
- Not specifying point of view/tense, leading to inconsistent narrative perspective within the piece.
- Treating genre as a rigid formula rather than a flexible set of reader expectations, producing cliché-heavy writing.
- Requesting creative writing with an overly restrictive brief that leaves no room for genuine creative discovery in the writing process.

## 18. Prompt Variations

- **Basic Version**: Premise + form only, no genre/POV/theme specification.
- **Advanced Version**: Full structure with genre, POV, tone, theme, and craft constraints (Section 10).
- **Expert Version**: Adds a request for the piece to be written twice with two different structural approaches (e.g., linear chronology vs. a fragmented/non-linear structure) for the same premise and theme, useful for exploring which structural choice best serves the material.

## 19. Related Prompts

- `26_Content_Writing_Prompts.md` — shares long-form writing principles, though for informational rather than creative purposes
- `10_Self_Reflection.md` — useful for a self-critique/revision pass on a creative draft against specific craft goals
- `17_Multi_Agent_Prompting.md` — can simulate a Writer/Editor role pair for structured creative feedback

## 20. Tips

- For a genuinely distinct voice, providing a short example of writing in the desired voice (even unrelated in subject) is often more effective than describing the voice in adjectives — voice is easier to demonstrate than define.
- When revising a creative draft, asking for feedback focused on one specific craft element at a time (just pacing, just dialogue naturalism, just sensory detail) tends to produce more actionable revision guidance than an open-ended "make this better" request.

## 21. Limitations

- Creative writing quality and voice authenticity have natural variance; what reads as compelling is inherently subjective, and iteration/revision typically improves on a first draft significantly.
- For long-form creative projects (novels, extended series), maintaining full consistency (character details, world rules, prior plot threads) across many separate generations is a real challenge — see Prompt Chaining (Template 14) for managing this across a longer project.
- Original published creative works remain protected by copyright; this template is for generating new original creative writing, not for reproducing existing copyrighted stories, poems, or characters.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ (noted for strong creative writing) |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#creative-writing` `#fiction` `#poetry` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
