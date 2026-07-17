# Contribution Guide

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-54 · Governance

---

## Overview

This guide explains how to add new templates or improve existing ones while keeping the library internally consistent. Whether you're extending this collection for personal use, a team, or a public-facing resource, following this structure keeps every file navigable in the same way and prevents the library from fragmenting into inconsistent formats over time.

---

## 1. Adding a New Technique or Domain Template (Files 01-40 Style)

New technique/domain templates must follow the exact 25-section structure used throughout files 01-40:

```
01. Overview                    10. Prompt Template           19. Related Prompts
02. Purpose                     11. Placeholder Explanation    20. Tips
03. Use Cases                   12. Example Input               21. Limitations
04. Target AI Models            13. Example Output              22. Model Compatibility
05. Prompt Category             14. Customization Guide         23. Tags
06. Difficulty Level             15. Output Format Options       24. Version History
07. Required Inputs              16. Best Practices              25. License / Credits
08. Optional Inputs              17. Common Mistakes
09. Variables                    18. Prompt Variations
```

**Checklist for a new template:**

- [ ] All 25 sections present, in order, with matching headers (`## NN. Title`)
- [ ] Section 10's Prompt Template uses `{{variable}}` placeholder syntax consistently
- [ ] Section 11's Placeholder Explanation table covers every variable used in Section 10
- [ ] Sections 12-13 (Example Input/Output) are a genuine, complete worked example — not a fragment
- [ ] Section 18 includes exactly three variations: Basic, Advanced, Expert
- [ ] Section 19 links to at least 2 genuinely related existing templates, with brief reasoning
- [ ] Section 22's Model Compatibility table uses the same model list and ✅/⚠️/❌ convention as other templates
- [ ] Section 23 tags are added to `53_Tagging_System.md` in the appropriate categories
- [ ] The new file is added to `52_Prompt_Library_Index.md` in the correct part/section
- [ ] The new file is added to `50_Cheat_Sheet.md`'s situational lookup table
- [ ] A version history entry exists (Section 24) even for a first release ("1.0 | [date] | Initial release")
- [ ] File naming follows the `NN_Title_Case_With_Underscores.md` convention, continuing the existing numbering sequence

## 2. Deciding Whether Domain-Specificity Applies

Before writing a new domain template, decide explicitly: should this template contain genuinely domain-specific language and examples (like SQL, video generation), or should it stay universal/abstract (like the foundational techniques 01-15)? This decision should be made deliberately, not defaulted — and once made, should be consistent with how similar existing templates in the same category were built. Mixing abstraction levels within the same category confuses users trying to compare templates.

## 3. Adding a New Reference/Governance Document (Files 41-56 Style)

Files 41-56 don't follow the 25-section structure — each is shaped to its actual purpose (a checklist, an index, a comparison table). If adding a new document in this range:

- [ ] Include a standard header block (Library name, Author, Document ID, document type)
- [ ] Include an "Overview" section explaining the document's purpose
- [ ] Include a "Related Documents" section linking to genuinely connected files
- [ ] Include a "Version History" table
- [ ] Include a "License / Credits" section matching the rest of the library
- [ ] Structure the body content in whatever format actually serves the document's purpose — don't force an unrelated structure onto it

## 4. Updating an Existing Template

When revising an existing template rather than adding a new one:

- [ ] Update the Version History table (Section 24) with the new version number, date, and a brief description of what changed
- [ ] If the change affects tags, update `53_Tagging_System.md` accordingly
- [ ] If the change affects difficulty level or category, update `52_Prompt_Library_Index.md` and `50_Cheat_Sheet.md` accordingly
- [ ] Note significant library-wide changes in `56_Changelog.md`

## 5. Style Consistency Guidelines

- **Tone:** Direct, practical, instructional — avoid marketing language or unnecessary hedging.
- **Placeholder syntax:** Always `{{variable_name}}`, lowercase with underscores.
- **Tables:** Use consistent column headers across similar tables (e.g., all Model Compatibility tables use the same model list and status symbols).
- **Cross-references:** Always use the full filename with `.md` extension when linking to another template, so links remain valid regardless of viewing context.
- **Examples:** Worked examples (Sections 12-13, or equivalent in reference docs) should be realistic and complete enough to actually demonstrate the technique — not so abbreviated that the reader can't see the technique in action.

## 6. Quality Bar for New Contributions

A new template should be able to answer "yes" to all of the following before being considered complete:

1. Could someone unfamiliar with this technique understand what it is and when to use it from Sections 01-06 alone?
2. Could someone copy Section 10's template, fill in the variables, and get a usable prompt without needing to read the rest of the file?
3. Does the worked example (Sections 12-13) genuinely illustrate the technique, not just restate the template abstractly?
4. Are the Common Mistakes (Section 17) genuinely specific to this technique, not generic advice that could apply to any prompt?
5. Is the Model Compatibility table (Section 22) based on genuine capability differences, not just copied uniformly from another template?

## Related Documents

- `52_Prompt_Library_Index.md` — where new templates must be added
- `53_Tagging_System.md` — where new tags must be registered
- `56_Changelog.md` — where library-wide changes are logged

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
