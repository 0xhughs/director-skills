---
name: style-cinematography-director
description: "Translate genre, tone, cinematic references, lens language, lighting, framing, blocking, texture, realism, and audience experience into reusable creative direction for scripts, shot lists, and prompts."
---

# style-cinematography-director

## When to use
- The user asks for cinematic style, genre look, camera language, lensing, lighting, blocking, realism, texture, visual tone, or art-direction guidance.
- The user has a story but needs a visual language before shot lists or prompts.
- The user wants style consistency across scenes or model outputs.

## When not to use
- The user only wants model-specific parameter conversion.
- The user needs screenplay dialogue rather than visual direction.
- The user asks for a single still prompt and already has full visual specs.

## Required inputs
- Story/scene/concept
- Genre/tone/audience experience
- Desired realism level
- References if any

## Optional inputs
- Runtime
- Target platform/aspect ratio
- Color palette
- Continuity bible
- Model/tool constraints

## Workflow
1. Translate abstract tone into visible choices: contrast, palette, lens distance, camera stability, light source, texture, blocking, and production design.
2. Select a genre grammar but avoid copying a specific protected work.
3. Define lens and framing rules that express emotional distance and power dynamics.
4. Define lighting rules with direction, quality, source, color temperature, and shadow behavior.
5. Define texture and realism rules: skin, fabric, weather, grain, imperfections, and artifact guardrails.
6. Create a compact style bible and shot-level style tags for downstream prompts.
7. Flag style choices that conflict with target model limits.

## Decision logic
- If the user gives only mood words, convert them into concrete camera/light/color decisions.
- If multiple references conflict, choose a dominant anchor and one accent.
- If photorealism matters, prioritize physical light, lens behavior, and micro-texture over quality adjectives.
- If the result is for video, include motion and blocking rules.

## Output formats
- Visual direction brief
- Genre/tone translation
- Cinematography rules
- Lighting palette
- Texture/realism rules
- Prompt-ready style block

## Quality checks
- Every style claim maps to a visible or audible execution detail.
- Camera, lighting, color, and production design reinforce the same emotional goal.
- References are used as inspiration, not reproduction.
- Style rules are concise enough for repeated prompting.
- Conflicts with model behavior are noted.

## Anti-patterns
- Generic cinematic adjectives without technical choices
- Overloading prompts with many film references
- One-note palettes that flatten emotional range
- Style rules that fight the story purpose
- Copying a living artist or exact protected image when a descriptive alternative works.

## Exit criteria
- A reusable style/cinematography brief is ready for story, shot list, bible, image prompt, video prompt, or model adaptation.

## Supporting files
Read only the supporting file needed for the active task:
- `references/cinematic_language.md`
- `references/camera_lens_movement.md`
- `references/lighting_and_photorealism.md`
- `references/genre_style_tone.md`
- `templates/visual_style_bible.md`
