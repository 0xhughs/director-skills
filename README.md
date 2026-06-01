# director-skills

`director-skills` is an agent-skills-compatible creative production system for AI-assisted story writing, AI filmmaking, cinematic prompting, and model-specific prompt export.

It helps an AI assistant move a project through this pipeline:

`idea -> story -> screenplay -> shot list -> visual bible -> image prompts -> video prompts -> model-specific exports -> iteration`

## What agent-skills-compatible means here

Each skill lives in `skills/<skill-name>/SKILL.md` with YAML frontmatter containing `name` and `description`. The `SKILL.md` file gives routing guidance, workflows, decision logic, outputs, quality checks, anti-patterns, exit criteria, and pointers to local references, templates, checklists, examples, and tests.

The suite is designed for agents such as ChatGPT, Claude, Gemini, Grok, Cursor agents, Codex/local agents, or other assistants that can read a skill folder and follow procedural instructions.

## Skill map

| Task | Use this skill |
|---|---|
| Raw idea to short-story plan, logline, premise, treatment, scene list | `short-film-development` |
| Fountain scenes, screenplay writing, dialogue, beats, emotional turns | `screenplay-and-scene-writing` |
| Script/scene to shot list, camera plan, asset list | `shotlist-and-visual-breakdown` |
| Character, location, prop, keyframe, poster, still prompts | `cinematic-image-prompting` |
| Text-to-video, image-to-video, time-blocked prompts | `cinematic-video-prompting` |
| Character/location/prop/costume/style continuity | `character-location-prop-bible` |
| Diagnose failed outputs and revise prompts | `prompt-iteration-and-diagnostics` |
| Genre, tone, camera, lens, lighting, realism, style | `style-cinematography-director` |
| Translate prompts/settings for specific models/tools | `model-adaptation` |

## Example user requests

- "Turn this premise into a 5-minute short-film treatment."
- "Turn this raw idea into a short-story plan with a revision audit."
- "Write this scene in Fountain format."
- "Write a tense screenplay scene from this beat sheet."
- "Break this scene into a shot list for AI video generation."
- "Create a character reference sheet prompt for the protagonist."
- "Make this still prompt cinematic and photoreal."
- "Animate this image as an 8-second I2V prompt."
- "Convert this prompt for Kling, Seedance, Veo, and Grok."
- "The output changed the character's face. Diagnose and revise."

## Expected workflow

1. Start with `short-film-development` to define story, theme, point of view if prose, character pressure, scene list, and visual anchors.
2. Use `screenplay-and-scene-writing` to write or revise key scenes, including Fountain output when needed.
3. Use `character-location-prop-bible` to lock recurring assets and continuity rules.
4. Use `style-cinematography-director` to define camera, lens, light, palette, texture, and genre rules.
5. Use `shotlist-and-visual-breakdown` to convert scenes into shots and asset requirements.
6. Use `cinematic-image-prompting` for reference sheets, keyframes, locations, props, posters, and stills.
7. Use `cinematic-video-prompting` for T2V/I2V/extension prompts with timing, motion, audio, and constraints.
8. Use `model-adaptation` whenever a named model or multi-model export is involved.
9. Use `prompt-iteration-and-diagnostics` after outputs fail or drift.
10. For release-minded projects, use `prompt-iteration-and-diagnostics` for story, voice, continuity, rights, provenance, subtitle, and post-production QC.

## Model adaptation layer

`model-adaptation` separates universal creative/cinematic intent from model-specific syntax and controls. It tracks prompt format, negative prompt support, reference image support, duration, aspect ratio, resolution, seeds, text/logo behavior, motion control, audio, and common failure modes.

If a capability is not clearly supported by the reviewed guides, the suite marks it `unknown` instead of guessing.

## Adding new guides later

1. Add the guide outside `director-skills`.
2. Read it for repeatable workflows, not just facts.
3. Update `SOURCE_MAP.md` with source influence and cautions.
4. Update the relevant skill references/templates/tests.
5. If the guide changes model capabilities, update `skills/model-adaptation/references/*` and add a test.

## Updating model profiles

Use `skills/model-adaptation/references/model_update_protocol.md`. Prefer current official documentation for live specs, mark source confidence, and keep unknowns explicit.
