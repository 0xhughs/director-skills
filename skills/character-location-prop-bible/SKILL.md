---
name: character-location-prop-bible
description: "Create and maintain continuity bibles for characters, locations, props, costumes, color palettes, style rules, reference assets, and cross-shot visual anchors."
---

# character-location-prop-bible

## When to use
- The user needs consistency across images, shots, scenes, or models.
- The user asks for a character bible, location bible, prop list, wardrobe continuity, style bible, or continuity checklist.
- The project is moving from idea/script into repeatable image/video generation.

## When not to use
- The user only wants one disposable prompt with no continuity need.
- The task is pure model parameter research.
- The user asks for story structure without visual asset continuity.

## Required inputs
- Project title or scene
- Existing descriptions or outputs
- Characters/locations/props/costumes to track
- Target visual style

## Optional inputs
- Reference images
- Shot list
- Model-specific requirements
- Palette or genre anchors
- Version history

## Workflow
1. Create stable IDs for characters, locations, props, costumes, and style rules.
2. Record immutable anchors: identity, silhouette, proportions, palette, materials, prop condition, location geography, and lighting baseline.
3. Separate mutable state: emotion, wardrobe changes, damage, weather, time of day, prop position, and story-state changes.
4. Create golden-image reference prompt entries for clean sheets before dramatic variants.
5. After each generated output or script change, update only the changed fields and preserve a changelog note.
6. Prepare a continuity packet for prompting: minimal anchors for each shot plus exclusions for drift-prone details.

## Decision logic
- If a detail must never change, place it in immutable anchors.
- If a detail changes by scene, place it in state timeline.
- If two sources conflict, prefer the latest user-approved bible entry and log the conflict.
- If model transfer causes drift, route to model-adaptation and use reference-image workflows where supported.

## Output formats
- Character profile
- Location profile
- Prop profile
- Costume profile
- Visual style bible
- Continuity checklist
- Reference asset index
- Golden image plan
- State timeline

## Quality checks
- Every recurring asset has an ID and stable anchor fields.
- Mutable state is tied to scene/shot numbers.
- Prompt anchors are concise enough to reuse.
- Style rules distinguish creative intent from execution details.
- Conflicts are logged instead of silently resolved.

## Anti-patterns
- Changing character descriptions between prompts
- Mixing immutable identity with temporary emotion
- Overlong bible entries that agents cannot practically reuse
- Ignoring prop state after action beats
- Relying on text-only consistency when references are available.

## Exit criteria
- A concise continuity packet exists for downstream screenplay, shot list, image prompts, video prompts, and model exports.

## Supporting files
Read only the supporting file needed for the active task:
- `references/continuity_system.md`
- `references/visual_bible_system.md`
- `references/identity_anchors.md`
- `references/golden_image_workflow.md`
- `templates/character_profile.md`
- `templates/location_profile.md`
- `templates/continuity_checklist.md`
