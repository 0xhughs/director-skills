# Video Prompt Components

## Universal video stack
1. Format: T2V, I2V, first/last frame, extension, editing, multi-shot.
2. Duration and aspect ratio.
3. Subject and stable identity anchors.
4. One dominant action per short shot.
5. One dominant camera behavior per short shot.
6. Framing, angle, and lens feel.
7. Lighting, color, and texture.
8. Motion physics and consequences.
9. Audio: dialogue, ambience, foley/SFX, music mood when supported.
10. Continuity guardrails and model-appropriate constraints.

## Time blocking
Use time blocks when the model/source guide supports sequential behavior:
- [0:00-0:02] establish subject and movement.
- [0:02-0:05] action and camera continue.
- [0:05-0:08] consequence/reveal/end state.

## I2V rule
Preserve the uploaded image. Do not redescribe every visual detail unless the target model asks for it. Focus on motion, camera behavior, lighting change, audio, and what must not change.

## Dialogue math
Short clips cannot carry long lines. Prefer one sentence, natural lip sync, and visible performance beats. If dialogue is not essential, use sound or behavior.
