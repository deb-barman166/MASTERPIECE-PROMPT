# Web Development Prompts

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-24

---

## 01. Overview

Web Development prompting is a domain-specific technique for generating front-end and full-stack web code — components, pages, styling, and client-server interactions. Effective web dev prompts need to specify the framework (React, Vue, Svelte, vanilla JS, etc.), styling approach (CSS, Tailwind, styled-components, etc.), responsiveness/accessibility requirements, and browser support constraints — dimensions that generic code prompting doesn't fully capture, and that significantly affect what "correct" output looks like for a UI.

## 02. Purpose

- Produce framework-correct, idiomatic front-end code matching the project's actual stack.
- Ensure generated UI is responsive and accessible by default, not as an afterthought.
- Reduce mismatches between generated styling approach and the project's actual CSS methodology.
- Handle both new component creation and modification of existing UI code.

## 03. Use Cases

- Building a new UI component (form, modal, navigation, card, table)
- Implementing a responsive page layout
- Adding client-side interactivity (state, event handling, API calls)
- Converting a design mockup or description into working markup/styling
- Improving accessibility or fixing responsive layout issues in existing code

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models — strong front-end code generation)
- Gemini
- Grok
- Perplexity (less common for this use case)

## 05. Prompt Category

`Domain-Specific` · `Software Development` · `Front-End`

## 06. Difficulty Level

**Intermediate**

## 07. Required Inputs

- **Component/page description**: What UI needs to be built
- **Framework**: React, Vue, Svelte, Angular, vanilla HTML/CSS/JS, etc.

## 08. Optional Inputs

- Styling approach (Tailwind, CSS Modules, styled-components, plain CSS)
- State management approach (useState, Redux, Pinia, etc.)
- Responsiveness requirements (breakpoints, mobile-first vs. desktop-first)
- Accessibility requirements (WCAG level, screen reader support, keyboard navigation)
- Browser support constraints
- Existing design system/component library to match

## 09. Variables

| Variable | Required? |
|---|---|
| `{{component_description}}` | Yes |
| `{{framework}}` | Yes |
| `{{styling_approach}}` | No |
| `{{state_management}}` | No |
| `{{responsiveness_requirements}}` | No |
| `{{accessibility_requirements}}` | No |
| `{{browser_support}}` | No |
| `{{design_system_context}}` | No |

## 10. Prompt Template

```text
Build the following UI component/page.

DESCRIPTION:
{{component_description}}

FRAMEWORK:
{{framework}}

STYLING APPROACH:
{{styling_approach}}

STATE MANAGEMENT:
{{state_management}}

RESPONSIVENESS REQUIREMENTS:
{{responsiveness_requirements}}

ACCESSIBILITY REQUIREMENTS:
{{accessibility_requirements}}

BROWSER SUPPORT:
{{browser_support}}

EXISTING DESIGN SYSTEM CONTEXT (if matching an existing look/pattern):
{{design_system_context}}

INSTRUCTIONS:
- Use idiomatic patterns for the specified framework and version.
- Follow the specified styling approach consistently; do not mix
  methodologies (e.g., don't add inline styles if Tailwind is specified).
- Include appropriate semantic HTML elements and ARIA attributes for
  accessibility, even if not explicitly requested, unless this conflicts
  with a stated requirement.
- Ensure the component is responsive by default unless told otherwise.
- If any part of the visual design is ambiguous, state your assumption
  briefly before the code.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{component_description}}` | What the component should do/look like | "A dismissible notification banner with an icon, message, and close button" |
| `{{framework}}` | The target framework/version | "React 18 with hooks" |
| `{{styling_approach}}` | CSS methodology to use | "Tailwind CSS utility classes only" |
| `{{state_management}}` | How component state is handled | "Local useState only, no external state library" |
| `{{responsiveness_requirements}}` | Breakpoints/mobile behavior | "Mobile-first, must work well down to 320px width" |
| `{{accessibility_requirements}}` | A11y standards to meet | "WCAG 2.1 AA, full keyboard navigation support" |
| `{{browser_support}}` | Compatibility constraints | "Must support Safari 15+, no bleeding-edge CSS features" |
| `{{design_system_context}}` | Existing patterns to match | "Match the rounded-lg, shadow-md card style used elsewhere in the app" |

## 12. Example Input

```text
DESCRIPTION:
A dismissible notification banner with a success/error/warning variant,
an icon, a message, and a close button.

FRAMEWORK: React 18 with hooks
STYLING APPROACH: Tailwind CSS
STATE MANAGEMENT: Local useState for visibility
ACCESSIBILITY REQUIREMENTS: Must announce to screen readers when shown;
close button must be keyboard-accessible
```

## 13. Example Output

```jsx
import { useState } from "react";
import { CheckCircle, AlertTriangle, XCircle, X } from "lucide-react";

const VARIANT_STYLES = {
  success: "bg-green-50 text-green-800 border-green-200",
  warning: "bg-yellow-50 text-yellow-800 border-yellow-200",
  error: "bg-red-50 text-red-800 border-red-200",
};

const VARIANT_ICONS = {
  success: CheckCircle,
  warning: AlertTriangle,
  error: XCircle,
};

export default function NotificationBanner({ variant = "success", message }) {
  const [visible, setVisible] = useState(true);

  if (!visible) return null;

  const Icon = VARIANT_ICONS[variant];

  return (
    <div
      role="alert"
      aria-live="polite"
      className={`flex items-center justify-between gap-3 rounded-lg border px-4 py-3 ${VARIANT_STYLES[variant]}`}
    >
      <div className="flex items-center gap-2">
        <Icon className="h-5 w-5 flex-shrink-0" aria-hidden="true" />
        <p className="text-sm font-medium">{message}</p>
      </div>
      <button
        onClick={() => setVisible(false)}
        aria-label="Dismiss notification"
        className="rounded p-1 hover:bg-black/5 focus:outline-none focus:ring-2 focus:ring-offset-1"
      >
        <X className="h-4 w-4" />
      </button>
    </div>
  );
}
```

```text
NOTES:
- role="alert" and aria-live="polite" ensure screen readers announce the
  banner when it appears without needing a page reload.
- The close button uses aria-label since its icon has no visible text label.
- focus:ring-2 ensures the close button has a visible focus state for
  keyboard navigation, satisfying the accessibility requirement.
```

## 14. Customization Guide

- **Always specify the framework and version**: React class components vs. hooks, Vue 2 Options API vs. Vue 3 Composition API, and similar version splits produce meaningfully different idiomatic code.
- **Commit to one styling approach**: Mixing Tailwind with inline styles or CSS Modules in the same component creates maintenance inconsistency — state the approach and expect it followed exclusively.
- **State accessibility requirements even when basic**: Models will include reasonable defaults, but explicit requirements (keyboard nav, screen reader announcements, contrast) ensure these aren't treated as optional polish.
- **Provide existing design system context for consistency**: A short description or code snippet of existing similar components prevents visual/structural drift from the rest of the application.

## 15. Output Format Options

- Component code block (framework-tagged, e.g., ` ```jsx `)
- Component + separate stylesheet
- Component + Storybook story
- HTML + CSS + JS (vanilla stack)
- Full page markup

## 16. Best Practices

- Specify framework, version, and styling approach explicitly — these three details drive most of the structural decisions in the output.
- Ask for accessibility considerations by default rather than as an afterthought request.
- Provide existing design system context whenever the component needs to visually match an established application.
- Request that visual ambiguities be flagged as assumptions rather than silently resolved.

## 17. Common Mistakes

- Not specifying the framework version, resulting in outdated patterns (e.g., class components when hooks were expected).
- Leaving styling approach unspecified, leading to inconsistent or mixed styling methodologies.
- Treating accessibility as optional, resulting in components that work visually but fail for keyboard or screen-reader users.
- Omitting responsiveness requirements and receiving a desktop-only layout that breaks on mobile.

## 18. Prompt Variations

- **Basic Version**: Component description + framework only, no styling/accessibility specification.
- **Advanced Version**: Full structure with styling, state management, responsiveness, and accessibility (Section 10).
- **Expert Version**: Adds a request for the model to also provide a brief testing checklist (keyboard nav paths to verify, screen reader behavior to check, breakpoints to test) alongside the code, useful for QA handoff.

## 19. Related Prompts

- `21_Code_Generation_Prompts.md` — the general code-generation principles this template specializes for front-end work
- `22_Debugging_Prompts.md` — for fixing issues in existing UI code
- `31_Image_Generation_Prompts.md` — useful when a visual mockup needs to be generated before implementation begins

## 20. Tips

- Pasting a short snippet of an existing, similar component from the same codebase is often more effective at conveying "house style" than describing conventions in prose.
- For accessibility-critical components (forms, modals, navigation), explicitly asking the model to note which WCAG success criteria the implementation addresses makes the accessibility work auditable, not just assumed.

## 21. Limitations

- Generated components should be visually reviewed in-browser before shipping — code that's structurally correct can still have visual issues a model can't fully anticipate without seeing rendered output.
- Model knowledge of very recent framework versions, APIs, or browser features may lag behind the actual current state of fast-moving front-end ecosystems.
- Complex, highly stateful interactions spanning multiple components are often better handled via Prompt Chaining (Template 14) — building and reviewing one piece at a time — than requested all at once.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ⚠️ Limited (less common use case) |
| Llama (open-source) | ✅ (code-specialized variants recommended) |
| Mistral | ✅ (code-specialized variants recommended) |

## 23. Tags

`#web-development` `#frontend` `#react` `#accessibility` `#intermediate` `#domain-specific`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
