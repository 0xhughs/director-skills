# Changelog

## 0.2.0 - Master skill router

- Added a root `SKILL.md` so `director-skills` can be imported as one master skill in chat-based or ZIP-based agent environments.
- Preserved all nine existing modular sub-skills under `skills/` for native multi-skill agent environments.
- Added root router tests covering story routing, Kling/video routing, failure diagnostics, ZIP upload behavior, and multi-stage handoffs.
- Updated README install guidance to explain master skill mode and modular native mode.
- Updated the manifest to include the master router and root tests.

## 0.1.1 - Story-writing integration

- Integrated additional private story-writing research notes covering AI-assisted short-story writing, Fountain screenplay drafting, golden-image production, audio/post workflows, release QC, rights/provenance cautions, and reusable story prompts.
- Added short-story workflow references and templates to `short-film-development`.
- Added Fountain workflow support to `screenplay-and-scene-writing`.
- Added golden-image production guidance to `character-location-prop-bible`.
- Added AI film production pipeline notes to `cinematic-video-prompting`.
- Added story/voice/release QC and release checklist support to `prompt-iteration-and-diagnostics`.

## 0.1.0 - Initial generated suite

- Created nine modular skills for short-film development, screenplay support, shot lists, image prompting, video prompting, continuity bibles, iteration diagnostics, cinematography/style direction, and model adaptation.
- Distilled the initial 29 model/cinematography source guides into operational workflows, templates, references, checklists, examples, and Markdown tests.
- Added a model capability matrix and profiles for source-covered models: Grok/Aurora, Gemini/Nano Banana, GPT-image-2, Le Chat/FLUX Ultra, Veo 3.1, Gemini Omni video, Kling AI, and Seedance 2.0.
- Added conservative placeholder handling for models mentioned but not deeply profiled: Midjourney, Stable Diffusion, Ideogram, Runway, Pika, Luma, Sora, Hailuo, DALL-E, and direct FLUX workflows.
- Excluded unsafe bypass-oriented material while preserving safety and policy cautions.

## Known gaps

- Detailed production scheduling, jurisdiction-specific legal clearance, festival rules, and executable validation remain outside the current source coverage.
- Model specs are time-sensitive. Verify current official docs before relying on exact parameters, durations, reference limits, costs, or policy behavior.
- Tests are Markdown validation scenarios, not executable tests.
