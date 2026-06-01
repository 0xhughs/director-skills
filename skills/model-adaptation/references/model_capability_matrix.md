# Model Capability Matrix

Source confidence reflects the local guides only. Unknown means the suite should not guess.

| Model/tool | Modality | Best use | Negative support | Reference support | Text/logo reliability | Duration | Aspect/seed/resolution | Source confidence |
|---|---|---|---|---|---|---|---|---|
| Grok Imagine / Aurora | image, edit, T2V, I2V, extension | photoreal image/video, fast variants, permissive creative exploration | no separate consumer negative field in guides; use positive restatement | image references via supported workflows/API per guides | moderate, not best for dense text | 1-15s video; edits capped in guides | aspect ratios/API fields documented in Grok guides | high |
| Gemini image / Nano Banana | image, edit, multi-image composition | natural-language image generation, editing, text rendering, reference-heavy composition | semantic/positive negatives favored; model-specific support varies | up to many references in source guides | strong in source guides | n/a for image | prompt/in-platform controls; some claims need verification | medium |
| GPT-image-2 | image, edit | high-fidelity image craft, text rendering, editing, consistency workflows | model-specific; verify current tool | references/editing per guide | strong in source guide | n/a | parameter surface in source guide, verify current docs | medium |
| Le Chat / FLUX Ultra | image, edit | natural-language image prompting, typography, product/design visuals | no negative field per guide; use positive restatement | upload/edit workflow; aspect ratio preserved on edit per guide | strong but not perfect | n/a | no seed/CFG/steps through Le Chat per guide | high |
| Gemini Veo 3.1 | T2V, I2V, references, extension, audio | cinematic video with audio and reference ingredients | supports concise constraints per guide | up to 4 reference ingredients in guide | limited/risky in video | 4/6/8s clips, extendable per guide | model settings in guide; verify current docs | medium |
| Gemini Omni video | video, conversational editing | cinematic prompt-to-video, audio, iterative edits | supported per guide | reference-driven workflows | unknown to medium | guide-dependent | parameter table in source guide | medium |
| Kling AI | T2V, I2V, elements, start/end, extend, lip sync | controllable video, references, keyframe interpolation | negative prompts supported in guide | Elements/multi-reference workflows | text/logos risky | model/tier-specific; see profile | tier-dependent | high |
| Seedance 2.0 | T2V, I2V, quad-modal refs | multimodal video, asset-role prompting, shot-by-shot prompts | constraints supported as prompt text | images/video/audio roles per guide | unknown | 4-15s in guide | input-driven/aspect support per guide | high |
| Midjourney | image | stylized and cinematic stills | model-specific; unknown in local suite | reference features unknown in local suite | weak/unknown | n/a | unknown | low |
| Stable Diffusion | image, edit, local workflows | parameterized local image generation | supported in common ecosystem but not profiled here | model/workflow-dependent | weak/unknown | n/a | extensive but unknown here | low |
| Ideogram | image/text design | text-heavy images, posters | unknown | unknown | strong relative mention only | n/a | unknown | low |
| Runway | video | video generation/editing | unknown | unknown | unknown | unknown | unknown | low |
| Pika | video | video generation | unknown | unknown | unknown | unknown | unknown | low |
| Luma | video | video generation | unknown | unknown | unknown | unknown | unknown | low |
| Sora | video | cinematic video | unknown | unknown | unknown | unknown | unknown | low |
| Hailuo | video | video generation | unknown | unknown | unknown | unknown | unknown | unknown |
| DALL-E | image | general image generation | unknown in local suite | unknown | model-dependent | n/a | unknown | low |
| FLUX | image | photoreal/design image generation | ecosystem-dependent | ecosystem-dependent | strong relative mention | n/a | unknown outside Le Chat | low |
