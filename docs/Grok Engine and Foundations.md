# Grok Imagine Prompting Guide — Engine & Foundations

> **Part 1 of 6** | Aurora architecture, prompt pipeline, how prompts are processed, aspect ratio control, and common mistakes to avoid.

---

## 1. Engine Overview

### Aurora Architecture

Aurora is xAI's proprietary multimodal generation engine. The image model is built on a **modified FLUX.1 architecture** from Black Forest Labs, extended with an **autoregressive mixture-of-experts (MoE)** design. This architecture is what distinguishes Aurora from vanilla diffusion models — it processes tokens autoregressively rather than in parallel, which gives it stronger prompt adherence and superior text rendering. ([XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/), [WeShop AI Blog](https://www.weshop.ai/blog/grok-image-ai-generate-high-quality-images-from-prompts-with-aurora-technology/))

**Key architectural facts:**

- Autoregressive MoE pipeline, not a standard UNet diffusion model
- FLUX.1-derived base (Black Forest Labs), heavily modified by xAI
- ~1,000 character prompt capacity — far above most competitors
- High-fidelity NLP parsing: understands nuanced multi-clause instructions
- Style transfer memory: latent space encodes learned style vectors from artists, photographers, and design movements
- Multi-resolution synthesis: generates images progressively from low to high resolution, allowing compositional correction before committing to fine details

The **video model** (Aurora video) employs a **unified multimodal architecture** that processes text, audio, and visual data simultaneously. Audio and visual modalities share latent representations during training, which is why Grok Imagine Video produces natively synchronized audio — it does not add audio in post-production. Background music, dialogue, singing, and sound effects are all generated in the initial render pass. ([Vidofy AI](https://vidofy.ai/en/models/grok-imagine), [Scenario](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))

### How Prompts Are Processed

Every prompt you submit passes through a **two-stage pipeline**:

```
[Your Prompt]
     ↓
[Chat Model Revision]     ← rewrites your prompt with added detail
     ↓
[Image/Video Generation Model]
     ↓
[Output + revised_prompt field]
```

**Stage 1 — Chat model revision:** Before your prompt reaches the Aurora generation model, a chat model rewrites it. The chat model expands sparse prompts, adds compositional and lighting details, interprets intent, and normalizes the instruction for the generation model. This happens automatically with no option to disable.

**Stage 2 — Generation:** The revised prompt is fed to the Aurora image or video model for final synthesis.

**The `revised_prompt` field:** The API response always includes a `revised_prompt` field showing exactly what the generation model received. Example:

| Input | `revised_prompt` |
|-------|-----------------|
| `"A cat in a tree"` | `"3D render of a gray cat with green eyes perched on a thick branch of a leafy tree, set in a suburban backyard during the day."` |
| `"A beautiful woman on the beach"` | Expanded description with skin tone, clothing details, wave patterns, lighting specifics, camera angle, and mood |

The `revised_prompt` is your diagnostic tool. If outputs don't match intent, read the revised prompt to understand what the model actually saw. ([Grok API Docs via Apidog](https://grok-api.apidog.io/-image-generations-15799848e0), [Reddit r/grok](https://www.reddit.com/r/grok/comments/1qtdbqs/a_glimpse_into_groks_image_prompt_rewriting/))

### Models

| Model ID | Type | Endpoint |
|----------|------|----------|
| `grok-imagine-image` | Text-to-image, image editing | `/v1/images/generations`, `/v1/images/edits` |
| `grok-imagine-video` | Text-to-video, image-to-video, video editing, video extension | `/v1/videos/generations`, `/v1/videos/edits`, `/v1/videos/extensions` |

> **Note:** Older documentation may reference `grok-2-image` — the current canonical model ID is `grok-imagine-image`. Always check [docs.x.ai](https://docs.x.ai) for the latest model identifiers.

### Platform Access

| Platform | Notes |
|----------|-------|
| [grok.com](https://grok.com) | Web interface, all features |
| X (Twitter) app | Integrated access, more restricted content policy than standalone |
| Standalone Grok iOS/Android app | Full feature access including Spicy Mode |
| [api.x.ai](https://api.x.ai) (xAI API) | Full programmatic access, requires API key |

**Subscription tiers that affect image/video access:**
- **Free:** 10 images per 2-hour window, no NSFW
- **Premium+:** Higher limits, NSFW unlockable
- **SuperGrok:** Highest limits, NSFW unlockable, all modes


---

## 2. Image Prompting — Foundations

### Natural Language, Not Tag Lists

Aurora processes natural language. The fundamental mistake users make coming from Midjourney or Stable Diffusion is writing tag-stacked prompts:

```
❌ Tag-list style (Midjourney habit):
portrait, woman, red hair, green eyes, studio lighting, bokeh, 4k, ultra realistic, detailed skin

✅ Natural language (Aurora style):
Close-up portrait of a woman with red hair and vivid green eyes, soft studio lighting casting gentle shadows, shallow depth of field with background bokeh, photoreal skin detail, 4K render.
```

Aurora's chat model revision layer handles intent comprehension — it was trained on language, not tag syntax. Sentence structure gives it more context to make better decisions about composition, mood, and style relationships. ([GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine))

### Think Like a Director

> "A prompt that names an object usually creates an object. A prompt that directs a scene creates a moment." — [GenAIntel Prompting Guide](https://www.genaintel.com/guides/how-to-prompt-grok-imagine)

Director-style prompting means specifying:
- **What** is happening (subject + action)
- **Where** it is happening (environment + time of day)
- **How** it looks (lighting + camera + style)
- **How** it should feel (mood + emotion)

This four-axis framing reliably produces cinematic, intentional outputs rather than generic renders. ([LinkedIn — Bruce Canales](https://www.linkedin.com/posts/brucecanales_how-to-prompt-on-grok-imagine-for-better-activity-7414104674225725441-F5DN))

### Core Prompt Formula

```
Subject + Environment + Lighting + Style + Camera
```

Extended version used by [CyberLink Learning Center](https://www.cyberlink.com/blog/ai-prompts/5098/best-grok-prompts-for-images):

```
Subject / Action + Style / Mood + Background / Environment + Camera / Perspective + Special Effects / Enhancements
```

**Latenode component breakdown:**

| Component | Description | Example |
|-----------|-------------|---------|
| Subject | Main focus | "A gray tabby cat" |
| Setting | Environment/background | "In a sunlit Victorian library" |
| Style | Artistic approach | "Digital art, photorealistic" |
| Lighting | Illumination details | "Warm natural lighting, soft shadows" |
| Perspective | Viewing angle and framing | "Close-up shot, rule of thirds" |
| Mood | Emotional atmosphere | "Peaceful, contemplative" |

([Latenode](https://latenode.com/blog/ai-technology-language-models/xai-grok-grok-2-grok-3/step-by-step-how-to-create-amazing-images-with-grok-ai-generator-on-x-platform))

### The Five-Part Formula

Structured approach for consistency across projects:

```
Scene + Style + Mood + Lighting + Camera
```

- **Scene:** What's happening — subject, action, environment
- **Style:** Visual aesthetic — realism, anime, painterly, cinematic
- **Mood:** Emotional direction — nostalgic, tense, dreamlike, electric
- **Lighting:** Time of day, light quality, color temperature
- **Camera:** Shot type, lens, focus, framing

This formula works as a reusable template — change one variable per generation run for controlled iteration. ([GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine))

### Prompt Length

| Parameter | Value |
|-----------|-------|
| System capacity | ~1,000 characters |
| Optimal range | 50–150 words |
| Minimum effective | ~10 words |
| Diminishing returns | >200 words |

Aurora's NLP layers were trained on millions of image-caption pairs and can decode up to ~1,000 characters of detailed instruction — capturing nuanced concepts like "golden hour lighting filtering through stained glass" or "Wes Anderson-style symmetrical composition with pastel color grading." ([WeShop AI Blog](https://www.weshop.ai/blog/grok-image-ai-generate-high-quality-images-from-prompts-with-aurora-technology/))

### Prompt Enhancement Behavior

The chat model revision is aggressive. Submitting a simple prompt like "a dog in a park" will yield a `revised_prompt` with breed specifics, park environment details, weather, lighting, camera angle, and rendering style — all inferred and added. This is a feature, not a bug, but it means:

1. Your short prompts will be elaborated whether you want it or not
2. Contradictory instructions in your prompt may be silently resolved by the chat model
3. The actual generation uses the revised prompt, not yours
4. To control output precisely, read the `revised_prompt` and use it as a starting point for your next iteration


---

## 16. Aspect Ratio Control

### Critical Behavior

Aspect ratio for both image and video is **set via API parameter or UI dropdown**, not via prompt text. Prompt text can influence composition framing within the ratio, but does not reliably change the actual output dimensions.

```
❌ Attempting ratio via prompt text:
"A portrait photo in 9:16 vertical format..."
→ May or may not produce 9:16 output

✅ Correct approach:
Set aspect_ratio: "9:16" in API call, then describe composition normally
```

([XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))

**Pro tip from XsOne:** Including "wide shot" or "portrait orientation" in the text still helps frame the composition within the chosen ratio, even though it doesn't change the ratio itself.

### Platform Recommendations

| Platform | Recommended Ratio | Notes |
|----------|------------------|-------|
| TikTok | `9:16` | Fills screen, native format |
| Instagram Reels | `9:16` | Stories format |
| YouTube Shorts | `9:16` | Vertical mobile |
| YouTube (standard) | `16:9` | Widescreen, landscape |
| Instagram Feed (standard) | `1:1` | Square, works in all feeds |
| Twitter/X media | `16:9` | Landscape for timeline |
| Pinterest | `2:3` | Tall pin format |
| LinkedIn | `1:1` or `16:9` | Both work in feed |
| Facebook Feed | `1:1` | Square for consistency |
| Presentation slides | `16:9` | Widescreen slides |
| Product banners | `2:1` | Wide header format |

([SuperGrok — Video Generation Aspect Ratios](https://supergrok.online/grok-imagine-video-generation-aspect-ratios/))

### Image Aspect Ratios (Full List)

| Ratio | Width:Height | Primary Use |
|-------|-------------|-------------|
| `auto` | Model selects | Let model decide |
| `1:1` | Square | Social media, thumbnails |
| `16:9` | Landscape wide | YouTube, presentations |
| `9:16` | Portrait narrow | Mobile, stories, TikTok |
| `4:3` | Landscape | Traditional display |
| `3:4` | Portrait | Traditional |
| `3:2` | Landscape | Photography (DSLR) |
| `2:3` | Portrait | Photography portrait |
| `2:1` | Wide banner | Headers, banners |
| `1:2` | Tall | Tall banners |
| `19.5:9` | Ultra-wide landscape | Modern smartphones |
| `9:19.5` | Ultra-tall | Modern smartphone tall |
| `20:9` | Ultra-wide | Wide displays |
| `9:20` | Ultra-tall | Tall displays |

### Video Aspect Ratios (Full List)

| Ratio | Primary Use |
|-------|-------------|
| `16:9` | Default, YouTube, widescreen |
| `9:16` | TikTok, Reels, Stories |
| `1:1` | Social feed, thumbnails |
| `4:3` | Presentations |
| `3:4` | Portrait video |
| `3:2` | Cinematic |
| `2:3` | Vertical |


---

## 18. Common Mistakes

### 1. Tag Stacking Instead of Natural Language

```
❌ "portrait, woman, red hair, green eyes, 4k, bokeh, studio, realistic"

✅ "A close-up portrait of a woman with red hair and green eyes in soft studio 
lighting, shallow depth of field with background bokeh, photoreal."
```

Aurora is a language model at its core. Sentence structure communicates relationships between elements. Tag lists lose all relational context.

### 2. Weak Verbs

```
❌ "A woman standing in the rain"
✅ "A woman standing motionless in the rain, water streaming down her face, 
staring into the distance"

❌ "A fighter standing in an arena"
✅ "A fighter lunges forward, fist connecting, sweat spraying from the impact"
```

Strong verbs imply motion, energy, and narrative. Weak verbs produce static, generic renders. ([GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine))

### 3. Missing Time/Weather Cues

Without time of day and weather, Aurora defaults to generic daylight conditions. Always include at least one:

```
❌ "A mountain with a forest below"
✅ "A mountain at sunrise, fog rolling through the pine forest below, 
pink light on the snow-capped peak"
```

### 4. Vague or No Style Direction

Without style, Aurora defaults to a photorealistic/cinematic hybrid. This is fine if that's what you want — but specify if you want anything else:

```
❌ "A fox in a forest" → probably photorealistic
✅ "A fox in a forest, watercolor illustration style, soft edges, muted palette"
✅ "A fox in a forest, anime key visual, vibrant colors, Studio Ghibli atmosphere"
```

### 5. Overloading with Conflicting Instructions

```
❌ "Bright neon colors, dark shadows, muted palette, vibrant saturation, 
desaturated film look, vivid pop art"

✅ Pick one aesthetic register and commit to it
```

The chat model revision will attempt to resolve conflicts, but often produces averaged or incoherent results.

### 6. Negative Instructions

Aurora does not reliably support negative instructions in prompts:

```
❌ "No blur" (often ignored)
❌ "Without shadows" (often ignored)
❌ "Not photorealistic" (often ignored)

✅ Specify what you DO want: "sharp throughout, deep focus"
✅ Specify what you DO want: "flat clean studio lighting, no dramatic shadows"
✅ Specify what you DO want: "anime illustration style, cel-shaded"
```

### 7. Too Many Camera Moves (Video)

```
❌ "Slow dolly in, then orbit 180, then tilt up, ending with a zoom out"
→ Produces unstable, flickering, incoherent motion

✅ "Slow dolly in"
→ Single clean movement, stable output
```

([Chat4O](https://chat4o.ai/blog/detail/Grok-Imagine-AI-Video-Generation-on-Chat4O-A-Step-by-Step-Tutorial-Ready-to-Use-Prompts-25fa95f0df9d/))

### 8. Trying to Direct a Full Movie in One Video Prompt

```
❌ "A woman walks through Paris, stops at the Eiffel Tower, sits at a café, 
runs to catch a train, and waves goodbye as it departs"
→ This is 5 shots; one video generation handles one shot

✅ Generate each shot separately, then extend or chain
```

### 9. Overloading Video Prompts

Keep video prompts **shorter than image prompts**. Long video prompts cause motion instability:

```
❌ 150-word video prompt with 5 character descriptions, 3 environments, 
   4 camera moves, and 2 audio styles

✅ 40-60 word video prompt: subject, one action, one camera move, style
```

### 10. Ignoring the Revised Prompt

Your prompt gets rewritten before generation. If you're getting unexpected results:

1. Check the `revised_prompt` field in the API response
2. Read what the model actually generated from
3. Use the revised prompt as your new baseline
4. Edit the revised prompt directly for tighter control

The `revised_prompt` is the most useful debugging tool available and most users never look at it.

### 11. Vague Edit Instructions

```
❌ "Edit the image to look better"
✅ "Keep the subject and pose exactly. Replace the white studio background 
with a golden wheat field at sunset. Maintain the current lighting on the subject."
```


---

