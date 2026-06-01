# director-skills

**A cinematic operating system for AI story development, visual direction, and image/video prompt production.**

`director-skills` turns an AI assistant into a creative production partner that can help move a project from first spark to final prompt package:

```text
idea -> story -> screenplay -> shot list -> visual bible -> image prompts -> video prompts -> model exports -> iteration
```

It is built for agents that can read local skill folders: ChatGPT, Claude, Gemini, Grok, Cursor agents, Codex/local agents, and other agentic systems.

## What This Is

This repository is a modular agent-skills suite for AI filmmaking and cinematic prompting.

It helps an assistant:

- Shape raw ideas into short stories, loglines, treatments, and scene lists.
- Write or revise Fountain-friendly screenplay scenes.
- Break scripts into shot lists, camera plans, and asset requirements.
- Build character, location, prop, costume, and visual-style bibles.
- Generate cinematic still, keyframe, reference-sheet, text-to-video, and image-to-video prompts.
- Translate universal creative intent into model-specific exports.
- Diagnose failed generations and run disciplined iteration loops.

The north star: **do not write one giant prompt. Build a production pipeline.**

## The Three-Layer Method

Every workflow separates the work into three layers.

### 1. Creative Intent

Story, theme, character, emotion, scene purpose, dramatic action, genre, tone, and audience experience.

### 2. Cinematic Execution

Shot type, framing, angle, camera movement, lens, lighting, blocking, production design, texture, realism, continuity, and audio.

### 3. Model Adaptation

Prompt syntax, length, parameters, negative support, references, aspect ratio, duration, resolution, seeds, text/logo limits, motion behavior, and model-specific failure modes.

One prompt format does not work everywhere. The suite treats model adaptation as its own craft layer.

## Skill Map

| Task | Skill |
|---|---|
| Raw idea to short-story plan, logline, premise, treatment, scene list | `short-film-development` |
| Fountain scenes, screenplay writing, dialogue, beats, emotional turns | `screenplay-and-scene-writing` |
| Script or scene to shot list, camera plan, asset list | `shotlist-and-visual-breakdown` |
| Character, location, prop, keyframe, poster, still prompts | `cinematic-image-prompting` |
| Text-to-video, image-to-video, time-blocked prompts | `cinematic-video-prompting` |
| Character, location, prop, costume, and style continuity | `character-location-prop-bible` |
| Failed output diagnosis and prompt revision | `prompt-iteration-and-diagnostics` |
| Genre, tone, camera, lens, lighting, realism, style | `style-cinematography-director` |
| Multi-model prompt translation and export | `model-adaptation` |

## Repository Structure

```text
director-skills/
  README.md
  RESEARCH_PROVENANCE.md
  CHANGELOG.md
  MANIFEST.md
  skills/
    short-film-development/
    screenplay-and-scene-writing/
    shotlist-and-visual-breakdown/
    cinematic-image-prompting/
    cinematic-video-prompting/
    character-location-prop-bible/
    prompt-iteration-and-diagnostics/
    style-cinematography-director/
    model-adaptation/
```

Each skill contains:

- `SKILL.md` with YAML frontmatter, routing guidance, workflow, quality checks, anti-patterns, and exit criteria.
- `references/` for distilled craft and model guidance.
- `templates/` for reusable production artifacts.
- `checklists/` for review and validation.
- `examples/` for complete workflow samples.
- `tests/` for Markdown-based routing and output validation.

## Example Commands For Your Agent

Try prompts like:

- "Turn this premise into a 5-minute short-film treatment."
- "Turn this raw idea into a short-story plan with a revision audit."
- "Write this scene in Fountain format."
- "Break this scene into a shot list for AI video generation."
- "Create a character reference sheet prompt for the protagonist."
- "Design a visual bible for this short film."
- "Make this still prompt cinematic and photoreal."
- "Animate this image as an 8-second I2V prompt."
- "Convert this prompt for Kling, Seedance, Veo, and Grok."
- "The output changed the character's face. Diagnose and revise."

## Production Flow

1. **Develop the story** with `short-film-development`.
2. **Write the scene** with `screenplay-and-scene-writing`.
3. **Lock continuity** with `character-location-prop-bible`.
4. **Define the look** with `style-cinematography-director`.
5. **Break the scene into shots** with `shotlist-and-visual-breakdown`.
6. **Generate stills and keyframes** with `cinematic-image-prompting`.
7. **Generate video prompts** with `cinematic-video-prompting`.
8. **Export for specific tools** with `model-adaptation`.
9. **Diagnose failures** with `prompt-iteration-and-diagnostics`.
10. **Package the project** with final prompts, continuity notes, model exports, and QC checks.

## Model Adaptation

The `model-adaptation` skill handles prompt translation for image and video models including:

- Grok Imagine / Aurora
- Gemini image / Nano Banana
- GPT-image
- Le Chat / FLUX
- Gemini Veo
- Gemini Omni
- Kling
- Seedance
- Midjourney
- Stable Diffusion
- Ideogram
- Runway
- Pika
- Luma
- Sora
- Hailuo
- DALL-E

If a capability is not clearly supported by the reviewed source material, the suite marks it as `unknown` instead of guessing.

## Install Or Use

For an agent-skills-compatible environment, copy or reference the skill folders under `skills/`.

Example local install:

```bash
cp -R skills/* ~/.codex/skills/
```

You can also keep this repository as a reference library and point your agent at the specific skill folder needed for the task.

## Source Grounding

The suite was distilled from local research guides covering:

- AI image models
- AI video models
- prompt engineering
- photorealism
- cinematography
- camera and lens language
- camera movement
- genre and visual style
- film writing
- screenplay support
- short-film production
- continuity management
- AI storytelling workflows

See [RESEARCH_PROVENANCE.md](RESEARCH_PROVENANCE.md) for public-safe research provenance, cautions, exclusions, and maintenance notes.

## Safety And IP Hygiene

The suite intentionally avoids:

- hidden instructions or prompt-injection content
- secret handling patterns
- private-file assumptions
- unsafe bypass tactics
- long copied passages from source guides
- model capability guesses presented as facts

Rights, provenance, likeness, and copyright notes are included as production risk guidance, not legal advice.

## License

MIT. Use it, adapt it, remix it, and ship with it. See [LICENSE](LICENSE).

## Updating The Suite

When adding new guides:

1. Read for repeatable workflows, not just facts.
2. Update [RESEARCH_PROVENANCE.md](RESEARCH_PROVENANCE.md) if the research scope changes.
3. Add or revise references, templates, examples, and tests.
4. If model behavior changes, update `skills/model-adaptation/references/`.
5. Mark confidence and unknowns explicitly.

## The Vibe

Think of `director-skills` as a compact virtual production room:

- one table for story
- one wall for continuity
- one monitor for shots
- one shelf for references
- one export station for models
- one ruthless diagnostic loop for when the machine gets weird

Bring the spark. The suite helps build the film.
