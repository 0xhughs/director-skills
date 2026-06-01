---
name: cinematic-image-prompting
description: "Generate cinematic image prompts for characters, locations, props, costumes, keyframes, posters, concept art, reference sheets, and scene stills using creative intent plus camera, lighting, texture, and continuity anchors."
---

# cinematic-image-prompting

## When to use
- The user wants still image prompts, character sheets, location references, prop/costume concepts, keyframes, posters, thumbnails, concept art, or scene stills.
- The user needs image prompts before video generation to lock identity, composition, or style.
- The task requires photorealism, cinematic language, texture, camera/lens terms, or negative/positive constraints.

## When not to use
- The user asks for moving video prompts only.
- The user asks to adapt a finished prompt to a named model only.
- The user wants actual image generation rather than prompt writing, unless paired with image generation tools.

## Required inputs
- Subject or asset type
- Purpose of image
- Creative intent
- Continuity anchors
- Style/genre/tone

## Optional inputs
- Target model
- Aspect ratio
- Reference images
- Text/logo needs
- Photorealism level
- Negative constraints

## Workflow
1. Start with creative intent: who/what, why this image exists, emotional read, and audience impression.
2. Build cinematic execution: subject specificity, action/pose, environment, framing, lens feel, lighting direction/quality, color, texture, and realism level.
3. Add continuity anchors from the bible: face, wardrobe, prop state, location geography, palette, and design rules.
4. Select format: natural prose, priority stack, shot card, or model-specific export through model-adaptation.
5. Handle exclusions according to model behavior: true negative field where supported, positive restatement where not.
6. Create variants only by changing one meaningful variable at a time.
7. Add quality checklist and revision hooks.

## Decision logic
- If character consistency matters, create a clean reference sheet before dramatic scene stills.
- If the image contains text, route to model-adaptation and choose a model/profile that supports text better.
- If the style is too broad, ask for or infer one strong visual anchor plus specific execution details.
- If the target model is unknown, output a universal prompt brief and flag model-dependent fields.

## Output formats
- Universal image prompt brief
- Cinematic still prompt
- Character/location/prop reference prompt
- Negative or positive constraint block
- Prompt variants
- Model-adaptation handoff

## Quality checks
- Prompt has a clear subject, action/pose, environment, composition, lighting, style, texture, and output purpose.
- The first sentence front-loads the most important identity and scene elements.
- No contradictory style or lighting instructions.
- Continuity anchors are explicit and not overlong.
- Model-specific claims are not guessed.

## Anti-patterns
- Keyword soup for natural-language models
- Overloaded prompts with many competing references
- Negative prompts in models that lack negative support
- Vague words like epic or cinematic without camera/lighting specifics
- Using copyrighted or trademarked specifics when a generic visual description is safer.

## Exit criteria
- The prompt is ready for universal use or handoff to model-adaptation for a named image model.

## Supporting files
Read only the supporting file needed for the active task:
- `references/image_prompt_components.md`
- `references/lighting_and_photorealism.md`
- `references/prompt_anatomy.md`
- `references/negative_prompt_patterns.md`
- `templates/cinematic_still_prompt.md`
- `templates/character_reference_sheet_prompt.md`
