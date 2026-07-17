# Image Generation Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-31

---

## 01. Overview

Image Generation prompting is a domain-specific technique for producing text-to-image prompts for AI image models (Midjourney, DALL-E, Stable Diffusion, Adobe Firefly, and similar tools). Unlike text-generation prompting, image prompts work best as dense, descriptive strings covering subject, composition, lighting, style/medium, color palette, and camera/lens characteristics — plus, for some tools, technical parameters (aspect ratio, style weight, negative prompts) that constrain generation directly.

## 02. Purpose

- Produce precise, richly descriptive prompts that reliably guide image generation toward the intended result.
- Specify visual parameters (composition, lighting, style) that are often left implicit and under-specified.
- Support iterative refinement through negative prompts and parameter adjustment.
- Adapt prompt syntax to the conventions of the specific image generation tool being used.

## 03. Use Cases

- Concept art and illustration generation
- Marketing/social media visual asset creation
- Product mockups and visualization
- Mood boards and style exploration
- Icon and graphic asset generation
- Photorealistic scene generation

## 04. Target AI Models

Image-generation-specific models/tools:

- Midjourney (v6 and later)
- DALL-E 3 (via ChatGPT or API)
- Stable Diffusion (various versions/fine-tunes)
- Adobe Firefly
- Google Imagen / Gemini image generation

## 05. Prompt Category

`Domain-Specific` · `Visual Generation` · `Text-to-Image`

## 06. Difficulty Level

**Beginner to Intermediate**

## 07. Required Inputs

- **Subject**: The main focus of the image
- **Style/medium**: Photography, illustration, 3D render, watercolor, etc.

## 08. Optional Inputs

- Composition/framing (close-up, wide shot, rule of thirds)
- Lighting description
- Color palette
- Camera/lens characteristics (for photorealistic styles)
- Mood/atmosphere
- Aspect ratio
- Negative prompt (what to avoid)
- Reference artist/style influence

## 09. Variables

| Variable | Required? |
|---|---|
| `{{subject}}` | Yes |
| `{{style_medium}}` | Yes |
| `{{composition}}` | No |
| `{{lighting}}` | No |
| `{{color_palette}}` | No |
| `{{camera_lens}}` | No |
| `{{mood_atmosphere}}` | No |
| `{{aspect_ratio}}` | No |
| `{{negative_prompt}}` | No |

## 10. Prompt Template

```text
{{subject}}, {{composition}}, {{style_medium}}, {{lighting}}, {{color_palette}}, {{camera_lens}}, {{mood_atmosphere}}

--ar {{aspect_ratio}} --no {{negative_prompt}}
```

*Note: The `--ar` and `--no` parameter syntax shown follows Midjourney
conventions. Adjust parameter syntax for other tools: DALL-E and Firefly
typically take these as natural-language descriptions within the prompt
itself rather than flag-based parameters; Stable Diffusion interfaces often
have separate positive/negative prompt fields.*

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{subject}}` | The main focus of the image | "a red fox sitting in a snow-covered forest" |
| `{{composition}}` | Framing and shot type | "close-up portrait shot, shallow depth of field" |
| `{{style_medium}}` | Artistic medium/style | "photorealistic photography" or "watercolor illustration" |
| `{{lighting}}` | Light source and quality | "soft golden hour backlighting" |
| `{{color_palette}}` | Dominant colors/tones | "warm oranges and cool blue shadows" |
| `{{camera_lens}}` | Camera/lens simulation | "85mm lens, f/1.8 aperture" |
| `{{mood_atmosphere}}` | Overall feeling | "serene, quiet, contemplative" |
| `{{aspect_ratio}}` | Image dimensions | "16:9" or "1:1" |
| `{{negative_prompt}}` | What to exclude | "blurry, distorted, extra limbs, text, watermark" |

## 12. Example Input

```text
SUBJECT: A cozy coffee shop interior with warm wooden furniture
STYLE/MEDIUM: Photorealistic photography
COMPOSITION: Wide shot, eye-level angle
LIGHTING: Soft morning light streaming through large windows
COLOR PALETTE: Warm browns, amber tones, soft cream
CAMERA/LENS: 35mm lens, natural depth of field
MOOD: Inviting, calm, quiet morning atmosphere
ASPECT RATIO: 16:9
NEGATIVE PROMPT: people, blurry, oversaturated, cluttered
```

## 13. Example Output

```text
A cozy coffee shop interior with warm wooden furniture, wide shot at
eye-level angle, photorealistic photography, soft morning light streaming
through large windows, warm browns and amber tones with soft cream
accents, shot on 35mm lens with natural depth of field, inviting calm
quiet morning atmosphere

--ar 16:9 --no people, blurry, oversaturated, cluttered
```

## 14. Customization Guide

- **Order matters for emphasis**: Most image models weight earlier terms in the prompt more heavily — lead with the subject and most important compositional details, and place secondary descriptors later.
- **Adapt syntax to the specific tool**: Midjourney uses `--` flag parameters; DALL-E and Firefly generally work best with fully natural-language descriptions without flag syntax; Stable Diffusion tools often separate positive and negative prompts into distinct fields rather than combining them in one string.
- **Use negative prompts to correct recurring issues**: If a tool consistently over-generates a specific unwanted element (extra fingers, watermark-like text, a particular unwanted style), explicitly excluding it in the negative prompt is often more effective than only describing the wanted result.
- **Reference photography/art terminology for precision**: Terms like "shallow depth of field," "rule of thirds," "golden hour," or specific lens focal lengths give the model concrete visual parameters that vague language ("nice lighting") doesn't convey.

## 15. Output Format Options

- Plain text prompt string (tool-native format)
- Structured prompt (subject / style / technical parameters listed separately for documentation)
- Prompt + negative prompt pair

## 16. Best Practices

- Lead with the subject and most important details; secondary descriptors can come later in the prompt.
- Use specific photography/art terminology (lens type, lighting quality, composition rules) rather than vague adjectives for precision.
- Include a negative prompt when using tools that support it, especially to address recurring unwanted elements.
- Match aspect ratio to the actual intended use case (social post, print, banner) rather than defaulting to square.

## 17. Common Mistakes

- Vague, adjective-heavy prompts ("beautiful, amazing image of...") that give the model little concrete visual direction.
- Not adapting parameter syntax to the specific tool being used, resulting in flags being read as literal prompt text.
- Overloading a single prompt with too many conflicting style references, producing a muddled result.
- Ignoring aspect ratio, resulting in generated images that don't fit the intended placement (e.g., square images cropped awkwardly for a banner).

## 18. Prompt Variations

- **Basic Version**: Subject + style only, no compositional/technical detail.
- **Advanced Version**: Full structure with composition, lighting, color, and technical parameters (Section 10).
- **Expert Version**: Adds explicit reference to a specific artistic movement, named technique, or lighting setup (e.g., "Rembrandt lighting," "Dutch angle," "impasto brushwork") for more precise stylistic control, plus a note on which parameters to adjust first when iterating on a result that's close but not quite right.

## 19. Related Prompts

- `32_Video_Generation_Prompts.md` — shares many compositional/style principles, extended into motion and time
- `24_Web_Development_Prompts.md` — generated images are often used as visual assets within web UI work
- `30_Social_Media_Prompts.md` — image generation frequently supports social content creation

## 20. Tips

- When a generated result is close but not quite right, changing one variable at a time (just the lighting, or just the composition) rather than rewriting the whole prompt makes it much easier to identify which change produced which effect.
- Studying a few real photographs or artworks in the target style and noting their specific technical qualities (lens choice, lighting setup, color grading) often produces more precise prompt language than general aesthetic adjectives.

## 21. Limitations

- Prompt syntax and supported parameters vary significantly between tools and change as tools update; always verify current parameter conventions for the specific tool and version being used.
- Image models can struggle with precise text rendering, specific counts of objects, and exact spatial relationships even with careful prompting.
- Generating images of real, identifiable people, copyrighted characters, or trademarked content raises legal and ethical considerations that vary by tool's usage policy and jurisdiction — these should be reviewed independently of prompt construction.

## 22. Model Compatibility

| Model/Tool | Supported |
|--------|-----------|
| Midjourney | ✅ |
| DALL-E 3 | ✅ |
| Stable Diffusion | ✅ |
| Adobe Firefly | ✅ |
| Google Imagen | ✅ |

## 23. Tags

`#image-generation` `#text-to-image` `#midjourney` `#dalle` `#beginner-friendly` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
