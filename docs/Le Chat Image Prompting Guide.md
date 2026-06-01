# Le Chat Mistral Image Prompting Guide — A to Z

> **Audience:** Technical users and AI system builders. Nothing is censored or omitted.  
> **Engine:** Black Forest Labs FLUX Ultra (upgraded February 2025)  
> **Last verified:** April 2026

---

## Table of Contents

1. [Engine Overview](#1-engine-overview)
2. [Prompt Fundamentals](#2-prompt-fundamentals)
3. [The Self-Report Reality Check](#3-the-self-report-reality-check)
4. [Prompt Anatomy — Component Deep Dive](#4-prompt-anatomy--component-deep-dive)
5. [Official Prompt Templates](#5-official-prompt-templates)
6. [Style Keyword Library](#6-style-keyword-library)
7. [Camera, Lighting, and Color Libraries](#7-camera-lighting-and-color-libraries)
8. [Text Rendering](#8-text-rendering)
9. [Image Editing](#9-image-editing)
10. [Aspect Ratio & Resolution](#10-aspect-ratio--resolution)
11. [API Reference](#11-api-reference)
12. [Content Policy](#12-content-policy)
13. [Common Mistakes](#13-common-mistakes)
14. [Advanced Techniques](#14-advanced-techniques)
15. [Quick Reference Card](#15-quick-reference-card)

---

## 1. Engine Overview

### Powered by FLUX Ultra

Le Chat's image generation is powered by **Black Forest Labs FLUX Ultra**, upgraded from FLUX Pro in February 2025. Mistral's [official announcement](https://mistral.ai/news/all-new-le-chat) describes it as "currently the leading image generation model."

The initial integration launched in November 2024 with [FLUX Pro](https://the-decoder.com/mistral-ai-adds-flux-image-generation-and-web-search-to-le-chat-launches-pixtral-large/), then upgraded to FLUX Ultra in the February 2025 product refresh alongside Flash Answers, improved document understanding, and Canvas improvements.

### Architecture: Rectified Flow Transformer + Mistral-3 24B VLM

FLUX Ultra (and its successor FLUX.2) uses a **hybrid architecture** with two core components:

| Component | Role |
|-----------|------|
| **Mistral-3 24B Vision-Language Model** | Processes text and image inputs; provides world knowledge, contextual understanding, spatial reasoning |
| **Rectified Flow Transformer** | Handles actual image generation; captures spatial relationships, material properties, compositional logic |
| **VAE (Variational Autoencoder)** | Encodes/decodes images efficiently without quality loss |

Sources: [Black Forest Labs FLUX.2 announcement](https://bfl.ai/blog/flux-2), [Digital Applied FLUX.2 Max guide](https://www.digitalapplied.com/blog/flux-2-max-black-forest-labs-guide)

Unlike traditional diffusion models that iteratively add and remove noise, the Rectified Flow architecture learns **direct paths from noise to image**, enabling faster inference and more predictable output.

### How Prompts Flow Through the System

```
User types prompt
       ↓
Le Chat LLM (Mistral model) processes and ENHANCES the prompt
       ↓
Enhanced prompt passed to FLUX Ultra
       ↓
FLUX Ultra VLM (Mistral-3 24B) re-interprets the enhanced prompt
       ↓
Rectified Flow Transformer generates pixel data
       ↓
VAE decodes to final image
       ↓
PNG returned to user (~10 seconds total)
```

**Critical implication:** Your prompt passes through TWO language model layers before FLUX renders anything. The Le Chat LLM rewrites your prompt; then the embedded Mistral-3 24B VLM in FLUX processes the rewritten version. You are not directly controlling FLUX parameters.

### Prompt Enhancement Is ON by Default

Le Chat automatically rewrites/enhances your prompt before passing it to FLUX — similar to how Grok handles Flux-backed generation. The LLM adds implicit details (lighting, style cues, compositional language) when your prompt is sparse.

**Consequence:** Short, vague prompts still generate reasonable images because Le Chat fills in gaps. Detailed, specific prompts give you direct control and override the defaults.

There is no documented way to disable prompt enhancement from within the Le Chat UI. The "RAW:" prefix Le Chat claimed to support is undocumented and unverified — see Section 3.

### Platform Access

| Platform | URL / Notes |
|----------|-------------|
| Web | [chat.mistral.ai](https://chat.mistral.ai) |
| Mobile | iOS and Android apps available |
| API | Agent-based via `client.beta.agents` + Conversations API |

Image generation must be **manually enabled** via the Tools menu toggle at the bottom of the chat window. If image generation is not enabled, Le Chat will not generate images regardless of your prompt. ([Mistral Help](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat))

### Performance

- **Generation speed:** Sub-10 seconds per image
- **Daily limits:** Based on plan tier — free users have lower daily quotas than paid subscribers
- **Output format:** PNG
- **Base resolution:** 1024×1024 (see Section 10 for full resolution discussion)

---

## 2. Prompt Fundamentals

### Pure Natural Language — Not Tags

Le Chat's FLUX integration is **not Stable Diffusion**. Do not write prompts as comma-separated tag lists. The LLM layer processes natural language; it does not tokenize keyword tags the way SD's CLIP encoder does.

**Wrong (SD-style):**
```
masterpiece, best quality, 1girl, long hair, blue eyes, cityscape, neon lights, night, bokeh, 8k
```

**Right (natural language):**
```
A young woman with long dark hair and blue eyes standing on a rain-slicked city street at night, surrounded by neon signs reflecting in puddles. Shallow depth of field, cinematic mood.
```

The second prompt passes cleanly through the LLM layer and gives FLUX unambiguous compositional instructions.

### The LLM Understands Context and Nuance

Because a full language model processes your input before it hits FLUX, you can write conversationally:

- Relative instructions: "darker than the last one", "more dramatic lighting"
- References to previous generations in the same conversation
- Ambiguous aesthetic terms like "cozy" or "eerie" — the LLM translates these into concrete visual parameters
- Multi-sentence scene descriptions with implied relationships between elements

### Core Formula (Official)

From [Mistral's official help documentation](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat):

```
Subject + Style + Composition + Lighting + Aspect
```

Not all components are required — Subject is mandatory, everything else is optional. The LLM will fill in omitted components with sensible defaults.

### "Think Like a Director" Principle

Write what you'd tell a photographer or film director on set:

- What is in the frame?
- What is happening?
- Where is the camera?
- What is the light source?
- What is the mood?

This mental model aligns with how the Mistral LLM processes intent.

### Prompt Length

FLUX's embedded VLM accepts up to **32K text tokens** at the architecture level ([Digital Applied](https://www.digitalapplied.com/blog/flux-2-max-black-forest-labs-guide)). In practice, Le Chat's prompt enhancement layer processes and forwards your prompt without a hard character cap at the user-facing level.

Practical guidance:
- **50–150 words:** Sweet spot for most prompts — specific enough to control output, short enough to stay coherent
- **150–300 words:** Use for complex multi-element scenes, technical diagrams, or precise style specifications
- **Under 20 words:** Works but Le Chat will auto-fill significant detail — you're delegating creative control to the LLM

### What Le Chat Fills In When You Don't Specify

When prompt is sparse, the LLM typically adds:
- Natural or soft studio lighting
- Slight bokeh/depth of field for portraits
- Neutral or harmonious color grading
- Centered or rule-of-thirds composition
- Landscape orientation (see Section 10)

To override these defaults, you must explicitly specify alternatives.

### Language

Prompts work in any language the LLM supports, but the community [recommends English](https://www.reddit.com/r/MistralAI/comments/1ohit02/minitutorial_prompting_for_beginners_by_unefhis/) for most reliable results — the LLM's image vocabulary and FLUX's training data are predominantly English.

---

## 3. The Self-Report Reality Check

### Why LLMs Hallucinate About Their Own Image Capabilities

Le Chat is a language model describing its own toolchain. The LLM does not have direct introspection into the FLUX engine's parameters, configuration, or API schema. When asked about its image capabilities, it reasons by analogy — drawing from training data about other image systems (Stable Diffusion, Midjourney, DALL-E) and making plausible-sounding extrapolations.

This produces confident-sounding answers that are sometimes accurate, sometimes partially accurate, and sometimes completely fabricated. The LLM's confidence does not correlate with accuracy when describing internal system behavior.

**The pipeline problem:** The FLUX engine is a black box from the LLM's perspective. The LLM knows it can trigger image generation, but it has no runtime access to FLUX's parameter schema or actual execution context.

### Verified vs. Claimed Feature Table

| Feature | Le Chat Claimed | Reality | Verdict |
|---------|----------------|---------|---------|
| Weighting syntax `(keyword:1.2)` | Supported | No evidence in FLUX-via-Le-Chat pipeline; this is SD/ComfyUI syntax | **Likely hallucinated** |
| Negative prompts `--no` or `NOT` | Supported | Community explicitly advises against it; FLUX uses natural language, not Midjourney syntax | **Likely hallucinated** |
| `RAW:` prefix disables enhancement | Disables enhancement | Undocumented anywhere; FLUX has a Raw *mode* at API level, but not via Le Chat prompt prefix | **Likely hallucinated** |
| Pipe `\|` for batch/OR | Supported | No evidence in docs or community reports | **Unverified** |
| `<s>` special token | Image control token | This is a Mistral LLM sentence boundary token, not an image generation control | **Hallucinated** |
| Resolution up to 4096×4096, 7680×4320 | Supported | FLUX Ultra generates up to 4MP (2048×2048); Le Chat output appears to be ~1024×1024; Reddit reports landscape only | **Exaggerated** |
| Hex color codes | Supported | Unverified — natural language color descriptions are confirmed to work | **Unverified** |
| Prompt enhancement enabled by default | Enabled | Confirmed — LLM rewrites prompts before passing to FLUX | **Accurate** |
| Text rendering "medium reliability" | Medium | FLUX is actually industry-leading at text rendering — this is a strength, not a limitation | **Underestimated** |
| Image editing via conversation | Supported | Confirmed — conversational follow-ups modify generated images | **Accurate** |
| Max prompt 500 characters | 500 chars | FLUX VLM accepts 32K tokens; no documented 500-char limit | **Underestimated** |
| Canvas integration | Supported | Confirmed — Canvas is an interactive editor alongside chat | **Accurate** |
| Image generation must be toggled on | Required | Confirmed — Tools menu toggle required | **Accurate** |

### Practical Takeaway for System Builders

Do not build system prompts or automation workflows based on claimed syntaxes (`--no`, `(keyword:1.2)`, `RAW:`) without empirical verification. These almost certainly pass as plain text to FLUX, potentially degrading your output.

What actually works: natural language descriptions with the structured format documented in Section 4.

---

## 4. Prompt Anatomy — Component Deep Dive

Each component maps to a specific part of the image. Order matters because the LLM processes prompts sequentially and FLUX's attention is higher for earlier tokens.

### Component 1: Subject (Required, First)

**What it is:** The primary object, person, creature, or scene the image depicts.  
**Importance:** Critical — this is what FLUX generates. Without a clear subject, output is unpredictable.  
**Position:** Always first.  
**Rules:**
- Be specific about identity: "a red fox" not "an animal"
- Be specific about count: "two engineers" not "some people"
- Specify age, gender, build for people if they matter to your output
- Specify species, size, distinguishing marks for creatures

**Examples:**

```
A middle-aged Japanese woman with silver-streaked hair
```
```
An abandoned stone church in a pine forest
```
```
A hyperrealistic macro photograph of a monarch butterfly wing
```
```
A minimalist flat-pack cardboard box product packaging, front view
```
```
Three neon-lit vending machines on an empty Tokyo street at 3am
```

---

### Component 2: Action / Context (Recommended, Second)

**What it is:** What the subject is doing, or the environment/circumstance it exists in.  
**Importance:** High — transforms static objects into scenes with implied narrative.  
**Position:** Immediately after subject.

**Examples:**

```
...reading a worn paperback novel under a single desk lamp
```
```
...half-submerged in floodwater, surrounded by floating debris
```
```
...reflected in a rain-soaked cobblestone street
```
```
...displayed on a white pedestal with soft directional lighting
```
```
...casting long shadows across a cracked concrete floor at sunset
```

---

### Component 3: Style / Medium (Recommended, Third)

**What it is:** The visual aesthetic, artistic medium, or rendering style applied to the image.  
**Importance:** High — one of the most powerful control levers available.  
**Position:** After subject + action. Use "Style:" label for structured prompts.

FLUX responds well to both named artistic movements and technical photography terms.

**Photography styles:**

```
Style: photorealistic, shot on a Canon EOS R5, f/1.8 aperture
```
```
Style: documentary photography, gritty, natural grain
```
```
Style: high-fashion editorial photography, Vogue aesthetic
```

**Illustration styles:**

```
Style: flat illustration, minimal, geometric shapes
```
```
Style: ink and watercolor, loose brushwork, visible paper texture
```
```
Style: isometric 3D illustration, clean lines
```

**Artistic styles:**

```
Style: oil painting, impasto texture, rich shadows
```
```
Style: anime, Studio Ghibli aesthetic, soft color palette
```
```
Style: pixel art, 16-bit, limited color palette
```

See Section 6 for the complete style keyword library.

---

### Component 4: Composition / Camera (Optional)

**What it is:** Shot type, camera angle, framing, and spatial arrangement of elements.  
**Importance:** Medium-high — determines how much of the scene is visible and from what perspective.  
**Position:** After style.

**Examples:**

```
Composition: extreme close-up, filling the frame
```
```
Composition: wide establishing shot, subject in lower third
```
```
Camera: bird's-eye view, flat lay arrangement
```
```
Camera: low angle, looking up at a towering figure
```
```
Framing: Dutch angle, slightly disorienting
```

See Section 7 for the complete shot type library.

---

### Component 5: Lighting (Optional)

**What it is:** The light source, direction, quality, and mood of illumination.  
**Importance:** Medium-high — lighting is the single most impactful factor in photorealistic image quality.  
**Position:** After composition.

**Examples:**

```
Lighting: golden hour, warm sidelight from left
```
```
Lighting: hard overhead fluorescent, clinical
```
```
Lighting: rim light from behind, silhouette effect
```
```
Lighting: studio three-point setup, neutral color temperature
```
```
Lighting: foggy diffused daylight, no harsh shadows
```

See Section 7 for the complete lighting library.

---

### Component 6: Color Palette (Optional)

**What it is:** Dominant hues, tonal range, color temperature, or named palette.  
**Importance:** Medium — sets mood and visual cohesion.  
**Position:** After lighting.

**Examples:**

```
Colors: muted earth tones, ochre and sienna
```
```
Colors: high contrast black and white with single red accent
```
```
Colors: pastel, soft mint and peach
```
```
Colors: cyberpunk neon, magenta and cyan on black
```
```
Colors: film photography color grading, slightly desaturated, warm highlights
```

See Section 7 for the complete color palette library.

---

### Component 7: Quality / Detail Modifiers (Optional, Near End)

**What it is:** Instructions for detail density, texture fidelity, or finishing quality.  
**Importance:** Low-medium — FLUX Ultra produces high quality by default; these refine specifics.  
**Position:** Before aspect ratio, near the end.

**Examples:**

```
Highly detailed, every texture sharp
```
```
Painterly, soft edges, impressionistic detail
```
```
Clean and minimal, no unnecessary complexity
```
```
Ultra-sharp foreground, smooth bokeh background
```

**Note:** Unlike Stable Diffusion, generic quality tags like "masterpiece", "best quality", "8k" have limited effect in FLUX. They may pass through the LLM but FLUX Ultra already generates high-quality output by default. Specific detail instructions ("visible wood grain", "individual hair strands visible") are more effective.

---

### Component 8: Aspect Ratio (Optional, Last)

**What it is:** The width-to-height ratio of the output image.  
**Importance:** Medium — documented in official templates but with significant caveats.  
**Position:** Always last (per official documentation).  
**Format:** `Aspect: [ratio]` (e.g., `Aspect: 16:9`, `Aspect: 4:3`)

Per [Mistral's official help docs](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat), aspect ratio is specified in the prompt itself. See Section 10 for the full discussion of what actually works vs. what's documented.

---

## 5. Official Prompt Templates

These templates are taken directly from [Mistral's official image generation help article](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat) and represent the documented, supported format.

### Scene (Clean Illustration)

```
Subject: cozy reading corner with books and warm lamp.
Style: flat, minimal.
Composition: medium-wide, eye level.
Aspect: 4:3.
```

### Photographic Look

```
Subject: ceramic mug on a wooden desk with morning light.
Style: photorealistic.
Lighting: soft diffuse.
Lens: 35mm.
Aspect: 3:2.
```

### Product Mockup

```
Subject: wireless earbuds on matte surface.
Style: studio product shot.
Background: neutral gray.
Composition: centered, slight top-down.
Aspect: 1:1.
```

### Diagram / Technical Illustration

```
Subject: simple architecture diagram for a web app (client, API, DB).
Style: clean lines, readable labels.
Colors: accessible palette.
Aspect: 16:9.
```

### Additional Official Example

```
Modern office interior with natural light and plants. Flat illustration style. 16:9.
```

---

### Custom Templates (Extended)

These follow the official format but are constructed for specific use cases.

#### Portrait (Editorial)

```
Subject: elderly fisherman with weathered skin and white stubble, direct gaze.
Style: film photography portrait, Leica aesthetic, slight grain.
Lighting: soft window light from camera left, deep shadow on right.
Composition: tight crop at shoulders, centered.
Colors: desaturated, warm skin tones.
Aspect: 3:2.
```

#### Landscape (Environment Art)

```
Subject: abandoned Victorian greenhouse overrun with vines and wildflowers at dusk.
Style: hyperrealistic environment concept art.
Lighting: golden hour backlight, volumetric light shafts through broken glass.
Composition: wide establishing shot, strong foreground element (rusted gate).
Colors: warm amber and deep teal contrast.
Aspect: 16:9.
```

#### Fantasy Character

```
Subject: armored female warrior with glowing runes on her breastplate, standing at the edge of a cliff overlooking a burning city.
Style: cinematic fantasy illustration, painterly.
Lighting: dramatic rim light from below (fire glow), dark storm sky above.
Composition: full body, low angle, silhouette partially obscured by smoke.
Colors: deep crimson and ash gray.
Aspect: 16:9.
```

#### Technical Illustration (Exploded Diagram)

```
Subject: exploded-view technical diagram of a mechanical wristwatch movement, showing all gear components labeled.
Style: clean engineering illustration, white background, thin black lines.
Colors: components in soft blue, gold, and silver; labels in dark gray.
Composition: centered, slight isometric angle.
Aspect: 4:3.
```

#### Marketing / Social Post

```
Subject: glass bottle of artisanal hot sauce on a rustic wooden table surrounded by red chili peppers and garlic.
Style: commercial food photography.
Lighting: soft natural window light, slight backlight for translucency effect.
Background: dark wood grain, shallow focus.
Composition: product centered, slight 3/4 angle.
Aspect: 1:1.
```

#### UI Mockup / Wireframe

```
Subject: mobile app screen showing a fitness tracking dashboard with step count, heart rate graph, and daily streak.
Style: clean UI design mockup, flat design, modern sans-serif fonts.
Colors: dark mode, deep navy background, electric blue accents, white text.
Aspect: 9:16.
```

---

## 6. Style Keyword Library

Use these keywords in the `Style:` field or inline within your prompt. FLUX responds well to specific named aesthetics.

### Photorealism

| Keyword | Effect |
|---------|--------|
| `photorealistic` | General high-fidelity photography look |
| `hyperrealistic` | Extreme detail, almost indistinguishable from photo |
| `DSLR photograph` | Camera-specific aesthetic, natural depth of field |
| `shot on Leica` | High-contrast, slight grain, reportage feel |
| `shot on Canon EOS R5` | Clinical sharpness, rich color |
| `shot on Fujifilm` | Warm film tones, slight desaturation |
| `35mm film photography` | Grain, color shift, light leaks possible |
| `medium format photography` | Extremely shallow DoF, luxury feel |
| `documentary photography` | Raw, unposed, gritty |
| `commercial photography` | Clean, polished, product-ready |
| `editorial photography` | High-fashion, dramatic, magazine-quality |
| `macro photography` | Extreme close-up, fine detail |
| `long exposure photograph` | Motion blur, light trails |
| `aerial photography` | Top-down or near-top-down perspective |

### Illustration

| Keyword | Effect |
|---------|--------|
| `flat illustration` | Minimal, geometric, no depth or shadow |
| `minimal illustration` | Simple, clean, sparse |
| `vector art` | Clean edges, solid fills, scalable look |
| `line art` | Outlines only, varying weights |
| `ink illustration` | Bold ink strokes, hand-drawn feel |
| `children's book illustration` | Soft, friendly, simple shapes |
| `editorial illustration` | Conceptual, often symbolic |
| `technical illustration` | Precise, labeled, diagram-style |
| `infographic style` | Data visualization, icons, readable |
| `isometric illustration` | 3D-looking from a fixed isometric angle |
| `retro illustration` | Mid-century modern, vintage palette |
| `vintage poster art` | Art Nouveau or 1920s–1960s aesthetics |
| `silkscreen print` | Limited colors, slight registration offset |

### Anime / Manga

| Keyword | Effect |
|---------|--------|
| `anime style` | Japanese animation aesthetic, large eyes |
| `manga` | Black and white, panel-ready, screentone |
| `Studio Ghibli aesthetic` | Soft, painterly, nature-focused |
| `Makoto Shinkai style` | Hyper-detailed urban environments, lens flare |
| `chibi` | Super-deformed, oversized head, cute |
| `seinen manga` | Adult-oriented, darker tones |
| `shonen anime` | Action-focused, dynamic poses, bold colors |
| `cyberpunk anime` | Neon, rain, high-tech low-life |
| `fantasy light novel cover` | Ornate character art, soft glow effects |

### Painterly

| Keyword | Effect |
|---------|--------|
| `oil painting` | Rich texture, deep shadows, classical feel |
| `impasto oil painting` | Thick visible brushstrokes |
| `watercolor` | Soft edges, wet-on-wet blending, white paper |
| `watercolor and ink` | Clean ink lines with watercolor fill |
| `gouache` | Opaque watercolor, flat and matte |
| `acrylic painting` | Vivid colors, versatile texture |
| `impressionist painting` | Loose brushwork, captured light |
| `expressionist painting` | Distorted, emotional, gestural |
| `digital painting` | Painterly but precision of digital tools |
| `concept art` | Pre-production sketches and renders |
| `matte painting` | Cinematic environment paintings |
| `fresco` | Ancient wall painting, aged texture |
| `ukiyo-e` | Japanese woodblock print aesthetic |
| `pointillism` | Dots of color creating an image |

### Cinematic

| Keyword | Effect |
|---------|--------|
| `cinematic` | Movie-quality framing and lighting |
| `movie still` | Single frame from a film |
| `film grain` | Analogue texture overlay |
| `anamorphic lens` | Horizontal lens flare, oval bokeh |
| `Blade Runner aesthetic` | Rain, neon, retro-futurism |
| `noir film` | High contrast black and white, shadows |
| `horror movie still` | Dark, desaturated, threatening |
| `blockbuster movie` | Polished, dynamic, commercial |
| `indie film aesthetic` | Natural light, handheld feel, muted palette |
| `Wes Anderson style` | Symmetrical, pastel, deadpan |
| `epic fantasy` | Grand scale, dramatic skies, hero lighting |
| `sci-fi movie concept` | Clean technology, speculative design |

### Graphic / Digital Design

| Keyword | Effect |
|---------|--------|
| `pixel art` | 8-bit or 16-bit game aesthetic |
| `pixel art, 32x32 sprite` | Ultra-low resolution sprite style |
| `3D render` | Computer-generated three-dimensional |
| `Blender render` | Open-source 3D software aesthetic |
| `octane render` | High-quality photoreal 3D |
| `voxel art` | Minecraft-like cubic 3D |
| `low poly` | Simplified 3D geometry |
| `clay render` | 3D objects with matte clay material |
| `neon art` | Glowing neon tubes on dark background |
| `glitch art` | Digital corruption, scan lines |
| `synthwave` | 80s retro-futurism, grid, sunset |
| `vaporwave` | 90s nostalgia, pink/purple, Roman statues |
| `brutalist design` | Heavy, raw, stark |

---

## 7. Camera, Lighting, and Color Libraries

### Shot Types

| Shot Type | Description | Use Case |
|-----------|-------------|----------|
| `extreme close-up (ECU)` | Single detail fills frame (eye, fingernail) | Texture, emotion |
| `close-up` | Head and shoulders or smaller | Portraits, emotions |
| `medium close-up` | Chest and above | Conversational, editorial |
| `medium shot` | Waist up | Characters in context |
| `medium wide shot` | Full body with some background | Character in environment |
| `wide shot` | Subject + significant environment | Establishing scene |
| `extreme wide shot` | Landscape dominant, subject tiny | Scale, isolation |
| `full shot` | Full body from head to toe | Fashion, character design |
| `over-the-shoulder (OTS)` | From behind one subject looking at another | Dialogue, confrontation |
| `point-of-view (POV)` | Camera is the character's eyes | Immersive, first person |
| `aerial shot` | Camera directly above or near above | Maps, architecture |
| `flat lay` | Top-down, subjects laid flat | Products, food |
| `worm's-eye view` | Camera at ground level looking up | Dominance, scale |
| `bird's-eye view` | Camera from high above looking down | Overview, scale |

### Lens Keywords

| Keyword | Focal Length Equivalent | Effect |
|---------|------------------------|--------|
| `ultra-wide lens` | 10–24mm | Dramatic distortion, expansive |
| `wide-angle lens` | 24–35mm | Environmental context, slight distortion |
| `35mm lens` | 35mm | Classic photojournalism look |
| `50mm lens` | 50mm | Natural, close to human eye |
| `85mm portrait lens` | 85mm | Flattering portraits, background compression |
| `telephoto lens` | 100–400mm | Background compression, distant subjects |
| `macro lens` | 1:1 magnification | Extreme close-up detail |
| `fisheye lens` | ~8mm | 180° field of view, heavy distortion |
| `tilt-shift lens` | Any | Miniature-world effect, selective focus |
| `anamorphic lens` | Wide + oval bokeh | Cinematic horizontal flares |

### Perspective / Angle Keywords

| Keyword | Effect |
|---------|--------|
| `eye level` | Natural, neutral, grounded |
| `low angle` | Subject appears powerful, dominant |
| `high angle` | Subject appears smaller, vulnerable |
| `Dutch angle` | Tilted, disorienting, tension |
| `isometric` | Diagonal 2D view of 3D space |
| `frontal` | Direct, symmetrical |
| `3/4 angle` | Slightly off-axis, dimensional |
| `profile` | Pure side view |
| `back view` | Camera behind subject, anonymous |
| `overhead` | Directly above |

### Framing Keywords

| Keyword | Effect |
|---------|--------|
| `rule of thirds` | Classic compositional balance |
| `centered composition` | Symmetrical, formal |
| `negative space` | Large empty area to balance subject |
| `leading lines` | Lines drawing eye toward subject |
| `framing within frame` | Subject visible through arch, window, doorway |
| `tight crop` | Little to no space around subject |
| `loose crop` | Subject has breathing room in frame |
| `foreground interest` | Object in foreground adds depth |

### Natural Lighting

| Keyword | Effect |
|---------|--------|
| `golden hour` | Warm amber/orange, long shadows, cinematic |
| `blue hour` | Just before sunrise or after sunset, cool blue |
| `midday sun` | Harsh overhead, strong shadows |
| `overcast daylight` | Diffuse, even, no harsh shadows |
| `foggy diffuse light` | Atmospheric, soft, mysterious |
| `dappled sunlight` | Light filtered through leaves |
| `sunset backlight` | Subject silhouetted or rim-lit |
| `moonlight` | Cool blue, low intensity, deep shadows |
| `storm light` | Dark clouds, dramatic contrast |
| `northern lights` | Green/purple aurora in dark sky |
| `underwater light` | Caustics, blue-green, rippling |

### Studio Lighting

| Keyword | Effect |
|---------|--------|
| `three-point studio lighting` | Key, fill, and rim lights — balanced |
| `soft box lighting` | Soft, even, minimal shadow |
| `ring light` | Catch light in eyes, even skin |
| `hard directional light` | Defined shadows, sculptural |
| `Rembrandt lighting` | Triangle of light on cheek, dramatic portrait |
| `split lighting` | Half face lit, half in shadow |
| `butterfly lighting` | Overhead, symmetrical, fashion |
| `high-key lighting` | Bright, minimal shadow, commercial |
| `low-key lighting` | Dark, dramatic, mysterious |
| `clamshell lighting` | Under-eyes removed, beauty photography |

### Stylized / Environmental Lighting

| Keyword | Effect |
|---------|--------|
| `neon lighting` | Colored neon glow, urban |
| `candlelight` | Warm flame, flickering feel |
| `firelight` | Orange/red, dancing shadows |
| `bioluminescence` | Glowing organisms, underwater/forest |
| `volumetric lighting` | God rays, smoke, haze |
| `lens flare` | Optical artifact, cinematic |
| `rim lighting` | Subject outlined with bright edge |
| `subsurface scattering` | Light through skin/wax/leaves |
| `blacklight / UV` | Fluorescent colors, dark background |
| `strobe flash` | Sharp freeze, hard shadows |
| `window light` | Natural soft-directional indoor light |
| `glowing screen light` | Blue-toned, digital, tech environments |

### Color Palette Keywords

| Palette Keyword | Description |
|-----------------|-------------|
| `warm tones` | Reds, oranges, yellows dominant |
| `cool tones` | Blues, greens, purples dominant |
| `monochromatic` | Single hue with varied saturation/value |
| `black and white` | No color, pure grayscale |
| `muted / desaturated` | Faded, washed out, analog |
| `high saturation` | Vivid, bold, intense |
| `earth tones` | Browns, tans, ochres, terracotta |
| `pastel palette` | Soft, light, low saturation |
| `neon palette` | Electric, high-saturation glowing hues |
| `duotone` | Two dominant contrasting colors |
| `sepia` | Warm brownish monochrome, antique |
| `film color grade` | Specific LUT aesthetic |
| `Kodak Portra palette` | Warm skin tones, slightly muted |
| `Fujifilm palette` | Slightly cool, vivid, slightly green shadows |
| `teal and orange` | Hollywood blockbuster color grade |
| `complementary colors` | Opposing hues on color wheel |
| `analogous palette` | Adjacent hues on color wheel |

---

## 8. Text Rendering

### FLUX's Core Strength

Text rendering is one of FLUX's most notable competitive advantages. Traditional diffusion models notoriously fail at legible text — producing garbled characters, letter inversions, and random gibberish. FLUX's architecture, with its embedded vision-language model and flow matching, handles text significantly better than SD-family models.

Sources: [getimg.ai FLUX.1 overview](https://getimg.ai/blog/what-is-flux-1-the-breakthrough-ai-model-you-need-to-know), [MindStudio FLUX 1.1 Pro Ultra guide](https://www.mindstudio.ai/blog/what-is-flux-1-1-pro-ultra/)

### How to Prompt for Text

**Use quotation marks to define exact text content:**

```
A street sign that reads "DEAD END" in reflective green letters
```

```
A retro neon sign spelling out "OPEN 24 HOURS" in pink neon tubes
```

```
A coffee shop chalkboard menu listing "Espresso $3.50", "Latte $5.00", "Cold Brew $4.50"
```

**Specify font/style characteristics:**

```
A book cover with the title "THE LAST SIGNAL" in bold serif typeface, white on dark background
```

```
A startup logo with the word "NORI" in a clean modern sans-serif, teal color
```

**Specify placement and size:**

```
A poster with large headline text reading "SUMMER SALE" at the top, and smaller body text below saying "Up to 50% off all items"
```

### Best Practices for Text Rendering

| Practice | Reason |
|----------|--------|
| Keep text short (1–5 words per element) | Longer strings increase error probability |
| Use quotation marks around exact text | Signals to FLUX that precision is required |
| Specify clear area for text in composition | Ensures background is appropriate for legibility |
| Request simple font styles ("bold", "serif", "sans-serif") | Complex/decorative fonts reduce accuracy |
| Avoid mixing many text elements | Each additional text element multiplies error risk |

### Text Rendering Limitations

Despite FLUX's strength, limitations remain:

- **Very long strings** (full sentences, paragraphs): High error rate
- **Small text** at low relative size in frame: May blur or garble
- **Complex decorative fonts** (scripts, blackletter): Inconsistent
- **Text at unusual angles** (diagonal, curved): Lower accuracy
- **Non-Latin scripts** (Arabic, CJK, Devanagari): Significantly lower reliability than Latin
- **Multiple text elements in one image**: Accuracy degrades with each addition

**Mitigation strategy:** For critical text (product labels, logos, signs), generate the image first and add text in post-production with a graphics tool. FLUX is reliable enough that the image structure will be correct; only the text pixels need replacement.

### Example Prompts with Text

**Sign:**
```
Subject: rusty metal roadside sign on a wooden post reading "ROUTE 66" with weathered paint.
Style: documentary photography.
Lighting: harsh midday sun.
Aspect: 3:2.
```

**Book cover:**
```
Subject: book cover design. Dark navy background, silhouette of a lighthouse. Title reads "THE FORGOTTEN SHORE" in weathered serif typography at top. Author name "J.M. REED" in smaller caps at bottom.
Style: commercial book cover design.
Aspect: 2:3.
```

**Infographic:**
```
Subject: simple infographic showing three steps labeled "1. Research", "2. Design", "3. Launch" with icons for each step.
Style: clean flat design, readable labels, icons.
Colors: accessible, high contrast.
Aspect: 16:9.
```

---

## 9. Image Editing

### Conversational Editing

Le Chat supports **iterative image editing** through conversational follow-up messages in the same chat thread. You do not need to start a new conversation — simply describe what you want changed.

This is confirmed in [Mistral's official help article](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat) and across multiple community reports.

### Edit Command Patterns

**Add element:**
```
Add a whiteboard on the back wall. Keep lighting and color palette unchanged.
```

**Remove element:**
```
Remove the car in the background. Keep everything else exactly the same.
```

**Change element:**
```
Change the background from office to outdoor rooftop. Keep the subject and lighting style.
```

**Modify attribute:**
```
Make the sky more dramatic — darker storm clouds, more contrast.
```

**Add person:**
```
Add an employee looking through the window. Match the lighting style of the existing scene.
```

**Style shift:**
```
Convert this to a watercolor illustration style while keeping the same composition.
```

**Mood adjustment:**
```
Make this image more cinematic — add film grain, slight desaturation, teal and orange color grade.
```

### The "Lock What Stays" Technique

When editing, explicitly state what should remain unchanged. Without this, Le Chat may regenerate elements you wanted to preserve.

**Pattern:**
```
[Change]: [what to change to]
[Keep]: [list of elements to preserve]
```

**Example:**
```
Change the woman's dress from red to midnight blue.
Keep the lighting, composition, background, and facial expression exactly as they are.
```

### Multi-Step Iteration Workflow

```
Step 1: Generate base image with complete initial prompt
Step 2: Identify what's closest to your vision and what needs adjustment
Step 3: Send targeted edit instruction — change ONE thing
Step 4: Evaluate result
Step 5: Repeat from Step 2 until satisfied
```

The one-change-per-step approach prevents compounding errors. Changing multiple elements simultaneously increases the probability that FLUX re-generates parts you wanted to keep.

### Uploading an Image for Editing

You can upload an existing image (your own or generated elsewhere) and ask Le Chat to edit it:

```
[Upload image]
"Add a sunset sky to this architectural photograph. Keep the building unchanged."
```

```
[Upload image]
"Colorize this black and white portrait in the style of 1950s hand-painted photographs."
```

**Important observation from community:** When you upload an image with a specific aspect ratio and request editing, Le Chat will maintain the uploaded image's aspect ratio in the output. This is a documented workaround for generating non-landscape images — upload a portrait or square crop and ask for edits. ([YouTube tutorial](https://www.youtube.com/watch?v=hHqAQ5PzAFM))

### Canvas Integration

Canvas is Le Chat's interactive editor that opens alongside the chat window. For image generation workflows:

- Canvas is **off by default** — must be enabled via the Tools menu ([Mistral Help: Canvas](https://help.mistral.ai/en/articles/393385-what-is-canvas-and-how-do-i-use-it-to-create-content-interactively))
- You can open multiple Canvases simultaneously (tabbed interface)
- Canvas supports versioning — navigate between previous versions with arrows
- Diff view shows what changed between versions
- Canvas pairs with image generation for complex creative projects (e.g., generate image, open in Canvas, edit layout, iterate)

For pure image editing, the conversational workflow is simpler. Canvas is more useful for mixed content projects (image + document, image + code).

---

## 10. Aspect Ratio & Resolution

### The Official Documentation vs. Reality Gap

This section has the biggest discrepancy between what Mistral documents and what users actually get.

**Official documentation** ([Mistral Help](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat)) shows prompt templates explicitly using aspect ratios including `1:1`, `3:2`, `4:3`, `16:9`, and even `9:16`.

**Community reality** ([Reddit, r/MistralAI, July 2025](https://www.reddit.com/r/MistralAI/comments/1m67o4c/why_le_chat_can_only_generates_landscape_images/)): Multiple users report that only landscape orientation is produced. One user confirmed that Mistral support gave a **firm "no"** to portrait image support.

This suggests aspect ratio specification in prompts may be **partially or inconsistently implemented**, or that support has changed between the documentation date and community reports.

### What Is Known

| Aspect Ratio | Documentation Status | Community Reports | Confidence |
|-------------|---------------------|-------------------|------------|
| `16:9` (landscape wide) | Listed in official templates | Confirmed working | High |
| `4:3` (landscape) | Listed in official templates | Likely works | Medium-high |
| `3:2` (landscape) | Listed in official templates | Likely works | Medium |
| `1:1` (square) | Listed in official templates | Conflicting — one Facebook community report of square output; Reddit users unable to get it | Low |
| `9:16` (portrait tall) | Listed in official UI mockup template | Reddit + Mistral support confirm NOT supported | Not supported |
| `2:3` (portrait) | Not in official templates | Almost certainly not supported | Not supported |

### Resolution

- **FLUX Ultra architecture supports:** Up to 4MP (2048×2048 or equivalent area) natively ([Digital Applied](https://www.digitalapplied.com/blog/flux-2-max-black-forest-labs-guide), [MindStudio](https://www.mindstudio.ai/blog/what-is-flux-1-1-pro-ultra/))
- **FLUX 1.1 Pro (previous engine):** 1024×1024 standard ([MindStudio](https://www.mindstudio.ai/blog/what-is-flux-1-1-pro-ultra/))
- **Le Chat output resolution:** Appears to be approximately 1024×1024 for standard output. It is unclear whether Le Chat exposes FLUX Ultra's full 4MP capability — no official documentation confirms this.
- **Facebook community report:** One tester ([Facebook AI group, August 2025](https://www.facebook.com/groups/1336489033692358/posts/1634221687252423/)) documented `1024×1024 px` at `1:1` square ratio — though this contradicts most Reddit reports

### How to Specify Aspect Ratio

Use the `Aspect:` field at the end of your prompt, per official documentation:

```
Aspect: 16:9
```
```
Aspect: 4:3
```
```
Aspect: 3:2
```
```
Aspect: 1:1
```

You can also write it inline:
```
...wide landscape composition. 16:9 format.
```

### Workaround for Non-Standard Aspect Ratios

The most reliable workaround for portrait or square output is the **upload-and-edit method**:

1. Create or find an image with your desired aspect ratio (portrait, square, etc.)
2. Upload it to Le Chat
3. Prompt: "Edit this image to [your subject/style]. Maintain the exact same aspect ratio as the uploaded image."

Community testing confirms that Le Chat preserves the uploaded image's aspect ratio during edits. This is currently the most reliable path to portrait output.

---

## 11. API Reference

### Architecture: Agent + Conversations API

Le Chat's image generation is **not available as a direct image generation endpoint**. There is no `/v1/images/generate` call. Image generation is exposed as a **built-in tool** within the agent framework, accessed via the Conversations API.

Source: [Mistral official API documentation](https://docs.mistral.ai/agents/tools/built-in/image_generation)

### Required Components

1. **Agent** — created with `image_generation` tool enabled
2. **Conversation** — started via `client.beta.conversations.start()`
3. **File download** — image returned as `file_id`, must be downloaded separately

### Step 1: Create an Image Generation Agent

```python
from mistralai import Mistral
import os

api_key = os.environ["MISTRAL_API_KEY"]
client = Mistral(api_key=api_key)

image_agent = client.beta.agents.create(
    model="mistral-medium-latest",
    name="Image Generation Agent",
    description="Agent used to generate images.",
    instructions="Use the image generation tool when you have to create images.",
    tools=[{"type": "image_generation"}],
    completion_args={
        "temperature": 0.3,
        "top_p": 0.95,
    }
)

print(f"Agent ID: {image_agent.id}")
```

**Parameters:**

| Parameter | Value | Notes |
|-----------|-------|-------|
| `model` | `"mistral-medium-latest"` | Recommended per docs |
| `tools` | `[{"type": "image_generation"}]` | Enables the tool |
| `temperature` | `0.3` | Lower = more consistent interpretation |
| `top_p` | `0.95` | Standard sampling |

### Step 2: Start Conversation and Generate Image

```python
response = client.beta.conversations.start(
    agent_id=image_agent.id,
    inputs="Generate an orange cat sitting at a wooden desk in a home office, photorealistic, warm afternoon light."
)
```

The `inputs` string is your image prompt. The agent decides when to invoke the image_generation tool based on its instructions.

### Step 3: Download the Generated Image

```python
from mistralai.client.models import ToolFileChunk

# Download single generated image (assumes one image per response)
for chunk in response.outputs[-1].content:
    if isinstance(chunk, ToolFileChunk):
        file_bytes = client.files.download(file_id=chunk.file_id).read()
        with open("generated_image.png", "wb") as f:
            f.write(file_bytes)
        print(f"Saved: generated_image.png")
        break
```

### Step 4: Download All Images in a Response (Batch)

```python
from mistralai.client.models import ToolFileChunk

for i, chunk in enumerate(response.outputs[-1].content):
    if isinstance(chunk, ToolFileChunk):
        file_bytes = client.files.download(file_id=chunk.file_id).read()
        with open(f"image_generated_{i}.png", "wb") as f:
            f.write(file_bytes)
        print(f"Saved: image_generated_{i}.png (file_id: {chunk.file_id})")
```

### Full Working Example

```python
import os
from mistralai import Mistral
from mistralai.client.models import ToolFileChunk

def generate_image(prompt: str, output_path: str = "output.png") -> str:
    """
    Generate an image via Le Chat's FLUX Ultra integration.
    
    Args:
        prompt: Natural language image description
        output_path: Local path to save the PNG
    
    Returns:
        output_path on success
    """
    client = Mistral(api_key=os.environ["MISTRAL_API_KEY"])
    
    # Create agent (cache this in production — don't recreate per request)
    agent = client.beta.agents.create(
        model="mistral-medium-latest",
        name="Image Generator",
        description="Generates images on demand.",
        instructions="Use the image generation tool when asked to create images.",
        tools=[{"type": "image_generation"}],
        completion_args={"temperature": 0.3, "top_p": 0.95}
    )
    
    # Start conversation with prompt
    response = client.beta.conversations.start(
        agent_id=agent.id,
        inputs=prompt
    )
    
    # Extract and save the image
    for chunk in response.outputs[-1].content:
        if isinstance(chunk, ToolFileChunk):
            file_bytes = client.files.download(file_id=chunk.file_id).read()
            with open(output_path, "wb") as f:
                f.write(file_bytes)
            return output_path
    
    raise RuntimeError("No image chunk found in response")


# Usage
if __name__ == "__main__":
    path = generate_image(
        prompt="""
        Subject: minimalist home office with a standing desk, laptop, and small potted plant.
        Style: clean architectural photography.
        Lighting: soft natural window light from left.
        Colors: white walls, warm wood tones, muted green plant.
        Aspect: 16:9.
        """,
        output_path="office.png"
    )
    print(f"Image saved to {path}")
```

### Response Structure Reference

#### Tool Execution Entry (`tool.execution`)

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | `"image_generation"` |
| `object` | string | `"entry"` |
| `type` | string | `"tool.execution"` |
| `created_at` | timestamp | When execution started |
| `completed_at` | timestamp | When execution finished |
| `id` | string | Unique execution identifier |

#### Message Output Entry (`message.output`)

| Field | Type | Description |
|-------|------|-------------|
| `content` | list | Mixed list of text chunks and ToolFileChunks |
| `type` | string | `"message.output"` |
| `role` | string | `"assistant"` |
| `model` | string | `"mistral-medium-latest"` |
| `agent_id` | string | The agent that produced the response |

#### ToolFileChunk Fields

| Field | Value |
|-------|-------|
| `tool` | `"image_generation"` |
| `file_id` | Unique file identifier (use to download) |
| `type` | `"tool_file"` |
| `file_name` | Generated filename |
| `file_type` | `"png"` |

### API Limitations and Notes

- **No direct resolution control** — cannot set width/height via API parameters
- **No aspect ratio parameter** — aspect ratio must be specified in the prompt text (`Aspect: 16:9`)
- **No FLUX-specific parameters** — no raw mode, no CFG scale, no step count, no seed control via API
- **No negative prompt field** — all prompt control is through the natural language `inputs` string
- **Output format** — always PNG, no JPEG or WebP option
- **Agent caching** — in production systems, create the agent once and reuse the `agent_id` rather than creating a new agent per request
- **Prompt enhancement** — the LLM layer still applies even via API; the `inputs` string is processed by the agent LLM before reaching FLUX

---

## 12. Content Policy

### Scope

Mistral's [Usage Policy](https://legal.mistral.ai/terms/usage-policy) applies to:

- All Mistral AI products including Le Chat and Mistral AI Studio
- All users (individual, organizational, commercial)
- All content generated or accessed through these products

It does **not** apply to self-hosted deployments or open-source models running on your own infrastructure.

### Prohibited Content Categories

#### CSAM — Zero Tolerance

> "Mistral AI has a zero tolerance policy regarding CSAM. Any generation or attempt to generate CSAM on our Mistral AI Products is strictly prohibited. We will report all actual or suspected CSAM to the relevant law enforcement authorities and will terminate your account."

**Enforcement:** Immediate account termination. Law enforcement reporting. No exceptions.

#### Non-Consensual Intimate Imagery

> "You shall not use the Mistral AI Products to generate intimate images of any person without the explicit consent of all individuals involved."

This applies to real identifiable people. Fictional characters are subject to other content rules but not this specific clause.

#### Hate and Discrimination

Prohibited content includes anything that:
- Promotes hate or discrimination based on race, gender, ethnicity, religion, nationality, sexual orientation, disability status, or caste
- Engages in revisionism or denialism of documented historical events (Holocaust, genocides)
- Includes harassing language toward any target
- Glorifies suffering or humiliation of others

#### Violence and Threats

> "Use of the Mistral AI Products to conduct or generate any activity or content that promotes, incites, threatens, or glorifies violence is not permitted."

Includes threats of physical harm and glorification of terrorist acts.

#### Self-Harm

Prohibited to generate content that promotes, encourages, or provides instructions for self-harm or suicide. Includes:
- Graphic depictions of self-harm
- Detailed descriptions of self-harm methods
- Encouragement of suicidal behavior

#### Fraud and Impersonation

Prohibited uses include:
- Phishing materials
- Financial scam assets
- Identity impersonation (images of real people without consent)
- Misrepresentation of facts

#### Privacy Violations

> "Prohibited to generate content that invades or violates privacy of others. Includes using someone else's likeness or voice to generate outputs or impersonate without prior consent."

Generating images that appear to be a specific real private individual without their consent is prohibited.

#### Security Circumvention

> "Shall not circumvent security protections and AI safety filters."

Explicitly includes jailbreaking or prompt injection attempts targeting the image generation pipeline.

### NSFW Policy Analysis

Le Chat has **no adult content mode**. Unlike xAI Grok ("Aurora Spicy Mode") or some other platforms, there is no toggle, no age verification bypass, no documented mechanism to access explicit content.

The usage policy does not contain any exception for:
- Artistic nudity
- Educational content depicting nudity
- Historical imagery with nudity
- Medical content

This is stricter than many US-based platforms. Mistral is a French company subject to **EU AI Act** regulations and European content standards, which are typically more conservative regarding generated intimate imagery than US legal frameworks.

**Comparison:**

| Platform | Adult Content Mode | Artistic Nudity | API Bypass |
|----------|-------------------|-----------------|------------|
| Le Chat (Mistral) | No | Not documented | No |
| Grok (xAI) | Yes ("Spicy Mode") | Permitted | API-level |
| ChatGPT (OpenAI) | Age-verified (limited rollout) | Limited | No |
| Stable Diffusion (self-hosted) | N/A — self-hosted | User's discretion | N/A |
| Midjourney | No | Limited | No |

### What Does Work Within Policy

The policy prohibits content that "glorifies" or "promotes" violence — not all depictions of violence. Artistic, historical, and narrative contexts exist within bounds:

**Acceptable (within policy):**
- Fantasy combat scenes without explicit gore
- Historical scenes depicting conflict (battle scenes)
- Horror imagery (atmospheric, not instructional)
- Violence implied through aftermath (not depicted act)
- Villain characters and antagonist design
- Dark or dystopian aesthetics
- Fictional weapons and military equipment
- Stylized action and fighting scenes

**Prohibited:**
- Step-by-step weapon construction or modification
- Glorification of real terrorist acts or real perpetrators
- Content that sexualizes minors in any context
- Real person intimate imagery without consent

### Enforcement

Per the Usage Policy: violations result in temporary suspension or permanent termination of account. Serious violations (CSAM, terrorism) are reported to law enforcement.

Prompt blocking also occurs for:
- Copyright and derivative works restrictions
- Safety filter triggers

If you believe a block is incorrect: contact Mistral support with your prompt and a screenshot. This is documented in the official help article.

---

## 13. Common Mistakes

### Mistake 1: Using Stable Diffusion Syntax

**What people do:**
```
(masterpiece:1.4), (best quality:1.2), (photorealistic:1.3), detailed face, [low quality:0.5], --no blur
```

**Why it fails:** This is SD/ComfyUI syntax that assumes a CLIP text encoder with specific attention weighting mechanics. Le Chat's LLM layer processes this as plain text. The parentheses and colons either pass through to FLUX as literal text or get interpreted as prose — neither produces the intended weighting effect.

**What to do instead:**
```
A photorealistic portrait with exceptional facial detail and sharp focus.
```

---

### Mistake 2: Using Negative Prompts

**What people do:**
```
A beautiful landscape. No mountains. No people. No fog. Don't include any buildings.
```

**Why it fails:** FLUX uses natural language generation, not classifier-free guidance with a separate negative conditioning channel. Saying "no mountains" may simply confuse the generation rather than exclude mountains. The community subreddit [r/MistralAI explicitly advises against this](https://www.reddit.com/r/MistralAI/comments/1nv45g5/lechat_prompt_engineer_agent/): "avoid negative prompts with image generation models (like 'don't think of a pink elephant!')."

**What to do instead:**
Describe what you WANT, not what you DON'T want:
```
A rolling green grassland with a clear blue sky, empty of any structures, featuring only low hills and wildflowers.
```

---

### Mistake 3: Keyword Lists Instead of Descriptions

**What people do:**
```
cyberpunk, female, warrior, neon, rain, dark, dramatic, glowing eyes, armor
```

**Why it fails:** With the LLM layer interpreting your prompt, context and relationships between elements matter. A keyword list gives the LLM nothing to work with compositionally — it doesn't know how these elements relate to each other.

**What to do instead:**
```
A female cyberpunk warrior standing in a rain-soaked alley, her powered armor illuminated by neon signs reflecting in puddles. Her eyes glow faint blue. Dark, dramatic composition.
```

---

### Mistake 4: Vague Aesthetics Without Specifics

**What people do:**
```
A beautiful mountain landscape with amazing colors at sunset.
```

**Why it fails:** "Beautiful", "amazing", "stunning" are editorial opinions, not visual specifications. The LLM has no instruction about what kind of mountains, what palette, what composition, what shot type.

**What to do instead:**
```
Rocky alpine peaks dusted with early snow, reflected in a still glacial lake at golden hour. Warm amber light on the rock faces, cool blue shadows in the valleys. Wide establishing shot, rule of thirds.
```

---

### Mistake 5: Conflicting Styles

**What people do:**
```
A photorealistic anime portrait of a woman in a pixel art office.
```

**Why it fails:** Photorealistic, anime, and pixel art are mutually incompatible aesthetic styles. The model has to choose which to honor; results are unpredictable.

**What to do instead:**

Choose one dominant style and stick to it:
```
An anime-style portrait of a woman sitting at a desk in a detailed office environment. Clean cell-shaded style, soft pastel colors.
```

Or blend compatible styles:
```
A painterly anime portrait, watercolor washes with ink linework, Makoto Shinkai aesthetic.
```

---

### Mistake 6: Not Enabling Image Generation

Image generation must be enabled via the **Tools menu** toggle. Without it, Le Chat treats your prompt as a text request. Community tutorials consistently flag this as the most common setup error. ([YouTube tutorial](https://www.youtube.com/watch?v=5gaGcL9jyWU))

**Check:** Bottom of chat window → Tools → Image generation checkbox = enabled.

---

### Mistake 7: Expecting Portrait or Square Output

Le Chat primarily generates landscape images. Requesting "portrait", "vertical", "9:16" or similar may have no effect. Mistral support has confirmed portrait format is not supported. ([Reddit](https://www.reddit.com/r/MistralAI/comments/1m67o4c/why_le_chat_can_only_generates_landscape_images/))

**Workaround:** Upload a portrait-oriented image and request edits — Le Chat preserves uploaded image aspect ratios.

---

### Mistake 8: Fighting the Prompt Enhancement

Le Chat rewrites your prompt. You cannot fully control exactly what FLUX receives. Trying to counteract this with extremely rigid or technical prompt syntax often backfires.

**Work with it:** Write clear, detailed natural language. Le Chat's prompt enhancement is often additive, not substitutive — it typically builds on your description rather than replacing it.

---

### Mistake 9: One-Shot Complex Compositions

Trying to get everything right in a single dense prompt is less reliable than iterative refinement.

**Ineffective:**
```
[300-word description with 15 specific elements, precise measurements, exact color hex codes, multiple text elements, specific lighting rigs, exact aspect ratio, custom film look]
```

**Better approach:**
1. Generate with core subject and style
2. Evaluate
3. Add one element via conversational edit
4. Repeat

---

### Mistake 10: Using Technical Le Chat Claims Without Verification

Do not use Le Chat's self-descriptions of its image capabilities as documentation. As detailed in Section 3, several claimed features are hallucinated or exaggerated. Test every non-obvious claimed syntax empirically.

---

## 14. Advanced Techniques

### Technique 1: Conversational Refinement Loop

Le Chat's biggest differentiator from non-conversational image generators is the ability to build iteratively.

**Workflow:**

```
Turn 1: Generate base image (core subject + rough style)
Turn 2: "Keep the composition. Change the lighting to golden hour from the left."
Turn 3: "The sky is too busy. Simplify to a clean gradient."
Turn 4: "Add a lone figure in the middle distance, silhouetted."
Turn 5: "Perfect. Increase overall contrast slightly."
```

Each edit builds on previous context. The model retains the prior generation as a reference point.

---

### Technique 2: Structured Field Format

For reproducible, consistent outputs — especially for templates or system prompts — use the labeled field format from official documentation:

```
Subject: [primary content]
Style: [aesthetic/medium]
Composition: [shot type and framing]
Lighting: [light source and quality]
Colors: [palette specification]
Background: [environment if relevant]
Aspect: [ratio]
```

This format is unambiguous, easy to parameterize, and maps cleanly to how the Mistral LLM parses image instructions.

---

### Technique 3: Single-Variable Iteration

When testing prompt components, change one variable at a time. This is essential for understanding what actually affects output:

```
# Baseline
Subject: leather armchair. Style: photorealistic. Lighting: soft window light. Aspect: 4:3.

# Iteration A (change style only)
Subject: leather armchair. Style: flat illustration. Lighting: soft window light. Aspect: 4:3.

# Iteration B (change lighting only)  
Subject: leather armchair. Style: photorealistic. Lighting: dramatic hard directional. Aspect: 4:3.
```

---

### Technique 4: Style Mixing

Combining compatible styles can produce distinctive hybrid aesthetics:

| Combination | Effect |
|-------------|--------|
| `oil painting + cyberpunk` | Classical technique, futuristic subject |
| `watercolor + architectural photography` | Soft organic rendering of hard structures |
| `pixel art + horror` | Nostalgic retro + unsettling subject |
| `ukiyo-e + sci-fi` | Japanese woodblock meets space opera |
| `Wes Anderson + documentary` | Symmetrical, deadpan but gritty |
| `brutalist + fashion photography` | Raw concrete backdrop, high-fashion subject |

**Important:** Combine aesthetic styles, not rendering paradigms. "Photorealistic + anime" = conflict. "Film photography + impressionist color" = viable.

---

### Technique 5: Artist and Director References

You can reference real artists and directors as aesthetic shorthand. FLUX's VLM has strong visual knowledge from training data.

**Effective references:**

| Reference | Effect |
|-----------|--------|
| `in the style of Edward Hopper` | Solitude, urban Americana, directional light |
| `Ansel Adams black and white` | High contrast landscape, large format sharpness |
| `Vermeer lighting` | Window light from one side, warm interior |
| `Syd Mead retrofuturism` | 1970s–80s sci-fi industrial design |
| `Moebius / Jean Giraud` | Clean ligne claire sci-fi illustration |
| `H.R. Giger aesthetic` | Biomechanical dark surrealism |
| `Stanley Kubrick cinematography` | Symmetrical, cold, geometric |
| `Roger Deakins lighting` | Naturalistic, golden, precise |

**Caution:** Le Chat may decline prompts that appear to directly reproduce copyrighted specific works. References to aesthetic style (not reproduction) are generally fine.

---

### Technique 6: Canvas + Image Generation Workflow

For complex creative projects:

```
1. Generate initial image via chat (Image Generation tool enabled)
2. Enable Canvas (Tools menu → Canvas)
3. Generate a document or layout structure in Canvas (e.g., poster layout)
4. Switch between Canvas and image generation to iteratively refine
5. Export Canvas content alongside generated imagery
```

Canvas supports HTML, React, Mermaid diagrams, and Marp presentations — useful for building image-integrated deliverables.

---

### Technique 7: Agent-Based Programmatic Generation

For production systems, cache the agent:

```python
import os
import json
from mistralai import Mistral
from mistralai.client.models import ToolFileChunk

class ImageGenerator:
    def __init__(self):
        self.client = Mistral(api_key=os.environ["MISTRAL_API_KEY"])
        self._agent_id = None
    
    @property
    def agent_id(self):
        if not self._agent_id:
            agent = self.client.beta.agents.create(
                model="mistral-medium-latest",
                name="Production Image Agent",
                description="High-quality image generation agent.",
                instructions=(
                    "You are an image generation agent. "
                    "When asked to create an image, use the image generation tool immediately. "
                    "Do not add commentary before or after the image unless asked."
                ),
                tools=[{"type": "image_generation"}],
                completion_args={"temperature": 0.3, "top_p": 0.95}
            )
            self._agent_id = agent.id
        return self._agent_id
    
    def generate(self, prompt: str, output_path: str) -> str:
        response = self.client.beta.conversations.start(
            agent_id=self.agent_id,
            inputs=prompt
        )
        for chunk in response.outputs[-1].content:
            if isinstance(chunk, ToolFileChunk):
                file_bytes = self.client.files.download(file_id=chunk.file_id).read()
                with open(output_path, "wb") as f:
                    f.write(file_bytes)
                return output_path
        raise RuntimeError("Generation failed — no image in response")


# Usage
gen = ImageGenerator()
gen.generate("A minimal product shot of a glass perfume bottle. Aspect: 3:2.", "perfume.png")
gen.generate("A flat illustration of a city skyline at night. Aspect: 16:9.", "skyline.png")
```

---

### Technique 8: Prompt Chaining for Complex Outputs

Generate base content → refine with targeted edits:

```python
# Stage 1: Generate base image
response1 = client.beta.conversations.start(
    agent_id=agent_id,
    inputs="Subject: empty white-walled art gallery. Style: architectural photography. Lighting: diffuse overhead. Aspect: 16:9."
)

# Stage 2: Add specific artwork (using conversation continuation)
conversation_id = response1.id
response2 = client.beta.conversations.append(
    conversation_id=conversation_id,
    inputs="Add a large abstract oil painting in blues and golds on the main wall. Keep the gallery architecture unchanged."
)

# Stage 3: Add visitors
response3 = client.beta.conversations.append(
    conversation_id=conversation_id,
    inputs="Add two gallery visitors (backs to camera) studying the painting. Keep everything else identical."
)
```

---

### Technique 9: Use Think Mode for Prompt Optimization

Before generating, ask Le Chat to analyze and optimize your prompt using Think mode:

```
[Enable Think mode]
"I want to generate an image of: a jazz musician playing trumpet in a smoky bar at midnight. Optimize this as an image generation prompt with all necessary visual components. Then generate the image."
```

Le Chat's reasoning will fill in visual components you may have overlooked, and the generated prompt becomes a template for future iterations.

---

### Technique 10: System Prompt Engineering for Agents

When building API agents, the `instructions` field shapes how aggressively the agent uses image generation and how it interprets requests:

```python
# Minimal instruction (generates only when explicitly requested)
instructions = "Use the image generation tool only when the user explicitly asks for an image."

# Aggressive instruction (generates images in response to any visual request)
instructions = (
    "You are an image generation specialist. "
    "Whenever a user describes a scene, object, concept, or visual they want, "
    "immediately invoke the image generation tool. "
    "Do not ask for clarification unless the request is completely ambiguous. "
    "Always use the structured format: Subject, Style, Composition, Lighting, Colors, Aspect."
)

# Batch instruction (generates multiple variations)
instructions = (
    "You are an image variation generator. "
    "When asked for an image, generate 3 variations of the requested subject "
    "in different styles (photorealistic, illustration, and painterly). "
    "Label each variation clearly in your response."
)
```

---

## 15. Quick Reference Card

### Prompt Formula

```
[Subject] + [Action/Context] + [Style] + [Composition] + [Lighting] + [Colors] + [Aspect]
```

**Minimal working prompt:**
```
Subject: [what]. Style: [how]. Aspect: [ratio].
```

**Full prompt:**
```
Subject: [specific subject with attributes].
Action: [what it's doing or where it exists].
Style: [medium and aesthetic].
Composition: [shot type, angle, framing].
Lighting: [source, direction, quality].
Colors: [palette or dominant hues].
Aspect: [ratio].
```

---

### Top 10 Style Keywords

| # | Keyword | Best For |
|---|---------|----------|
| 1 | `photorealistic` | Products, people, environments |
| 2 | `flat illustration` | UI, icons, marketing |
| 3 | `cinematic` | Dramatic scenes |
| 4 | `oil painting` | Art, portraits |
| 5 | `anime style` | Characters, storytelling |
| 6 | `watercolor` | Soft, organic subjects |
| 7 | `3D render` | Products, tech, architecture |
| 8 | `pixel art` | Games, retro, icons |
| 9 | `concept art` | Environments, characters |
| 10 | `Studio Ghibli aesthetic` | Warmth, nature, narrative |

---

### Top 10 Lighting Keywords

| # | Keyword | Effect |
|---|---------|--------|
| 1 | `golden hour` | Warm, cinematic |
| 2 | `soft diffuse` | Even, shadow-free |
| 3 | `studio three-point` | Professional, controlled |
| 4 | `Rembrandt lighting` | Dramatic portrait |
| 5 | `rim lighting` | Separation, silhouette |
| 6 | `volumetric lighting` | God rays, atmospheric |
| 7 | `neon lighting` | Urban, night, colorful |
| 8 | `candlelight` | Intimate, warm |
| 9 | `overcast daylight` | Natural, flat |
| 10 | `window light` | Indoor natural |

---

### Top 10 Camera Keywords

| # | Keyword | Use Case |
|---|---------|----------|
| 1 | `close-up` | Portraits, emotions |
| 2 | `wide establishing shot` | Scenes, environments |
| 3 | `overhead flat lay` | Products, food |
| 4 | `low angle` | Power, scale |
| 5 | `35mm lens` | Natural portraits |
| 6 | `85mm portrait lens` | Flattering close-ups |
| 7 | `macro` | Texture, detail |
| 8 | `bird's-eye view` | Maps, layouts |
| 9 | `cinematic widescreen` | Movies, epic scenes |
| 10 | `eye level medium shot` | Characters, dialogue |

---

### Aspect Ratios

| Ratio | Format | Status |
|-------|--------|--------|
| `16:9` | Landscape wide | Confirmed working |
| `4:3` | Landscape standard | Likely working |
| `3:2` | Landscape photo | Likely working |
| `1:1` | Square | Conflicting reports |
| `9:16` | Portrait tall | NOT SUPPORTED |
| `2:3` | Portrait photo | NOT SUPPORTED |

**Specify as:** `Aspect: 16:9` at end of prompt.

---

### API Setup Steps

```bash
pip install mistralai
export MISTRAL_API_KEY=your_key_here
```

1. Create agent: `client.beta.agents.create(tools=[{"type": "image_generation"}])`
2. Start conversation: `client.beta.conversations.start(agent_id=..., inputs=prompt)`
3. Download: `client.files.download(file_id=chunk.file_id)`
4. Save as PNG

---

### Content Policy Summary

**Always prohibited:**
- CSAM (zero tolerance, law enforcement reporting, instant account termination)
- Non-consensual intimate imagery of real people
- Hate/discrimination content
- Violence glorification
- Self-harm encouragement
- Copyright infringement
- Impersonation without consent

**Not available:**
- Adult content mode
- NSFW toggle
- Age verification bypass
- Artistic nudity exception

**Allowed within policy:**
- Fantasy violence (not glorified, not instructional)
- Dark/horror aesthetics
- Villain and antagonist characters
- Historical conflict scenes
- Dystopian/post-apocalyptic imagery
- Stylized combat
- Educational and documentary content

---

### Common Mistakes Cheat Sheet

| Wrong | Right |
|-------|-------|
| `(keyword:1.2)` weighting | Natural language description |
| `--no blur` negative prompts | Describe what you WANT |
| Comma-separated keyword lists | Full sentences with context |
| "Beautiful", "amazing" | Specific visual properties |
| Multiple conflicting styles | One coherent style per prompt |
| Forgetting to enable Tools | Always check Tools menu first |
| Expecting portrait output | Use landscape or upload-edit workaround |
| Dense 300-word first prompt | Iterate: base → edit → edit |
| Trusting Le Chat's self-description | Cross-reference with Section 3 |

---

## Sources

- [Mistral AI — The All New Le Chat (Feb 2025)](https://mistral.ai/news/all-new-le-chat)
- [Mistral AI — Le Chat Launch with FLUX Pro (Nov 2024)](https://mistral.ai/news/mistral-chat)
- [Mistral Help — How do I generate images with le Chat?](https://help.mistral.ai/en/articles/347534-how-do-i-generate-images-with-le-chat)
- [Mistral Help — Canvas Overview](https://help.mistral.ai/en/articles/393385-what-is-canvas-and-how-do-i-use-it-to-create-content-interactively)
- [Mistral Docs — Image Generation Tool (API)](https://docs.mistral.ai/agents/tools/built-in/image_generation)
- [Mistral Usage Policy](https://legal.mistral.ai/terms/usage-policy)
- [Black Forest Labs — FLUX.2 Announcement](https://bfl.ai/blog/flux-2)
- [The Decoder — Black Forest Labs launches Flux 2](https://the-decoder.com/black-forest-labs-launches-flux-2-with-a-new-multi-reference-feature/)
- [The Decoder — Mistral adds FLUX image generation to Le Chat](https://the-decoder.com/mistral-ai-adds-flux-image-generation-and-web-search-to-le-chat-launches-pixtral-large/)
- [Digital Applied — FLUX.2 Max Complete Guide](https://www.digitalapplied.com/blog/flux-2-max-black-forest-labs-guide)
- [MindStudio — FLUX 1.1 Pro Ultra Guide](https://www.mindstudio.ai/blog/what-is-flux-1-1-pro-ultra/)
- [Reddit r/MistralAI — Aspect ratio thread (July 2025)](https://www.reddit.com/r/MistralAI/comments/1m67o4c/why_le_chat_can_only_generates_landscape_images/)
- [Reddit r/MistralAI — LeChat Prompt Engineer Agent](https://www.reddit.com/r/MistralAI/comments/1nv45g5/lechat_prompt_engineer_agent/)
- [Reddit r/MistralAI — Prompting for Beginners Tutorial](https://www.reddit.com/r/MistralAI/comments/1ohit02/minitutorial_prompting_for_beginners_by_unefhis/)
- [getimg.ai — What is FLUX.1?](https://getimg.ai/blog/what-is-flux-1-the-breakthrough-ai-model-you-need-to-know)
- [Mistral Help — Better Answers with Simple Prompting Techniques](https://help.mistral.ai/en/articles/424366-get-better-answers-with-simple-prompting-techniques)
