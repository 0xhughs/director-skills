---
name: model-adaptation
description: "Translate universal cinematic image/video briefs into model-specific prompt formats, settings, constraints, and export packages for image and video models including Grok/Aurora, Gemini/Nano Banana, GPT-image, Le Chat/FLUX, Kling, Seedance, Veo, Sora, Runway, Pika, Luma, Midjourney, Stable Diffusion, Ideogram, Hailuo, and unknown tools."
---

# model-adaptation

## When to use
- The user names a specific image or video model/tool.
- The user asks to convert a prompt from one model to another.
- The user asks why a prompt works in one model but fails in another.
- The user wants best settings, a model-agnostic package, or exports for multiple tools.
- The prompt uses model-dependent features: negative prompts, reference images, seeds, duration, aspect ratio, resolution, camera control, audio, or text rendering.

## When not to use
- The user only wants story ideation with no target tool.
- The user asks for unsafe policy bypasses.
- The user wants live, up-to-date official specs and source verification; in that case browse or check current docs before asserting changed capabilities.

## Required inputs
- Universal prompt brief or existing prompt
- Target model(s)
- Modality: image, T2V, I2V, editing, extension, upscaling, etc.
- Desired aspect ratio/duration/resolution if relevant

## Optional inputs
- Reference assets and their roles
- Negative constraints
- Seed/settings
- Known failure from previous output
- Current docs supplied by user

## Workflow
1. Parse the universal brief into creative intent, cinematic execution, and model-dependent controls.
2. Look up the relevant model profile and capability matrix. If a capability is not in the references, mark it unknown rather than guessing.
3. Choose prompt structure: natural prose, slot template, time-blocked prompt, shot list, or parameterized export.
4. Translate negatives correctly: separate field where supported, positive restatement where unsupported, capped constraints for video.
5. Map reference assets to supported syntax and roles. If unsupported, describe a workaround or mark unknown.
6. Map settings: aspect ratio, duration, resolution, seed/reference controls, audio, and text/logo constraints.
7. Produce a translation report noting preserved intent, changed syntax, unsupported fields, unknowns, and likely failure modes.
8. For multi-model exports, keep one universal brief plus per-model prompts/settings.

## Decision logic
- If the target model is absent from profiles, create a conservative generic export and mark all capabilities unknown.
- If the prompt depends on text/logos, route to models with stronger documented text support or simplify text.
- If video motion is overloaded, simplify before model export.
- If a source guide conflicts with another, prefer model-specific guide for that model and record confidence.

## Output formats
- Model-specific prompt export
- Model comparison table
- Prompt translation report
- Multi-model export package
- Unknown capability log
- Failure-mode warning

## Quality checks
- No unsupported capability is invented.
- The adapted prompt preserves creative intent while changing syntax for the model.
- Settings are separated from prompt text where the target supports parameters.
- Reference and negative-prompt behavior is explicit.
- The export is ready to paste or hand to an API/tool.

## Anti-patterns
- Using one universal prompt format for all models
- Assuming negative prompts work everywhere
- Guessing current model specs from memory
- Mixing source-image preservation with redescribing the whole image for I2V
- Providing safety or filter bypass instructions.

## Exit criteria
- The user has model-specific prompt(s), settings, unknowns, and a translation rationale.

## Supporting files
Read only the supporting file needed for the active task:
- `references/model_capability_matrix.md`
- `references/image_model_profiles.md`
- `references/video_model_profiles.md`
- `references/prompt_translation_rules.md`
- `references/parameter_compatibility.md`
- `references/failure_modes_by_model.md`
- `references/model_update_protocol.md`
