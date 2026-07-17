# Translation Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-35

---

## 01. Overview

Translation prompting is a domain-specific technique for converting text between languages while handling the considerations that distinguish good translation from mechanical word substitution: register/formality (many languages have formal vs. informal address forms English doesn't distinguish as clearly), regional dialect variation (e.g., European vs. Latin American Spanish, Brazilian vs. European Portuguese), idiomatic expressions that don't translate literally, and domain-specific terminology that may need to stay untranslated or use an established technical convention.

## 02. Purpose

- Produce translations that preserve meaning and tone, not just literal word-for-word equivalence.
- Handle formality/register appropriately for the target language and context.
- Account for regional dialect differences within a single target language.
- Correctly handle idioms, cultural references, and domain-specific terminology.

## 03. Use Cases

- Document and content translation
- Website/UI localization
- Business correspondence translation
- Marketing content adaptation (which often requires more than literal translation)
- Technical/legal document translation requiring terminology precision
- Subtitle or dialogue translation requiring natural, spoken-register phrasing

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Language` · `Translation`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Source text**: The text to translate
- **Target language**: The language to translate into (with regional variant if relevant)

## 08. Optional Inputs

- Formality/register level
- Context/purpose (marketing, legal, casual conversation, technical documentation)
- Terms that should NOT be translated (brand names, technical terms)
- Regional dialect specification
- Tone preservation notes

## 09. Variables

| Variable | Required? |
|---|---|
| `{{source_text}}` | Yes |
| `{{target_language}}` | Yes |
| `{{formality_register}}` | No |
| `{{context_purpose}}` | No |
| `{{do_not_translate}}` | No |
| `{{regional_dialect}}` | No |

## 10. Prompt Template

```text
Translate the following text.

SOURCE TEXT:
{{source_text}}

TARGET LANGUAGE:
{{target_language}}

REGIONAL DIALECT:
{{regional_dialect}}

FORMALITY/REGISTER:
{{formality_register}}

CONTEXT/PURPOSE:
{{context_purpose}}

DO NOT TRANSLATE (keep as-is):
{{do_not_translate}}

INSTRUCTIONS:
- Prioritize natural, idiomatic phrasing in the target language over literal
  word-for-word translation — a good translation should read as though
  originally written in the target language.
- Apply the specified formality/register consistently throughout.
- If an idiom or cultural reference in the source doesn't translate
  directly, find an equivalent that preserves the meaning/tone rather than
  translating it literally, and briefly note the adaptation if it's
  significant.
- Preserve terms listed as "do not translate" exactly as given.
- If any part of the source text is ambiguous in a way that affects
  translation choice, briefly note the ambiguity and your interpretation.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{source_text}}` | The text to be translated | "We're thrilled to have you on board!" |
| `{{target_language}}` | The destination language | "Spanish" |
| `{{regional_dialect}}` | Specific regional variant | "Latin American Spanish (not European Spanish)" |
| `{{formality_register}}` | Formal vs. informal address | "Informal/friendly (use 'tú' not 'usted')" |
| `{{context_purpose}}` | What this translation is for | "New employee welcome email" |
| `{{do_not_translate}}` | Terms to leave untranslated | "Product name 'CloudSync', company name" |

## 12. Example Input

```text
SOURCE TEXT: "We're thrilled to have you on board! If you hit any snags
during onboarding, just reach out — we've got your back."

TARGET LANGUAGE: Spanish
REGIONAL DIALECT: Latin American Spanish
FORMALITY: Informal/friendly (tú form)
CONTEXT: New employee welcome email at a tech startup
DO NOT TRANSLATE: none
```

## 13. Example Output

```text
"¡Nos emociona muchísimo tenerte con nosotros! Si tienes algún problema
durante el proceso de incorporación, no dudes en contactarnos — estamos
aquí para apoyarte."

TRANSLATION NOTES:
- "Hit any snags" (an English idiom) was adapted to "tienes algún
  problema" (have any issue) rather than translated literally, since a
  direct idiom-for-idiom match isn't natural in this context in Spanish.
- "We've got your back" was adapted to "estamos aquí para apoyarte" (we're
  here to support you) to preserve the warm, reassuring tone without
  forcing an awkward literal translation of the English idiom.
- Used "tú" form throughout per the informal register specification,
  consistent with typical Latin American startup workplace communication
  style.
```

## 14. Customization Guide

- **Always specify regional dialect when it matters**: Spanish, Portuguese, French, Arabic, and Chinese (among others) all have significant regional variation in vocabulary, formality conventions, and sometimes grammar — leaving this unspecified risks a translation that sounds noticeably "off" to the actual target region's readers.
- **State formality/register explicitly**: Many languages (Spanish, German, French, Japanese, Korean) have grammatically distinct formal/informal address forms that English doesn't mark as clearly — this is one of the most common gaps in under-specified translation requests.
- **List "do not translate" terms upfront**: Brand names, product names, and sometimes technical terms should often stay in the source language — specify these explicitly rather than risk them being translated inappropriately.
- **Provide context/purpose for tone-sensitive content**: A legal document, a marketing tagline, and a casual chat message all call for different translation approaches even for structurally similar source text.

## 15. Output Format Options

- Plain text (translation only)
- Translation + notes (adaptation explanations)
- Side-by-side (source and target text paired)
- Table (for translating multiple strings/phrases at once, e.g., UI localization)

## 16. Best Practices

- Specify regional dialect for any language with significant regional variation, not just the language name alone.
- State formality/register explicitly rather than leaving it to the model's default assumption.
- Request translation notes for idioms or culturally-specific content, so adaptation choices are visible and can be reviewed.
- Provide a do-not-translate list for brand names, product names, and technical terms with established conventions.

## 17. Common Mistakes

- Specifying only the language without regional dialect, risking a translation that reads as foreign or slightly off to the actual target audience.
- Not specifying formality/register, resulting in inconsistent or contextually inappropriate formal/informal usage.
- Translating idioms and cultural references literally, producing awkward or nonsensical phrasing in the target language.
- Failing to list brand/product names for exclusion, risking inappropriate translation of terms that should stay fixed.

## 18. Prompt Variations

- **Basic Version**: Source text + target language only, no register/dialect specification.
- **Advanced Version**: Full structure with dialect, formality, context, and do-not-translate list (Section 10).
- **Expert Version**: Adds a request for the model to flag any content that may not translate well culturally at all (e.g., a joke, wordplay, or reference that has no reasonable equivalent) rather than forcing an awkward adaptation, and to suggest an alternative approach for that specific piece of content.

## 19. Related Prompts

- `26_Content_Writing_Prompts.md` — marketing translation often requires more creative adaptation than literal content translation, overlapping with content writing principles
- `24_Web_Development_Prompts.md` — UI localization intersects with front-end development considerations (text expansion/contraction, RTL languages)
- `36_Education_Prompts.md` — language-learning content sometimes benefits from translation alongside pedagogical explanation

## 20. Tips

- For content where getting the tone exactly right matters a lot (marketing taglines, brand voice), requesting 2-3 translation options with slightly different approaches (more literal vs. more adapted) gives a meaningful choice rather than committing to a single interpretation.
- Native speaker review remains valuable for any translation used publicly or at scale — even careful prompting can miss subtle regional or cultural nuances that a native speaker would immediately catch.

## 21. Limitations

- Machine translation, even with careful prompting, may not fully capture every cultural nuance, especially for creative content like humor, poetry, or wordplay that depends on features specific to the source language.
- Low-resource languages (those with less training data available) may see less reliable translation quality than widely-spoken languages.
- For legal, medical, or other high-stakes documents, professional human translation and review is strongly recommended in addition to (not instead of) AI-assisted translation, given the consequences of subtle errors in these domains.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ (quality varies by language pair) |
| Mistral | ✅ (quality varies by language pair) |

## 23. Tags

`#translation` `#localization` `#language` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
