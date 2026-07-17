# Changelog

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-56 · Version History

---

## Overview

This is the master changelog for the Prompt Engineering Template Collection as a whole, tracking when major sets of files were added or restructured. Individual template files also carry their own Section 24 "Version History" for changes specific to that file; this document tracks library-wide milestones instead.

---

## Version 1.2 — Reference & Governance Layer (Files 41-56)

**Added:**
- `41_Common_Mistakes.md` — cross-library mistake reference
- `42_Best_Practices.md` — cross-library best-practices reference
- `43_Real_World_Case_Studies.md` — five composite case studies showing template combinations in practice
- `44_AI_Model_Compatibility.md` — cross-model comparison matrix
- `45_OpenAI_Prompting.md` through `49_Perplexity_Prompting.md` — five platform-specific prompting guides
- `50_Cheat_Sheet.md` — one-page situational quick reference
- `51_Prompt_Checklist.md` — pre-flight checklist by task category
- `52_Prompt_Library_Index.md` — complete master index of all 56 files
- `53_Tagging_System.md` — consolidated tag taxonomy across all 40 technique/domain templates
- `54_Contribution_Guide.md` — structural guidelines for extending the library
- `55_Resources.md` — external reference categories
- `56_Changelog.md` — this document

**Structural note:** Files 41-56 intentionally do not follow the 25-section template structure used in files 01-40, since they serve a reference/governance function rather than being individual technique templates. Each is structured to its specific purpose instead.

**Library size after this update:** 56 files total (40 technique/domain templates + 16 reference/governance documents)

---

## Version 1.1 — Domain-Specific Expansion (Files 16-40)

**Added — Agentic & Architectural Techniques (16-20):**
- `16_Agentic_Prompting.md`
- `17_Multi_Agent_Prompting.md`
- `18_Tool_Use_Prompting.md`
- `19_Function_Calling.md`
- `20_RAG_Prompting.md`

**Added — Domain-Specific Templates (21-40):**
- Software Development: `21_Code_Generation_Prompts.md`, `22_Debugging_Prompts.md`, `23_SQL_Prompts.md`, `24_Web_Development_Prompts.md`
- Data & Analytics: `25_Data_Analysis_Prompts.md`
- Content & Marketing: `26_Content_Writing_Prompts.md`, `27_SEO_Prompts.md`, `28_Marketing_Prompts.md`, `29_Email_Prompts.md`, `30_Social_Media_Prompts.md`
- Media Generation: `31_Image_Generation_Prompts.md`, `32_Video_Generation_Prompts.md`
- Research & Language: `33_Research_Prompts.md`, `34_Summarization_Prompts.md`, `35_Translation_Prompts.md`
- Education, Business & Creative: `36_Education_Prompts.md`, `37_Business_Prompts.md`, `38_Productivity_Prompts.md`, `39_Creative_Writing_Prompts.md`, `40_Security_Best_Practices.md`

**Key decision made this version:** Domain-specific templates (21-40) were built with genuine field-specific language, terminology, and examples (e.g., the SQL template references actual dialects and JOIN syntax; the video generation template references actual camera movement vocabulary) rather than staying abstract/universal like the foundational templates (01-15). This was a deliberate scope decision distinguishing this file range from the foundational layer.

**Library size after this update:** 40 files total (technique/domain templates only; reference layer added in v1.2)

---

## Version 1.0 — Foundational Layer (Files 00-15)

**Added:**
- `00_README_Index.md` — original library index and navigation guide
- `01_Zero_Shot_Prompting.md` through `15_Loop_Prompting.md` — 15 foundational, domain-agnostic prompting technique templates

**Structural decisions established this version (carried through the entire library):**
- 25-section template structure adopted as the standard for all technique/domain templates
- `{{variable}}` placeholder syntax established as the standard for prompt templates
- Model Compatibility table format (✅/⚠️/❌ against a consistent model list) established
- Three-tier Prompt Variations structure (Basic/Advanced/Expert) established for Section 18

**Library size after this update:** 16 files total (15 templates + README index)

---

## Versioning Convention for This Library

- **Major version increments (1.0 → 1.1 → 1.2):** Addition of a new major file range or structural category.
- **Individual file version increments:** Tracked within each file's own Section 24 (or equivalent), not reflected as a library-wide major version bump unless the change is structurally significant.

## Related Documents

- `52_Prompt_Library_Index.md` — current complete file listing
- `54_Contribution_Guide.md` — guidelines for future additions, which should also be logged here

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
