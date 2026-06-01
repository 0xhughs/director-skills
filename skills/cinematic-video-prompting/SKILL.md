---
name: cinematic-video-prompting
description: "Generate text-to-video and image-to-video prompts with shot timing, subject motion, camera movement, lensing, lighting, audio cues, continuity anchors, and model-aware constraints."
---

# cinematic-video-prompting

## When to use
- The user wants text-to-video, image-to-video, first/last-frame, video extension, multi-shot, audio-aware, or motion-control prompts.
- The user has a shot list or still image and wants to animate it.
- The task requires duration math, camera movement, subject motion, physical consequence, lip sync, or video-specific failure prevention.

## When not to use
- The user only needs a still image prompt.
- The user is still developing story with no visual beat.
- The user wants editing of a real video file rather than prompt design.

## Required inputs
- Scene or shot goal
- Target duration
- Subject and action
- Camera/framing
- Continuity anchors

## Optional inputs
- Reference image/video/audio roles
- Target model
- Aspect ratio/resolution
- Dialogue line
- Audio design
- Negative constraints

## Workflow
1. Identify the shot purpose and emotional turn.
2. Respect the clock: choose one dominant action and one dominant camera behavior for short clips unless the model explicitly supports multi-shot.
3. Write time blocks or beat blocks when the model benefits from sequential structure.
4. Pair every action with physical consequence: weight, friction, follow-through, environmental reaction, or sound.
5. Specify camera movement, lens feel, framing, lighting, palette, texture, and realism guardrails.
6. For I2V, preserve source composition and describe only motion, camera, lighting shift, and audio.
7. Add audio layers where supported: dialogue, ambience, foley/SFX, and music mood.
8. Add edit/post notes when this prompt belongs to a larger AI short-film package: take count, cut point, color-grain unification, and audio bed.
9. Route to model-adaptation when a named model is involved.

## Decision logic
- If a prompt contains two or more big actions, split into shots.
- If identity drift is likely, generate/reference a character sheet first.
- If hands, mirrors, text, or logos are central, redesign framing or use a more suitable model.
- If the model supports negative prompts, cap constraints to the few failures that would ruin the clip.

## Output formats
- Universal video prompt brief
- Text-to-video prompt
- Image-to-video prompt
- Time-blocked prompt
- Audio cue block
- Continuity guardrails
- Model-adaptation handoff

## Quality checks
- Duration, shot count, camera movement, and action complexity are compatible.
- Motion is concrete and continuous, not a vague mood.
- Subject and camera motion do not conflict.
- Continuity anchors protect identity, wardrobe, props, and location state.
- Known failure modes are addressed without over-constraining.

## Anti-patterns
- Trying to direct a full film in one prompt
- Multiple camera moves in one short clip
- Long dialogue in an 8-second clip
- Describing an uploaded image again instead of animating it
- Using negative prompts as a dumping ground for every fear.

## Exit criteria
- The video prompt is ready for the target workflow or for model-specific export.

## Supporting files
Read only the supporting file needed for the active task:
- `references/video_prompt_components.md`
- `references/camera_lens_movement.md`
- `references/audio_motion_timing.md`
- `references/ai_film_production_pipeline.md`
- `references/prompt_anatomy.md`
- `templates/text_to_video_prompt.md`
- `templates/image_to_video_prompt.md`
