---
name: alejo-prototype
description: Build an Alejo UI prototype from reference URLs or images. Use when the user asks for Alejo Prototype, wants a quick HTML prototype, shares visual references, uploads UI screenshots/mockups/images, or needs a post-PRD/pre-SAD prototype that captures reference look-and-feel, UX/UI patterns, screenshots, and design evidence before architecture or implementation issues.
---

# Alejo Prototype

Create a disposable HTML prototype from reference websites or images. The main job is to study references, write detailed look-and-feel notes, ask what to build, ask which design system to use, then produce a single HTML prototype that uses those references.

## Inputs

When running inside the Alejo flow, also read relevant context if available:

- Latest Alejo Questions log in `docs/questions/`.
- Root `CONTEXT.md` and relevant ADRs in `docs/adr/`.
- Relevant PRD Linear Project content.

Do not block on missing Alejo docs. For quick visual prototypes, the required inputs are reference URLs or images, plus the user's build description.

## Workflow

### 1. Ask for references

If the user did not provide references, ask for 1-3 reference URLs, uploaded images, screenshots, or mockups unless they clearly want more.

For URLs, use the browser or a browser automation tool when available. Open each URL, wait for it to render, inspect the page, and take at least one desktop screenshot. Take mobile screenshots too when responsive behavior matters.

For uploaded images, inspect the image directly. If the user gives a local image path, open it with the available image viewer tool.

### 2. Write detailed design analysis

For each reference page or image, create a detailed temporary look-and-feel file:

```text
.scratch/prototypes/YYYY-MM-DD-<topic>/references/<reference-slug>-look-and-feel.md
```

Save screenshots beside the notes when possible:

```text
.scratch/prototypes/YYYY-MM-DD-<topic>/references/<site-slug>-desktop.png
.scratch/prototypes/YYYY-MM-DD-<topic>/references/<site-slug>-mobile.png
.scratch/prototypes/YYYY-MM-DD-<topic>/references/<image-slug>.png
```

For every reference type, write a detailed design analysis before using it as prototype input. Cover:

- Layout structure, density, spacing, rhythm, and viewport behavior.
- Typography scale, weight, casing, line length, and hierarchy.
- Color palette, contrast, backgrounds, borders, shadows, and surface treatments.
- Navigation, calls to action, forms, cards, tables, lists, and repeated UI patterns.
- Motion, hover states, affordances, empty/loading/error states if visible.
- Imagery, icons, illustration style, product/brand signals, and content tone.
- Composition, visual hierarchy, component anatomy, interaction implications, and UX intent.
- UX takeaways to reuse and things to avoid copying too literally.

Do not copy proprietary text, logos, images, or exact trade dress unless the user owns it or explicitly has rights. Use the references as design direction.

### 3. Ask what to build

After the look-and-feel notes are written, ask:

```text
Okay, what do you want to build?
```

Wait for the user's answer. If the answer is ambiguous, ask one short multiple-choice clarification with a recommended option.

### 4. Ask about design system

Before building, ask whether the prototype should use a design system. Use multiple choice and wait for the user's answer:

```text
Which design system should I use?
A. Reference-derived mini design system (Recommended: fastest way to preserve the reference look and feel)
B. Existing design system in this repo, if one exists (best when this prototype should match production UI)
C. Named external design system or CSS framework, such as Material, shadcn, Bootstrap, Tailwind, or a company system (useful when the user wants that exact vocabulary)
D. No design system; custom HTML/CSS only
E. Other / correction
```

If the user chooses an existing repo design system, inspect the repo enough to follow it. If they choose a named external system, use it as visual guidance unless the user explicitly asks to install dependencies.

### 5. Build the HTML prototype

Build a single disposable HTML file:

```text
.scratch/prototypes/YYYY-MM-DD-<topic>/prototype.html
```

Use inline CSS and JavaScript unless the user asks for a different shape. The prototype should be directly openable in a browser, reflect the user's requested product, and apply the reference look-and-feel notes without cloning protected assets.

Make the prototype feel complete enough to evaluate: include realistic layout, core states, representative content, responsive behavior, and the primary interaction path.

### 6. Verify and report

Open the HTML prototype in a browser, take a screenshot, and fix obvious layout or responsiveness issues.

Write a concise report:

```text
docs/prototypes/YYYY-MM-DD-<topic>-prototype.md
```

Report:

- Reference URLs and look-and-feel note files.
- Chosen design system or design-system decision.
- Prototype file and screenshots.
- What design decisions were borrowed from the references.
- What the prototype proves, what it does not prove, and any open UX/SAD/issues notes.

The next Alejo step is `alejo-sad`, which should read the prototype report when architecture or slicing depends on the prototype.
