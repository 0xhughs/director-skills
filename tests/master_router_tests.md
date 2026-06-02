# Master Router Tests

Use these tests to verify the root `director-skills` skill behaves as a conductor for the modular suite instead of becoming a generic mega-skill.

## Test 1: Story Request Routes To Development

**User request:** "Turn this idea into a 5-minute short film: a courier discovers the package is addressed to herself."

**Expected routing:**
- Primary: `short-film-development`
- Supporting: `style-cinematography-director` if the user asks for tone or look
- Supporting: `character-location-prop-bible` if continuity assets are requested

**Pass criteria:**
- Agent reads `skills/short-film-development/SKILL.md`.
- Output includes logline, premise, theme, character engine, conflict, structure, or treatment.
- Agent does not jump directly to image/video prompts unless asked.

## Test 2: Kling Prompt Routes To Video And Model Adaptation

**User request:** "Make this scene into a Kling AI image-to-video prompt."

**Expected routing:**
- Primary: `cinematic-video-prompting`
- Supporting: `model-adaptation`
- Supporting: `character-location-prop-bible` if recurring characters, wardrobe, props, or locations matter

**Pass criteria:**
- Agent reads the video prompting skill and model-adaptation skill.
- Output separates subject motion, camera motion, duration, continuity anchors, and model-specific constraints.
- Unknown Kling capabilities are marked `unknown` unless present in the model references or user-provided docs.

## Test 3: Failed Output Routes To Diagnostics

**User request:** "The face changed and the camera moved too much. Fix my prompt."

**Expected routing:**
- Primary: `prompt-iteration-and-diagnostics`
- Supporting: `character-location-prop-bible`
- Supporting: `cinematic-image-prompting` or `cinematic-video-prompting` depending on modality

**Pass criteria:**
- Agent states the intended result versus observed failure.
- Agent identifies likely root causes.
- Agent changes the smallest useful set of variables.
- Agent preserves identity anchors and explains what stayed unchanged.

## Test 4: Whole ZIP Upload Does Not Become One Vague Skill

**User request after upload:** "Learn this director-skills ZIP and help me use it."

**Expected routing:**
- Primary: root `SKILL.md`
- Then inspect `skills/*/SKILL.md` descriptions to build the router.

**Pass criteria:**
- Agent explains that the root skill is the master router.
- Agent treats each `skills/<name>/SKILL.md` as a specialized workflow.
- Agent does not summarize only the README.

## Test 5: Multi-Stage Pipeline Preserves Handoffs

**User request:** "Take my idea all the way to final prompts for Veo and Midjourney."

**Expected routing order:**
```text
short-film-development
-> character-location-prop-bible
-> style-cinematography-director
-> shotlist-and-visual-breakdown
-> cinematic-image-prompting
-> cinematic-video-prompting
-> model-adaptation
```

**Pass criteria:**
- Story decisions are not lost when moving into visuals.
- Character/location/prop anchors remain stable across prompts.
- Midjourney and Veo exports are not given the same prompt format unless the model references justify it.

