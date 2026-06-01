# Gemini Image & Video Prompting Guide — A to Z

> **Scope**: Nano Banana (gemini-2.5-flash-image), Nano Banana 2 (gemini-3.1-flash-image-preview), Nano Banana Pro (gemini-3-pro-image-preview), Veo 2, Veo 3, Veo 3.1.  
> **Audience**: Technical users and developers building AI systems.  
> **Sources**: [Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation), [Google Cloud Veo Prompt Guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide), [Google Cloud Veo API Reference](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/veo-video-generation), [Google Developer Blog – Prompting Best Practices](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/), [fal.ai Veo 2 Guide](https://blog.fal.ai/mastering-video-generation-with-veo-2-a-comprehensive-guide/), [DataNorth Nano Banana Guide](https://datanorth.ai/blog/nano-banana-the-ultimate-guide-to-googles-image-generation-ai), [Apiyi Content Safety](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html), [LaoZhang AI Blog – People Restrictions](https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction).

---

## Table of Contents

1. [Engine Overview](#1-engine-overview)
2. [Self-Report Reality Check](#2-self-report-reality-check)
3. [Image Prompting — Fundamentals](#3-image-prompting--fundamentals)
4. [Image Prompting — Component Deep Dive](#4-image-prompting--component-deep-dive)
5. [Image Prompting — Templates](#5-image-prompting--templates)
6. [Style Keyword Library](#6-style-keyword-library)
7. [Camera, Lighting, Color Libraries](#7-camera-lighting-color-libraries)
8. [Text Rendering](#8-text-rendering)
9. [Image Editing & Multi-Image Composition](#9-image-editing--multi-image-composition)
10. [Aspect Ratio & Resolution — Complete Reference](#10-aspect-ratio--resolution--complete-reference)
11. [API Reference — Image](#11-api-reference--image)
12. [Video Prompting — Fundamentals (Veo)](#12-video-prompting--fundamentals-veo)
13. [Video Prompting — Component Deep Dive](#13-video-prompting--component-deep-dive)
14. [Video Prompting — Templates](#14-video-prompting--templates)
15. [Video Modes & API Reference](#15-video-modes--api-reference)
16. [Content Policy](#16-content-policy)
17. [Common Mistakes](#17-common-mistakes)
18. [Advanced Techniques](#18-advanced-techniques)
19. [Quick Reference Card](#19-quick-reference-card)

---

## 1. Engine Overview

### What Is Nano Banana?

"Nano Banana" is the community codename (originally leaked from LMSYS Chatbot Arena in August 2025) for Google DeepMind's native image generation architecture within Gemini. It refers to three models — **Nano Banana**, **Nano Banana 2**, and **Nano Banana Pro** — that share a unified multimodal transformer architecture fundamentally different from diffusion pipelines like Stable Diffusion or Midjourney. ([DataNorth AI](https://datanorth.ai/blog/nano-banana-the-ultimate-guide-to-googles-image-generation-ai))

### Architecture: Unified Transformer (NOT Diffusion)

| Aspect | Diffusion Models (SD, MJ, FLUX) | Nano Banana (Gemini Native) |
|--------|--------------------------------|----------------------------|
| Pipeline | Separate LLM + diffusion model | Single unified transformer |
| Text processing | CLIP → 512-dim vector embedding | Full 256K context window |
| Text-in-image | CLIP loses semantic text structure | Native token-level text understanding |
| Editing | Requires inpainting model | Conversational, in-context |
| Multi-turn | Stateless (each gen is independent) | Stateful (references previous outputs) |
| Image+text input | Separate vision encoder | Processed in shared attention layers |

The core innovation is that text and images are processed natively in **shared attention layers** — the model "thinks" about text and visual tokens together, rather than compressing text into a fixed vector and passing it to a separate visual model. This is why Nano Banana excels at text rendering and complex instruction following. ([ZenML / Google DeepMind](https://www.zenml.io/llmops-database/native-image-generation-with-multimodal-context-in-gemini-2-5-flash))

### Three Nano Banana Models

| Model | API ID | Generation | Optimized For | Key Differentiators |
|-------|--------|------------|---------------|---------------------|
| **Nano Banana** | `gemini-2.5-flash-image` | Gemini 2.5 | Speed, high-volume, low-latency | 1K only, 10 aspect ratios |
| **Nano Banana 2** | `gemini-3.1-flash-image-preview` | Gemini 3.1 | Speed + volume at production scale | 512px–4K, 14 aspect ratios, Image Search grounding, 10 object refs + 4 character refs |
| **Nano Banana Pro** | `gemini-3-pro-image-preview` | Gemini 3 | Professional asset production | 1K–4K, advanced reasoning, 6 object refs + 5 character refs, highest quality |

([Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation))

### Veo Video Models

| Model | API ID | Resolution | Duration | Audio | Key Features |
|-------|--------|------------|----------|-------|-------------|
| **Veo 2** | `veo-2.0-generate-001` / `veo-2.0-generate-preview` / `veo-2.0-generate-exp` | 720p | 5–8 seconds | None | latent diffusion transformer, enhancePrompt, reference images (exp only) |
| **Veo 3** | `veo-3.0-generate-preview` / `veo-3.0-generate-001` | 720p / 1080p | 4, 6, or 8 seconds | Native audio (SFX, ambient, dialogue) | generateAudio parameter |
| **Veo 3.1** | `veo-3.1-generate-preview` / `veo-3.1-fast-generate-preview` | 720p / 1080p / 4K | 4, 6, or 8 seconds | Native audio | negativePrompt, reference images (3 asset + 1 style), mask editing, 4K |

([Google Cloud Veo API Reference](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/veo-video-generation))

### Two-Stage Pipeline

Every image generation goes through two stages:

```
User Prompt
     │
     ▼
┌────────────────────────────────┐
│   Gemini LLM (prompt layer)    │  ← enhances, interprets, adds context
│   256K context window           │  ← can receive images, prior turns
│   "Thinking mode" active        │  ← generates interim thought images
└────────────────────────────────┘
     │  enhanced prompt + visual context
     ▼
┌────────────────────────────────┐
│   Image/Video Generation Model │  ← Nano Banana / Veo
│   Unified multimodal tokens    │
│   Generates final output        │
└────────────────────────────────┘
     │
     ▼
Final Image/Video + SynthID Watermark
```

This pipeline is why the model can follow complex natural language — the LLM layer handles language reasoning before the visual model handles visual generation.

### Thinking Mode

Thinking mode is **always enabled** and cannot be disabled. The model:
1. Generates up to 2 interim "thought images" to explore composition (these are **not billed** and not returned by default)
2. Uses those internal compositions to inform the final output
3. Can be configured to return thought images via `include_thoughts=True`
4. Supports `thinking_level="high"` (Nano Banana 2 / 3.1 Flash only) for more deliberate reasoning

Thinking tokens ARE billed even when `include_thoughts=False`. ([Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation))

### Google Search Grounding

Both Nano Banana 2 and Nano Banana Pro can use Google Search as a live tool during generation:

- **Web Search**: Real-time data (weather maps, stock charts, current events, factual entities). Available to all Gemini 3 image models.
- **Image Search** (Nano Banana 2 / `gemini-3.1-flash-image-preview` **only**): Retrieves reference images from the web during generation. Has display requirements (source attribution, direct click-through). **Cannot search people**.

### SynthID Invisible Watermarks

**ALL** Gemini-generated images — regardless of tier, API access level, or settings — carry SynthID watermarks. These are:

- Embedded at the pixel level; invisible to the naked eye
- Survive cropping, scaling, color adjustment, screenshots, and re-saving
- Cannot be removed without measurable quality degradation
- Verifiable by third parties using Google's SynthID verification tool
- Applied even to images you generate via the raw API

This is non-negotiable and cannot be bypassed. ([Apiyi Content Safety Guide](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html))

### Platform Access

| Platform | Models Available | Notes |
|----------|-----------------|-------|
| Gemini App (consumer) | Nano Banana 2, Nano Banana Pro | Most conservative content enforcement |
| Google AI Studio | All Nano Banana models | Developer UI, good for iteration |
| Gemini API (v1beta) | All Nano Banana models | Direct API access |
| Vertex AI | All Nano Banana + Veo models | Enterprise, production SLAs |
| fal.ai (third-party) | Veo 2, Veo 3 | Alternative API host |

---

## 2. Self-Report Reality Check

When Gemini (the LLM) is asked about its own image/video generation capabilities, it systematically under-reports. The reason: **the LLM processing the prompt does not have full awareness of the underlying image/video model's parameter space and limits**. The LLM layer knows general facts about Gemini but doesn't have precise runtime knowledge of model-specific specs like exact resolution tables or API parameters.

| Feature | Gemini Claimed | Verified Reality | Verdict |
|---------|---------------|-----------------|---------|
| Resolutions | 1024×1024, 1536×1024, 1024×1536 | 512px / 1K / 2K / 4K tiers across 14 aspect ratios | **Severely underestimated** |
| Aspect ratios | 1:1, 16:9, 9:16, 4:3, 3:4 | 14 ratios: 1:1, 1:4, 1:8, 2:3, 3:2, 3:4, 4:1, 4:3, 4:5, 5:4, 8:1, 9:16, 16:9, 21:9 | **Incomplete** |
| Default resolution | 1024×1024 | 1K (1024px base) — accurate but omits 2K/4K options | **Partially accurate** |
| Veo max duration | 60 seconds | Veo 2: 5–8 sec; Veo 3/3.1: 4, 6, or 8 sec | **Likely hallucinated** |
| Veo frame rates | 24, 30, 60 fps | Not documented in API; 24fps commonly observed | **Unverified** |
| Veo resolution | 1080p | Veo 2: 720p default; Veo 3: 720p/1080p; Veo 3.1: adds 4K | **Partially accurate** |
| Veo lip sync | Not supported | Veo 3+ has native dialogue/speech + audio generation | **Underestimated** |
| SynthID watermark | Not mentioned | ALL generated images have SynthID | **Critical omission** |
| Thinking mode | Not mentioned | Always enabled; generates thought images; billed | **Critical omission** |
| Google Search grounding | Not mentioned | Available; Image Search on 3.1 Flash | **Critical omission** |
| Character consistency | Not mentioned | Up to 5 characters maintained across generations | **Critical omission** |
| Person generation policy | Generic photorealistic people allowed | Complex: 2024 controversy, Jan 2026 zero-tolerance, Feb 2026 4 new categories | **Oversimplified** |
| Video editing | Extend duration only | Veo 3.1: mask editing, inpainting, object insertion/removal | **Underestimated** |
| Video aspect ratios | 16:9, 9:16, 1:1 | Only 16:9 and 9:16 documented in API; 1:1 unconfirmed | **Possibly inaccurate** |
| Negative prompts (video) | Not mentioned | Veo 3.1 has `negativePrompt` parameter | **Omission** |
| Seed control (video) | Not mentioned | `seed` parameter: 0–4,294,967,295 for deterministic generation | **Omission** |
| Prompt enhancement (video) | Not mentioned | `enhancePrompt` parameter (default `true`) for Veo 2 models | **Omission** |
| Reference images (video) | Not mentioned | Veo 3.1: up to 3 asset + 1 style reference image | **Omission** |

**Why this happens**: The Gemini LLM that processes your prompt has general training knowledge about Gemini capabilities, but that training data has a knowledge cutoff, may reflect older model specs, and does not include live access to the current API parameter schema. When the LLM self-reports capabilities, it's drawing on training data — not querying the actual underlying image/video model's runtime parameters. Always consult the [official API docs](https://ai.google.dev/gemini-api/docs/image-generation) for ground truth.

---

## 3. Image Prompting — Fundamentals

### Core Principle: Natural Language, NOT Tag Lists

Nano Banana's unified transformer architecture means it processes text with full semantic understanding. Writing prompts as keyword tag lists — the way you'd prompt Stable Diffusion or Midjourney — actively degrades output quality.

**Wrong (SD/MJ syntax):**
```
4k, ultra-realistic, portrait, man, dark background, bokeh, --ar 16:9 --v 6
```

**Right (Nano Banana syntax):**
```
A photorealistic portrait of a middle-aged man with weathered features and a contemplative expression, 
set against a deep charcoal background. Soft Rembrandt lighting falls from camera-left, 
highlighting the texture of his stubble. Shot with an 85mm lens, shallow depth of field 
creates gentle bokeh. Vertical portrait orientation.
```

Google's own stated principle from the [official developer blog](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/):

> *"Describe the scene, don't just list keywords. The model's core strength is its deep language understanding. A narrative, descriptive paragraph will almost always produce a better, more coherent image than a simple list of disconnected words."*

### "Think Like a Photographer/Director"

For realistic images, approach the prompt as a cinematographer would approach a shot:
- What is the subject doing, not just what they look like?
- Where is the light source, not just "good lighting"?
- What lens is on the camera, not just "sharp"?
- What is the mood of the shot, not just "nice"?

This isn't a metaphor — specific cinematographic and photographic terms directly influence output. ([Google Developer Blog](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/))

### Core Formula

```
[Subject + Action/State] + [Environment/Setting] + [Style/Medium] + [Lighting] + [Camera/Composition]
```

Each element can be a sentence or clause. You don't need all five in every prompt, but more specificity = more control.

### Prompt Length: The 256K Advantage

| Model | Token Limit for Prompts | Effective Length |
|-------|------------------------|-----------------|
| FLUX / Stable Diffusion | ~77 tokens (CLIP) | ~60 words max |
| Midjourney | ~256 tokens | ~200 words max |
| **Nano Banana** | **256K context window** | **Full narrative paragraphs; thousands of words if needed** |

You are not constrained to short prompts. For complex scenes, write full paragraphs. The model can process them coherently.

### Prompt Enhancement: Default ON

By default, the Gemini LLM layer **rewrites and expands your prompt** before passing it to the image model. This usually improves output — the LLM adds photography terms, compositional guidance, and style cues you may not have included.

**To disable enhancement** (to get literal interpretation):
- Add to your prompt: `"Do not modify this prompt."` or `"Generate exactly as described, without additions."`
- In the Gemini app, there is a toggle for "Enhance prompt" in some interfaces

Prompt enhancement is the LLM layer acting on your behalf. It's a strength for casual prompts and a nuisance when you need precise control.

### Step-by-Step Instructions for Complex Scenes

For scenes with multiple elements, Google officially recommends structuring your prompt as explicit sequential steps. ([Google Cloud Best Practices](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-best-practices))

**Example:**
```
First, create a background of a serene, misty forest at dawn with soft light filtering through tall conifers.
Then, in the foreground, add a moss-covered ancient stone altar partially obscured by morning fog.
Finally, place a single glowing sword upright on the altar, with faint magical light radiating from the blade.
The overall mood is mystical and reverent. Wide shot, cinematic framing.
```

This reduces hallucination of arbitrary elements and gives the model an explicit compositional plan to execute.

### "Semantic Negative Prompts": Describe What You Want

Nano Banana does not have a native negative prompt parameter (unlike Stable Diffusion). Instead, use **positive framing** to exclude unwanted elements. ([Google Cloud Best Practices](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-best-practices))

| Instead of saying... | Say... |
|---------------------|--------|
| "No cars" | "An empty, deserted street with no signs of traffic" |
| "No text" | "A clean image with no text, labels, or typography" |
| "No people" | "A solitary landscape, completely uninhabited" |
| "Not blurry" | "Sharp, tack-focused throughout, crisp detail" |
| "Avoid X" | Use `Avoid: [X]` as a suffix if needed |

Alternatively, you can write `"Avoid: [comma-separated list]"` at the end of a prompt and the LLM layer will interpret it correctly.

---

## 4. Image Prompting — Component Deep Dive

### Subject (Required)

**Description**: The primary entity — person, object, animal, concept, or abstraction.  
**Importance**: Critical. Without a clear subject, the model generates generic scenes.  
**Position**: Beginning of the prompt.  
**Tips**: Be specific about identity markers (age, appearance, state), not just category.

| Generic | Specific |
|---------|----------|
| "A woman" | "A 60-year-old Japanese ceramicist with silver hair and clay-stained hands" |
| "A car" | "A 1967 Ford Mustang fastback in midnight blue with chrome trim" |
| "A building" | "A crumbling Brutalist concrete tower partially reclaimed by vines" |
| "A dog" | "A 6-month-old Shiba Inu puppy mid-leap, ears fully extended, mouth open" |
| "A crystal" | "A 30cm amethyst geode split open, deep purple inner cavities catching light" |

### Action / Pose

**Description**: What the subject is doing. Verb-forward.  
**Importance**: High. Static subjects produce static images. Dynamic actions produce dynamic images.  
**Position**: Directly after subject description.

| Category | Example Actions |
|----------|----------------|
| Physical | running, leaping, falling, spinning, crouching, reaching |
| Expressive | laughing, grimacing, concentrating, weeping, smiling mid-conversation |
| Subtle | fingers tapping, hair blowing in wind, a single bead of sweat |
| Functional | writing, painting, soldering, cooking, disassembling |
| Arrested motion | "mid-swing", "frozen at the apex of a jump", "caught at the moment of impact" |

### Environment / Setting

**Description**: Where and when the scene takes place.  
**Importance**: High. Establishes context, mood, and lighting logic.  
**Position**: After subject and action.

| Dimension | Example Descriptors |
|-----------|---------------------|
| Interior | "a cluttered 1970s detective office", "sterile laboratory with green-tinted fluorescents" |
| Exterior | "sun-scorched Atacama desert at high noon", "rainy Tokyo backstreet at 2am" |
| Time of day | "blue hour", "golden hour", "harsh midday", "pre-dawn twilight" |
| Weather | "thick coastal fog", "dry lightning over plains", "heavy snow, zero visibility" |
| Period | "medieval castle courtyard", "1920s jazz club", "cyberpunk megacity" |
| Atmospheric details | "floating dust motes in a sunbeam", "steam rising from asphalt after rain", "heat shimmer over desert sand" |

### Style / Medium

**Description**: The artistic or photographic style of the output.  
**Importance**: High. Determines whether the output looks like a photograph, illustration, painting, 3D render, etc.  
**Position**: Can appear anywhere but is most effective in the first third of the prompt.

From the [official Google developer blog](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/):

| Category | Keywords |
|----------|---------|
| Photorealistic | photorealistic, shot on 35mm film, Kodak Portra 400, cinematic, documentary photography |
| Illustration | digital illustration, vector art, flat design, concept art, editorial illustration |
| Painterly | oil painting, watercolor, gouache, acrylic, impressionist brushwork |
| Anime/Animation | Japanese anime style, Pixar 3D, Disney animation, Studio Ghibli aesthetic |
| 3D/Technical | Unreal Engine render, Octane render, isometric, architectural visualization |
| Vintage | daguerreotype, Victorian illustration, 1950s ad, hand-tinted photograph |
| Abstract | surrealist, abstract expressionism, geometric abstraction, collage |

See full keyword library in [Section 6](#6-style-keyword-library).

### Camera / Composition

**Description**: Shot type, lens focal length, perspective angle, framing, depth of field.  
**Importance**: Medium-high. Dramatically affects the emotional register and visual hierarchy.  
**Position**: Usually near the end of the prompt.

| Sub-element | Examples |
|-------------|---------|
| Shot type | close-up, extreme close-up, medium shot, wide shot, establishing shot |
| Lens | 24mm wide-angle, 50mm standard, 85mm portrait, 200mm telephoto, macro |
| Perspective | eye-level, low-angle, bird's-eye view, Dutch angle, over-the-shoulder |
| Framing | rule of thirds, centered, negative space, tight crop |
| Depth of field | shallow DOF (bokeh), deep DOF (everything sharp), rack focus effect |

See full tables in [Section 7](#7-camera-lighting-color-libraries).

### Lighting

**Description**: Source, quality, direction, and color temperature of light.  
**Importance**: High. Lighting is often what separates a flat image from a compelling one.  
**Position**: Usually in the environment section or as its own sentence.

| Type | Example Phrases |
|------|----------------|
| Natural | "soft golden hour light streaming through west-facing windows" |
| Studio | "three-point softbox setup, soft diffused highlights, no harsh shadows" |
| Cinematic | "Rembrandt lighting from camera-left", "film noir: deep shadows, single key light" |
| Practical | "warm glow of a single Edison bulb", "blue-green flicker of a CRT monitor" |
| Stylized | "volumetric god rays", "neon sign casting magenta light on wet pavement" |

See full lighting keyword tables in [Section 7](#7-camera-lighting-color-libraries).

### Color Palette

**Description**: Dominant hues, tonal range, saturation, color grading.  
**Importance**: Medium. Strongly affects mood; specific palette control is useful for brand work.  
**Position**: Anywhere after the main scene description.

| Palette Type | Examples |
|-------------|---------|
| Warm | "warm autumnal oranges and deep reds", "golden amber tones throughout" |
| Cool | "desaturated blue-grey palette", "cool silver and slate tones" |
| Monochromatic | "black and white with strong contrast", "sepia-toned monochrome" |
| Vibrant | "vivid tropical colors, high saturation", "neon pinks and electric blues" |
| Muted/desaturated | "muted earthy tones, low saturation", "faded film look with lifted blacks" |
| Specific grading | "teal and orange color grade", "Matrix green tint", "bleach bypass look" |

### Quality Modifiers

**Description**: Terms that signal resolution, detail, and professional grade.  
**Importance**: Low-medium. Nano Banana interprets these as signals, not absolute commands — but they help set intent.  
**Position**: Usually at end of prompt or in style section.

| Modifier | Effect |
|----------|--------|
| "ultra-detailed", "highly detailed" | Encourages fine detail in textures |
| "sharp focus", "tack sharp" | Reinforces crispness |
| "8K", "4K resolution" | Signals high-detail intent (actual output resolution set via API parameter) |
| "professional photography", "studio quality" | Encourages clean, polished aesthetic |
| "award-winning", "magazine quality" | Pushes toward commercial/editorial aesthetic |
| "photorealistic" | Signals photographic rendering intent |

**Note**: Resolution is controlled via the `image_size` API parameter, not via prompt text. Writing "4K" in the prompt does not generate a 4K image.

### Aspect Ratio

**Description**: The width-to-height proportion of the output image.  
**Importance**: Critical for intended use case.  
**How to specify**: Via `image_config.aspect_ratio` API parameter — NOT in the prompt text.  
**Default**: 1:1 at 1K resolution.

Writing "16:9" or "widescreen" in the prompt text has minimal effect on actual output dimensions. Use the API parameter:

```python
image_config=types.ImageConfig(
    aspect_ratio="16:9",
    image_size="2K"
)
```

See full resolution tables in [Section 10](#10-aspect-ratio--resolution--complete-reference).

---

## 5. Image Prompting — Templates

All templates are from the [Google Developer Blog](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/).

---

### Template 1: Photorealistic Scene

```
A photorealistic [shot type] of [subject], [action or expression], set in [environment].
The scene is illuminated by [lighting description], creating a [mood] atmosphere.
Captured with a [camera/lens details], emphasizing [key textures and details].
The image should be in a [aspect ratio] format.
```

**Example 1 (Portrait):**
```
A photorealistic close-up portrait of an elderly Japanese ceramicist with deep, sun-etched 
wrinkles and a warm, knowing smile. He is carefully inspecting a freshly glazed tea bowl. 
The setting is his rustic, sun-drenched workshop. The scene is illuminated by soft, golden 
hour light streaming through a window, highlighting the fine texture of the clay. 
Captured with an 85mm portrait lens, resulting in a soft, blurred background (bokeh). 
The overall mood is serene and masterful. Vertical portrait orientation.
```

**Example 2 (Environment):**
```
A photorealistic wide establishing shot of a derelict Soviet-era research station half-buried 
in Antarctic snow, barely visible through a raging blizzard. The scene is illuminated by the 
weak grey light of a polar day, with bioluminescent emergency lighting still flickering in 
cracked windows. Captured with a 24mm wide-angle lens in extreme weather conditions, 
emphasizing the scale of the structure against the vast empty tundra. 
Horizontal widescreen format. The overall mood is isolating and ominous.
```

---

### Template 2: Stylized Illustration

```
A [art style] illustration of [subject], [action], in [setting].
The color palette is [palette description]. 
The line work is [line quality]. 
The overall feel is [mood/tone].
```

**Example 1 (Flat Design):**
```
A flat design digital illustration of a lone astronaut sitting cross-legged on the surface of 
a ringed gas giant, eating a sandwich. The color palette is muted pastels — dusty rose, 
sage green, and warm cream — against a deep indigo space background. 
Clean vector shapes, no gradients. The overall feel is quietly whimsical and melancholic.
```

**Example 2 (Concept Art):**
```
A detailed concept art illustration of a bio-mechanical cathedral where the architecture 
is made of living tissue — ribcages form the arched ceilings, veins pulse through the 
flying buttresses, and stained glass windows are made of cross-sectioned organs. 
Dark biopunk aesthetic. Rendered in the style of a professional concept art for a game. 
The color palette is cold blues and purples with warm amber light pulsing from within 
the organic structures. The overall feel is grotesquely beautiful.
```

---

### Template 3: Text Rendering

```
Create an image of [medium/object] that displays the text "[exact text]" in [font style/type].
The [medium] should be [visual description]. 
The text should be [placement, size, color, treatment].
```

**Example 1 (Sign):**
```
Create an image of a vintage neon sign mounted on a brick wall that displays the text 
"OPEN LATE" in a classic script neon font. The sign should be lit up in warm pink-red 
neon against a dark, rainy-night exterior. The text should be centered, with a slight 
neon glow bleeding onto the wet brick behind it.
```

**Example 2 (Infographic label):**
```
Create an image of a botanical illustration of a coffee plant with clear, handwritten-style 
labels identifying the following parts: "Coffea arabica", "cherry", "bean", "leaf", "stem". 
Each label should be connected to the corresponding part with a thin, elegant line. 
Scientific illustration style on aged parchment paper.
```

---

### Template 4: Product Mockup

```
A high-resolution, studio-lit product photograph of [product description], presented on 
[surface/background]. The lighting is [lighting setup] designed to [lighting goal]. 
The camera angle is [angle] to showcase [key feature]. 
[Quality descriptor]. [Additional details].
```

**Example 1 (Minimalist):**
```
A high-resolution, studio-lit product photograph of a minimalist ceramic coffee mug in 
matte black, presented on a polished concrete surface. The lighting is a three-point 
softbox setup designed to create soft, diffused highlights and eliminate harsh shadows. 
The camera angle is a slightly elevated 45-degree shot to showcase its clean geometric lines. 
Ultra-realistic, with sharp focus on the steam rising from the coffee. Square image.
```

**Example 2 (Lifestyle):**
```
A high-resolution lifestyle product photograph of a premium leather-bound journal lying 
open on a reclaimed oak desk, next to a steaming espresso and a vintage mechanical pencil. 
Warm morning light from a window to the left creates long, raking shadows that emphasize 
the texture of the leather and the grain of the wood. Shallow depth of field with the 
journal's open page in sharp focus. 4:3 landscape orientation.
```

---

### Template 5: Multi-Image Composition

```
Compose an image that combines the following elements:
- [Element 1 from reference image 1: description]
- [Element 2 from reference image 2: description]
Place [element 1] in [position], and [element 2] in [position].
The scene should be [environment/context].
Lighting: [unified lighting description that makes both elements feel coherent].
Style: [consistent style directive].
```

**Example 1 (Character + Object):**
```
Compose an image featuring the character from the first reference image 
(maintain their exact appearance and costume) holding the product from the second 
reference image. Place the character in a busy Tokyo street market at night. 
Unify the lighting with warm yellow lantern light from above. 
Photorealistic, cinematic quality. 16:9 widescreen.
```

**Example 2 (Style Transfer):**
```
Transform the provided photograph of a modern city street at night into the artistic 
style of Vincent van Gogh's 'Starry Night'. Preserve the original composition of 
buildings and street lights, but render all elements with swirling, impasto brushstrokes 
and a dramatic palette of deep blues, cobalt, and luminous yellows. 
The street lights should become swirling halos of gold.
```

---

### Template 6: Stock / Marketing Photography

```
A [mood descriptor] stock photograph of [subject], [action/state], [environment].
[Demographic descriptors if needed]. 
Lighting: [natural or studio, warm/cool, quality].
Composition: [shot type, framing — especially negative space for text overlay].
Style: commercial photography, professionally lit, clean.
[Format].
```

**Example 1 (Negative space for copy):**
```
A minimalist composition featuring a single, delicate red maple leaf positioned in the 
bottom-right corner of the frame. The background is a vast, empty off-white canvas, 
creating significant negative space for text overlay in the top-left two-thirds. 
Soft, diffused lighting from the top-left. No shadows. Clean, minimal, commercial. 
Square format.
```

**Example 2 (Lifestyle):**
```
A warm, authentic lifestyle stock photograph of two people in their early 30s having 
a relaxed conversation at an outdoor café, both laughing naturally. Generic appearance, 
not identifiable as specific individuals. Morning light, tables with coffee cups. 
Slightly elevated camera angle, medium shot. Warm color grade, shallow depth of field 
with background café bokeh. Professional commercial photography. 
16:9 horizontal format.
```

---

## 6. Style Keyword Library

### Photorealism

| Keyword | Effect |
|---------|--------|
| `photorealistic` | General photographic rendering |
| `cinematic` | Film-quality color grade and composition |
| `shot on 35mm film` | Film grain, organic color |
| `Kodak Portra 400` | Warm film tones, fine grain |
| `Fujifilm Provia` | Saturated, cool film look |
| `documentary photography` | Candid, unposed, natural |
| `editorial photography` | Polished, intentional, professional |
| `fashion photography` | High-contrast, stylized, model-forward |
| `HDR photography` | High dynamic range, wide tonal latitude |
| `macro photography` | Extreme close-up, high depth of detail |
| `long exposure` | Motion blur in moving elements, sharp static |

### Illustration

| Keyword | Effect |
|---------|--------|
| `digital illustration` | Clean, professional digital art |
| `flat design` | Minimal shadows, vector shapes, solid colors |
| `vector art` | Crisp scalable geometric look |
| `concept art` | Detailed, painterly, game/film development style |
| `editorial illustration` | Stylized, expressive, suited for print |
| `children's book illustration` | Warm, friendly, simple forms |
| `technical illustration` | Precise, labeled, exploded views |
| `line art` | Pen-and-ink look, clean outlines |
| `sticker art` | Bold outlines, clean fills, character-driven |
| `infographic style` | Data visualization, clear labels, flat icons |

### Anime & Animation

| Keyword | Effect |
|---------|--------|
| `Japanese anime style` | Classic anime proportions and shading |
| `Studio Ghibli aesthetic` | Painterly, environmental, warm |
| `classic Disney animation style` | Traditional cel look, expressive characters |
| `Pixar-like 3D animation` | High-quality CG animated film look |
| `4K animated movie still` | Polished CG film frame |
| `chibi style` | Super-deformed, exaggerated cute proportions |
| `shonen manga` | Dynamic action, heavy ink, speed lines |
| `shojo manga` | Soft lines, floral details, romance aesthetic |
| `mecha anime` | Industrial robots, detailed mechanical design |
| `webtoon style` | Vertical-optimized, clean digital line art |

### Painterly

| Keyword | Effect |
|---------|--------|
| `oil painting` | Thick paint texture, rich colors |
| `watercolor painting` | Soft washes, visible paper texture, bleeding edges |
| `gouache` | Opaque, matte, flat painterly look |
| `acrylic painting` | Versatile, can mimic oil or watercolor |
| `impressionist` | Broken color, loose brushwork, atmospheric |
| `in the style of Van Gogh` | Swirling impasto, expressive color |
| `in the style of Monet` | Soft light, water reflections, loose form |
| `in the style of Klimt` | Gold leaf, decorative patterns, Art Nouveau |
| `pointillist` | Thousands of dots forming image |
| `fresco painting` | Ancient wall-painting texture, desaturated |
| `encaustic` | Layered wax texture, translucent depth |

### Cinematic

| Keyword | Effect |
|---------|--------|
| `film noir` | Deep shadows, high contrast, moody B&W or desaturated |
| `anamorphic widescreen` | Horizontal lens flares, cinematic aspect ratio |
| `neo-noir` | Modern noir with neon color accents |
| `Kodachrome color grade` | Warm reds, boosted contrast, vintage |
| `teal and orange color grade` | Hollywood blockbuster color grading |
| `bleach bypass` | Desaturated, high contrast, muted colors |
| `movie still` | Frame from a professional film |
| `IMAX cinematography` | Ultra-high detail, wide-format composition |
| `Wes Anderson aesthetic` | Centered symmetry, pastel palette, flat staging |
| `vintage film look` | Grain, light leaks, faded blacks |

### 3D / Technical

| Keyword | Effect |
|---------|--------|
| `Unreal Engine render` | Real-time game engine quality, photo-real |
| `Octane render` | Physically-based ray tracing, glass/metal quality |
| `Cinema 4D render` | Smooth, polished 3D commercial look |
| `isometric illustration` | Fixed 3D angle, no perspective distortion |
| `architectural visualization` | Building renders, real estate quality |
| `product render` | Studio-quality 3D product photography |
| `blueprint schematic` | Technical drawing, white lines on blue |
| `wireframe model` | 3D mesh visualization |
| `x-ray visualization` | See-through, medical/technical look |
| `voxel art` | Minecraft-style cubic 3D |
| `low poly 3D` | Faceted, simplified geometry, angular |

### Additional Artistic Styles (from Veo Docs, applicable to images)

| Keyword | Effect |
|---------|--------|
| `claymation style` | Clay-textured, stop-motion aesthetic |
| `stop-motion animation` | Physical model quality |
| `cel-shaded animation` | Flat shading with hard outlines |
| `charcoal sketch` | Dark, grainy, hand-drawn |
| `watercolor painting coming to life` | Animated watercolor aesthetic |
| `gritty graphic novel illustration` | Heavy ink, desaturated, dramatic |
| `surrealist painting` | Dali-like impossible juxtapositions |
| `Art Deco design` | Geometric, golden, 1920s luxury |
| `Bauhaus aesthetic` | Form follows function, primary colors, geometry |

---

## 7. Camera, Lighting, Color Libraries

### Shot Types

| Shot Type | Description | Use Case |
|-----------|-------------|----------|
| Extreme close-up (ECU) | Isolates a tiny detail (eye, texture, coin) | Emphasize detail, emotional intensity |
| Close-up (CU) | Face or single object fills the frame | Emotion, character focus |
| Medium close-up (MCU) | Chest up | Interview, conversational |
| Medium shot (MS) | Waist up | Dialogue, character context |
| Medium wide / cowboy shot | Thighs up | Western genre, action setup |
| Wide shot / full shot (WS) | Entire subject with environment | Character in context |
| Long shot (LS) | Subject is small in large environment | Scale, isolation |
| Establishing shot | Wide, shows location | Scene introduction, geography |
| Two-shot | Two subjects in frame | Relationship, conversation |
| Insert shot | Isolated object detail | Draw attention to prop/detail |

### Lens Keywords

| Lens | Focal Length | Visual Effect |
|------|-------------|---------------|
| Ultra-wide | 14–21mm | Exaggerated perspective, room distortion |
| Wide-angle | 24–35mm | Environmental context, slight distortion |
| Normal | 50mm | Human eye perspective, neutral |
| Portrait | 85–105mm | Flattering compression, subject isolation |
| Telephoto | 135–200mm | Strong compression, distant subject |
| Super telephoto | 300–600mm | Extreme compression, wildlife distance |
| Macro | 1:1 ratio | Life-size or larger detail |
| Tilt-shift | Variable | Miniaturize effect, plane of focus control |
| Fisheye | 8–15mm | 180° hemispheric distortion |
| Anamorphic | Variable | Horizontal lens flares, wide bokeh ovals |

### Perspective / Angle

| Angle | Description | Effect |
|-------|-------------|--------|
| Eye-level | Camera at subject's eye height | Neutral, natural, relatable |
| Low-angle | Camera below subject, looking up | Subject appears powerful, imposing |
| High-angle | Camera above, looking down | Subject appears small, vulnerable |
| Bird's-eye / top-down | Directly overhead | Map-like, pattern emphasis |
| Worm's-eye | Extreme low, looking straight up | Dramatic scale, architectural |
| Dutch angle / canted | Tilted frame (horizon not level) | Unease, disorientation, tension |
| Over-the-shoulder (OTS) | Behind character, looking at scene/person | POV proximity, conversation |
| POV shot | From inside character's eyes | First-person immersion |
| Three-quarter angle | 45° from front | Classic portrait angle |

### Framing

| Framing Term | Description |
|-------------|-------------|
| Rule of thirds | Subject at 1/3 or 2/3 horizontal/vertical line |
| Centered / symmetrical | Subject perfectly centered |
| Negative space | Empty area to balance or allow text |
| Frame within a frame | Subject seen through doorway, window, arch |
| Leading lines | Roads, railings, rivers draw eye to subject |
| Tight crop | Subject fills frame with minimal background |
| Loose composition | Subject small, environment prominent |

### Depth of Field

| DOF Term | Description | Example Prompt Fragment |
|---------|-------------|------------------------|
| Shallow DOF | Subject sharp, background blurred (bokeh) | "f/1.4 aperture, beautiful bokeh background" |
| Deep DOF | Everything sharp | "deep focus, f/22, everything sharp front to back" |
| Rack focus | Focus shifts from background to foreground (or reverse) | "rack focus from the distant mountain to the flower in the foreground" |
| Tilt-shift | Selective focus plane | "tilt-shift lens effect, miniaturized scene" |
| Lensbaby effect | Swirly bokeh, selective focus | "Lensbaby swirly bokeh on subject" |

### Natural Lighting

From [Google official developer blog](https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/) and [Veo prompt guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide):

| Type | Example Prompt Fragment | Quality |
|------|------------------------|---------|
| Golden hour | "soft golden hour light streaming through west-facing windows" | Warm, directional, flattering |
| Blue hour | "cool blue hour light just after sunset, city lights beginning to glow" | Cool, melancholic, transitional |
| Midday sun | "harsh overhead midday sunlight, deep shadows directly below" | High-contrast, dramatic |
| Overcast / diffused | "soft overcast daylight, even diffused light, no shadows" | Soft, neutral, even |
| Moonlight | "cool blue-white moonlight, long soft shadows" | Ethereal, low-level, cool |
| Sunrise backlight | "warm sunrise backlight, subject silhouetted with golden rim" | Silhouette, romantic |
| Window light | "soft window light from the north, gentle directional fill" | Studio-quality natural |
| Forest light | "dappled light through a forest canopy, moving leaf shadows" | Organic, dreamy |
| Storm light | "dramatic pre-storm sky, greenish cast, high contrast" | Threatening, cinematic |

### Studio Lighting

| Setup | Description | Effect |
|-------|-------------|--------|
| Three-point lighting | Key + fill + backlight | Professional, clean, standard broadcast |
| Softbox | Large diffused light source | Soft, even, shadowless |
| Ring light | Circular light around lens | Even, catchlights in eyes, beauty look |
| Butterfly / Paramount | Light directly above, casting butterfly shadow under nose | Classic Hollywood glamour |
| Rembrandt | One-sided light creating triangle of light on shadowed cheek | Dramatic, portrait classic |
| Split lighting | Exactly half face lit, half shadow | Dramatic, high-contrast |
| Rim / edge lighting | Light from behind, edges subject | Separation from background |
| Broad lighting | Key light on wider side of face | Opens up face, flatters |
| Short lighting | Key light on narrow side of face | Slims face, dramatic |

### Cinematic Lighting

| Type | Description | Example Fragment |
|------|-------------|-----------------|
| Film noir | Single overhead or side source, deep cast shadows, high contrast | "classic film noir lighting, single overhead source, pools of shadow" |
| High-key | Very bright, minimal shadows, flat | "high-key studio lighting, minimal shadows, bright and airy" |
| Low-key | Predominantly dark, small lit areas | "low-key lighting, deep shadows, small area of focused light" |
| Chiaroscuro | Extreme contrast between light and dark areas | "dramatic chiaroscuro lighting, Caravaggio-style" |
| Silhouette | Subject is dark against bright background | "backlit silhouette against a burning orange sunset" |
| Volumetric | Visible light rays through atmosphere | "volumetric lighting, god rays through dusty air" |

### Stylized Lighting

| Type | Example Fragment |
|------|----------------|
| Neon | "magenta neon sign casting colored light across wet pavement" |
| Bioluminescence | "glowing bioluminescent organisms lighting an underwater cave in blue-green" |
| Candlelight | "flickering warm candlelight, intimate close-up" |
| Fire | "crackling campfire lighting, orange-red directional light from below" |
| LED/RGB | "RGB LED strips casting colored shadows, gaming setup aesthetic" |
| Holographic | "cool holographic blue projection light, translucent" |
| Blacklight/UV | "UV blacklight, fluorescent colors glowing" |

### Color Temperature

| Temperature | Kelvin | Visual Effect | Example Context |
|-------------|--------|---------------|----------------|
| Candlelight | 1800K | Deep orange-amber | Intimate, historical |
| Incandescent | 2700K | Warm yellow | Home interior, cozy |
| Early sunrise | 3000K | Orange-warm | Golden hour |
| Studio tungsten | 3200K | Warm white | Classic film look |
| Neutral/daylight | 5500K | Natural white | Outdoor midday |
| Overcast sky | 6500K | Slightly cool | Cloudy day |
| Blue sky shade | 8000K | Cool blue | Open sky shade |
| Clear blue sky | 10000K | Intense blue | Arctic, high altitude |

### Color Palette Keywords

| Palette | Keywords |
|---------|---------|
| Warm | warm amber tones, golden hour palette, autumnal oranges and reds, earthy terracotta |
| Cool | cool blue-grey, desaturated steel palette, icy silver and white |
| Neutral | muted earth tones, natural ochres and greys, organic neutral palette |
| High contrast | stark black and white, bold complementary colors |
| Pastel | soft pastels, muted pinks and lavenders, chalky tones |
| Neon/Vibrant | electric neon palette, vivid saturated colors, fluorescent accents |
| Monochrome | monochromatic blue, sepia monochrome, green tinted monochrome |
| Film grade | teal and orange Hollywood grade, Kodachrome warmth, cross-processed |

---

## 8. Text Rendering

### Why Nano Banana Excels at Text

This is one of the most important architectural advantages of the unified transformer approach:

**Diffusion models (SD, MJ, DALL-E 2):**
- Text description is encoded through CLIP or a similar text encoder
- CLIP produces a fixed 512-dimensional vector
- Individual character information is compressed and often lost
- Result: garbled, misspelled, or nonsensical text in generated images

**Nano Banana:**
- Processes the full prompt in a 256K token context window
- Each letter, word, and phrase is tokenized and attended to directly
- The model "reads" the text to be generated as a semantic token stream
- Result: accurate, stylizable, multi-language text in complex compositions

([ZenML analysis of Gemini 2.5 Flash architecture](https://www.zenml.io/llmops-database/native-image-generation-with-multimodal-context-in-gemini-2-5-flash))

### How to Prompt Text

1. **Use quotation marks** to clearly delineate the exact text to render:
   ```
   A wooden sign above a tavern door that reads "The Rusty Anchor"
   ```

2. **Specify the medium** so the model knows how text should be styled:
   | Medium | Example |
   |--------|---------|
   | Sign | "a chalkboard sign that reads..." |
   | Label | "a hand-typed label on a jar that reads..." |
   | Banner | "a hung banner printed with the text..." |
   | Logo | "a circular logo badge with the text..." |
   | Neon | "neon tube letters spelling..." |
   | Graffiti | "graffiti-style spray-painted letters reading..." |
   | Printed | "bold printed text on a magazine cover..." |
   | Handwritten | "handwritten in cursive ink..." |
   | Engraved | "deeply engraved letters in stone..." |

3. **Specify font character** if important:
   - "serif font", "sans-serif", "script/cursive", "monospace", "display/decorative"
   - "bold", "italic", "all-caps"

4. **Specify placement** if needed:
   - "centered on the sign", "positioned in the lower-left", "wrapping around the circular logo edge"

5. **For multiple distinct text elements**, list them individually:
   ```
   A coffee shop menu board with three sections:
   - "ESPRESSO" as the header in bold chalk letters
   - The items listed below: "Americano $3 | Latte $4.50 | Cold Brew $5"  
   - A footer note in smaller text: "Oat milk +$0.75"
   ```

### Multi-Language Text Rendering

Nano Banana supports text rendering in the following 15 languages ([Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation)):

| Code | Language |
|------|---------|
| EN | English |
| ar-EG | Arabic (Egyptian) |
| de-DE | German |
| es-MX | Spanish (Mexican) |
| fr-FR | French |
| hi-IN | Hindi |
| id-ID | Indonesian |
| it-IT | Italian |
| ja-JP | Japanese |
| ko-KR | Korean |
| pt-BR | Portuguese (Brazilian) |
| ru-RU | Russian |
| ua-UA | Ukrainian |
| vi-VN | Vietnamese |
| zh-CN | Chinese (Simplified) |

**Example — Japanese sign:**
```
A ramen restaurant facade in Shinjuku at night, with a traditional暖簾 (noren curtain) 
hanging in the doorway printed with the kanji "拉麺" in bold black ink. 
Warm orange light spills from inside onto the wet sidewalk. Cinematic, 35mm film look.
```

### Tips from Official Docs

- Write the exact text in quotation marks: `"text goes here"`
- For multi-line text, describe the layout: `"two lines, first line reads 'OPEN', second line reads 'WELCOME'"`
- For stylized text (e.g., vintage poster): describe both the text AND its visual treatment in the same phrase
- Use the official phrase `"include the text [X] in the image"` explicitly when the LLM layer might otherwise suppress text generation

### Limitations

- Very long strings of text (50+ characters) with very small rendered size can produce errors
- Highly stylized handwriting remains the hardest category (cursive/calligraphy can have errors)
- RTL languages (Arabic, Hebrew) require explicit mention of directionality in complex layouts
- Text accuracy improves with Nano Banana Pro over Nano Banana 2, which improves over the original Nano Banana

---

## 9. Image Editing & Multi-Image Composition

### Conversational Editing

Nano Banana maintains the previous image in context across conversation turns. Send follow-up prompts to modify previous generations without re-describing the whole scene:

```python
# Turn 1: Generate image
client.chats.create(model="gemini-3.1-flash-image-preview", config=...)
chat.send_message("A photorealistic portrait of a woman in a red dress standing in a forest.")

# Turn 2: Edit specific element
chat.send_message("Change the dress color to deep navy blue.")

# Turn 3: Add element
chat.send_message("Add a golden crown on her head.")

# Turn 4: Adjust lighting
chat.send_message("Make the lighting more dramatic — add deep shadows from the right side.")
```

Each turn modifies the accumulated image state. You do not need to re-describe unchanged elements.

### Upload Image + Describe Changes

Send an existing image (your own photo or a previous generation) plus a text instruction:

```python
response = client.models.generate_content(
    model="gemini-3.1-flash-image-preview",
    contents=[
        "Remove the car in the background and replace it with a bicycle leaning against the wall.",
        Image.open("my_photo.jpg")
    ]
)
```

Common edit operations:
- "Change [element] to [new version]"
- "Remove [element] from the scene"
- "Add [element] in [position]"
- "Change the style to [art style]"
- "Make the lighting [warmer/cooler/more dramatic]"
- "Extend the image [direction] to show more of the scene"

### Multi-Image Composition: Up to 14 Reference Images

The Gemini 3 image models can ingest multiple reference images and compose a new scene incorporating elements from all of them. ([Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation))

| Model | Total Refs | Object Images | Character Images |
|-------|-----------|---------------|-----------------|
| Nano Banana 2 (`gemini-3.1-flash-image-preview`) | Up to 14 | Up to 10 | Up to 4 |
| Nano Banana Pro (`gemini-3-pro-image-preview`) | Up to 14 | Up to 6 | Up to 5 |
| Nano Banana (`gemini-2.5-flash-image`) | Best with up to 3 | — | — |

**Object references**: Products, props, environments, vehicles, textures — the model renders these with high visual fidelity to the reference.

**Character references**: People/characters whose appearance should be maintained consistently. The model tracks facial features, body type, and distinguishing characteristics.

```python
response = client.models.generate_content(
    model="gemini-3.1-flash-image-preview",
    contents=[
        "An office group photo of these people, they are making funny faces.",
        Image.open('person1.png'),
        Image.open('person2.png'),
        Image.open('person3.png'),
        Image.open('person4.png'),
        Image.open('person5.png'),
    ],
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
        image_config=types.ImageConfig(aspect_ratio="5:4", image_size="2K")
    )
)
```

### Character Consistency Across Multiple Generations

Nano Banana Pro can maintain up to **5 characters** with consistent appearance across multiple separate generation calls. The model tracks:
- Facial features and structure
- Hair style and color
- Body type and height proportions
- Distinguishing marks or accessories
- Character's overall visual identity

To use this: provide the same character reference image(s) in each generation call and describe the character by name or consistent descriptor across prompts.

### Style Transfer

Provide a photograph and request it be rendered in a different artistic style:

```
Template:
Transform the provided photograph of [subject] into the artistic style of [artist/art style].
Preserve the original composition but render it with [description of stylistic elements].
```

```
Example:
Transform the provided photograph of a modern city street at night into the artistic 
style of Vincent van Gogh's 'Starry Night'. Preserve the original composition of 
buildings and cars, but render all elements with swirling, impasto brushstrokes and 
a dramatic palette of deep blues, cobalt, and luminous yellows.
```

### Thought Signatures: Multi-Turn Consistency

Thought Signatures are **encrypted reasoning context blobs** returned by the model after each generation. For multi-turn image editing with Nano Banana Pro, Google officially recommends passing them back in subsequent requests. ([Google Cloud Best Practices](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-best-practices))

**What they do**: Preserve the model's reasoning state — composition decisions, style choices, element placement logic — across API calls.

**How to pass them**:
1. After generation, extract thought signature from the response
2. In the next request, include it in `inline_data` image parts
3. The model re-anchors its reasoning to the previous state

Thought signatures are required in `inline_data` image parts, as the **first non-thought text part** after images. They must be passed back exactly.

### Step-by-Step Instructions for Complex Edits

For complex modifications, break the request into explicit sequential steps:

```
Step 1: Keep the background forest scene exactly as it is.
Step 2: Remove the existing figure from the foreground.
Step 3: Add a new figure: a young woman in a Victorian-era gown, standing in the same 
         position, facing left.
Step 4: Ensure the lighting on the new figure matches the dappled forest light in 
         the background.
```

This approach dramatically reduces hallucination and ensures each step is executed in order.

---

## 10. Aspect Ratio & Resolution — Complete Reference

> **How to specify**: Via `image_config.aspect_ratio` and `image_config.image_size` API parameters. NOT via prompt text.
> **Default**: 1:1 at 1K.

### Nano Banana 2 (`gemini-3.1-flash-image-preview`) — 14 Aspect Ratios × 4 Resolutions

| Aspect Ratio | 512px (0.5K) | 1K (1024px) | 2K (2048px) | 4K (4096px) |
|-------------|-------------|------------|------------|------------|
| **1:1** | 512×512 | 1024×1024 | 2048×2048 | 4096×4096 |
| **1:4** | 256×1024 | 512×2048 | 1024×4096 | 2048×8192 |
| **1:8** | 192×1536 | 384×3072 | 768×6144 | 1536×12288 |
| **2:3** | 424×632 | 848×1264 | 1696×2528 | 3392×5056 |
| **3:2** | 632×424 | 1264×848 | 2528×1696 | 5056×3392 |
| **3:4** | 448×600 | 896×1200 | 1792×2400 | 3584×4800 |
| **4:1** | 1024×256 | 2048×512 | 4096×1024 | 8192×2048 |
| **4:3** | 600×448 | 1200×896 | 2400×1792 | 4800×3584 |
| **4:5** | 464×576 | 928×1152 | 1856×2304 | 3712×4608 |
| **5:4** | 576×464 | 1152×928 | 2304×1856 | 4608×3712 |
| **8:1** | 1536×192 | 3072×384 | 6144×768 | 12288×1536 |
| **9:16** | 384×688 | 768×1376 | 1536×2752 | 3072×5504 |
| **16:9** | 688×384 | 1376×768 | 2752×1536 | 5504×3072 |
| **21:9** | 792×168 | 1584×672 | 3168×1344 | 6336×2688 |

**Token costs**: 512px = 747 tokens | 1K = 1120 tokens | 2K = 1680 tokens | 4K = 2520 tokens (flat across aspect ratios)

*Note: 1:4, 4:1, 1:8, 8:1 are new in Nano Banana 2 and not available in Nano Banana (original) or Nano Banana Pro.*

([Google AI Developer Docs](https://ai.google.dev/gemini-api/docs/image-generation))

---

### Nano Banana Pro (`gemini-3-pro-image-preview`) — 10 Aspect Ratios × 3 Resolutions

| Aspect Ratio | 1K (1024px) | Tokens | 2K (2048px) | Tokens | 4K (4096px) | Tokens |
|-------------|------------|--------|------------|--------|------------|--------|
| **1:1** | 1024×1024 | 1120 | 2048×2048 | 1120 | 4096×4096 | 2000 |
| **2:3** | 848×1264 | 1120 | 1696×2528 | 1120 | 3392×5056 | 2000 |
| **3:2** | 1264×848 | 1120 | 2528×1696 | 1120 | 5056×3392 | 2000 |
| **3:4** | 896×1200 | 1120 | 1792×2400 | 1120 | 3584×4800 | 2000 |
| **4:3** | 1200×896 | 1120 | 2400×1792 | 1120 | 4800×3584 | 2000 |
| **4:5** | 928×1152 | 1120 | 1856×2304 | 1120 | 3712×4608 | 2000 |
| **5:4** | 1152×928 | 1120 | 2304×1856 | 1120 | 4608×3712 | 2000 |
| **9:16** | 768×1376 | 1120 | 1536×2752 | 1120 | 3072×5504 | 2000 |
| **16:9** | 1376×768 | 1120 | 2752×1536 | 1120 | 5504×3072 | 2000 |
| **21:9** | 1584×672 | 1120 | 3168×1344 | 1120 | 6336×2688 | 2000 |

*No 512px tier. No 1:4, 4:1, 1:8, 8:1 ratios.*

---

### Nano Banana (`gemini-2.5-flash-image`) — 10 Aspect Ratios × 1 Resolution

| Aspect Ratio | Resolution | Tokens |
|-------------|------------|--------|
| **1:1** | 1024×1024 | 1290 |
| **2:3** | 832×1248 | 1290 |
| **3:2** | 1248×832 | 1290 |
| **3:4** | 864×1184 | 1290 |
| **4:3** | 1184×864 | 1290 |
| **4:5** | 896×1152 | 1290 |
| **5:4** | 1152×896 | 1290 |
| **9:16** | 768×1344 | 1290 |
| **16:9** | 1344×768 | 1290 |
| **21:9** | 1536×672 | 1290 |

*1K only. No other resolution tiers.*

---

### Aspect Ratio Use Cases

| Aspect Ratio | Primary Use Cases |
|-------------|-----------------|
| 1:1 | Instagram feed, profile photos, product square shots |
| 16:9 | YouTube thumbnails, desktop wallpapers, presentations, widescreen video stills |
| 9:16 | TikTok, Instagram Reels, Stories, vertical mobile content |
| 4:3 | Classic photography, print photos, older display formats |
| 3:4 | Portrait orientation for prints, A4 proportion |
| 2:3 | Poster format (standard movie poster), portrait photos |
| 3:2 | Classic DSLR sensor ratio, landscape photography |
| 4:5 | Instagram portrait (preferred over 9:16 for feed) |
| 5:4 | Group photography, medium format |
| 21:9 | Ultrawide desktop wallpaper, cinematic stills |
| 4:1 | Banner ads, website header strips |
| 8:1 | Ultra-panoramic banners |
| 1:4 | Vertical strip banners, elevator digital signage |
| 1:8 | Ultra-tall vertical format |

---

## 11. API Reference — Image

### Model IDs

| Model Name | API ID | Endpoint Base |
|-----------|--------|---------------|
| Nano Banana | `gemini-2.5-flash-image` | `generativelanguage.googleapis.com/v1beta` |
| Nano Banana 2 | `gemini-3.1-flash-image-preview` | `generativelanguage.googleapis.com/v1beta` |
| Nano Banana Pro | `gemini-3-pro-image-preview` | `generativelanguage.googleapis.com/v1beta` |

### REST Endpoint

```
POST https://generativelanguage.googleapis.com/v1beta/models/{MODEL_ID}:generateContent
Header: x-goog-api-key: $GEMINI_API_KEY
Content-Type: application/json
```

### GenerateContentConfig Parameters

| Parameter | Type | Values | Notes |
|-----------|------|--------|-------|
| `response_modalities` | list | `['TEXT', 'IMAGE']` or `['IMAGE']` | Default: `['TEXT', 'IMAGE']` |
| `image_config` | object | See ImageConfig below | Resolution and aspect ratio |
| `tools` | list | `[{"google_search": {}}]` | Enable Search grounding |
| `thinking_config` | object | See ThinkingConfig below | Control thinking behavior |

### ImageConfig Parameters

| Parameter | Type | Values | Notes |
|-----------|------|--------|-------|
| `aspect_ratio` | string | `"1:1"`, `"1:4"`, `"1:8"`, `"2:3"`, `"3:2"`, `"3:4"`, `"4:1"`, `"4:3"`, `"4:5"`, `"5:4"`, `"8:1"`, `"9:16"`, `"16:9"`, `"21:9"` | Default: `"1:1"`. `"1:4"`, `"4:1"`, `"1:8"`, `"8:1"` are Nano Banana 2 only. |
| `image_size` | string | `"512"`, `"1K"`, `"2K"`, `"4K"` | Default: `"1K"`. `"512"` is Nano Banana 2 only. Uppercase 'K' required. |

### ThinkingConfig Parameters

| Parameter | Type | Values | Notes |
|-----------|------|--------|-------|
| `thinking_level` | string | `"minimal"`, `"high"` | Default: `"minimal"`. Only on Nano Banana 2. |
| `include_thoughts` | bool | `true` / `false` | Whether to return thought content in response. Thinking tokens always billed. |

### Code Examples

#### Basic Text-to-Image (Python)

```python
from google import genai
from google.genai import types
from PIL import Image

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.1-flash-image-preview",
    contents=["A photorealistic close-up of a red maple leaf on wet pavement, golden hour lighting."],
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
        image_config=types.ImageConfig(
            aspect_ratio="4:3",
            image_size="2K"
        )
    )
)

for part in response.parts:
    if part.text is not None:
        print(part.text)
    elif part.inline_data is not None:
        image = part.as_image()
        image.save("output.png")
```

#### Basic Text-to-Image (JavaScript)

```javascript
import { GoogleGenAI } from "@google/genai";
import * as fs from "node:fs";

const ai = new GoogleGenAI({});

const response = await ai.models.generateContent({
    model: "gemini-3.1-flash-image-preview",
    contents: "A photorealistic close-up of a red maple leaf on wet pavement, golden hour lighting.",
    config: {
        responseModalities: ['TEXT', 'IMAGE'],
        imageConfig: {
            aspectRatio: "4:3",
            imageSize: "2K"
        }
    }
});

for (const part of response.candidates[0].content.parts) {
    if (part.text) {
        console.log(part.text);
    } else if (part.inlineData) {
        const buffer = Buffer.from(part.inlineData.data, "base64");
        fs.writeFileSync("output.png", buffer);
    }
}
```

#### Basic Text-to-Image (REST / curl)

```bash
curl -s -X POST \
  "https://generativelanguage.googleapis.com/v1beta/models/gemini-3.1-flash-image-preview:generateContent" \
  -H "x-goog-api-key: $GEMINI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "contents": [{"parts": [{"text": "A photorealistic close-up of a red maple leaf on wet pavement."}]}],
    "generationConfig": {
      "responseModalities": ["TEXT", "IMAGE"],
      "imageConfig": {
        "aspectRatio": "4:3",
        "imageSize": "2K"
      }
    }
  }'
```

#### Multi-Image Composition (Python)

```python
from google import genai
from google.genai import types
from PIL import Image

client = genai.Client()

response = client.models.generate_content(
    model="gemini-3.1-flash-image-preview",
    contents=[
        "An office group photo of these people, they are making funny faces.",
        Image.open('person1.png'),
        Image.open('person2.png'),
        Image.open('person3.png'),
        Image.open('person4.png'),
        Image.open('person5.png'),
    ],
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
        image_config=types.ImageConfig(
            aspect_ratio="5:4",
            image_size="2K"
        )
    )
)

for part in response.parts:
    if part.text is not None:
        print(part.text)
    elif (image := part.as_image()):
        image.save("group_photo.png")
```

#### Thinking Mode at High Level (Go)

```go
model := client.GenerativeModel("gemini-3.1-flash-image-preview")
model.GenerationConfig = &pb.GenerationConfig{
    ResponseModalities: []pb.ResponseModality{genai.Image},
    ThinkingConfig: &pb.ThinkingConfig{
        ThinkingLevel:   "High",
        IncludeThoughts: true,
    },
}

prompt := "A futuristic city built inside a giant glass bottle floating in space"
resp, _ := model.GenerateContent(ctx, genai.Text(prompt))

for _, part := range resp.Candidates[0].Content.Parts {
    if part.Thought {
        continue // Skip thought images
    }
    if img, ok := part.(genai.ImageData); ok {
        os.WriteFile("image.png", img.Data, 0644)
    }
}
```

#### Google Search Grounding (Python)

```python
from google import genai
from google.genai import types

client = genai.Client()

chat = client.chats.create(
    model="gemini-3.1-flash-image-preview",
    config=types.GenerateContentConfig(
        response_modalities=['TEXT', 'IMAGE'],
        tools=[{"google_search": {}}]
    )
)

response = chat.send_message(
    "Visualize the current weather forecast for the next 5 days in San Francisco as a clean, modern weather chart."
)
```

#### Image Search Grounding (Nano Banana 2 Only — Go)

```go
model.Tools = []*pb.Tool{
    {
        GoogleSearch: &pb.GoogleSearch{
            SearchTypes: &pb.SearchTypes{
                WebSearch:   &pb.WebSearch{},
                ImageSearch: &pb.ImageSearch{},
            },
        },
    },
}
model.GenerationConfig = &pb.GenerationConfig{
    ResponseModalities: []pb.ResponseModality{genai.Image},
}

prompt := "A detailed painting of a Timareta butterfly resting on a flower"
resp, _ := model.GenerateContent(ctx, genai.Text(prompt))
```

### Response Modalities

| Modality Setting | Returns | Use Case |
|-----------------|---------|----------|
| `['TEXT', 'IMAGE']` | Both text commentary and images | Default; model explains its choices |
| `['IMAGE']` | Images only, no text | Production pipelines; no commentary overhead |

### Token Costs Per Resolution (Summary)

| Model | 512px | 1K | 2K | 4K |
|-------|-------|----|----|-----|
| Nano Banana 2 | 747 | 1120 | 1680 | 2520 |
| Nano Banana Pro | N/A | 1120 | 1120 | 2000 |
| Nano Banana | N/A | 1290 | N/A | N/A |

> **Note**: Thinking tokens are billed on top of image tokens, even when `include_thoughts=False`.

### Batch API

For high-volume production use cases, the Batch API provides:
- Higher rate limits than standard API
- Up to 24-hour turnaround window
- Same model capabilities
- Cost savings for large-scale generation

Use when generating hundreds or thousands of images in a pipeline context.

---

## 12. Video Prompting — Fundamentals (Veo)

### Architecture: Latent Diffusion Transformer

Veo uses a **latent diffusion transformer** architecture. Unlike Nano Banana's unified image+text transformer, Veo:
1. Compresses video data into a lower-dimensional latent space
2. Adds noise during training to learn video statistical structure
3. Reverses the noise process during generation, guided by text/image input
4. The transformer component maintains temporal consistency across frames

The result is strong physics understanding (fluid dynamics, lighting, motion) and temporal coherence across the video clip. ([MindStudio – What Is Google Veo 2](https://www.mindstudio.ai/blog/what-is-google-veo-2-video-generation/))

### Model Capabilities Comparison

| Capability | Veo 2 | Veo 3 | Veo 3.1 |
|-----------|-------|-------|---------|
| Resolution | 720p default | 720p / 1080p | 720p / 1080p / **4K** |
| Duration | 5–8 sec | 4, 6, or 8 sec | 4, 6, or 8 sec |
| Native audio | ✗ | ✓ (SFX, ambient, dialogue) | ✓ |
| `enhancePrompt` | ✓ (Veo 2 only) | ✗ | ✗ |
| `generateAudio` | ✗ | ✓ | ✓ |
| `negativePrompt` | ✗ | ✗ | ✓ |
| Reference images | Exp model only | ✗ | ✓ (3 asset + 1 style) |
| Mask editing | ✗ | ✗ | ✓ |
| First+last frame interp. | ✗ | ✗ | ✓ |
| `resolution` param | ✗ | ✓ | ✓ |
| Aspect ratios | 16:9, 9:16 | 16:9, 9:16 | 16:9, 9:16 |

### How Video Prompts Differ from Image Prompts

| Dimension | Image Prompts | Video Prompts |
|-----------|--------------|--------------|
| Duration of scene | Static, timeless | 4–8 seconds max |
| Primary concern | Composition and aesthetics | Motion, action, camera movement |
| Camera | Static descriptor | Explicit camera movements drive the shot |
| Audio | Not applicable | SFX, ambient, dialogue (Veo 3+) |
| Complexity | Many elements OK | Keep to one shot, one action, one camera move |
| Temporal logic | Irrelevant | Describe what changes over time |

### Core Principle: One Shot, One Action, One Camera Move

Unlike image prompts where you can stack multiple elements, video prompts work best when each clip is a single focused idea. ([fal.ai Veo 2 Guide](https://blog.fal.ai/mastering-video-generation-with-veo-2-a-comprehensive-guide/), [Shep Bryan Veo 2 Guide](https://www.shepbryan.com/blog/google-veo-2-video-prompt-guide))

**Works:**
```
A slow dolly-in on an elderly man's face as he reads a letter by candlelight, 
his expression shifting from neutral to quiet devastation.
```

**Doesn't work well:**
```
A man reading a letter while his daughter plays piano in the background, his wife 
cooks dinner, their dog runs around, a cat sits on the windowsill, it's raining outside, 
and there are children laughing in the street.
```

### Prompt Enhancement for Veo 2

The `enhancePrompt` parameter (default `true`) in Veo 2 models uses Gemini to expand and enhance your video prompt before passing it to the video model. This mirrors Nano Banana's prompt enhancement behavior.

To disable: set `enhancePrompt: false` in your request parameters.

Note: `enhancePrompt` is only supported by Veo 2 models:
- `veo-2.0-generate-001`
- `veo-2.0-generate-preview`  
- `veo-2.0-generate-exp`

### Audio Descriptions in Separate Sentences

For Veo 3+, Google officially recommends using **separate sentences** in your prompt to describe audio elements. ([Google Cloud Veo Prompt Guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide))

**Example:**
```
A medium shot of a detective sitting alone in a dimly lit office, rain streaming 
down the window behind him, slowly pouring whiskey into a glass. 
The only sounds are the rhythmic ticking of a wall clock, rain hitting the glass, 
and the quiet glug of whiskey pouring.
```

### Positive Language for Video

Use positive language in video prompts. List unwanted elements directly rather than "no X" or "don't include X". The exception is Veo 3.1's `negativePrompt` parameter, which accepts direct terms. ([Google Cloud Veo Prompt Guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide))

| Avoid | Use Instead |
|-------|-------------|
| "no urban background" | List in negativePrompt: `"urban background, man-made structures"` |
| "don't show people" | Keep prompt subject-focused on non-human subjects |
| "without any text" | Describe a scene where text naturally wouldn't appear |

---

## 13. Video Prompting — Component Deep Dive

All components drawn directly from the [official Google Cloud Veo prompt guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide).

### Subject

People, animals, objects, or combinations:

| Category | Example Descriptors |
|----------|---------------------|
| People | "a seasoned detective", "a joyful baker with flour-dusted hands", "an elderly woman in a saree", "a group of diverse friends" |
| Animals/Creatures | "a playful Golden Retriever puppy", "a majestic bald eagle", "a miniature dragon with iridescent scales", "a wise ancient talking tree" |
| Objects | "a vintage typewriter", "a 1960s muscle car", "a glowing orb", "a weathered pirate ship" |
| Combinations | "A group of diverse friends laughing around a campfire while a curious fox watches from the shadows" |

### Action Verbs

| Category | Examples |
|----------|---------|
| Basic movements | walking, running, jumping, flying, swimming, dancing, spinning, falling, standing still, sitting |
| Interactions | talking, laughing, arguing, hugging, fighting, playing a game, cooking, building, writing, reading, observing |
| Emotional expressions | smiling, frowning, surprise, concentrating deeply, appearing thoughtful, showing excitement, crying |
| Subtle actions | a gentle breeze ruffling hair, leaves rustling, a subtle nod, fingers tapping impatiently, eyes blinking slowly |
| Transformations | a flower blooming in fast-motion, ice melting, a city skyline developing over time |

### Scene / Context

| Dimension | Examples |
|-----------|---------|
| Interior | cozy living room with crackling fireplace, sterile futuristic laboratory, cluttered artist's studio, grand ballroom, dusty attic |
| Exterior | sun-drenched tropical beach, misty ancient forest, bustling futuristic cityscape at night, desolate alien planet |
| Time | golden hour, midday sun, twilight, deep night, pre-dawn |
| Weather | clear blue sky, overcast and gloomy, heavy thunderstorm with visible lightning, gentle snowfall, swirling fog |
| Historical period | medieval castle courtyard, roaring 1920s jazz club, cyberpunk alleyway |
| Atmospheric details | floating dust motes in a sunbeam, shimmering heat haze, reflections on wet pavement |

### Camera Angles — All 13 Official

From the [Google Cloud Veo prompt guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide):

| Angle | Description | Example Prompt Fragment |
|-------|-------------|------------------------|
| **Eye-level shot** | Neutral human height perspective | `"eye-level shot of a woman sipping tea in a café"` |
| **Low-angle shot** | Below subject, looking up — makes subject powerful/imposing | `"low-angle tracking shot of a superhero landing"` |
| **High-angle shot** | Above subject, looking down — makes subject small/vulnerable | `"high-angle shot of a child lost in a crowd"` |
| **Bird's-eye view / top-down** | Directly from above, map-like | `"bird's-eye view of a vast intricate maze with a lone figure in red"` |
| **Worm's-eye view** | Very low, looking straight up | `"worm's-eye view of towering skyscrapers against a grey sky"` |
| **Dutch angle / canted angle** | Tilted horizon, creates unease/disorientation | `"dutch angle shot of a character running down a hallway"` |
| **Close-up (CU)** | Tight frame on face or significant detail | `"close-up of a character's determined eyes"` |
| **Extreme close-up (ECU)** | Isolates tiny detail | `"extreme close-up of a drop of water landing on a leaf"` |
| **Medium shot (MS)** | Waist up, balances detail and context | `"medium shot of two people in tense conversation"` |
| **Full shot / long shot** | Entire subject head-to-toe with environment | `"full shot of a dancer performing on an empty stage"` |
| **Wide shot / establishing shot** | Subject in broad environment | `"wide establishing shot of a lone cabin in a snowy landscape"` |
| **Over-the-shoulder (OTS)** | Behind one person, looking at other person or object | `"over-the-shoulder shot during a tense negotiation"` |
| **Point-of-view (POV) shot** | From character's direct visual perspective | `"POV shot as someone rides a rollercoaster, hands raised"` |

### Camera Movements — All 12 Official

From the [Google Cloud Veo prompt guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide):

| Movement | Description | Example Prompt |
|----------|-------------|----------------|
| **Static / fixed** | Camera remains completely still | `"static shot of an empty swing moving gently in the breeze"` |
| **Pan (left/right)** | Rotates horizontally from fixed position | `"slow pan left across a city skyline at dusk, revealing the full skyline"` |
| **Tilt (up/down)** | Rotates vertically from fixed position | `"tilt down from the character's shocked face to the revealing letter in their hands"` |
| **Dolly (in/out)** | Camera physically moves closer or further | `"dolly out from the character to emphasize their isolation in the vast desert"` |
| **Truck (left/right)** | Camera moves horizontally parallel to subject | `"truck right, following a character as they walk along a busy sidewalk"` |
| **Pedestal (up/down)** | Camera moves vertically while maintaining level | `"pedestal up to reveal the full height of an ancient towering tree"` |
| **Zoom (in/out)** | Lens changes focal length | `"slow zoom in on a mysterious artifact on a table, filling the frame"` |
| **Crane shot** | Camera on crane, sweeping arcs or vertical | `"crane shot rising from street level to reveal a vast medieval battlefield"` |
| **Aerial / drone shot** | High altitude, smooth flying movement | `"sweeping aerial drone shot flying over a tropical island chain at dawn"` |
| **Handheld / shaky cam** | Less stable, intimate, urgent feel | `"handheld camera shot during a chaotic marketplace chase"` |
| **Whip pan** | Extremely fast pan that motion-blurs the transition | `"whip pan from one arguing character to the other's reaction"` |
| **Arc shot** | Camera moves in circular or semi-circular path around subject | `"arc shot circling slowly around a couple embracing in the rain"` |

**Example of a fully specified camera movement prompt:**
```
A slow, dramatic zoom in on a mysterious ancient compass lying on a dusty map. 
The camera starts wide, showing the map and a flickering candle, then smoothly zooms in 
until the intricate glowing symbols on the compass face fill the entire frame.
```

### Lens / Optical Effects

| Effect | Description | Example Fragment |
|--------|-------------|-----------------|
| Wide-angle lens | Exaggerated perspective, environmental context | `"wide-angle lens, distorted perspective"` |
| Telephoto lens | Compressed perspective, distant subject | `"telephoto lens compressing the crowd"` |
| Shallow depth of field | Bokeh background | `"shallow depth of field, soft bokeh behind subject"` |
| Deep depth of field | Everything sharp | `"deep focus, everything sharp front to back"` |
| Lens flare | Sun or light source creates flare artifact | `"anamorphic lens flares from the sunset"` |
| Rack focus | Focus shifts between foreground and background | `"rack focus from the foreground flower to the distant mountain"` |
| Fisheye lens effect | 180° hemispheric distortion | `"fisheye lens effect, extreme barrel distortion"` |
| Dolly zoom (vertigo effect) | Dolly out + zoom in simultaneously = surreal spatial effect | `"vertigo effect / dolly zoom on the character's face"` |

### Visual Style & Aesthetics

#### Tone / Mood Keywords

| Tone | Keywords |
|------|---------|
| Joyful | bright, vibrant, cheerful, uplifting, whimsical |
| Melancholic | somber, muted, slow, poignant, wistful |
| Thriller | dark, shadowy, quick cuts, thrilling, suspenseful |
| Tranquil | calm, tranquil, soft, gentle, meditative |
| Epic | sweeping, majestic, dramatic, awe-inspiring |
| Sci-fi/Tech | sleek, metallic, neon, technological, dystopian, utopian |
| Nostalgic | sepia, grainy, 1950s Americana, 1980s vaporwave |
| Romantic | soft focus, warm, intimate, dreamy |
| Horror | dark, unsettling, eerie, gory |

#### Artistic Style Keywords

| Style | Keywords |
|-------|---------|
| Cinematic realism | ultra-realistic, shot on 8K camera, cinematic film look, anamorphic widescreen |
| Film stock | shot on 35mm film, Super 8 film, 16mm film grain |
| Animation | Japanese anime style, classic Disney animation style, Pixar-like 3D animation |
| Stop-motion | claymation style, stop-motion animation |
| Cel/toon | cel-shaded animation |
| Art movements | in the style of Van Gogh, surrealist painting, Impressionistic, Art Deco design, Bauhaus aesthetic |
| Illustration | gritty graphic novel illustration, watercolor painting coming to life, charcoal sketch animation, blueprint schematic style |

#### Ambiance Keywords

| Ambiance | Keywords |
|---------|---------|
| Color | monochromatic black and white, vibrant saturated tropical colors, muted earthy tones, cool blue and silver futuristic palette, warm autumnal oranges and browns |
| Atmospheric | thick fog rolling across a moor, swirling desert sands, gentle falling snow, heat haze shimmering above asphalt, magical glowing particles in the air |
| Texture | rough-hewn stone walls, smooth polished chrome surfaces, soft velvety fabric, dewdrops clinging to a spiderweb, subsurface scattering on a translucent object |

### Temporal Elements

| Element | Examples |
|---------|---------|
| Pacing | "slow-motion", "fast-paced action", "time-lapse", "real-time" |
| Evolution | "a flower bud slowly unfurling over the clip", "a candle burning down slightly", "dawn breaking, sky gradually lightening" |
| Rhythm | "pulsating light synchronizing with implied music", "rhythmic repetitive movement" |

### Audio (Veo 3+ Only)

Audio is supported by `veo-3.0-generate-001` and later. Use `generateAudio: true` in the API parameters.

Google recommends using **separate sentences** for audio descriptions in the prompt.

| Category | Example Prompt Sentences |
|----------|--------------------------|
| Sound effects | `"The sound of a rotary phone ringing echoes in the empty room."` |
| Ambient noise | `"The sounds of city traffic and distant sirens fill the background."` `"Waves crash rhythmically on the shore."` `"The quiet hum of fluorescent office lighting."` |
| Dialogue | `"The man in the red hat says: 'Where is the rabbit?'"` `"A voiceover with a polished British accent speaks in a serious, urgent tone."` |
| Complex audio scene | `"The seasoned detective says: 'Your story has holes.' The nervous informant, sweating under a single bare bulb, replies: 'I'm telling you everything I know.' The only other sounds are the slow rhythmic ticking of a wall clock and the faint sound of rain against the window."` |

### Negative Prompts (Veo 3.1 Only)

Veo 3.1 supports a `negativePrompt` parameter. Provide items to exclude as a comma-separated list of direct terms:

**Correct format (Veo 3.1 `negativePrompt` parameter):**
```
"urban background, man-made structures, dark atmosphere, stormy weather, threatening imagery"
```

**Not recommended (in main prompt text):**
```
"no walls, don't include cars, without any buildings"
```

The official recommendation is to list unwanted elements directly rather than using "no" or "don't" phrasing even in the `negativePrompt` field. ([Google Cloud Veo Prompt Guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide))

---

## 14. Video Prompting — Templates

### Template 1: Text-to-Video Cinematic

```
[Camera movement] of [subject], [action], in [environment].
[Lighting description]. [Style/aesthetic].
[Optional: additional atmospheric detail].
[Optional audio sentence for Veo 3+.]
```

**Example 1 (Crystal Cave — from fal.ai):**
```
A cinematic tracking shot through a magical ice cave, massive crystalline icicles hanging 
from the ceiling, glowing with an ethereal blue light. The camera gracefully moves between 
the translucent formations, capturing the slow drips of water that create rainbow-like 
refractions. The scene has a dreamy, otherworldly quality with misty air and subtle particles 
floating in the beams of light.
```

**Example 2 (Epic Landscape):**
```
A sweeping aerial drone shot flying over a volcanic island chain at dawn, active lava flows 
visible on distant peaks, glowing orange against the dark ocean. The camera moves slowly 
forward, revealing more islands emerging from morning sea mist. Ultra-realistic, 8K 
cinematography. Deep ambient ocean sounds and distant volcanic rumble.
```

---

### Template 2: Image-to-Video

When animating from a still image, **describe motion — not appearance**. The model already sees the appearance from your image.

```
[Camera movement], [what moves in the scene and how], [atmospheric element that changes].
[Avoid describing static visual elements already visible in the image.]
```

**Example 1 (Portrait animation):**
```
Static camera. The woman's hair moves gently in a slow breeze. She blinks slowly and 
turns her head slightly to the left, lips parting as if about to speak. 
Soft light shimmer from the candles in the background.
```

**Example 2 (Landscape animation — from fal.ai):**
```
Create a video with a tracking drone view of a man driving a red convertible car 
in Palm Springs, 1970s, warm sunlight, long shadows.
```

---

### Template 3: Dialogue Scene (Veo 3+)

```
A [shot type] in [setting]. [Character 1 description], [action]. 
[Character 1] says: "[dialogue]". [Character 2 description] [reaction]. 
[Character 2] says: "[dialogue]". 
[Ambient audio description as a separate sentence.]
```

**Example 1 (Interrogation — from official docs):**
```
A medium shot in a dimly lit interrogation room. The seasoned detective says: 
"Your story has holes." The nervous informant, sweating under a single bare bulb, 
replies: "I'm telling you everything I know." The only other sounds are the slow, 
rhythmic ticking of a wall clock and the faint sound of rain against the window.
```

**Example 2 (Phone call — from fal.ai):**
```
A video with smooth motion that dollies in on a desperate man in a green trench coat, 
using a vintage rotary phone against a wall bathed in an eerie green neon glow. 
The camera starts from a medium distance, slowly moving closer to the man's face, 
revealing his frantic expression and the sweat on his brow as he urgently dials. 
The sound of the rotary dial clicking, muffled street noise, and the man's labored 
breathing fill the scene.
```

---

### Template 4: Nature / Landscape

```
[Camera movement], [subject/environment], [time of day/weather].
[Specific detail that makes it cinematic].
[Atmospheric audio for Veo 3+.]
```

**Example 1 (Waterfall — from fal.ai):**
```
Create a video with a smooth motion of a majestic Hawaiian waterfall within a lush 
rainforest. Focus on realistic water flow, detailed foliage, and natural lighting 
to convey tranquility. Capture the rushing water, misty atmosphere, and dappled 
sunlight filtering through the dense canopy.
```

**Example 2 (Snow Leopard — from fal.ai):**
```
Create a short 3D animated scene in a joyful cartoon style. A cute creature with 
snow leopard-like fur, large expressive eyes, and a friendly rounded form happily 
prances through a whimsical winter forest. The scene should feature rounded 
snow-covered trees, gentle falling snowflakes, and warm sunlight filtering through 
the branches.
```

---

### Template 5: Product Showcase

```
[Camera movement] revealing [product] on [surface/environment].
[Lighting description that emphasizes product qualities].
[Style: commercial photography aesthetic].
[Optional: brand/mood descriptor].
```

**Example 1 (Luxury watch):**
```
A slow dolly-in on a luxury mechanical watch resting on dark slate, face up, 
second hand ticking. Studio lighting with a single overhead softbox creates 
specular highlights on the case and crystal. Ultra-realistic commercial photography. 
The subtle tick of the mechanical movement is audible.
```

---

### Template 6: Action Sequence

```
[Shot type], [subject], [action verb + specific detail], [environment].
[Camera movement that follows or enhances the action]. [Style/aesthetic].
```

**Example 1 (Rally car — from LinkedIn/fal.ai synthesis):**
```
Low-angle tracking shot as a rally car tears into an icy hairpin turn, 
rear wheels breaking loose in a controlled drift, ice chips flying. 
The camera tracks alongside at wheel level, panning right to follow. 
Cinematic atmosphere, dynamic lighting from overcast grey sky, suspenseful energy.
```

---

## 15. Video Modes & API Reference

### Text-to-Video

Submit a text prompt. Model generates video from scratch.

```bash
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/veo-3.0-generate-preview:predictLongRunning \
  -d '{
    "instances": [{"prompt": "A slow dolly-in on a glowing campfire at night, stars visible above."}],
    "parameters": {
      "aspectRatio": "16:9",
      "durationSeconds": 8,
      "generateAudio": true,
      "sampleCount": 1
    }
  }'
```

### Image-to-Video

Provide a `image` field with the first frame. The model generates motion from that still.

```bash
-d '{
  "instances": [{
    "prompt": "The flames grow taller and sparks drift upward in the breeze.",
    "image": {
      "bytesBase64Encoded": "<BASE64_IMAGE>",
      "mimeType": "image/png"
    }
  }],
  "parameters": {
    "durationSeconds": 6
  }
}'
```

### First + Last Frame Interpolation (Veo 3.1)

Provide both `image` (first frame) and `lastFrame` fields. The model generates the transition.

```bash
-d '{
  "instances": [{
    "prompt": "The flower slowly blooms from bud to full open.",
    "image": {"bytesBase64Encoded": "<FIRST_FRAME_BASE64>", "mimeType": "image/jpeg"},
    "lastFrame": {"bytesBase64Encoded": "<LAST_FRAME_BASE64>", "mimeType": "image/jpeg"}
  }],
  "parameters": {"durationSeconds": 8}
}'
```

### Video Editing with Masks (Veo 3.1)

```bash
-d '{
  "instances": [{
    "prompt": "Replace this area with a blooming cherry tree.",
    "video": {"gcsUri": "gs://bucket/video.mp4", "mimeType": "video/mp4"},
    "mask": {
      "gcsUri": "gs://bucket/mask.mp4",
      "mimeType": "video/mp4",
      "maskMode": "foreground"
    }
  }]
}'
```

### Reference Images (Veo 3.1)

Up to 3 asset images + 1 style image:

```bash
"referenceImages": [
  {"image": {"gcsUri": "gs://bucket/product.jpg", "mimeType": "image/jpeg"}, "referenceType": "REFERENCE_TYPE_SUBJECT"},
  {"image": {"gcsUri": "gs://bucket/style.jpg", "mimeType": "image/jpeg"}, "referenceType": "REFERENCE_TYPE_STYLE"}
]
```

### API Parameters — Complete Reference

| Parameter | Type | Default | Supported By | Description |
|-----------|------|---------|-------------|-------------|
| `prompt` | string | required | All | Text description of the video |
| `aspectRatio` | string | `"16:9"` | All | `"16:9"` or `"9:16"` |
| `compressionQuality` | string | `"optimized"` | All | `"optimized"` or `"lossless"` |
| `durationSeconds` | integer | `8` | All | Veo 2: 5–8; Veo 3/3.1: 4, 6, or 8; with referenceImages: 8 only |
| `enhancePrompt` | boolean | `true` | Veo 2 models only | Use Gemini to enhance prompt |
| `generateAudio` | boolean | — | Veo 3+ | Generate native audio |
| `negativePrompt` | string | — | Veo 3.1 only | Items to exclude (direct terms, not "no X") |
| `personGeneration` | string | `"allow_adult"` | All | `"allow_adult"` or `"disallow"` |
| `resolution` | string | `"720p"` | Veo 3 models only | `"720p"`, `"1080p"`, `"4k"` (3.1 only) |
| `resizeMode` | string | `"pad"` | Veo 3 image-to-video | `"pad"` or `"crop"` |
| `sampleCount` | integer | 1 | All | 1–4 videos per request |
| `seed` | uint32 | — | All | 0–4,294,967,295 for deterministic generation |
| `storageUri` | string | — | All | GCS URI for output storage |

### Model-Specific Parameter Availability

| Parameter | veo-2.0-generate-001 | veo-2.0-generate-preview | veo-2.0-generate-exp | veo-3.0-generate-001 | veo-3.0-generate-preview | veo-3.1-generate-preview | veo-3.1-fast-generate-preview |
|-----------|----------------------|--------------------------|----------------------|----------------------|--------------------------|--------------------------|-------------------------------|
| `prompt` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `aspectRatio` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| `durationSeconds` | 5–8 | 5–8 | 5–8 | 4,6,8 | 4,6,8 | 4,6,8 | 4,6,8 |
| `enhancePrompt` | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ | ✗ |
| `generateAudio` | ✗ | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ |
| `negativePrompt` | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| `resolution` | ✗ | ✗ | ✗ | ✓ | ✓ | ✓ | ✓ |
| `referenceImages` | ✗ | ✗ | ✓ | ✗ | ✗ | ✓ | ✓ |
| `seed` | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

### Polling Workflow

Veo generation is asynchronous. The workflow:

```python
import time
from litellm import video_generation, video_status, video_content

# Step 1: POST to start generation
response = video_generation(
    model="gemini/veo-3.0-generate-preview",
    prompt="A serene lake at sunset with mountains in the background",
    size="1280x720",  # Maps to aspectRatio "16:9"
    seconds="8"
)
video_id = response.id

# Step 2: Poll status until complete
while True:
    status = video_status(video_id=video_id)
    if status.status == "completed":
        break
    elif status.status == "failed":
        raise Exception("Video generation failed")
    time.sleep(10)  # Wait 10s between polls

# Step 3: Download video
video_bytes = video_content(video_id=video_id)
with open("output.mp4", "wb") as f:
    f.write(video_bytes)
```

Via Vertex AI REST (Veo 2):

```bash
# Step 1: POST generate
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/veo-2.0-generate-001:predictLongRunning \
  -d '{"instances": [{"prompt": "YOUR_PROMPT"}], "parameters": {"aspectRatio": "16:9", "durationSeconds": 8, "sampleCount": 1}}'
# Returns: {"name": "projects/.../operations/OPERATION_ID"}

# Step 2: GET status
curl -X GET \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/operations/OPERATION_ID

# Step 3: Response when done includes video URI
```

---

## 16. Content Policy

### The 2024 Controversy

In **February 2024**, Gemini's image generation went viral for producing historically inaccurate and racially substituted images — including generating Black and Asian soldiers in WWII German military uniforms and diverse Founding Fathers of the United States. The controversy revealed that the model had been over-trained with diversity correction prompts that were being applied indiscriminately, even to historical scenarios where demographic accuracy matters.

The fallout:
- **Google CEO Sundar Pichai issued a public apology**, calling the outputs "completely unacceptable"
- Google **paused all people image generation** across Gemini products
- Internal reviews led to a complete overhaul of the safety filtering architecture
- The incident created a lasting institutional memory at Google: any loosening of people image restrictions carries extreme reputational risk

([LaoZhang AI Blog](https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction))

By Q3 2024, limited people image generation was restored for Gemini Advanced users using Imagen 3. The base tier remained restricted. Photorealistic images of identifiable real people remained hard-blocked.

### January 2026 Zero-Tolerance Policy Update

In **January 2026**, Google enacted a **zero-tolerance policy** specifically covering photorealistic images of identifiable individuals. ([Reddit r/GoogleGeminiAI](https://www.reddit.com/r/GoogleGeminiAI/comments/1qguyj4/major_policy_change_in_gemini/))

Key provisions:
- The model is prohibited from generating or modifying photorealistic images of identifiable individuals, even if the original image is user-supplied
- Any edits that add elements to or alter the pose/action of a real person in an uploaded photo are blocked
- This applies even with explicit user consent — there is no self-portrait exemption

### February 2026: Nano Banana 2 — 4 New Restriction Categories

On **February 27, 2026**, with the launch of Nano Banana 2 (`gemini-3.1-flash-image-preview`), four additional restriction categories were added to the model's architecture — not as a post-processing filter, but baked in at model level. ([Apiyi Content Safety Guide](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html), [LaoZhang AI Blog](https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction))

| New Category | Description |
|-------------|-------------|
| **Celebrity/Public Figure Images** | Named celebrities, politicians, athletes, actors, musicians — regardless of context, framing, or stated artistic purpose |
| **Face Swapping / Deepfakes** | Any prompt describing placing one person's face on another body, implicit or explicit |
| **Celebrity Outfit & Appearance Changes** | Requests to modify clothes, body, or appearance of a specific real person's image |
| **Financial Document Modification** | Generating images that appear to be modified financial documents, statements, or records |

### The 8 Blocking Categories

From the [Apiyi Content Safety Guide](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html), these are the eight major categories that trigger blocking in the Gemini image generation API:

| # | Category | Blocking Level | Notes |
|---|----------|---------------|-------|
| 1 | **NSFW / Pornographic** | 🔴 Hard Block — cannot be bypassed | Zero-tolerance; includes nudity, sexual content, sexual violence |
| 2 | **Watermark Removal** | 🟠 Policy Block — strengthening | Was bypassed in 2025 (Getty controversy); now strengthening |
| 3 | **Famous IP / Copyright Characters** | 🟡 Context-dependent | Fan art may pass; commercial-intent replication blocked |
| 4 | **Minors in harmful contexts** | 🔴 Hard Block | Strict — any suggestive content involving minors |
| 5 | **Celebrities / Public Figures** | 🔴 Hard Block | Added February 2026; categorical, no context exemptions |
| 6 | **Financial Documents** | 🔴 Hard Block | Added February 2026; bank statements, checks, IDs |
| 7 | **Face Swapping / Deepfakes** | 🔴 Hard Block | Added February 2026; both explicit and implied |
| 8 | **Implicit Suggestions** | 🟡 Context-dependent | Ambiguous prompts that pattern-match harmful intent |

### Dual-Layer Safety Architecture

Gemini uses a **two-layer safety system**:

```
Your Prompt
     │
     ▼
┌──────────────────────────────────────────┐
│  LAYER 1: Configurable Input Filtering   │
│  - Controlled by HARM_BLOCK_THRESHOLD    │
│  - Can be set to BLOCK_NONE              │
│  - Handles ambiguous/edge cases          │
└──────────────────────────────────────────┘
     │  (if passes Layer 1)
     ▼
Generation Occurs
     │
     ▼
┌──────────────────────────────────────────┐
│  LAYER 2: Non-Configurable Output Filter │
│  - Baked into model architecture         │
│  - CANNOT be bypassed by BLOCK_NONE      │
│  - Hard-blocks all 8 categories above    │
└──────────────────────────────────────────┘
     │  (if passes Layer 2)
     ▼
Image Returned
```

**Critical implication**: Setting `BLOCK_NONE` or using `harm_block_threshold=HARM_BLOCK_THRESHOLD_UNSPECIFIED` only affects Layer 1. Layer 2 cannot be bypassed through any API configuration. A response with `status 200` but no image means Layer 2 blocked the generation.

([Apiyi Content Safety Guide](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html))

### SynthID Watermarks — Technical Details

All Gemini-generated images carry SynthID watermarks. Key technical properties:

| Property | Detail |
|----------|--------|
| Embedding method | Pixel-level, imperceptible to human vision |
| Robustness | Survives cropping, scaling, color adjustment, format conversion, screenshots |
| Removal | Technically possible only with measurable quality degradation |
| Scope | All tiers: free, paid, API, Vertex AI |
| Verification | Third-party verifiable via Google's SynthID verification tool |
| Asymmetry | Gemini adds watermarks to its outputs but (pre-2025) could remove watermarks from others' images — this generated significant controversy |

There is a notable asymmetry: in March 2025, it was widely reported that Gemini 2.0 Flash could remove copyright watermarks from Getty Images and similar sources via the API (while the consumer app warned against it). This sparked controversy. Google has stated watermark removal violates ToS and is implementing technical blocks, but it has not reached full hard-block status as of early 2026. ([Apiyi Content Safety Guide](https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html))

### Person Generation: What Works vs. What Doesn't

| Works | Doesn't Work |
|-------|-------------|
| Generic fictional characters (not anchored to a real person) | Named real people, celebrities, public figures |
| Illustrated/cartoon/anime people — ANY artistic style | Photorealistic specific individuals |
| Historical figures in explicitly non-photorealistic styles | Photorealistic historical figures or modern re-imaginings |
| Crowd silhouettes, anonymous background figures | Face swapping of any kind |
| Physical trait descriptions that don't converge on a real individual | Descriptions clearly targeting a specific person ("a tech CEO who founded an electric car company") |
| Character design concepts for fiction, games, etc. | Modifying the clothing/appearance of a real person's image |
| Non-photorealistic avatars | Photorealistic avatars or profile photos |

### API `personGeneration` Parameter

| Value | Effect |
|-------|--------|
| `"allow_adult"` | Default. Allows generation of adult people and faces within policy bounds. |
| `"disallow"` | Prevents all people and face generation. |

Note: `"allow_adult"` does not override the Layer 2 restrictions on celebrities, face swapping, or specific real individuals.

### API vs. Consumer App

| Dimension | Consumer Gemini App | API / AI Studio |
|-----------|---------------------|----------------|
| Core people restrictions | Applied | Applied (identical) |
| Edge case tolerance | Most conservative | Slightly higher for creative/fictional context |
| Layer 2 bypassing | Impossible | Impossible |
| Celebrity images | Blocked | Blocked |
| Fictional human characters | Works | Works |
| System prompt context | Not available | Available (fictional framing via system prompt helps) |

The API does **not** unlock photorealistic real people, celebrities, or other hard-blocked categories. It offers marginally higher precision in distinguishing clearly fictional contexts from real-person requests. ([LaoZhang AI Blog](https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction))

### No NSFW Mode

Unlike some competitors (e.g., Grok's "Spicy Mode"), Gemini has **no NSFW tier or unlock mechanism**. The zero-tolerance policy on explicit content applies universally across all access levels and configurations.

### EU AI Act Context

Google is subject to the EU AI Act as a provider of general-purpose AI (GPAI) systems. The Act requires:
- Transparency about AI-generated content (addressed by SynthID)
- Restrictions on generating synthetic content that could be mistaken for real events or real people (informs the people generation restrictions)
- Technical safeguards against systemic misuse

The 2026 content policy tightening reflects, in part, Google's compliance obligations under EU regulation. ([LaoZhang AI Blog](https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction))

---

## 17. Common Mistakes

### Mistake 1: Using Midjourney Syntax

**Wrong:**
```
stunning landscape --ar 16:9 --v 6 --style raw --q 2 --no blur
```

**Right:**
```
A photorealistic wide landscape photograph of the Dolomites at blue hour, 
shot in 16:9 format with a 24mm wide-angle lens. No motion blur. 
Sharp, high-contrast detail throughout.
```

Midjourney parameters (`--ar`, `--v`, `--style`, `--q`, `--no`) are proprietary syntax. Nano Banana will parse them as literal text and produce degraded outputs.

### Mistake 2: Using Stable Diffusion Syntax

**Wrong:**
```
(masterpiece:1.4), (best quality:1.3), [bad hands:0.7], ultra detailed,
<lora:specific_style:0.8>
```

**Right:**
```
A masterfully composed, ultra-detailed image. [describe what you want]
```

SD's parenthesis weighting `(term:weight)`, negative square brackets `[term:weight]`, and LoRA syntax `<lora:name:weight>` are meaningless to Nano Banana's language model.

### Mistake 3: Tag Lists Instead of Narratives

**Wrong:**
```
forest, night, moonlight, wolf, mysterious, cinematic, 4K
```

**Right:**
```
A lone timber wolf stands at the edge of an ancient pine forest on a moonlit night, 
its grey coat silvered by the full moon above. The trees behind it are dense and dark, 
with only faint blue moonlight filtering through. The scene has a quiet, 
mysterious tension. Cinematic wide shot.
```

### Mistake 4: Overloading Contradictory Styles

**Wrong:**
```
photorealistic AND anime AND watercolor AND oil painting AND 8K AND pixel art
```

**Right:** Choose one primary style and optionally one complementary modifier:
```
A detailed watercolor painting with loose impressionist brushwork
```

Multiple contradictory style directives cause the model to hedge and produce a muddy middle ground.

### Mistake 5: "No X" Negative Phrasing

**Wrong:**
```
A forest scene, no cars, no people, no buildings, no modern elements
```

**Right:**
```
A primeval, uninhabited old-growth forest, completely wild and untouched, 
no signs of human civilization, no structures, only ancient trees and undergrowth.
```

Nano Banana (image) does not have a native negative prompt. Writing "no X" in the main prompt sometimes works but is unreliable. Positive description of absence is more effective.

### Mistake 6: Not Using Step-by-Step Instructions for Complex Scenes

**Wrong:**
```
A fantasy scene with a dragon, a castle, mountains, a hero, a sunset, and magical effects.
```

**Right:**
```
Step 1: Create a background of jagged volcanic mountains at sunset, the sky deep orange and purple.
Step 2: In the midground, add an ancient stone castle on a clifftop, partially ruined.
Step 3: Above the castle, add a large red dragon with wings spread wide.
Step 4: In the foreground, silhouette a lone armored warrior facing the dragon.
Step 5: Add magical particle effects — glowing embers drifting upward from the scene.
```

### Mistake 7: Expecting Aspect Ratio Control from Prompt Text

**Wrong:**
```
Generate this in 16:9 format
```
*(as the only aspect ratio instruction, expecting the actual output dimensions to change)*

**Right:**
```python
image_config=types.ImageConfig(
    aspect_ratio="16:9",
    image_size="2K"
)
```

In-prompt text mentioning aspect ratios has no effect on actual output pixel dimensions. The `imageConfig.aspect_ratio` API parameter is the only way to control output dimensions.

### Mistake 8: Not Passing Thought Signatures in Multi-Turn Editing (Nano Banana Pro)

Multi-turn editing with Nano Banana Pro is significantly more consistent when thought signatures are passed back. Omitting them causes each turn to lose the reasoning context from the previous generation, leading to inconsistent style, composition drift, and ignored constraints.

### Mistake 9: Trying to Generate Photorealistic Real People

This will fail. The Layer 2 filter will block the output and return an empty response with status 200. No workaround exists for:
- Named celebrities or public figures
- Descriptions that clearly target specific real individuals
- Face swapping

Use fictional characters, illustrated styles, or generic physical trait descriptions instead.

### Mistake 10: Sending Complex Multi-Element Video Prompts

Video generation works best with one focused action and one camera move per clip. Complex multi-element prompts produce inconsistent, incoherent motion. Build sequences through multiple separate generations.

---

## 18. Advanced Techniques

### Multi-Image Composition

Feed up to 14 reference images to construct a new scene from combined elements:

```python
contents = [
    "Place this product (image 1) in this environment (image 2), "
    "with this person (image 3) as the user. Professional lifestyle photography.",
    Image.open("product.png"),
    Image.open("environment.png"),
    Image.open("character.png"),
]
```

Object references maintain high-fidelity visual matching. Character references maintain facial and body consistency.

### Character Consistency Across Multiple Generations

For a series of images featuring the same character:
1. Generate the character once, save the reference image
2. Include the reference image in every subsequent generation
3. Use consistent naming ("the woman with silver hair and glasses") across prompts
4. Nano Banana Pro supports up to 5 simultaneous characters

### Google Search Grounding for Factual Images

Use `tools=[{"google_search": {}}]` when your prompt requires real-world accuracy:
- "Current weather map of Europe for today"
- "Stock price chart of [company] for the last month"
- "Visualization of the Mars Perseverance rover's current location"
- "Accurate scientific illustration of [recently discovered species]"

The model queries Google Search in real-time to ground the visual generation in current factual data.

### Image Search Grounding (Nano Banana 2 Only)

Add `image_search` to retrieve visual references from the web before generating:

```python
tools=[types.Tool(google_search=types.GoogleSearch(
    search_types=types.SearchTypes(
        web_search=types.WebSearch(),
        image_search=types.ImageSearch()
    )
))]
```

Constraints: Cannot search people. Must display source attribution with direct click-through to source webpage.

### Thinking Mode at "High" Level

For complex, compositionally demanding prompts, set `thinking_level="high"` (Nano Banana 2 only):

```python
thinking_config=types.ThinkingConfig(
    thinking_level="High",
    include_thoughts=False  # Don't return thought images; just benefit from them
)
```

Use this for:
- Multi-element scenes with precise spatial relationships
- Complex text rendering in detailed illustrations
- Technical diagrams with many components
- Scenes requiring accurate real-world knowledge

### Thought Signatures for Multi-Turn Consistency

After each generation with Nano Banana Pro, the response includes a thought signature — an encrypted blob encoding the model's compositional reasoning. Pass it back in the next request:

1. After generation: extract thought signature from `inline_data` parts where `part.thought == True`
2. Include in next request as `inline_data` before your text prompt
3. The model re-anchors its style and composition decisions to the previous generation state

This is especially important for:
- Long editing sessions with many turns
- Maintaining consistent style across a series
- Preventing composition drift when making targeted edits

### Style Transfer

```python
contents = [
    "Transform this photograph into the style of a ukiyo-e woodblock print. "
    "Preserve the composition exactly, but render with flat color areas, "
    "bold outlines, and the characteristic Japanese woodblock print aesthetic.",
    Image.open("source_photo.jpg")
]
```

Works with any art style. The more specifically you describe the visual characteristics of the target style (not just its name), the more accurate the transfer.

### Iterative Conversational Refinement

Use the chat API (`client.chats.create`) for iterative refinement:

```
Turn 1: "Generate a minimalist poster design for a jazz festival."
Turn 2: "Make the color scheme warmer — shift to deep reds and golds."
Turn 3: "The typography feels too rigid. Make it feel more improvisational — vary the letter sizes."
Turn 4: "Add a small silhouette of a saxophonist in the lower right."
Turn 5: "Perfect. Now generate a version in 9:16 for mobile."
```

Each turn maintains the full image context. You're directing, not re-generating from scratch.

### Aspect Ratio Trick: Upload Reference for Dimensions

If you want to ensure a specific layout or spatial proportion, upload a reference image with the desired dimensions and white/neutral content:

```
contents = [
    "Create this composition at this exact aspect ratio and spatial proportions:",
    Image.open("white_canvas_21x9.png"),
    "A panoramic mountain landscape at dawn..."
]
```

### Batch API for High-Volume Production

For pipelines generating hundreds or thousands of images:
- Use the Batch API endpoint instead of the standard `generateContent`
- Rate limits are higher
- Turnaround is up to 24 hours (not real-time)
- Same models and parameters apply
- Appropriate for training data generation, asset pipelines, A/B testing at scale

### Veo: First + Last Frame Interpolation

Send both `image` and `lastFrame` to Veo 3.1. The model generates the transition between them:

- Both frames should be the same scene/subject
- The model infers physically plausible motion
- Duration: fixed at 8 seconds when using this mode
- Audio can be generated for the transition (Veo 3.1)
- Works well for: morph transitions, growth/decay sequences, day-to-night transitions

### Veo: Seed Control for Deterministic Outputs

Set `seed` to any integer 0–4,294,967,295 to get reproducible generation:

```bash
"parameters": {
    "seed": 42,
    "prompt": "...",
    "aspectRatio": "16:9"
}
```

Same seed + same prompt + same model = same output (barring model updates). Essential for:
- A/B testing prompt variations
- Reproducing successful generations
- Building deterministic pipelines

### Veo: One-Variable Iteration

Change **only one element per generation** when iterating on video prompts. ([Shep Bryan Veo 2 Guide](https://www.shepbryan.com/blog/google-veo-2-video-prompt-guide))

This isolates what variable is producing (or not producing) the desired effect:
```
Base prompt: "A slow pan right across a neon-lit Tokyo alley at night."
Iteration 1: Change camera → "A slow dolly-in across a neon-lit Tokyo alley at night."
Iteration 2: Change time → "A slow pan right across a neon-lit Tokyo alley at dawn."
Iteration 3: Change style → "A slow pan right across a neon-lit Tokyo alley at night. Film noir style."
```

---

## 19. Quick Reference Card

### Image Prompt Formula

```
[Subject + Action] in [Environment].
[Lighting]: [light source, quality, direction, color temperature].
Style: [art style or photographic style].
Camera: [shot type], [lens], [angle], [depth of field].
[Optional: color palette, quality modifiers, text to render].
[Optional: "Step 1... Step 2..." for complex compositions.]
```

### Video Prompt Formula

```
[Camera movement] of [subject] [action verb + specific details], 
[environment + atmospheric details].
[Lighting description].
[Style/aesthetic].
[Audio description as separate sentence — Veo 3+ only.]
```

### All 3 Image Model IDs + Capabilities

| Model | API ID | Resolution | Aspect Ratios | Ref Images | Audio |
|-------|--------|------------|--------------|------------|-------|
| Nano Banana | `gemini-2.5-flash-image` | 1K only | 10 | ~3 | No |
| Nano Banana 2 | `gemini-3.1-flash-image-preview` | 512/1K/2K/4K | 14 | 14 (10 obj + 4 char) | No |
| Nano Banana Pro | `gemini-3-pro-image-preview` | 1K/2K/4K | 10 | 14 (6 obj + 5 char) | No |

### All Veo Model IDs + Capabilities

| Model | API ID | Max Res | Duration | Audio |
|-------|--------|---------|----------|-------|
| Veo 2 | `veo-2.0-generate-001` | 720p | 5–8s | No |
| Veo 2 Preview | `veo-2.0-generate-preview` | 720p | 5–8s | No |
| Veo 2 Experimental | `veo-2.0-generate-exp` | 720p | 5–8s | No (+ ref images) |
| Veo 3 | `veo-3.0-generate-preview` | 1080p | 4/6/8s | Yes |
| Veo 3 GA | `veo-3.0-generate-001` | 1080p | 4/6/8s | Yes |
| Veo 3.1 | `veo-3.1-generate-preview` | **4K** | 4/6/8s | Yes |
| Veo 3.1 Fast | `veo-3.1-fast-generate-preview` | **4K** | 4/6/8s | Yes |

### All 14 Aspect Ratios (Nano Banana 2)

| Ratio | Primary Use | Nano Banana | Nano Banana Pro |
|-------|------------|-------------|----------------|
| 1:1 | Instagram square | ✓ | ✓ |
| 2:3 | Portrait, poster | ✓ | ✓ |
| 3:2 | Landscape, DSLR | ✓ | ✓ |
| 3:4 | Portrait print | ✓ | ✓ |
| 4:3 | Classic photo | ✓ | ✓ |
| 4:5 | Instagram portrait | ✓ | ✓ |
| 5:4 | Group photo | ✓ | ✓ |
| 9:16 | Mobile vertical | ✓ | ✓ |
| 16:9 | Widescreen | ✓ | ✓ |
| 21:9 | Ultrawide | ✓ | ✓ |
| **1:4** | Vertical strip banner | **NB2 only** | ✗ |
| **4:1** | Horizontal strip banner | **NB2 only** | ✗ |
| **1:8** | Ultra-tall vertical | **NB2 only** | ✗ |
| **8:1** | Ultra-wide panoramic | **NB2 only** | ✗ |

### All 4 Resolution Tiers

| Tier | Pixel Base | NB2 Tokens | NB Pro Tokens | NB Tokens | Available On |
|------|-----------|-----------|--------------|----------|-------------|
| **512 (0.5K)** | 512px | 747 | — | — | NB2 only |
| **1K** | 1024px | 1120 | 1120 | 1290 | All models |
| **2K** | 2048px | 1680 | 1120 | — | NB2, NB Pro |
| **4K** | 4096px | 2520 | 2000 | — | NB2, NB Pro |

### Top 10 Style Keywords (Images)

| # | Keyword | Best For |
|---|---------|---------|
| 1 | `photorealistic` | General high-fidelity |
| 2 | `cinematic` | Film-quality look |
| 3 | `shot on 35mm film` | Organic film aesthetic |
| 4 | `digital illustration` | Clean professional art |
| 5 | `concept art` | Game/film development |
| 6 | `watercolor painting` | Soft, natural look |
| 7 | `oil painting` | Classic painterly |
| 8 | `Japanese anime style` | Anime/illustrated |
| 9 | `Unreal Engine render` | High-detail 3D |
| 10 | `film noir` | Dark cinematic |

### Top 10 Lighting Keywords

| # | Keyword | Effect |
|---|---------|--------|
| 1 | `golden hour light` | Warm, directional, flattering |
| 2 | `Rembrandt lighting` | Classic portrait, dramatic |
| 3 | `soft diffused overcast daylight` | Even, neutral, versatile |
| 4 | `film noir lighting` | Deep shadows, high contrast |
| 5 | `volumetric god rays` | Atmospheric light beams |
| 6 | `three-point softbox setup` | Professional studio |
| 7 | `single candlelight` | Intimate, warm |
| 8 | `neon light` | Colored, stylized |
| 9 | `blue hour` | Cool, melancholic |
| 10 | `backlit silhouette` | Rim-lit, dramatic |

### All 13 Camera Angles (Video)

| # | Angle |
|---|-------|
| 1 | Eye-level shot |
| 2 | Low-angle shot |
| 3 | High-angle shot |
| 4 | Bird's-eye view / top-down |
| 5 | Worm's-eye view |
| 6 | Dutch angle / canted angle |
| 7 | Close-up (CU) |
| 8 | Extreme close-up (ECU) |
| 9 | Medium shot (MS) |
| 10 | Full shot / long shot |
| 11 | Wide shot / establishing shot |
| 12 | Over-the-shoulder (OTS) |
| 13 | Point-of-view (POV) |

### All 12 Camera Movements (Video)

| # | Movement | One-line Description |
|---|----------|---------------------|
| 1 | Static / fixed | Camera does not move |
| 2 | Pan left/right | Rotates horizontally on fixed axis |
| 3 | Tilt up/down | Rotates vertically on fixed axis |
| 4 | Dolly in/out | Physically moves closer/farther |
| 5 | Truck left/right | Physically moves sideways parallel to subject |
| 6 | Pedestal up/down | Physically moves vertically |
| 7 | Zoom in/out | Focal length change — no physical movement |
| 8 | Crane shot | Mounted arm, vertical or arc sweeps |
| 9 | Aerial / drone shot | High altitude, smooth flight |
| 10 | Handheld / shaky cam | Unstable, intimate or chaotic |
| 11 | Whip pan | Ultra-fast blur pan |
| 12 | Arc shot | Circular path around subject |

### Content Policy Summary

| What | Status |
|------|--------|
| Generic fictional human characters | ✅ Works |
| Illustrated/anime/cartoon humans | ✅ Works |
| Named celebrities / public figures | ❌ Hard blocked (Layer 2) |
| Photorealistic real individuals | ❌ Hard blocked |
| Face swapping | ❌ Hard blocked (Feb 2026) |
| Outfit/appearance changes on real people | ❌ Hard blocked (Feb 2026) |
| Financial document modification | ❌ Hard blocked (Feb 2026) |
| Explicit/NSFW content | ❌ Hard blocked (zero tolerance) |
| API `BLOCK_NONE` bypasses all restrictions | ❌ False — only affects Layer 1 |
| NSFW mode / unlock | ❌ Does not exist |
| SynthID watermark removal | ❌ Not possible without quality loss |

### API Endpoints Summary

| Service | Endpoint |
|---------|---------|
| Image generation (Gemini API) | `POST https://generativelanguage.googleapis.com/v1beta/models/{MODEL_ID}:generateContent` |
| Image generation (Vertex AI) | `POST https://{LOCATION}-aiplatform.googleapis.com/v1/projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL_ID}:generateContent` |
| Video generation (Vertex AI) | `POST https://{LOCATION}-aiplatform.googleapis.com/v1/projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL_ID}:predictLongRunning` |
| Video status polling | `GET https://{LOCATION}-aiplatform.googleapis.com/v1/projects/{PROJECT}/locations/{LOCATION}/operations/{OPERATION_ID}` |
| Gemini API (video via generativelanguage) | `POST https://generativelanguage.googleapis.com/v1beta/models/{MODEL_ID}:generateVideos` |

---

## Sources

| Source | URL |
|--------|-----|
| Google AI Developer Docs — Nano Banana Image Generation | https://ai.google.dev/gemini-api/docs/image-generation |
| Google Cloud Vertex AI — Veo Prompt Guide | https://docs.cloud.google.com/vertex-ai/generative-ai/docs/video/video-gen-prompt-guide |
| Google Cloud Vertex AI — Veo API Reference | https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/veo-video-generation |
| Google Cloud — Gemini Image Generation Best Practices | https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/gemini-image-generation-best-practices |
| Google Developer Blog — Prompting Nano Banana | https://developers.googleblog.com/how-to-prompt-gemini-2-5-flash-image-generation-for-the-best-results/ |
| fal.ai — Mastering Video Generation with Veo 2 | https://blog.fal.ai/mastering-video-generation-with-veo-2-a-comprehensive-guide/ |
| DataNorth AI — Nano Banana Complete Guide | https://datanorth.ai/blog/nano-banana-the-ultimate-guide-to-googles-image-generation-ai |
| Apiyi — Nano Banana 2 Content Safety | https://help.apiyi.com/en/nano-banana-2-content-safety-image-generation-failure-guide-en.html |
| LaoZhang AI Blog — Gemini People Restrictions | https://blog.laozhang.ai/en/posts/gemini-image-generation-people-restriction |
| MindStudio — What Is Google Veo 2 | https://www.mindstudio.ai/blog/what-is-google-veo-2-video-generation/ |
| Shep Bryan — Veo 2 Video Prompt Guide | https://www.shepbryan.com/blog/google-veo-2-video-prompt-guide |
| ZenML — Gemini 2.5 Flash Native Image Generation Architecture | https://www.zenml.io/llmops-database/native-image-generation-with-multimodal-context-in-gemini-2-5-flash |
| PCMag — Google Unleashes Gemini 3 on Nano Banana Pro | https://www.pcmag.com/news/google-unleashes-gemini-3-on-new-nano-banana-pro-ai-image-generator |
| LiteLLM — Gemini Video Generation (Veo) | https://docs.litellm.ai/docs/providers/gemini/videos |
