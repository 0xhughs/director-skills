# Prompt Translation Rules

## Translation workflow
1. Parse universal brief into intent, execution, and controls.
2. Remove source-model syntax that the target model does not support.
3. Preserve subject, action, emotion, continuity anchors, camera, light, and style.
4. Convert settings into parameters only if the target supports them.
5. Convert negatives according to target behavior.
6. Add a translation report with unsupported and unknown fields.

## Syntax conversion
- Tag soup to natural-language model: rewrite as coherent sentences.
- Natural prose to slot/template model: split into subject, action, camera, style, constraints.
- Image prompt to video prompt: keep identity and setting, add motion, camera behavior, duration, audio, and continuity guardrails.
- T2V to I2V: remove excessive appearance description and focus on animation instructions.

## Unknown rule
If a capability is not in the profile or current user-supplied docs, write `unknown` and provide a conservative fallback.
