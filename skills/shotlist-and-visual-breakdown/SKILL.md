---
name: shotlist-and-visual-breakdown
description: "Convert scripts, scene outlines, or treatments into shot lists, camera setups, production beats, continuity notes, asset requirements, and prompt-ready visual breakdowns."
---

# shotlist-and-visual-breakdown

## When to use
- The user asks for a shot list, scene breakdown, storyboard plan, camera plan, production beat map, or asset list.
- The user provides script pages or a scene outline and wants image/video prompt inputs.
- The user needs continuity notes for characters, locations, props, wardrobe, blocking, or screen direction.

## When not to use
- The user is still exploring the story premise and has no scene yet.
- The user only wants model-specific syntax conversion.
- The user wants a full production budget or call sheet.

## Required inputs
- Scene text or outline
- Runtime/clip duration target
- Visual style or genre
- Continuity bible if available

## Optional inputs
- Target model limits
- Aspect ratio
- Location/asset constraints
- Need for image prompts, video prompts, or both

## Workflow
1. Break the scene into story beats and visual beats.
2. For each beat, assign shot purpose: geography, emotion, reveal, action, detail, transition, or continuity insert.
3. Select shot scale, angle, lens feel, camera movement, lighting state, blocking, and production design anchors.
4. Respect duration math: one clear action per short shot unless the target model supports multi-shot or extension workflows.
5. Create continuity notes: eye lines, screen direction, wardrobe, prop state, weather, time of day, and emotional state.
6. Create an asset list for characters, locations, props, costumes, reference images, sound cues, and keyframes.
7. Prepare handoff rows for image and video prompting.

## Decision logic
- If identity consistency matters, request or generate reference sheet prompts before video prompts.
- If the scene has complex motion, split into simpler shots rather than one overloaded prompt.
- If the target model supports first/last frames, mark shots that need keyframes.
- If dialogue is present, check line length against clip duration.

## Output formats
- Shot list table
- Camera setup list
- Scene breakdown
- Asset list
- Continuity notes
- Image/video prompt handoff

## Quality checks
- Every shot has a purpose and a single dominant subject/action.
- Camera movement is motivated by story or emotion.
- Shot order preserves geography and screen direction.
- Asset needs are explicit enough to generate references.
- Prompts can be created without re-reading the full script.

## Anti-patterns
- Shot lists that merely restate the script
- Multiple camera moves in one short AI-video prompt
- Ignoring prop or wardrobe state changes
- Using style words without visual execution details
- Cutting away before a story beat has visual consequence

## Exit criteria
- The scene is decomposed into shot rows and asset requirements ready for image/video prompting or production packaging.

## Supporting files
Read only the supporting file needed for the active task:
- `references/shotlist_schema.md`
- `references/camera_plan.md`
- `references/production_breakdown.md`
- `templates/shot_list.md`
- `templates/scene_breakdown.md`
- `templates/asset_list.md`
