# Social Media Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-30

---

## 01. Overview

Social Media prompting is a domain-specific technique for producing platform-native content — posts, captions, and threads optimized for how each specific platform's audience actually consumes content. Each platform (Instagram, X/Twitter, LinkedIn, TikTok, Facebook) has meaningfully different conventions: character limits, hashtag culture, ideal post length, tone expectations, and what drives engagement (a LinkedIn post rewards professional insight; a TikTok caption rewards brevity and hook-driven curiosity). Treating "write a social post" as platform-agnostic produces content that underperforms everywhere.

## 02. Purpose

- Produce content matched to each platform's actual format conventions and audience expectations.
- Optimize the opening line/hook for platforms where feed algorithms and scroll behavior reward immediate engagement.
- Use hashtag and mention conventions appropriately per platform, not as an afterthought.
- Support repurposing a single core message across multiple platform-appropriate formats.

## 03. Use Cases

- Platform-specific post copywriting (LinkedIn, Instagram, X/Twitter, TikTok, Facebook)
- Caption writing for image/video content
- Thread creation for platforms that support them (X/Twitter, Threads)
- Repurposing one piece of content across multiple platforms
- Hashtag research and selection
- Community engagement responses (comments, replies)

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok (particularly attuned to X/Twitter conventions)
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Marketing` · `Social Content`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Core message/topic**: What the post is about
- **Platform**: Instagram, X/Twitter, LinkedIn, TikTok, Facebook, etc.

## 08. Optional Inputs

- Post format (single post, carousel, thread, story)
- Tone/voice
- Hashtag strategy
- Call to action
- Character/length constraints
- Whether this is part of a repurposing set (same message, multiple platforms)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{core_message}}` | Yes |
| `{{platform}}` | Yes |
| `{{post_format}}` | No |
| `{{tone_voice}}` | No |
| `{{hashtag_strategy}}` | No |
| `{{call_to_action}}` | No |
| `{{length_constraint}}` | No |

## 10. Prompt Template

```text
Write a social media post for the following.

CORE MESSAGE/TOPIC:
{{core_message}}

PLATFORM:
{{platform}}

POST FORMAT:
{{post_format}}

TONE/VOICE:
{{tone_voice}}

HASHTAG STRATEGY:
{{hashtag_strategy}}

CALL TO ACTION:
{{call_to_action}}

LENGTH CONSTRAINT:
{{length_constraint}}

INSTRUCTIONS:
- Open with a hook suited to how this platform's feed/algorithm works —
  the first line should earn attention before any expansion.
- Match the platform's native conventions for tone, formatting (line
  breaks, emoji use), and typical post length — a LinkedIn post and a
  TikTok caption should not read the same way even for the same core
  message.
- Use hashtags according to actual platform norms (e.g., different
  typical hashtag counts and placement conventions across platforms) —
  do not apply a one-size-fits-all hashtag approach.
- Include the call to action naturally, matched to how that platform's
  users typically engage (comment, share, click link in bio, etc.).
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{core_message}}` | The underlying idea/announcement | "We just launched a new feature that lets users export data to CSV" |
| `{{platform}}` | Target platform | "LinkedIn" |
| `{{post_format}}` | Structural format | "Single post, no carousel" |
| `{{tone_voice}}` | Desired personality | "Professional but not corporate-stiff" |
| `{{hashtag_strategy}}` | Hashtag approach | "2-3 relevant industry hashtags, no hashtag spam" |
| `{{call_to_action}}` | Desired engagement | "Encourage comments asking what feature they want next" |
| `{{length_constraint}}` | Platform-appropriate length | "Under 200 words, short paragraphs" |

## 12. Example Input

```text
CORE MESSAGE: We just launched CSV export for our analytics dashboard
PLATFORM: LinkedIn
TONE: Professional but approachable, not corporate-stiff
HASHTAG STRATEGY: 2-3 relevant hashtags
CALL TO ACTION: Invite comments on what feature to build next
```

## 13. Example Output

```text
We just shipped something our users have been asking for since day one:
CSV export.

It sounds small. It wasn't. Getting export right meant handling edge
cases across every report type in the dashboard — nested data, custom
date ranges, filtered views — without losing fidelity.

But "small" features like this are often the ones that unlock real
workflows. Analysts can now pull data straight into their own tools
instead of screenshotting charts (we see you, and we're sorry it took
this long).

What should we build next? Drop your top request in the comments —
we're planning the next quarter now, and this is exactly the kind of
feedback that shapes the roadmap.

#ProductUpdates #DataAnalytics #SaaS
```

## 14. Customization Guide

- **Always name the specific platform, not "social media" generically**: Conventions differ enough between platforms that a generic prompt produces generic, underperforming content everywhere.
- **State the post format if it matters**: A carousel, a thread, and a single post all have different structural requirements even for the same core message and platform.
- **Match hashtag strategy to actual platform norms**: Instagram traditionally supports more hashtags than LinkedIn or X/Twitter; specify a count/approach appropriate to the actual platform rather than defaulting to one convention everywhere.
- **Consider repurposing explicitly when creating for multiple platforms**: If the same core message needs versions for several platforms, request them together and ask the model to adapt structure/tone per platform rather than just resizing the same copy.

## 15. Output Format Options

- Plain text (platform-ready)
- Table (for multi-platform repurposing sets)
- Markdown (for internal review before posting)
- Bullet List (for a content calendar of multiple posts)

## 16. Best Practices

- Name the specific platform explicitly — this is the single most important variable for producing content that actually fits how that audience consumes posts.
- Request the opening hook be evaluated on its own merit — the first line often determines whether the rest gets read at all on fast-scrolling platforms.
- Use platform-appropriate hashtag conventions rather than a uniform approach across all platforms.
- For multi-platform campaigns, request adapted (not just resized) versions per platform to respect each one's actual norms.

## 17. Common Mistakes

- Writing platform-agnostic "social media" content that doesn't match any specific platform's actual conventions well.
- Using the same hashtag approach across all platforms regardless of their different norms.
- Under-investing in the opening hook, especially on platforms where feed algorithms and scroll behavior heavily reward immediate engagement.
- Simply resizing one platform's content for another instead of genuinely adapting tone and structure.

## 18. Prompt Variations

- **Basic Version**: Core message + platform only, no tone/hashtag/format specification.
- **Advanced Version**: Full structure with format, tone, hashtags, and CTA (Section 10).
- **Expert Version**: Adds a request for the same core message adapted across 3-4 platforms simultaneously, with a brief note on what changed and why for each platform's specific conventions — useful for planning a coordinated multi-platform launch.

## 19. Related Prompts

- `28_Marketing_Prompts.md` — social content often sits within a broader campaign strategy
- `26_Content_Writing_Prompts.md` — longer-form platform content (LinkedIn articles, Threads) shares long-form writing principles
- `31_Image_Generation_Prompts.md` — many social formats are inherently visual-first, with copy supporting an image or video

## 20. Tips

- Platform conventions change relatively often (algorithm changes, feature updates, shifting cultural norms); for anything where current best practice matters significantly, a quick check against current platform guidance or recent successful examples is worth doing alongside using this template.
- When repurposing one message across platforms, writing the LinkedIn version first (typically the most structured/complete) and then adapting down to shorter, punchier formats tends to work better than expanding a short version up.

## 21. Limitations

- Platform algorithms and best practices evolve frequently; the model's sense of "what performs well" reflects general principles and training-time knowledge, not real-time platform algorithm behavior.
- Actual engagement depends on many factors beyond copy quality (posting time, account size, algorithm favor, visual content quality) that this template doesn't address.
- Visual-first platforms (Instagram, TikTok) require the accompanying image/video to genuinely carry much of the engagement — caption quality alone has limited impact without strong visual content.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ (particularly attuned to X/Twitter conventions) |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#social-media` `#content-creation` `#marketing` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
