# Video Generation Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-32

---

## 01. Overview

Video Generation prompting is a domain-specific technique for producing text-to-video prompts for AI video models (Runway, Pika, Sora, Google Veo, Luma Dream Machine, and similar tools). It extends image generation prompting (Template 31) into the added dimension of time and motion: camera movement, subject motion/action, shot duration, and scene transitions. Because generated video is more prone to physical inconsistency and motion artifacts than static images, precision about movement — what moves, how, and at what pace — matters more here than in image prompting.

## 02. Purpose

- Produce prompts that reliably guide video generation toward intended motion and camera behavior, not just a static scene.
- Specify camera movement (pan, dolly, static, handheld) explicitly, since this is often under-specified by default.
- Control shot pacing and duration expectations appropriate to the tool's actual generation length limits.
- Support scene-to-scene consistency when generating multiple linked clips.

## 03. Use Cases

- Short marketing/social video clips
- Concept visualization for film/animation pre-production
- B-roll and background footage generation
- Product demonstration visuals
- Motion graphics and abstract visual content
- Storyboard-to-video concept exploration

## 04. Target AI Models

Video-generation-specific models/tools:

- Runway (Gen-3 and later)
- Pika Labs
- OpenAI Sora
- Google Veo
- Luma Dream Machine

## 05. Prompt Category

`Domain-Specific` · `Visual Generation` · `Text-to-Video`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Scene description**: What's happening in the shot
- **Camera movement**: Static, pan, dolly, tracking, handheld, aerial, etc.

## 08. Optional Inputs

- Subject motion/action detail
- Shot duration (within tool limits)
- Style/medium (photorealistic, animated, cinematic)
- Lighting and color grading
- Pacing (slow motion, real-time, time-lapse)
- Transition style (for multi-clip sequences)

## 09. Variables

| Variable | Required? |
|---|---|
| `{{scene_description}}` | Yes |
| `{{camera_movement}}` | Yes |
| `{{subject_motion}}` | No |
| `{{shot_duration}}` | No |
| `{{style_medium}}` | No |
| `{{lighting_grading}}` | No |
| `{{pacing}}` | No |

## 10. Prompt Template

```text
{{scene_description}}, {{subject_motion}}, {{camera_movement}}, {{style_medium}}, {{lighting_grading}}, {{pacing}}

Duration: {{shot_duration}}
```

*Note: Exact syntax and supported parameters vary by tool. Runway, Pika, and
Veo generally accept natural-language camera movement descriptions embedded
directly in the prompt text (e.g., "slow dolly forward") rather than
separate flags. Always check the specific tool's current prompt guide for
supported duration limits and parameter syntax.*

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{scene_description}}` | What's happening in the shot | "A barista steaming milk behind a coffee shop counter" |
| `{{camera_movement}}` | How the camera moves through the shot | "slow dolly-in, eye-level" |
| `{{subject_motion}}` | What the subject is doing | "steam rising steadily, hands moving in a practiced, calm rhythm" |
| `{{shot_duration}}` | Length of the generated clip | "4 seconds" |
| `{{style_medium}}` | Visual style | "cinematic, photorealistic" |
| `{{lighting_grading}}` | Light and color treatment | "warm color grade, soft window light" |
| `{{pacing}}` | Speed of motion | "real-time, no slow motion" |

## 12. Example Input

```text
SCENE: A barista steaming milk behind a coffee shop counter
SUBJECT MOTION: Steam rising steadily, calm practiced hand movements
CAMERA MOVEMENT: Slow dolly-in, eye-level angle
STYLE/MEDIUM: Cinematic, photorealistic
LIGHTING: Warm color grade, soft natural window light
PACING: Real-time
SHOT DURATION: 4 seconds
```

## 13. Example Output

```text
A barista steaming milk behind a coffee shop counter, steam rising
steadily as hands move in a calm, practiced rhythm, slow dolly-in camera
movement at eye-level angle, cinematic photorealistic style, warm color
grade with soft natural window light, real-time pacing

Duration: 4 seconds
```

## 14. Customization Guide

- **Always specify camera movement explicitly**: Video models default to varying behaviors when camera motion isn't stated — naming it directly (static, pan, dolly, handheld) gives much more predictable results than leaving it implicit.
- **Separate subject motion from camera motion clearly**: These are often conflated in a single vague description; being explicit about what the subject does versus how the camera moves through the scene produces more coherent results.
- **Respect the tool's actual duration limits**: Most current video generation tools support only short clips (a few seconds); requesting durations beyond the tool's actual capability will either be ignored or produce unexpected results.
- **State pacing explicitly if it matters**: "Real-time," "slow motion," or "time-lapse" changes the entire feel of a generated clip and isn't always inferred correctly from scene description alone.

## 15. Output Format Options

- Plain text prompt string (tool-native format)
- Structured prompt (scene / motion / camera / technical parameters listed separately for documentation)
- Shot list (for multi-clip sequences, each shot documented separately)

## 16. Best Practices

- Explicitly separate and specify both camera movement and subject motion — this is the biggest lever for coherent, intentional-feeling video output.
- Keep shot durations realistic to the specific tool's current generation limits rather than requesting long continuous shots.
- Use consistent style/lighting/grading language across a multi-clip sequence to maintain visual continuity between shots.
- Favor simpler, single-action scenes over complex multi-event scenes, since current video generation tools handle focused motion more reliably than intricate simultaneous action.

## 17. Common Mistakes

- Leaving camera movement unspecified, resulting in unpredictable or default camera behavior.
- Requesting shot durations beyond what the tool actually supports.
- Overloading a single prompt with too many simultaneous actions or events, which current video models often struggle to render coherently.
- Inconsistent style/lighting descriptions across a multi-clip sequence, breaking visual continuity between shots.

## 18. Prompt Variations

- **Basic Version**: Scene description only, no explicit camera movement or technical detail.
- **Advanced Version**: Full structure with camera movement, subject motion, style, and pacing (Section 10).
- **Expert Version**: For multi-shot sequences, adds a shot-by-shot list with consistent style/lighting anchors repeated across each shot's prompt, plus explicit transition descriptions between shots (cut, dissolve, match cut) for sequence planning.

## 19. Related Prompts

- `31_Image_Generation_Prompts.md` — the static-image foundation this template extends into motion
- `06_Skeleton_of_Thought.md` — useful for planning a multi-shot sequence's structure before generating each individual clip
- `30_Social_Media_Prompts.md` — generated video clips often support short-form social content

## 20. Tips

- Simpler scenes with one clear focal action tend to generate more coherently than complex scenes with many simultaneous events — when a complex scene is needed, breaking it into multiple simpler shots (and combining them in post) often works better than attempting it in one generation.
- Because video generation tools update their capabilities relatively quickly, checking the specific tool's current prompt guide for exact duration limits and supported camera-movement vocabulary before writing prompts is worth doing periodically.

## 21. Limitations

- Current text-to-video tools generally support only short clip durations (typically a few seconds), which significantly constrains what can be requested in a single generation.
- Physical consistency (object permanence, correct anatomy through motion, consistent lighting across a shot) remains an active challenge for most video generation models, more so than for static image generation.
- Generating video of real, identifiable people, copyrighted characters, or trademarked content raises legal and ethical considerations that vary by tool's usage policy and jurisdiction — these should be reviewed independently of prompt construction.
- Exact prompt syntax and parameter support vary significantly between tools and change frequently as the technology develops quickly.

## 22. Model Compatibility

| Model/Tool | Supported |
|--------|-----------|
| Runway | ✅ |
| Pika Labs | ✅ |
| OpenAI Sora | ✅ |
| Google Veo | ✅ |
| Luma Dream Machine | ✅ |

## 23. Tags

`#video-generation` `#text-to-video` `#runway` `#sora` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
