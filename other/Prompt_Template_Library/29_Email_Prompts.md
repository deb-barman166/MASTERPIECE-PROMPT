# Email Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-29

---

## 01. Overview

Email prompting is a domain-specific technique for composing effective emails across contexts — professional correspondence, marketing/newsletter emails, and transactional messages. Unlike general content writing, email has unique structural constraints: a subject line that determines open rates, a preview text snippet, a greeting/sign-off convention, and (for marketing email specifically) deliverability-conscious writing that avoids spam-trigger patterns. The right register also depends heavily on the relationship between sender and recipient — a cold outreach email, an internal team update, and a customer newsletter all follow different conventions.

## 02. Purpose

- Produce emails with subject lines that accurately reflect content and encourage opens.
- Match tone and formality to the actual sender-recipient relationship.
- Structure the body for how email is actually read (often skimmed, mobile-first).
- Avoid patterns that hurt deliverability or come across as spammy, for marketing email specifically.

## 03. Use Cases

- Professional/business correspondence (requests, follow-ups, introductions)
- Marketing and newsletter emails
- Cold outreach emails
- Internal team communications and updates
- Transactional emails (confirmations, receipts, notifications)
- Difficult or sensitive email conversations (declining, apologizing, delivering bad news)

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Communication` · `Correspondence`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Purpose**: What the email needs to accomplish
- **Recipient relationship**: Who this is going to and the existing relationship/formality level

## 08. Optional Inputs

- Subject line requirements
- Key points to include
- Tone (formal, friendly, urgent, apologetic)
- Length constraints
- Call to action / desired response
- Email type (marketing vs. transactional vs. personal correspondence)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{email_purpose}}` | Yes |
| `{{recipient_relationship}}` | Yes |
| `{{key_points}}` | No |
| `{{tone}}` | No |
| `{{length_constraint}}` | No |
| `{{call_to_action}}` | No |
| `{{email_type}}` | No |

## 10. Prompt Template

```text
Write an email for the following purpose.

PURPOSE:
{{email_purpose}}

RECIPIENT RELATIONSHIP:
{{recipient_relationship}}

EMAIL TYPE:
{{email_type}}

KEY POINTS TO INCLUDE:
{{key_points}}

TONE:
{{tone}}

LENGTH CONSTRAINT:
{{length_constraint}}

CALL TO ACTION / DESIRED RESPONSE:
{{call_to_action}}

INSTRUCTIONS:
- Write a subject line that accurately reflects the content and would
  encourage an open, without being clickbait-y or misleading.
- Match formality to the stated recipient relationship — don't default to
  either overly formal or overly casual without that context.
- Get to the point efficiently; assume the recipient is skimming, especially
  on mobile.
- State the desired response or call to action clearly, ideally by the end
  of the first or second paragraph for busy recipients.
- If this is a marketing email, avoid spam-trigger language patterns (e.g.,
  excessive urgency, all-caps subject lines, excessive exclamation points).
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{email_purpose}}` | What the email needs to accomplish | "Follow up on a proposal sent last week with no response" |
| `{{recipient_relationship}}` | Who this goes to and existing rapport | "A potential client I've met once at a conference, no email history yet" |
| `{{email_type}}` | The category of email | "Professional follow-up (not marketing)" |
| `{{key_points}}` | Must-include content | "Reference our conversation about their Q3 timeline" |
| `{{tone}}` | Desired register | "Polite, low-pressure, not pushy" |
| `{{length_constraint}}` | Desired brevity | "Under 100 words" |
| `{{call_to_action}}` | What response is wanted | "Ask if they've had a chance to review, offer a quick call this week" |

## 12. Example Input

```text
PURPOSE: Follow up on a proposal sent 8 days ago with no response
RECIPIENT RELATIONSHIP: Potential client met once at a conference, first
email follow-up
EMAIL TYPE: Professional follow-up
KEY POINTS: Reference their mentioned Q3 timeline concern
TONE: Polite, low-pressure
LENGTH: Under 100 words
CALL TO ACTION: Ask if they've reviewed it, offer a quick call this week
```

## 13. Example Output

```text
SUBJECT: Following up on the proposal — any questions?

Hi [Name],

Hope you've been well since we met at [Conference]! I wanted to follow up
on the proposal I sent over last week, since I know you mentioned wanting
to move quickly given your Q3 timeline.

No pressure at all if you're still reviewing — just wanted to check if any
questions have come up, or if it'd be helpful to hop on a quick 15-minute
call this week to walk through anything.

Let me know what works best for you.

Best,
[Your name]
```

*(87 words, meets the under-100-word constraint)*

## 14. Customization Guide

- **Always specify the recipient relationship**: The same purpose (e.g., "ask for something") reads completely differently to a close colleague vs. a first-time external contact — this is the single biggest driver of appropriate tone.
- **Distinguish marketing from transactional/personal email explicitly**: Marketing email has deliverability considerations (spam triggers, unsubscribe conventions) that don't apply to a one-to-one professional email.
- **State length constraints for busy-recipient contexts**: Executive or first-touch emails especially benefit from explicit brevity constraints, since length itself signals respect for the recipient's time.
- **Make the call-to-action concrete**: "Reach out" is vague; "reply with a yes/no on whether Thursday at 2pm works" gives the recipient an easy, low-friction action.

## 15. Output Format Options

- Plain text (subject + body)
- HTML (for marketing/newsletter emails with formatting)
- Markdown (for internal use before conversion to email format)

## 16. Best Practices

- Always specify the recipient relationship — this single input shapes formality, warmth, and structure more than any other variable.
- Request a subject line as part of the output, not as an afterthought — it materially affects whether the email gets read at all.
- State the desired call to action explicitly and ask for it to appear early, since many recipients skim rather than read fully.
- For marketing emails specifically, explicitly request spam-trigger avoidance rather than assuming it by default.

## 17. Common Mistakes

- Not specifying the recipient relationship, resulting in a tone that's either too formal for a close colleague or too casual for a first-time professional contact.
- Treating all email requests the same regardless of type (marketing vs. personal vs. transactional), missing type-specific conventions.
- Omitting a clear call to action, leaving the recipient unsure what response is actually wanted.
- Requesting long, thorough emails when the actual context calls for brevity and respect for the recipient's time.

## 18. Prompt Variations

- **Basic Version**: Purpose + recipient relationship only, no tone/length/CTA specification.
- **Advanced Version**: Full structure with tone, length, key points, and CTA (Section 10).
- **Expert Version**: For sensitive or high-stakes emails, adds a request for 2 tonal variations (e.g., "direct" vs. "softer") so the sender can choose based on their read of the situation, plus a brief note on the trade-off between the two approaches.

## 19. Related Prompts

- `28_Marketing_Prompts.md` — for the marketing/campaign strategy layer above individual marketing emails
- `26_Content_Writing_Prompts.md` — newsletter-style emails share long-form content writing principles
- `37_Business_Prompts.md` — many business communication scenarios (negotiation, feedback, declining) overlap with difficult email composition

## 20. Tips

- For difficult emails (declining a request, delivering bad news, addressing a conflict), explicitly requesting 2 versions — one more direct, one softer — gives the sender a meaningful choice based on their read of the relationship, rather than committing to a single guessed tone.
- Asking for the subject line to be generated last, after the body, sometimes produces a more accurate subject line since it can then genuinely reflect the finished content rather than being written from the purpose alone.

## 21. Limitations

- Tone-matching from a description of the relationship has natural variance; for especially sensitive or high-stakes correspondence, human review before sending remains important.
- Marketing email deliverability depends on many technical factors (sender reputation, authentication, list hygiene) beyond just the copy itself, which this template doesn't address.
- Cultural and organizational norms around email formality vary significantly; the model's defaults may not match a specific company's or region's particular conventions without that context being stated.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#email` `#business-communication` `#correspondence` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
