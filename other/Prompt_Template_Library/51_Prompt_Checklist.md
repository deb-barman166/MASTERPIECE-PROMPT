# Prompt Pre-Flight Checklist

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Document ID:** PTL-51 · Quick Reference

---

## How to Use This Checklist

Run through the relevant section(s) before sending an important prompt. Not every item applies to every prompt — use judgment about which sections are relevant to your specific task. Treat this as a diagnostic tool: if output quality disappoints, come back and check what was skipped.

---

## ✅ Universal Checklist (Every Prompt)

- [ ] I've stated the exact output format I want (prose, list, table, JSON, code)
- [ ] I've stated the desired length or scope
- [ ] I've front-loaded the most important instruction
- [ ] I haven't bundled multiple unrelated tasks into one prompt
- [ ] If anything is ambiguous, I've asked the model to state its assumptions rather than silently guess

## ✅ Example-Based Prompts (Templates 02-03)

- [ ] My example(s) reflect typical difficulty, not the easiest possible case
- [ ] I've included at least one edge case or boundary example (for few-shot)
- [ ] My examples are formatted consistently with each other
- [ ] Example length roughly matches my expected output length

## ✅ Reasoning Tasks (Templates 04-05, 07, 09-10, 12)

- [ ] I've explicitly requested step-by-step reasoning if this needs logic/math
- [ ] I've asked for a clearly labeled final answer, separate from the reasoning trace
- [ ] For high-stakes answers, I've considered multiple independent attempts (Self-Consistency) or a critique pass (Self-Reflection)
- [ ] For genuinely open-ended problems, I've considered exploring multiple approaches (Tree-of-Thought) rather than committing to the first idea

## ✅ Domain-Specific Technical Tasks (Templates 21-24)

- [ ] I've specified the exact language/framework version, not just the language name
- [ ] I've stated dependency/library constraints explicitly, even if "none"
- [ ] I've provided real existing code context for integration tasks
- [ ] I've specified error-handling expectations
- [ ] I've requested tests alongside implementation if correctness matters

## ✅ SQL Tasks (Template 23)

- [ ] I've provided the actual schema (real table/column names), not a description
- [ ] I've specified the exact SQL dialect
- [ ] I've defined ambiguous business terms explicitly ("recent," "top," "active")
- [ ] I've included index/scale context if performance matters

## ✅ Content/Marketing Tasks (Templates 26-30)

- [ ] I've described the actual target audience's expertise/interest level, not a generic label
- [ ] I've stated the content's purpose (inform, persuade, entertain)
- [ ] I've specified voice/tone
- [ ] For platform-specific content, I've named the exact platform, not "social media" generically
- [ ] I've stated length/character constraints if the format has real limits

## ✅ Research and Data Tasks (Templates 25, 33-34)

- [ ] I've stated real dataset structure (actual columns/types), not a vague description
- [ ] I've set explicit scope boundaries for the research question
- [ ] I've specified source quality requirements for anything consequential
- [ ] I've requested explicit handling of conflicting sources/findings
- [ ] I've requested a distinction between what the data/sources show directly vs. interpretation added
- [ ] I've asked for causal vs. correlational claims to be flagged appropriately

## ✅ Agentic and Tool-Use Workflows (Templates 11, 15-19)

- [ ] I've defined a concrete, checkable "definition of done"
- [ ] I've set a maximum iteration/step count as a safety limit
- [ ] I've named specific autonomy boundaries, not just "use good judgment"
- [ ] I've written precise tool/function definitions with exact input/output types
- [ ] I've specified what happens if a tool call fails
- [ ] For multi-agent setups, my roles have genuinely distinct objectives, not just different names

## ✅ Security-Sensitive Tasks (Template 40)

- [ ] I have NOT included any real credentials, API keys, or personal data in this prompt
- [ ] I've stated the actual threat model/exposure level (public-facing vs. internal)
- [ ] I've requested explicit security-by-default practices, not assumed them
- [ ] For code handling auth/payments/PII, I'm planning human security review in addition to this output

## ✅ Before Trusting a Repeated-Use Prompt (Templates 08, 13)

- [ ] I've tested this prompt on at least 2-3 varied real inputs, not just one
- [ ] I've checked whether output quality is consistent across runs
- [ ] For high-volume production use, I've considered systematic prompt testing (Automatic Prompt Engineering) rather than a single hand-written version

## ✅ Before Deploying an Agentic/Autonomous System (Template 16)

- [ ] The agent's plan is reviewed before it starts taking actions
- [ ] Escalation rules are defined for when the agent hits a decision outside its boundaries
- [ ] I've tested behavior at the maximum step count to confirm graceful stopping, not an abrupt cutoff
- [ ] I've considered what happens if the definition of done is never met

---

## Red Flags — Stop and Reconsider

If any of these are true, pause before sending:

- 🚩 The prompt asks for "the best" or "make it good" without defining criteria
- 🚩 A schema, codebase, or dataset is described in prose instead of pasted directly
- 🚩 A real credential, key, or personal data value is in the prompt
- 🚩 An agentic/loop prompt has no maximum iteration cap
- 🚩 A high-stakes reasoning task is being trusted on a single pass with no verification
- 🚩 Multiple unrelated tasks are bundled into one prompt "for efficiency"

## Related Documents

- `41_Common_Mistakes.md` — full explanation of what these checklist items prevent
- `42_Best_Practices.md` — full explanation of the positive practices behind this checklist
- `50_Cheat_Sheet.md` — quick template lookup by situation

## Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
