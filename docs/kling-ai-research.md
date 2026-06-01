# Kling AI: Exhaustive Prompt Engineering & Cinematic Production Guide

> **File:** `kling-ai-research.md` · **Target:** 12,000–16,000 words  
> **Verified:** May 25, 2026 · Sources: Kuaishou official (EN/ZH), fal.ai docs, Wikipedia, DataCamp, invideo.io, voiceoverstudioai.com, kling.ai official guides, community (YouTube, Reddit, Bilibili), third-party platforms

---

## 1. VERIFICATION NOTE — Current Model Lineup & Feature Inventory

*Verified against Kuaishou IR press releases (February 5, 2026), kling.ai official release notes, Wikipedia's Kling AI article (verified May 2026), fal.ai API docs (May 2026), and vo3ai.com pricing data (May 2026).*

### Active Models (May 2026)

| Model | Variants | Resolution | Max Duration | FPS | Key Capability |
|---|---|---|---|---|---|
| **Kling 1.6** | Standard, Pro | 720p / 1080p | 5s (Std) / 10s (Pro) | 24/30fps | T2V + I2V baseline; Pro: start+end frame (5s only) |
| **Kling 2.0 Master** | Master only | 720p | 5s | 24fps | Improved realism, camera motion, prompt adherence |
| **Kling 2.1** | Standard, Pro, Master | 720p / 1080p | 5–10s | 30fps | Standard+Pro: built-in sound effects; Master: premium dynamics |
| **Kling 2.5 / 2.5 Turbo** | Standard, Pro | 1080p | 10s | 30fps | ~2× faster, ~30% cheaper; Turbo led AI video leaderboards Oct 2025 |
| **Kling 2.6** | Standard, Pro | 1080p | 10s | 30fps | Native audio (EN+ZH); enhanced consistency; motion-reference video |
| **Kling O1 (Video O1 / Omni)** | Standard, Pro | 1080p | 10s | 30fps | Start/end frame, up to 4 Elements, video editing, scene extension |
| **Kling 3.0 (Video 3.0)** | Standard, Pro | 720p–1080p | 3–15s | 30–60fps | Multi-shot (up to 6 shots); native audio EN/ZH/JA/KO/ES; element ref |
| **Kling O3 (Video 3.0 Omni)** | Standard, Pro | 720p–4K | 3–15s | 30–60fps | All V3.0 + up to 7–10 element refs; video-element extraction; voice cloning |
| **Image 3.0 / 3.0 Omni** | — | Up to 4K | — | — | Ultra-HD image gen; text accuracy; style consistency |

**Launched:** Kling 3.0 and O3 — February 5, 2026. Early access Ultra subscribers; broadly available by March 2026.

### Quality Tier Summary (within a model)

| Tier | What Changes |
|---|---|
| **Standard** | Fastest, cheapest; lower visual fidelity; 720p typical |
| **Pro** | Higher detail, 1080p, slower; "richer details and superior quality" |
| **Master** | (Available in 2.0/2.1) — highest dynamics, best prompt adherence; ~100 credits/5s clip |

### Feature Inventory Confirmed (May 2026)

- ✅ **Text-to-Video (T2V)** — all models
- ✅ **Image-to-Video (I2V)** — all models; start+end frame in 1.6 Pro, 2.1+, O1, 3.0/O3
- ✅ **Video-to-Video / Reference Video** — O1, 2.6, O3 (motion transfer; style restyle)
- ✅ **Elements / Multi-Elements** — O1 (4 refs), 3.0 (ref support), O3 (up to 7–10 refs + video extraction)
- ✅ **Motion Brush** — 1.5+; incompatible with Camera Control presets and End Frame simultaneously
- ✅ **Camera Control (Presets)** — 6 basic + 4 Master Shots (see §B.5)
- ✅ **Start Frame + End Frame** — 1.6 Pro (5s only), 2.1+, O1, 3.0/O3
- ✅ **Extend** — all models; adds 5s segments from existing clips
- ✅ **Lip Sync** — dedicated feature; TTS + custom audio upload; separate from native audio
- ✅ **Multi-Shot Storyboarding** — 3.0 and O3 only; up to 6 shots per 15s generation
- ✅ **Native Audio Generation** — 2.6 (EN+ZH only); 3.0/O3 (EN, ZH, JA, KO, ES + accents/dialects)
- ✅ **Try-On** — virtual garment fitting (image-based); Kolors model; separate feature
- ✅ **Avatar / Talking Head** — via Kling Avatar 2.0 interface
- ✅ **Image Generation** — Image 3.0, Image 3.0 Omni (up to 4K)
- ✅ **Prompt Enhancement** — Built-in DeepSeek R1 prompt rewriter

### Native Audio: Honest Summary
- **2.1 Standard/Pro:** Built-in sound effects only (ambient SFX, toggleable free feature). No dialogue generation.
- **2.6:** Native audio in English and Chinese — dialogue + ambient. Lip-sync synced to generated speech.
- **3.0 / O3:** Full native audio — dialogue, ambient, SFX, background music — in EN, ZH, JA, KO, ES. Multi-character with separate voice tags. Voice cloning in O3 via reference video extraction.
- **All pre-2.6 models (1.6, 2.0, 2.5):** Silent by default. Audio only via Lip Sync feature or post-production.

### Surfaces
- **klingai.com** — International web interface (English); all major features
- **kling.kuaishou.com** — China interface (Chinese); may have additional model access and enterprise features; content policy stricter
- **Kling API** — Via Kuaishou developer portal; enterprise usage
- **fal.ai** — Most widely used Western API; Kling 3.0 and O3 API available; discount codes available
- **Pollo AI, Higgsfield, RunDiffusion, PixVerse, eachlabs, WaveSpeed, VIDEOAI.ME** — Third-party wrappers; variable model availability
- **Adobe Firefly integration** — Kling features available within Firefly workflow (multi-shot, I2V, audio)

### International vs. China Policy Differences
| Aspect | International (klingai.com) | China (kling.kuaishou.com) |
|---|---|---|
| Content moderation | Moderate — blocks NSFW, violence, political; some commercial scenes pass | Stricter — additional political/social sensitivity filtering |
| Model availability | 3.0, O3, 2.6, O1, 2.5, 2.1, 1.6 | Same + potential beta access to unreleased features |
| Language | English-first UI | Chinese-first; some features documented only in ZH |
| Commercial use | Basic plan: no commercial use; Standard+ plan: commercial use allowed | Enterprise contracts available |
| AI labeling | Embedded metadata per GB 45438-2025 standard | Required: visible labels + embedded metadata per CAC March 2025 regulation |

---

## 2. EXECUTIVE SUMMARY

Kling AI, developed by Kuaishou Technology (Beijing), has rapidly ascended from a niche Chinese AI video tool to what multiple independent benchmarks describe as the world's top-tier AI video generator as of early 2026. With the Kling 3.0 launch on February 5, 2026, Kuaishou unified video generation, image generation, native multimodal audio, multi-shot storyboarding, and character consistency under a single architecture — the Multi-modal Visual Language (MVL) framework.

For professional filmmakers and creative producers, Kling's strategic advantages are:

1. **Motion quality** — Kling consistently ranks highest for natural camera movement, physics simulation, and fluid character motion. Its DiT + 3D VAE architecture enables spatiotemporal coherence that translates to cinematic camera work without the mechanical jitter of competing models.

2. **Multi-shot native generation** — Starting with 3.0, Kling can generate up to six distinct shots in a single 15-second clip, each with independent camera direction, subject action, and framing. This eliminates the clip-stitching workflows that dominated prior AI video production pipelines.

3. **Native multimodal audio** — Kling 3.0/O3 generates synchronized dialogue, ambient sound, and background music natively in five languages including accents and dialects, with per-character voice tags enabling multi-person scenes. This is a direct competitor to Google Veo 3.1 for "one-generation" audiovisual production.

4. **Character and subject consistency** — The Elements system (up to 10 reference images in O3) solves the "gacha problem" of identity drift across shots and extensions. Combined with the `@ElementName` prompt syntax, producers can maintain a single character's face, build, and voice across an entire short-film pipeline.

5. **Prompt philosophy** — Kling is trained to understand *cinematic intent*, not just visual descriptions. Prompts written as scene directions ("the camera slowly pushes in as she looks away") consistently outperform tag-soup approaches. The model understands focal length references, lighting scheme names, cinematographer style references, and shot terminology.

**Weaknesses to acknowledge honestly:**
- Hand and finger anatomy: improved significantly in 3.0 but still occasionally fails on complex hand interactions, particularly multi-hand scenes. Negative prompting and zoomed-out framing mitigate.
- Text-in-frame rendering: 3.0 introduced meaningful improvement for in-frame text (signage, branding), but arbitrary complex text remains unreliable.
- Very fast motion (>100km/h subject speed): tends toward blur artifacts or physics violations; Kling excels at 30–120fps slow-motion but struggles with extreme velocity.
- Lip sync in non-photorealistic styles: anime and stylized animation lip sync quality degrades noticeably vs. photorealistic.
- Extreme spatial complexity: scenes with 5+ independently moving characters in tight frame risk identity confusion.

---

## 3. PRODUCT & MODEL FOUNDATIONS

### 3.1 Architecture

Kling uses a **Diffusion-based Transformer (DiT)** architecture enhanced with Kuaishou's proprietary components:

- **3D VAE (Variational Autoencoder):** Performs *synchronous spatiotemporal compression* — encoding both spatial (pixel-level) and temporal (motion-across-frames) information simultaneously, rather than treating them sequentially. This is the core reason for Kling's superior motion consistency versus architectures that model space and time separately.
- **Full-Attention Spatiotemporal Module:** A computationally efficient full-attention mechanism that integrates temporal and spatial features, allowing the model to capture both local intra-frame details and cross-frame dynamic patterns. This enables accurate rendering of fast-moving objects and drastic scene changes.
- **MVL (Multi-modal Visual Language) Framework** (introduced v2.0, expanded v3.0): Allows multimodal inputs (text, image, audio, video) to be processed as unified "documents" (the MMW concept — Multi-modal-document as a Word), enabling complex creative intent to be expressed without multiple separate tools.

The 3D VAE is why Kling beats many competitors on camera dolly and pan smoothness — the architecture understands the entire clip as a 3D space-time volume, not a sequence of still frames.

### 3.2 Model Version Timeline

| Version | Release | Key Milestone |
|---|---|---|
| Kling 1.0 | June 2024 | Beta in KuaiYing (China); global launch July 2024 |
| Kling 1.5 | ~Aug 2024 | Motion Brush introduced; 4K upscale |
| Kling 1.6 | December 2024 | Improved T2V + I2V; Start+End Frame in Pro |
| Kling 2.0 Master | April 2025 | MVL introduced; improved realism |
| Kling 2.1 | May 2025 | Standard/Pro/Master; SFX built-in for Std/Pro |
| Kling 2.5 / Turbo | ~Aug–Oct 2025 | 2× speed, 30% cost reduction; leaderboard #1 Oct 2025 |
| Kling 2.6 | ~Nov 2025 | Native audio EN+ZH; motion reference video |
| Kling O1 (Video O1) | ~Dec 2025 | Start/End frame, 4-element injection, editing |
| **Kling 3.0 + O3** | **Feb 5, 2026** | Multi-shot, 15s, 4K, 5-language audio, voice clone |

### 3.3 Clip Length, Resolution, Aspect Ratios per Tier

| Model | Std Resolution | Pro Resolution | Max Duration | Aspect Ratios |
|---|---|---|---|---|
| 1.6 Standard | 720p | — | 5s | 16:9, 9:16, 1:1 |
| 1.6 Pro | — | 1080p | 10s | 16:9, 9:16, 1:1 |
| 2.0 Master | 720p | — | 5s | 16:9, 9:16, 1:1 |
| 2.1 | 720p | 1080p | 5–10s | 16:9, 9:16, 1:1 |
| 2.5 / Turbo | 1080p | 1080p | 10s | 16:9, 9:16, 1:1 |
| 2.6 | 1080p | 1080p | 10s | 16:9, 9:16, 1:1 |
| O1 | 1080p | 1080p | 10s | 16:9, 9:16, 1:1 |
| **3.0** | **720p–1080p** | **1080p** | **3–15s** | **16:9, 9:16, 1:1** |
| **O3** | **720p–4K** | **up to 4K** | **3–15s** | **16:9, 9:16, 1:1** |

Frame rate: 30fps standard for Pro; 24fps for some Standard modes; 3.0/O3 supports 30–60fps.

### 3.4 Credit Cost Economics (Verified May 2026)

**Subscription Plans (klingai.com / vo3ai.com data, May 2026):**

| Plan | Monthly Price | Yearly (per mo.) | Key Access |
|---|---|---|---|
| Basic (Free) | $0 | — | Daily login credits; no commercial use; 30 element creations |
| Standard | $8.80/mo ($6.99 promo) | ~$6.60/mo | Commercial use; 660 credits/mo |
| Pro | $25.99/mo | ~$24.42/mo | Higher volume; ~1,320 credits/mo |
| Premier | $64.99/mo | ~$60.72/mo | ~3,500 credits/mo |
| Ultra | $127.99/mo | ~$119.17/mo | 8,000+ credits/mo; early model access |

**Credit Costs per Generation:**

| Tier/Setting | Cost per 5s clip | Cost per 10s clip | Notes |
|---|---|---|---|
| Kling 2.1 Standard | 20 credits | — | Fastest, cheapest |
| Kling 2.1 Pro | 35 credits | 70 credits | Sound effects free |
| Kling 2.1 Master | 100 credits | — | 5s only |
| Kling 3.0 Standard (no audio) | ~30–36 credits | ~60–72 credits | ~6 cr/sec |
| Kling 3.0 Pro (no audio) | ~50–60 credits | ~100–120 credits | |
| Kling 3.0 Pro (with audio) | ~70–90 credits | ~140–180 credits | ~12 cr/sec |
| Kling O3 Standard (no audio) | 125 credits | 250 credits | PixVerse pricing |
| Kling O3 Standard (with audio) | 175 credits | 350 credits | |
| Extend (+5s) | ~35 credits | — | Per extension segment |

**Real-cost reality check:** A 10-second 1080p Kling 3.0 Pro clip with audio on the official platform costs roughly $2.80–4.20 at list credit prices. With a Pro plan amortization, this drops to approximately $1.00–1.50/usable clip after accounting for generation failures.

**API (fal.ai):** Kling O1 billed at $0.112/second. Kling 3.0 standard at approximately $0.14/second; Pro with audio ~$0.28/second. No subscription required; pure pay-per-use.

### 3.5 API vs. Web vs. Third-Party Delta

| Capability | klingai.com Web | fal.ai API | Pollo / Higgsfield / RunDiffusion |
|---|---|---|---|
| Latest model access | Yes (Ultra for early access) | Yes (O3 + V3) | Variable — usually 1–2 weeks lag |
| Multi-shot storyboard UI | Yes (Custom + Smart modes) | Via API parameters | Some platforms support it |
| Elements UI | Yes (full GUI) | O3 via API | Limited |
| Prompt enhancer (DeepSeek) | Built-in | No | Some platforms |
| Negative prompts | Yes | Via `negative_prompt` param | Most support |
| Camera Control presets | Yes (GUI sliders) | Via parameters | Varies |
| Motion Brush | Yes (GUI) | No direct | No |
| Bulk generation | Limited | Yes (async jobs) | Varies |
| Cost | Credits (subscription) | Per-second billing | Varies; often more expensive |

---

## 4. COMPETITIVE LANDSCAPE

*Label: COMMUNITY-VERIFIED (multiple independent sources, May 2026)*

| Dimension | Kling 3.0 / O3 | Google Veo 3.1 | Sora 2 | Runway Gen-4 | Luma Ray 3 | Pika 2.5 | Hailuo / MiniMax | Wan 2.6 |
|---|---|---|---|---|---|---|---|---|
| **Best for** | Multi-shot narrative, character consistency, volume production | Cinematic B-roll, photorealism, 4K | Narrative realism, experimental | VFX, stylized, longer clips | Product shots, atmospheric | Social UGC, performance lip-sync | Cinematic quality output | Open-source, free |
| **Native audio** | ✅ 5 languages | ✅ | Partial | ❌ | ❌ | Partial (Pikaformance) | Limited | ❌ |
| **Max duration** | 15s (multi-shot) | ~8s | ~20s | 16s+ | 10s | 10s | 10s | 10s |
| **Multi-shot native** | ✅ (6 shots) | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Character consistency** | ✅ (Elements) | Limited | Good | Good | Limited | Limited | Good | Limited |
| **Prompt adherence** | High | Very high | High | High | Medium | Medium | High | Medium |
| **Physics sim** | Excellent | Excellent | Excellent | Good | Good | Moderate | Good | Good |
| **Hand anatomy** | Improved (3.0) | Good | Excellent | Good | Good | Moderate | Good | Moderate |
| **Cost** | Medium ($0.14–0.28/s) | Free–medium | Expensive / limited | Medium | Medium | Low–medium | Low | Free |
| **Availability** | Global | US/limited | Limited | Global | Global | Global | Global | Open source |
| **Kling's specific edge** | Multi-shot + audio + character consistency in one generation; best multi-reference control | — | — | — | — | — | — | — |

**Key Kling Strengths (vs. field):**
- Only model (as of May 2026) with 6-shot multi-shot native generation
- Most sophisticated Elements/multi-reference system for character consistency
- Best-in-class camera motion (dolly, orbit, techno-crane feel)
- Strongest slow-motion physics rendering
- Most complete native audio (5 languages, multi-character, voice cloning in O3)

**Key Kling Weaknesses (honest):**
- Photorealism ceiling below Veo 3.1 for pure establishing shots
- Maximum clip duration (15s) lags Sora 2 (~20s) and some Runway modes (16s+)
- Availability limitations (some features gated to Ultra plan on web)
- No true uncensored mode for mature commercial content (alcohol featured products, certain violence levels, etc.)

---

## 5. FEATURE-BY-FEATURE DEEP DIVE

### 5.1 Text-to-Video (T2V)

**Available:** All models. Best results on 3.0 Pro or O3.

**Optimal Prompt Structure for Kling:**

Kling performs best with **structured natural-language paragraphs**, not comma-separated tags. The model is trained on Chinese film and video content alongside global training data, and it responds to *directorial language* — descriptions of what the camera is doing, what the scene feels like, and what actions unfold sequentially.

**Confirmed optimal formula (COMMUNITY-VERIFIED, fal.ai + DataCamp + multiple practitioners):**

```
[Camera setup & movement] — [Subject description] — [Action sequence] — [Environment/scene] — [Lighting & atmosphere] — [Style reference] — [Audio if using 3.0/O3]
```

**Alternative mnemonic frameworks:**
- **SCACA** (from Dzine/YouTube community): Scene, Character, Action, Camera, Audio
- **Official Kling formula** (from kling.ai/quickstart): Subject + Movement + Scene + (Camera + Lighting + Atmosphere)
- **fal.ai multi-shot formula**: Shot label + framing + subject + motion + audio

**Paragraph vs. Tag approach:**
- ✅ Paragraph/cinematic prose: "A detective in a rumpled trench coat strides across rain-soaked cobblestones at night. The camera dollies slowly alongside him at mid-shot, capturing neon reflections on wet stone. Chiaroscuro lighting from a single sodium-vapor streetlamp casts long diagonal shadows."
- ❌ Tag soup: "detective, rain, noir, cinematic, 4K, dramatic lighting, neon, walking, trench coat"

**Optimal prompt length:**
- Standard tier: 50–150 words. Overloading causes drift.
- Pro tier: 100–250 words effective.
- 3.0 multi-shot: Each shot prompt capped at 500 characters; 6 shot fields = ~3,000 characters total.
- Single T2V: 200–400 words is the practical sweet spot for 3.0 Pro.

**Positional weighting:** CONFIRMED (community + official). The model gives stronger weight to the opening sentences. Lead with the most important visual instruction (camera position and subject action). Save stylistic modifiers for the second half.

**Negative prompts:** ✅ Fully supported. Separate field in the interface and as API parameter. Use comma-separated terms without the word "no" — just list the artifact or element to exclude. "blurry, distorted hands, extra limbs, watermark, text overlay, flickering, morphing face" is a standard baseline.

**Multi-shot prompting (3.0 only):**
- **Smart Storyboard mode:** Write a single prose paragraph with transition cues ("cut to," "then," "followed by"). Kling auto-segments into up to 6 shots.
- **Custom Multi-Shot mode:** Write one 500-character prompt per shot. Manually set each shot's duration (minimum 3s per shot). Reference elements with `@ElementName`.
- **Failure mode:** Ambiguous transition language causes the model to blend two shots rather than cut. Use explicit "CUT TO:" or "Shot 2:" labeling in Custom mode.

**Chinese vs. English prompting:**
- Both languages produce high-quality results (OFFICIAL — multilingual support confirmed).
- Chinese prompts may activate slightly different aesthetic defaults — more aligned with Chinese film aesthetics (certain color palettes, human expression conventions).
- For Western aesthetic targets, English prompts are more reliable.
- Technical tip (COMMUNITY-VERIFIED, Scribd/Kling guide): if a prompt triggers a refusal in English, rephrasing in Chinese or vice versa sometimes resolves false positives from the content filter.

### 5.2 Image-to-Video (I2V)

**Available:** All models. Most-used feature per official Kling data.

**Core principle:** The image IS the scene description. Your prompt must describe MOTION, not appearance.

**Official Kling formula for I2V:**
```
[Subject] + [Movement] + [Background Movement (optional)]
```

**What to omit from the I2V prompt:** Everything the image already shows — color, costume, location aesthetics, lighting setup. Describing what's already visible creates prompt-image tension that can destabilize the generation.

**Best practices for input image:**
- Resolution: minimum 720p; ideally 1080p or higher for Pro/3.0
- File size: under 10MB (JPG/PNG); official guidance says 512px–4096px
- Aspect ratio: match target output ratio (9:16 portrait for I2V that will be 9:16 output)
- Subject framing: center the primary subject; head+shoulders or full body clearly visible
- Lighting: avoid heavy backlighting or extreme shadows — these confuse the model's face detection for lip sync / motion brush
- Simple backgrounds produce more controllable animations; complex busy backgrounds drift

**Common failure: Prompt fighting the image.** If you describe a scene element that contradicts the image (e.g., image shows daylight, prompt says "moonlight"), the model tries to honor both and produces morphing artifacts or an unwanted cut. Always describe the CHANGE, not the state.

**Start Frame + End Frame specifics:**
- Available: 1.6 Pro (5s clips only), 2.1+, O1, 3.0, O3
- Both frames must share: similar aspect ratio, compatible lighting/color palette, logically bridgeable content
- Prompt describes the transition and motion path between frames
- 5s duration works better than 10s for sharp transitions; 10s better for transformation presets
- FAILURE MODE: Highly divergent start/end frames (e.g., indoors → outdoors) cause the model to morph rather than cut — use a transition element or accept morphing as the intended effect (timelapses, metamorphoses)

**"Bind Subject" consistency feature (3.0 I2V):**
- After uploading I2V source image, toggle "Bind Subject to Enhance Consistency"
- Creates a persistent 3D identity reference that prevents identity drift in motion
- Add 3–4 reference photos to Elements Library from different angles for best multi-angle stability

### 5.3 Elements / Multi-Elements (Multi-Reference)

**Available:** O1 (4 elements max), 3.0 (element refs), O3 (7–10 refs + video extraction)

**What Elements are:** Named, reusable visual assets (characters, objects, environments) stored in your Element Library. Referenced in prompts using the `@ElementName` syntax.

**Creating an element:**
- Provide up to 3–4 images from different angles (front, 3/4, side, profile)
- For O3 character with voice cloning: upload a 3–8 second video clip of the person speaking; system extracts visual features AND voice tone automatically
- Alternatively: upload multi-image set + separate 5–30s audio clip for voice binding

**Prompt structure when using Elements:**
```
[Shot setup] — @[CharacterName] [action] — [environment] — [camera movement] — [audio descriptor if 3.0/O3]
```

**Consistency tactics:**
- Use consistent character description across all shots even with Element binding — reinforces the anchor
- Include directional context ("facing left", "back to camera") to guide which angle of the element is used
- For scene/location elements: provide 4 images covering different corners/angles of the space so the model knows the full spatial layout
- Negative prompts for element stability: `changing clothes, shifting jawline, morphing features, de-aging`

**Limits:**
- O1: 4 elements per generation
- 3.0: Flexible element binding; exact simultaneous cap not publicly specified
- O3: 7 references confirmed in YouTube tutorials; PixVerse documentation cites up to 10

**COMMUNITY-VERIFIED failure mode:** Single-image elements fail when the subject moves to reveal an angle not covered by the reference. Multi-angle element sets (3–4 images) dramatically reduce this.

### 5.4 Motion Brush

**Available:** 1.5+. GUI-only feature (not available via API).

**What it does:** Allows mask-painting specific regions of the input image to define independent motion vectors for different objects. Uses AI auto-segmentation or manual paint tools.

**When to use Motion Brush vs. text-only motion:**
- **Use Motion Brush when:** Multiple objects in frame need different motion directions (foreground subject moves right, background elements drift left); specific object path control is critical (make character walk to exact destination); subtle ambient motion in a specific region
- **Use text prompt motion when:** Single subject; simple camera motion (dolly, pan); overall scene motion (water flowing, leaves rustling)

**Motion Brush workflow:**
1. Upload image to I2V
2. Open Motion Brush panel; AI auto-segments the image
3. Select subject mask(s); use manual brush for precision if auto-seg misses
4. Draw motion path/direction for each masked region (Track tool)
5. Confirm motion assignments; write complementary prompt describing the OVERALL scene context (not the motion — the brush handles that)
6. Generate

**IMPORTANT INCOMPATIBILITIES (OFFICIAL):**
- Motion Brush **cannot** be used simultaneously with Camera Control presets
- Motion Brush **cannot** be used simultaneously with End Frame

**Stroke strategy for natural motion:**
- Draw smooth, physics-plausible arcs — not sharp angles
- For walking: draw a horizontal path in the direction of movement
- For floating/rising: draw a slightly arcing upward path
- For camera orbit illusion: draw curved paths on background elements in the opposite direction to simulate camera rotation
- Shorter strokes with high overlap = slower, more subtle motion
- Longer strokes = faster, more dramatic motion

### 5.5 Camera Control (Preset Moves)

**Available:** GUI feature; all models with Camera Control panel.

**Official preset list (OFFICIAL — kling.ai/quickstart/ai-camera-control-guide):**

**6 Basic Movements:**
1. Horizontal (truck/dolly lateral)
2. Vertical (pedestal up/down)
3. Zoom (in/out)
4. Pan (horizontal axis rotation)
5. Tilt (vertical axis rotation)
6. Roll (camera barrel roll)

**4 Master Shots (compound movements):**
1. Move Left and Zoom In
2. Move Right and Zoom In
3. Move Forward and Zoom Up (crane-style ascent with push)
4. Move Down and Zoom Out (descend and reveal)

Each preset has a **displacement parameter slider** to control speed/magnitude. Reset to 0 removes all movement.

**INCOMPATIBILITY:** Camera Control presets are disabled when Motion Brush is active or when an End Frame is specified.

**Prompt-described moves vs. presets:**
- Presets give **mechanical precision** but are limited to the 10 options listed
- Prompt-only moves allow for **any described motion** — Steadicam, handheld, drone orbit, Vertigo/dolly-zoom, snorricam — but with less deterministic control
- **Best practice:** Use presets for reliable repeated moves (product shots, interview dolly-ins). Use prompt-described motion for creative/complex movements.

**For moves NOT available as presets (prompt-only):**
- Steadicam/gimbal float: "camera follows subject on a floating Steadicam, slight organic sway"
- Handheld: "handheld camera, subtle documentary shake, slightly desaturated"
- Drone orbit: "aerial drone circles the subject clockwise at 10 meters altitude, maintaining lock"
- Dolly-zoom (Vertigo): "slow dolly out combined with a focal length compression zoom in, maintaining subject size, creating spatial distortion effect"
- Snorricam: "camera is strapped to the subject's chest, the background moves chaotically while the subject stays centered in frame"

### 5.6 Start Frame + End Frame (Keyframe Interpolation)

**Available:** 1.6 Pro (5s only), 2.1+, O1, 3.0, O3

**Best practices for keyframe pairs:**
- Keep the subject's pose physically achievable between the two frames (no teleportation)
- Match color temperature between frames for smooth interpolation
- Use 5s duration for sharp transitions; 10s for complex transformations
- For product reveals: start with packaging close, end with product open — Kling fills in the reveal
- For character emotion arcs: start neutral, end expressive — Kling generates micro-expression transition

**How to write the interpolation prompt:**
```
[Subject] transitions from [starting state] to [ending state] via [motion path/action]. 
Camera [movement]. [Lighting maintains consistency / shifts toward X].
```

**FAILURE MODES:**
- **Morphing/melting:** Frames too dissimilar (different environments, colors, angles) cause the model to morph between states rather than animate a physical transition. Solution: ensure spatial/compositional continuity between frames.
- **Identity drift:** Subject's face or costume gradually changes between start and end. Solution: use Element binding; keep frame-to-frame costume consistency; use negative prompts.
- **Jump cut instead of interpolation:** Model decides it cannot interpolate and inserts a cut. Usually caused by irreconcilable perspective difference. Solution: reduce angular difference between frames.

### 5.7 Extend

**Available:** All models; requires active subscription plan.

**How it works:** The Extend feature takes the final frames of an existing clip as context and generates a new 5-second continuation that begins exactly where the source ends.

**Prompting for Extend:**
- The prompt describes WHERE THE SCENE GOES NEXT, not what's already happened
- Reinforce continuity descriptors: color palette, time of day, character name/appearance, camera style
- Specify the continuation action: "continues walking forward, camera pans right to reveal the city skyline"
- Keep camera movement consistent with the source clip unless you want a deliberate cut feel

**Chain length limits:**
- No official hard limit on number of extensions, but quality and consistency degrade with each extension
- COMMUNITY-VERIFIED: 3–4 extensions (15–20 total seconds) are reliable; beyond that, visual drift becomes significant
- Best practice: Generate clean base clips, extend once or twice, then stitch in editing software rather than chaining indefinitely

**Maintaining continuity across extensions:**
- Use identical prompt descriptors for environment and lighting
- Reference the character with consistent phrasing ("the detective in the rumpled trench coat")
- Avoid introducing new characters in extensions — consistency risk
- Identity drift mitigation: take the last frame of the generated clip as a new start frame for next I2V generation instead of using Extend

### 5.8 Lip Sync

**Available:** Dedicated feature; separate from native audio generation.

**Two modes:**
1. **TTS (Text-to-Speech input):** Type text; Kling generates speech from built-in TTS voices with emotion presets; auto-syncs to face
2. **Custom audio upload:** Upload MP3, WAV, or M4A; Kling analyzes audio and re-animates the face to match

**Input video requirements:**
- Format: MP4 or MOV; preferably 720p–1080p; under 100MB; max 10 seconds
- Face must be clearly visible and primarily front-facing (slight head turns accepted)
- Works with multiple faces in frame; model auto-selects one face (no manual face targeting without Pro mode)

**Audio limits:**
- Audio file: under 30 seconds, under 20MB
- Clean audio with no background noise for best accuracy
- If audio is longer than video: crop option available

**Language support (Lip Sync feature, distinct from 3.0 native audio):**
- Multiple languages supported — specific languages not exhaustively documented in English sources
- Chinese and English confirmed; Japanese/Korean/Spanish behavior less documented
- COMMUNITY-VERIFIED: Works for any language the TTS supports; custom audio in any language works for lip movement regardless

**Known limits:**
- Anime/stylized video: Lip sync accuracy degrades significantly — works but choppy
- 3D/non-humanoid characters: Model may refuse (cannot detect consistent humanoid face)
- Multiple faces: model picks one face; cannot target specific face in free/Standard plan; Pro unlocks up to 4 tracks with separate audio per character

**Best practices:**
- Generate the base video with prompt: "character is speaking, front-facing, subtle head motion, lips visible"
- Keep head movement minimal in source video: use "static camera, subtle motion" prompt
- Use ElevenLabs or Eleven v3 for custom voice input into Lip Sync for highest-quality results

**Kling 3.0 Native Audio vs. Lip Sync Feature:**
| Aspect | Lip Sync Feature | 3.0/O3 Native Audio |
|---|---|---|
| Works on | Existing video clips | Generation time only |
| Audio input | TTS or custom file | Prompt-described or via Element voice |
| Multi-character | Pro: up to 4 tracks | Native: multi-character via voice tags |
| Post-generation | Yes (apply to any generated clip) | No (must be enabled at generation) |
| Use case | Add speech to existing clip; dub old footage | Generate audio-synced video from scratch |

### 5.9 Video-to-Video (Style Transfer / Restyle)

**Available:** O1, 2.6, O3 (Reference Video mode); also via O3's Omni editing features.

**How it works:**
- Upload source video as motion reference
- Write a prompt describing the TARGET aesthetic
- System preserves the motion/camera path from the source while changing the visual style

**Prompt structure for style transfer:**
```
[Style description] — [subject description in target style] — [environment description in target style] — preserve camera movement and motion timing from reference
```

**Example (OFFICIAL kling.ai guide):**
- Source: live-action footage of a person walking in a city
- Target: "Anime-style animation, Studio Ghibli aesthetic, soft cel-shading, vibrant colors, neon city lights"
- Prompt includes the target style FIRST; motion direction comes from the reference video

**Preserving motion while changing aesthetic:**
- Keep the reference video short (3–6 seconds) for tightest motion transfer
- Simple backgrounds in the source video produce cleaner style transfer
- Very complex source motion (crowd scenes, fast action) may introduce artifacts in the restyle
- Reference video + element image combination for subject-specific consistency

### 5.10 Try-On and Utility Features

**Try-On:**
- Upload garment image (clean neutral background; 512px–4096px; under 50MB)
- Select or upload model photo (full-body preferred)
- Single Garment or Multiple Garments tabs
- Select garment type (top, bottom, dress)
- Cost: 5 credits per output
- Can generate static image OR animate to video showing fabric drape and movement
- COMMUNITY USE CASE: E-commerce product pages, fashion lookbook generation, virtual fitting for clients

**Kling Canvas:**
- In-painting and editing workspace
- Scene extension, object replacement, background swapping
- Primarily image editing; video editing via prompt-to-edit in O3 Omni

**Avatar 2.0:**
- Separate interface for talking-head avatar creation
- Upload face reference; input script or audio; generate lip-synced avatar video
- Designed for corporate training, digital humans, explainer content

---

*[Continued in next section...]*


---

## 6. PROMPT ANATOMY: EVIDENCE-BASED STRUCTURE

### 6.1 Format: Paragraph vs. Tags vs. Hybrid

**Evidence-based conclusion:** Kling responds best to **structured natural-language paragraphs** written as directorial descriptions, NOT comma-separated tag lists. This is confirmed by:
- Official Kling documentation describing the model as understanding "cinematic intent"
- fal.ai Kling 3.0 prompting guide explicitly stating: "Kling performs best when prompts are written like directions to a scene"
- DataCamp guide demonstrating paragraph-style prompts outperforming lists
- Multiple community practitioners (YouTube tutorials, Reddit, Scribd guide)

**Why:** The DiT + MVL architecture was trained on complete cinematic descriptions (scripts, scene directions, film breakdowns in Chinese and English), not keyword indices. The model has semantic understanding of how sentences relate to each other in a temporal sequence.

**Hybrid approach for complex prompts:** Use paragraph prose for the core description, then add a secondary clause with technical specs: "...cinematic 30fps, shallow depth of field, 4K output, no motion blur artifacts."

### 6.2 Token and Character Limits

| Surface | Single Prompt Limit | Multi-shot per-shot limit |
|---|---|---|
| klingai.com web | ~1,000–2,000 characters | 500 characters per shot |
| fal.ai API | ~2,000 characters | 500 per shot (Custom mode) |
| Negative prompt | ~500 characters | Shared |

### 6.3 Positional Weighting

**CONFIRMED (COMMUNITY-VERIFIED):** Front of prompt dominates. The model gives decreasing weight to terms as they appear later in the prompt. Strategic implications:
- Lead with CAMERA POSITION and PRIMARY SUBJECT ACTION
- Put quality/style references in the second half
- Most critical negative-space instruction (e.g., "no text overlay") should appear in the dedicated negative prompt field, not buried in the positive prompt

### 6.4 Multi-Shot Prompting Behavior

Kling (pre-3.0) is fundamentally a **single-shot model**. It does not naturally generate editorial cuts. The one-generation = one continuous shot principle holds for 1.6, 2.0, 2.1, 2.5, 2.6, O1.

Kling 3.0 introduces genuine multi-shot generation — but it requires explicit activation (Custom or Smart Storyboard mode). Without activating multi-shot, even a prompt that describes "cut to" will be interpreted as a single continuous camera movement or a match cut, not an editorial cut.

**In 3.0 Smart Storyboard:** Use phrases like "cut to," "then show," "followed by a close-up of" to signal shot boundaries. The model auto-generates 2–6 shots.

**In 3.0 Custom Multi-Shot:** Each field is an independent shot prompt. Reference elements with `@Name`. Minimum 3 seconds per shot.

### 6.5 Chinese vs. English Prompting

| Factor | English | Chinese (简体/繁体) |
|---|---|---|
| Output quality | High — model is multilingual | High — model trained on Chinese content |
| Default aesthetics | More Western film grammar | May favor Chinese film/drama aesthetic conventions |
| Content filter behavior | Filter tuned for English phrases | Different trigger words; some refusals avoidable by language-switching |
| Community knowledge | Extensive English tutorials | Chinese community (Bilibili, Xiaohongshu) often 2–4 weeks ahead on technique |
| Recommendation | Default for Western aesthetic | Use for content targeting Chinese audiences; try when English prompt is refused |

**COMMUNITY TIP (Scribd/Kling guide, ZH):** When English prompts hit refusals for non-problematic content (certain medical terms, religious imagery), reformulating in Chinese often resolves false positives. The content filters have different trained sensitivities per language.

---

## 7. THE CINEMATIC VOCABULARY

### 7.1 Camera Body & Format References

Kling responds to camera body references as style anchors — they invoke a learned palette of grain, contrast, color science, and latitude:

| Reference | Effect in Kling Output |
|---|---|
| "ARRI Alexa 35" | Organic, filmic, wide dynamic range, natural skin tones |
| "RED Komodo 6K" | Sharp, slightly cool, high-detail skin texture |
| "Sony Venice 2" | Warm, high-saturation, cinematic |
| "Blackmagic Pocket 6K" | Slightly rawer look, good for indie/naturalistic |
| "Vintage 16mm" | Grain, reduced dynamic range, warm/cool color shift, slightly soft |
| "Super 8 / 8mm" | Heavy grain, vintage saturation, vignetted corners, halation |
| "VHS / camcorder" | Scan lines, color bleeding, soft focus, '90s video aesthetic |
| "DV footage" | Low-res digital look, CMOS jello effect, compressed color |
| "Security/CCTV cam" | High angle, fish-eye mild distortion, timestamp overlay aesthetic |
| "iPhone 15 Pro" | Hyper-sharp, computational bokeh, HDR, slight video-game quality |
| "IMAX 70mm" | Extreme sharpness, near-zero grain, tall aspect implied |
| "Anamorphic scope" | Horizontal flares, oval bokeh, widescreen barrel distortion |

**[LABEL: COMMUNITY-VERIFIED]** — specific camera body prompts produce different output characteristics confirmed by multiple practitioners.

### 7.2 Lens Language

**Focal lengths (COMMUNITY-VERIFIED behavior):**
| Lens | Kling Behavior |
|---|---|
| "14mm ultra-wide" | Exaggerated perspective, slight edge distortion, environmental dominance |
| "24mm wide" | Environmental context, slight perspective drama |
| "35mm" | Natural walk-about feel, slight environmental context |
| "50mm normal" | Closest to eye, neutral perspective |
| "85mm portrait" | Subject isolation, mild compression, flattering |
| "135mm" | Strong compression, subject against blurred background |
| "200mm telephoto" | Extreme background compression, subject separated from environment |
| "Macro / micro" | Extreme close-up, subject fills frame, background destroyed |
| "Fisheye" | Spherical distortion, immersive but distorted |
| "Tilt-shift" | Selective focus plane, miniature effect on landscapes |

**Depth of field language:**
- "f/1.2, extremely shallow depth of field" — minimal focus plane, creamy bokeh
- "f/2.8, soft background separation" — medium separation
- "f/8, everything in sharp focus" — deep focus, environmental clarity
- "razor-thin focal plane" — implies macro/portrait shallow DoF
- "panfocus, Citizen Kane-style deep focus" — everything sharp

**Lens artifacts:**
- "anamorphic horizontal lens flare, blue/cyan streak" — classic anamorphic scope look
- "chromatic aberration on edges" — vintage/organic feel
- "soft halation in highlights" — dreamy, film-like
- "Black Pro-Mist filter diffusion" — Promist look, glow on highlights
- "vignette, darkened corners" — contained, focused frame
- "barrel distortion" — vintage wide-angle lens character

### 7.3 Camera Movement Reference Table

| Movement | Prompt Language for Kling | Available as Camera Preset? |
|---|---|---|
| Static | "fixed camera, locked-off tripod", "static wide shot" | Via zero-displacement preset or prompt |
| Pan left/right | "camera pans left across the room" | ✅ Pan preset |
| Tilt up/down | "camera tilts up to reveal the skyline" | ✅ Tilt preset |
| Roll | "Dutch angle roll, camera tilts 15 degrees" | ✅ Roll preset |
| Dolly in | "slow dolly push-in toward the subject" | Via Zoom in + Horizontal compound |
| Dolly out | "camera pulls back, dollying away from subject" | Via Zoom out |
| Truck/Dolly lateral | "camera trucks left, subject stays centered" | ✅ Horizontal preset |
| Pedestal up/down | "camera pedestal rises to reveal the ceiling" | ✅ Vertical preset |
| Crane/Jib | "camera cranes up, revealing the full cityscape" | Via Master Shot: Move Forward Zoom Up |
| Techno-crane | "camera swoops from low ground to high aerial in a single motion" | Compound: Move Up + Zoom |
| Steadicam | "Steadicam follows subject through corridor, smooth organic sway" | Prompt-only |
| Gimbal float | "gimbal-stabilized tracking shot, slight organic float" | Prompt-only |
| Handheld subtle | "handheld camera, gentle documentary presence" | Prompt-only |
| Handheld aggressive | "vérité handheld, urgent documentary shake" | Prompt-only |
| Drone orbit | "aerial drone circles the subject counterclockwise" | Prompt-only |
| Drone push-in | "drone pushes forward at low altitude over terrain" | Prompt-only |
| Drone top-down | "directly overhead drone shot, subject below" | Prompt-only |
| Snorricam | "camera mounted to subject's chest, background moves, face is locked in frame" | Prompt-only |
| FPV | "first-person view through-the-air FPV dive" | Prompt-only |
| Whip pan | "rapid whip pan right, motion blur transition" | Prompt-only |
| Snap zoom | "sudden crash zoom punch-in toward subject" | Prompt-only |
| Dolly zoom (Vertigo) | "dolly zoom: camera physically pulls back while lens zooms in, background appears to collapse" | Prompt-only |
| Master Shot 1 | Move left + zoom in | ✅ Preset |
| Master Shot 2 | Move right + zoom in | ✅ Preset |
| Master Shot 3 | Move forward + zoom up | ✅ Preset |
| Master Shot 4 | Move down + zoom out | ✅ Preset |
| Orbit/Arc | "rotating lens around the subject, 180-degree arc" | Prompt-only ("rotating lens" — COMMUNITY-VERIFIED) |
| Bullet-time | "frozen moment, camera rotates around static subject" | Prompt-only |

### 7.4 Shot Scale & Framing

```
ECU   — Extreme Close-Up: "extreme close-up of the eye, filling the frame"
CU    — Close-Up: "close-up on the face, shoulders barely visible"
MCU   — Medium Close-Up: "medium close-up, chest and above"
MS    — Medium Shot: "medium shot, waist up"
MWS   — Medium Wide Shot: "medium wide, full body visible"
WS    — Wide Shot: "wide shot, full body with environment context"
EWS   — Extreme Wide Shot: "extreme wide establishing shot, subject is tiny in landscape"
OTS   — Over-the-Shoulder: "over-the-shoulder shot, subject facing right, interlocutor in foreground left"
Two-shot — "two-shot, both characters facing each other, equal weight"
Group — "group shot, three characters in foreground"
POV   — "POV shot through the character's eyes"
Worm's eye — "low angle, worm's-eye view looking up at subject"
Bird's eye — "high overhead shot looking straight down"
Dutch angle — "tilted Dutch angle, 15 degrees counterclockwise"
Symmetrical — "perfectly symmetrical frame, Wes Anderson-style centered composition"
Negative space — "subject in lower-left third, vast negative space sky above"
```

### 7.5 Lighting

**Schemes:**
- "three-point lighting setup — key from left, fill from right, rim light from behind"
- "Rembrandt lighting — key light from upper-left, small triangle of light on right cheek"
- "butterfly/clamshell lighting — key from directly above, fill below chin"
- "split lighting — hard key on exactly half the face, deep shadow on other half"
- "chiaroscuro — extreme contrast, large pools of shadow, Renaissance painting quality"
- "high-key lighting — bright, even, low shadow ratio, commercial/comedic"
- "low-key lighting — dark, moody, dominant shadows, noir/horror"
- "naturalistic lighting — practical sources only, no studio look"

**Quality:**
- "hard light — sharp-edged shadows, specular highlights, noon sun quality"
- "soft diffused light — wrapping shadow edges, overcast sky quality"
- "Fresnel specular — theatrical narrow beam"

**Time of day (Kling responds well to these):**
- "golden hour — warm orange-amber, long shadows, 20 minutes after sunrise/before sunset"
- "blue hour — deep cobalt twilight, between sunset and night"
- "magic hour — diffuse gold, haze in the air"
- "high noon — harsh overhead, deep eye shadows"
- "overcast day — flat, even, shadowless, neutral color temperature"
- "night-for-night — practical street lighting, deep blacks, neon reflections on wet pavement"

**Sources:**
- "tungsten practicals — warm orange interior glow"
- "HMI daylight — crisp blue-white, commercial/studio quality"
- "sodium vapor streetlamps — orange-yellow cast, urban night"
- "fluorescent tubes — slightly green color cast, institutional/horror feel"
- "neon signs — colored light in reds, blues, pinks, casting colored shadows"
- "candle/firelight — dynamic warm orange, flickering, intimate"
- "screen light — cold blue spill from off-screen monitor or phone"
- "moonlight — blue-grey, soft directional, desaturated"
- "volumetric godrays through windows" — light shafts, dust particles visible

### 7.6 Color & Grade

**Palette specification:**
- Complementary: "teal shadows and orange highlights" (Hollywood blockbuster standard)
- Monochromatic: "desaturated, near black-and-white, only slight warm tones in skin"
- "neon noir — deep blacks, electric pinks and purples, wet reflective surfaces"
- "Nordic/Scandi — muted, desaturated, cool grey-blue palette, minimal contrast"
- "bleach bypass — desaturated, high contrast, silver retention look"
- "cross-process — shifted color channels, greens in shadows, magenta in midtones"

**Named film looks:**
- "Roger Deakins cinematography — warm shadows, natural light, no digital harshness" (Blade Runner 2049, 1917)
- "Emmanuel Lubezki — long handheld takes, natural light, organic movement" (The Revenant, Tree of Life)
- "Christopher Doyle — saturated jewel tones, rich greens and reds, humid atmosphere" (In the Mood for Love)
- "Darius Khondji — desaturated but textured, slight green in shadows" (Seven, City of Lost Children)
- "Blade Runner 2049 palette — amber dust and deep cobalt, layered fog"
- "In the Mood for Love palette — rich red, warm amber, luxurious slow decay"

**Film stock emulation:**
- "Kodak Vision3 5219 — warm highlights, natural grain, cinematic"
- "Kodak Portra 400 — film photography warmth, soft grain, slightly lifted shadows"
- "Fuji Velvia — hyper-saturated, vivid landscape colors"
- "Cinestill 800T — halation around lights, tungsten-balanced warmth in shadow/cool in highlight"
- "Ilford HP5 monochrome — classic black and white grain structure"

### 7.7 Subject Action & Performance

**Action verbs with predictable Kling results (COMMUNITY-VERIFIED):**
- "walks toward camera" — reliable forward motion
- "turns to face camera" — reliable head/body pivot
- "raises hand slowly" — works; use "gently" or "slowly" for smoothness
- "looks off-frame left/right" — reliable directional gaze
- "laughs softly" — visible smile + shoulder movement
- "takes a deep breath" — subtle chest rise, calming effect
- "runs through the scene" — may have gait inconsistency; works better at slower paces
- "picks up [object]" — works for simple objects; complex grip interactions may fail

**Actions prone to failure:**
- "juggles" — complex multi-hand physics
- "plays piano" — finger-key sync is unreliable
- "throws a punch and connects" — contact physics often breaks
- "types rapidly on keyboard" — hands/fingers often artifact
- "writes text by hand" — complex finger-pen-surface interaction

**Hand and finger anatomy — current state (May 2026):**
- Kling 3.0 shows significant improvement over prior versions (COMMUNITY-VERIFIED)
- Simple single-hand visible actions (waving, reaching, pointing) now largely reliable
- Complex multi-hand interactions, instrument playing, fine writing remain risky
- **Mitigation strategies:** Frame wide enough to avoid extreme close-ups of hands; use negative prompt "extra fingers, distorted hands, deformed limbs"; avoid prompting for multi-hand contact actions

**Micro-expressions:** Kling 3.0/O3 can generate subtle emotional transitions in faces. Use descriptive language: "a flicker of doubt crosses her face," "eyes widen in quiet recognition."

**Crowd behavior:** Use "crowd of people moving naturally through the plaza" — Kling handles ambient crowd movement well. Avoid prompting for specific synchronous crowd actions (everyone turns simultaneously, flash mobs) — consistency fails.

### 7.8 Environment & Production Design

- Be specific with location: "a brutalist Soviet-era apartment block, 1960s" > "old building"
- Atmospheric elements Kling handles well: "thick morning fog," "low-lying mist," "light rain on pavement," "snow falling," "dust particles in shafts of light," "smoke machine haze"
- Time period: "1970s New York — grain, warm color, gritty texture, taxi-yellow cabs in background"
- Architectural references: "Haussmann Paris facade," "Tokyo neon alley," "brutalist concrete interior," "gothic cathedral nave"
- Set dressing language: "scattered newspapers on the floor," "half-drunk coffee cup on a desk," "flickering overhead fluorescent"

### 7.9 Audio — Honest Assessment

**What Kling natively generates:**

| Model | What Audio It Generates Natively |
|---|---|
| 1.6, 2.0, 2.5 | **Nothing.** Silent video only. |
| 2.1 Std/Pro | Ambient sound effects only (toggleable). |
| 2.6 | Synchronized speech in EN + ZH; ambient audio. No music. |
| 3.0 / O3 | Full: dialogue (5 langs), ambient SFX, background music. Lip-sync automatic. |

**Designing prompts for post-production audio (when using pre-3.0 models):**
- Describe the acoustic environment for your own reference: note if the scene is outdoors/indoors, what would be heard
- Leave room for audio cues: don't fill the frame with visually competing action — leave pauses where dialogue would land
- Consider audio-informed framing: for dialogue scenes, generate the speaker in MCU/CU to enable easy lip-sync later

**Recommended external audio pipeline:**
| Need | Tool |
|---|---|
| Voice / dialogue | ElevenLabs (v3) — most natural synthesis; Eleven v3 supports expressive styles |
| Background music | Suno v4, Udio — generate style-matched underscore |
| Sound effects / foley | MMAudio, Adobe Firefly Audio, Freesound |
| Spatial audio / mix | Adobe Premiere, DaVinci Resolve |
| TTS with emotion | ElevenLabs, Play.ht, Murf |

**Diegetic vs. non-diegetic planning:**
- Diegetic audio (heard in the scene — footsteps, dialogue, radio): plan for realistic acoustic space matching the visual environment
- Non-diegetic (score, narrator): can be added freely in post with no visual constraint
- For 3.0/O3 native audio: include both in the prompt — "ambient traffic noise outside, a slow jazz piano underscoring the tension"

### 7.10 Rendering, Textures, VFX

**Skin realism:**
- "visible pore texture," "natural subsurface scattering," "slight sheen of sweat on temples"
- "translucent skin quality, veins faintly visible"
- Kling 3.0 handles skin convincingly in close-ups for photorealistic styles

**Fabric:**
- "the silk dress drapes and moves fluidly," "wool coat weight, heavy natural sway"
- "sheer gauze fabric, light-transparent, billowing"
- "leather jacket, slight creak and sheen"

**Materials Kling renders well:**
- Glass refraction, water surface tension and reflections, metal patina (rust, brushed aluminum), fire dynamics, smoke volumetrics
- "fire catches on the corner of the paper, flames spread slowly"
- "water droplets bead and run down the glass surface"
- "chrome surface reflects the distorted environment"

**Stylized rendering:**
- "cel-shaded 2D animation style, thick outlines, flat color fills"
- "Studio Ghibli anime — hand-painted backgrounds, soft cel animation, Miyazaki movement"
- "stop-motion animation — visible clay texture, slight frame jitter, puppet feel"
- "claymation — thick clay texture, Aardman-style exaggerated expression"
- "paper cut-out animation — flat layered paper with slight depth parallax"
- "2.5D — flat illustrated characters against 3D parallax backgrounds"

**Kling known strengths in VFX:**
- Slow-motion hero moments: liquid, fire, fabric in high-frame-rate dramatic slow-motion
- Atmospheric effects: fog, rain, smoke integrate naturally
- Water surface and underwater environments
- Natural physics (falling objects, cloth simulation)

**Kling known weaknesses:**
- Arbitrary text generation within frame (logos, signage with specific copy) — improved in 3.0 but still unreliable for custom text
- Complex particle collisions
- Hyper-realistic computer/phone screens in frame with specific content

### 7.11 Editing Implied in the Prompt

**Single-shot behavior (pre-3.0):** Kling generates a single continuous shot. Describing "cut to" in a pre-3.0 model results in either: (a) a match cut at a natural transition point, or (b) the model ignoring the cut instruction and continuing the shot.

**Pacing language:**
- "slow, deliberate" — reduces action intensity, more contemplative camera movement
- "fast-paced, urgent" — increases motion intensity
- "lingering hold on her face" — prompts a slow or static end to a motion
- "rapidly cuts between" — only works in 3.0 multi-shot mode

**Transition handling in Extend chains:**
- Between extensions, there is no natural editorial cut — continuity is maintained frame-to-frame
- To simulate a cut in an extended chain: take the last frame of clip 1 → use as start frame of new I2V generation with different angle → these are separate clips to be cut together in editing software
- Natural dissolves: use matching lighting and color; end clip with subject in a stable hold; begin extension with subtle camera shift

---

## 8. GENRE PATTERN LIBRARY — ALL 23 GENRES

*Each example is labeled with: [Model] [Tier] [Feature] + annotation.*

---

### Genre 1: Cinematic Narrative Drama

**Recommended:** Kling 3.0 Pro / O3 | Multi-shot | I2V + Elements

```
Shot 1 (5s): A dimly lit kitchen late at night. Only the refrigerator hum fills the silence.
@Elena — a woman in her mid-40s, dark circles under her eyes, grey cardigan — sits at the 
table, hands wrapped around a cold mug. Camera: slow push-in from medium shot to close-up.
Lighting: tungsten practical overhead, deep shadow on one side of her face.
[Elena, exhausted voice, barely audible]: "He's not coming back."

Shot 2 (4s): The front door in the background, slightly out of focus. Through the frosted 
glass pane, the blue light of headlights sweeps and disappears. Camera: static lockoff, 
eyes-level. Shallow depth of field. [Elena, whispering]: "I know."

Shot 3 (3s): Extreme close-up — the mug being set down too hard on the table. Ceramic 
sound. Camera static. Silence. No dialogue. Focus on the slight tremor in her hands.
```

**Annotation:** Multi-shot structure separates the performance, the environmental signal, and the physical action — classic dramatic three-beat rhythm. Elena is an Elements reference for consistency. Native audio creates synchronized delivery. O3 preferred for character voice cloning.

---

### Genre 2: Action / Thriller

**Recommended:** Kling 3.0 Pro | Single shot (T2V) or 2-shot multi-shot | High motion intensity

```
A black-clad operative sprints across a rain-soaked rooftop at night, pursuing a target 
10 meters ahead. Camera: low 35mm tracking shot at waist height, moving parallel at speed, 
slight handheld urgency. Both figures silhouetted against the city glow below. Neon 
reflections on wet concrete. Hard rain. The operative lunges, catches the target's jacket 
collar — they both skid to the roof edge, halting 30 centimeters from the drop. Camera 
holds on the operative's face: jaw set, eyes cold, breathing hard.

Lighting: ambient city glow from below, no key light — only the scattered neon pinks and 
blues of the urban night. Lens: 35mm equivalent. Shallow background focus. 
Style: Michael Mann Heat aesthetic — controlled chaos, documentary realism, wet environment.
Audio: rain pounding, distant traffic, breath heaving, no music.
```

**Annotation:** Keep action physically plausible. Specify the camera-to-subject relationship (parallel tracking) clearly. "Skid to the roof edge" is achievable; "backflip through an explosion" is not reliable. End on a dramatic hold for emotional impact.

---

### Genre 3a: Horror — Slow-Burn

**Recommended:** Kling 3.0 Pro | I2V (from atmospheric image) + Start Frame | 10s

```
A long, empty hospital corridor stretches away from camera. Overhead fluorescent tubes 
flicker irregularly — two-thirds of the lights are dead, leaving pools of shadow between 
dim amber pools of surviving light. Camera: extremely slow dolly push-in at knee height.
The perspective is slightly wrong — the corridor seems too long for the building.
At the far end, barely visible in the deep shadow, a door stands open.
Nothing moves. No sound. The camera continues pushing forward, the door getting slowly 
closer. Just before the shot ends, the door swings shut. No visible cause.
Lighting: flickering fluorescent, clinical green cast, deep blacks.
Style: Hereditary visual grammar — slow suffocation, no jump scare.
Audio: sub-bass drone, barely audible, getting slightly louder.
```

**Annotation:** Slow-burn horror is Kling's sweet spot. Static or near-static environments with one inexplicable motion. The "slightly wrong" spatial cue (corridor too long) is achievable because Kling's spatial geometry is imprecise — turn a weakness into an asset. No characters = no anatomy failure risk.

---

### Genre 3b: Horror — Jump Scare

**Recommended:** Kling 3.0 Pro | T2V or I2V | 5s | Tight framing

```
A woman sits alone at a vanity mirror, removing makeup in a quiet bedroom. Night. 
The only light is the warm vanity bulb reflected in the mirror. Camera: medium close-up 
of her reflection in the mirror. She reaches for a cotton pad. Then stops. Her eyes 
shift — looking slightly past her own reflection, to a point slightly behind her, in the 
dark room behind. Her breath catches. The camera holds on her face in the mirror.
Cut [Shot 2]: Extreme close-up on her eyes widening. [Audio: sudden loud string hit].

Negative prompt: extra faces, morphing mirror, distorted reflection.
```

**Annotation:** Jump scare requires precise timing setup. Use 3.0 multi-shot to separate the buildup shot from the scare shot. Native audio handles the musical sting. Avoid asking the model to show what she sees — implied horror performs better than literal.

---

### Genre 4a: Sci-Fi — Hard Sci-Fi

**Recommended:** Kling 3.0 Pro | T2V | 1080p 10–15s

```
Interior of a deep-space research station, 2157. Cramped, utilitarian. Real technology — 
no fantasy chrome, no colored lights. Brushed aluminum surfaces, worn rubber grip handles, 
cable management trays. A sole scientist in a grey EVA undersuit reviews holographic data 
projected from a handheld device. The holograms show orbital mechanics — not glamorous, 
technical. Microgravity: she reaches for a coffee bulb floating gently past her hand.
Camera: medium shot, static, documentary style. Slight film grain.
Lighting: cold fluorescent overheads, sharp shadow contrast. No cinematic beauty lighting.
Reference: The Martian production design, clinical authenticity.
Audio: HVAC hum, subtle equipment chirps, no music.
```

**Annotation:** Hard sci-fi requires restraint. No lens flares, no colored ambient light, no hero music. Reference known productions to anchor the aesthetic. The floating coffee bulb is a great Kling physics moment — it handles slow microgravity object movement beautifully.

---

### Genre 4b: Sci-Fi — Space Opera

**Recommended:** Kling 3.0 Pro | Multi-shot T2V | 15s

```
Shot 1 (5s): EWS — a vast interstellar fleet hangs in orbit above a gas giant, its rings 
catching the distant star's light. Hundreds of capital ships, each miles long, in formation.
Camera: slow crane-style descent from above-fleet to eye-level with the command vessel.
Epic orchestral score swells. Deep blacks of space, rich amber of the gas giant.

Shot 2 (5s): Interior bridge of the command vessel. Wide shot. The admiral stands at the 
forward viewport, back to us, watching the fleet through floor-to-ceiling glass. 
Camera: slow push-in, shoulders to the edges of frame. 
[Admiral, resonant commanding voice]: "We don't retreat. Not today."

Shot 3 (5s): ECU — the admiral's face in reflection on the viewport glass, the fleet 
visible through his face. Camera static. Silence for two beats. 
[Admiral, quiet]: "Helm. Take us forward."
Audio: orchestral score drops to silence, then a single low cello note.
```

**Annotation:** Space opera requires scale contrast — fleet EWS to bridge INT to face ECU. Multi-shot handles this perfectly. Native audio creates the score + dialogue combination. Fleet generation is reliable in 3.0 for distant formations.

---

### Genre 5: Fantasy / Epic

**Recommended:** Kling 3.0 Pro | Multi-shot I2V + Elements | 15s

```
Shot 1 (5s): A lone knight @ArthurKing on horseback crests a ridge at golden hour, 
overlooking a valley where two vast armies are arrayed for battle. The armies are 
thousands-strong, their banners catching the wind. Camera: crane shot from behind the 
knight, rising from low to high as he reaches the ridge crest — the battlefield revealed 
beneath. Epic brass fanfare begins.
[Style: practical battle scale, Peter Jackson Fellowship of the Ring composition]

Shot 2 (4s): Medium shot — @ArthurKing raises his sword overhead. His horse rears. 
The sword catches the golden hour light. Camera: low angle, looking up at the figure 
against the sky. The army behind him responds — a roar of voices.

Shot 3 (3s): ECU — @ArthurKing's face. Resolution. A single tear on his cheek. 
He exhales. Camera: static close-up. 
[Arthur, whispering]: "For everyone we carry with us."
```

**Annotation:** Fantasy benefits from Elements for consistent hero character. The scale of the battle army is handled impressionistically at this resolution — it's better to suggest mass than demand 10,000 individually animated soldiers. Kling's crane movement is excellent for reveal shots.

---

### Genre 6: Romance

**Recommended:** Kling 3.0 Std / Pro | I2V | Subtle motion | 5–10s

```
A sun-drenched Paris café terrace, late afternoon. @Sophie — a woman in her 30s, floral 
dress, reading a book — glances up at the sound of laughter from the street. 
Camera: medium shot, pushing in gently from 50mm to 35mm equivalent, very slowly over 7 
seconds. Golden hour light from the right, catching the wisps of her hair. 
She doesn't notice us. She's slightly amused by something we can't see. 
A breeze moves her hair and stirs the pages of her book. 
The image is still — the animation is all breath, breeze, and a faint smile forming.
Style: Wong Kar-wai visual grammar — stolen moments, warmth, nostalgia.
Color: amber highlights, soft warm shadows, slightly desaturated green in the background.
No dialogue. Ambient: café chatter distant, a scooter passing, birdsong.
```

**Annotation:** Romance often works best as pure atmosphere — Kling excels at subtle environmental animation (hair, breath, fabric) combined with a gentle camera push. Avoid dialogue in romantic I2V; save it for multi-shot T2V scenes. Wong Kar-wai reference strongly activates the model's aesthetic knowledge.

---

### Genre 7a: Comedy — Broad

**Recommended:** Kling 3.0 Std | T2V or multi-shot | High-key lighting

```
An office conference room. Three colleagues sit in a meeting. A presentation on the 
screen behind them reads "SYNERGISTIC PARADIGM SHIFT Q3." The speaker @Dave is mid-
sentence, very earnest. A paper airplane drifts in through the open door behind him, 
arcs gracefully, and lands perfectly in his coffee mug. Dave continues talking, 
oblivious. The other two colleagues exchange a wide-eyed look.

Camera: wide static two-shot on the two colleagues, Dave in the background.
Lighting: flat corporate fluorescent, high-key — comedy needs visibility.
Audio: generic corporate soft-jazz playing, paper airplane small splash sound.
Style: mockumentary sit-com visual grammar, The Office.
No dramatic lighting. Bright, over-exposed office look.
```

**Annotation:** Broad comedy requires readable framing — wide shots so the audience sees all three characters simultaneously. The paper airplane physics is a good Kling task. Native audio handles the comedy timing. Avoid fast cutting in single generations.

---

### Genre 7b: Comedy — Deadpan

**Recommended:** Kling 3.0 Pro | Static I2V | Minimal motion

```
A man sits perfectly upright on a park bench. He is wearing a tuxedo. It is clearly 
raining. He has no umbrella. He does not appear to notice the rain. He is eating a 
sandwich very deliberately. The camera is completely static, at eye level, framing him 
in a medium shot. The rain continues. He continues eating. He reaches into his jacket 
pocket and produces a newspaper, which immediately becomes soaked. He begins to read it 
anyway, as if it were perfectly fine.

Camera: completely locked-off, static. No camera movement whatsoever.
Lighting: flat overcast rain-day light. No drama.
Duration: 10 seconds. Nothing changes except the rain and the chewing.
Audio: only the sound of rain and the distant sound of a pigeon.
Style: Roy Andersson — deadpan Swedish comedy, static composition, moral absurdity.
```

**Annotation:** Deadpan comedy depends entirely on the audience waiting for something to happen and it not happening. Kling's static camera mode with minimal motion prompt is ideal. Roy Andersson reference strongly cues the aesthetic.

---

### Genre 8a: Documentary — Observational

**Recommended:** Kling 2.6 Pro or 3.0 Std | T2V | Handheld | 10s

```
A fish market at 5:30am. The floor is wet, neon tube overhead, ice glistening.
A fishmonger — early 60s, rubber apron, bare forearms reddened from cold water — sorts 
a new delivery without hurry. His movements are practiced, efficient, decades of muscle 
memory. He doesn't look at the camera. He doesn't know we're here.
Camera: handheld, 28mm equivalent, documentary presence — not stable, not frantic, 
just present. The camera finds its own interest moment by moment.
Lighting: mixed — sodium overheads, neon tubes, reflections off ice and wet surfaces.
Color: desaturated, cold temperature with warm skin tones.
No narration. No music. Only ambient: the slap of fish, ice shifting, distant dock sounds.
Style: Frederick Wiseman observational documentary grammar.
```

**Annotation:** Observational documentary requires restraint. No hero lighting, no dramatic music, no "looking at camera" moment. Kling handles this very well — the specific lighting mix (sodium + neon + wet reflection) produces beautiful naturalistic results.

---

### Genre 8b: Documentary — Interview

**Recommended:** Kling 3.0 Pro | I2V (from photorealistic generated portrait) + Lip Sync | 10s

```
[Use I2V from a clean portrait of the interview subject. Elements binding for face 
consistency.]

Camera: MCU, slightly off-center — interview style. Subject looks just off camera (to the 
interviewer's position), not directly at lens. Bokeh background — a blurred library or 
plain grey backdrop. Slight depth-of-field soft separation.

Motion prompt: "subject speaks naturally, occasional hand gesture into frame, 
subtle head movement, eyes are alive and engaged, occasional blink"

Then apply Lip Sync with custom audio (recorded interview audio or ElevenLabs voice).
Style: PBS Frontline — clean, dignified, no stylistic flourishes.
```

**Annotation:** Interview format is one of Kling's strongest use cases — Lip Sync + I2V from a portrait produces extremely convincing talking-head results. Keep background blurred to avoid background detail inconsistency across clip segments.

---

### Genre 9a: Music Video — Performance

**Recommended:** Kling 3.0 Pro | Multi-shot I2V + Elements | 15s

```
Shot 1 (5s): @ArtistName performs alone on a massive empty stage, single spotlight.
The arena is dark beyond the light. Camera: slow crane rising from floor level to high 
angle overhead, capturing the circular spotlight on the darkened stage. 
Artist: facing the dark arena, arms slightly spread.

Shot 2 (5s): MCU — @ArtistName singing directly into camera, eyes intense. 
Camera: slow push-in from MCU to CU. Hard key light from above, deep shadow below chin.
Reference: music video treatment for The Weeknd or Billie Eilish — high-contrast, 
dark atmosphere, single-source lighting.

Shot 3 (5s): EWS: from the back of the arena, the stage is a tiny bright dot in the 
darkness. Thousands of phone flashlights begin appearing in the audience below.
Camera: static wide. Music swells. 
[Audio: first chorus of the track building]
```

**Annotation:** Performance music video needs scale contrast between intimate artist shots and epic environmental shots. Elements ensures the artist's face stays consistent. Multi-shot enables cinematic jump cuts within a generation.

---

### Genre 9b: Music Video — Narrative

**Recommended:** Kling 3.0 O3 | Multi-shot I2V + Elements (characters) | 15s

```
Shot 1 (4s): @Maya drives alone on an empty desert highway at sunset. 
Interior car shot — her profile against the orange horizon. 
Camera: medium close-up from passenger seat, looking across at her face.
She's looking ahead. Not speaking. Just driving.

Shot 2 (4s): Exterior — the car receding into the desert horizon, tiny and alone.
Camera: static, the car driving away from us. Dust behind it.

Shot 3 (4s): @Maya's hand on the steering wheel. A photo tucked in the visor above her.
Extreme close-up of the photo — a face, out of focus, unidentifiable.
Her fingers grip tighter.

Shot 4 (3s): Her face again, tears catching the last of the golden hour light.
Camera: static close-up. One tear runs down.
[Audio: the track's bridge — sparse piano, no beat]
```

**Annotation:** Narrative music video is driven by subtext — what we don't see. Elements for @Maya ensures continuity across the four shots. O3's video element reference means we can feed a reference video of the real artist. The unanswered question (who is the photo?) lets the audience project the song's meaning.

---

### Genre 10: Commercial / TVC

**Luxury:**
```
A glass of aged whisky rests on a hand-carved mahogany bar, backlit by a single warm 
tungsten flame. The glass is perfect — no fingerprints, no imperfections. The liquid 
catches the light, amber pools shifting slowly as the glass is picked up by an elegant, 
age-weathered hand. Camera: extreme close-up macro, 100mm equivalent, razor-thin depth 
of field. The background is a warm-dark blur of wood and leather.
Motion: the hand lifts the glass; light ripples through the liquid; the glass pauses 
midway — a held moment before the first sip.
Style: LVMH luxury brand content — restraint, texture, authenticity over glamour.
No dialogue. Audio: the soft clink, the slight scrape of glass on wood, silence.
```

**[Recommended: Kling 3.0 Pro | I2V from studio product image | 5–7s]**

**Automotive:**
```
A matte-grey sports sedan rounds a mountain switchback at speed. The road is wet from 
recent rain. Late afternoon. Camera: tracking drone shot alongside the car at door height, 
maintaining perfect distance as the car takes the curve. Tire spray. The car is sharp; 
the mountain backdrop blurs with motion.
Style: BMW / Mercedes production aesthetic — precision, power, environment.
Color: desaturated landscape, rich metallic vehicle color, specular highlights on 
the wet road surface.
Audio: engine note, tire on wet tarmac, wind — no music in this cut.
```

**[Recommended: Kling 3.0 Pro | T2V | 10s]**

---

### Genre 11: UGC / Social-Native (TikTok / Reels / 9:16)

**Recommended:** Kling 2.5 Std or 3.0 Std | T2V or I2V | 9:16 aspect | 5–7s

```
Portrait (9:16) format. A barista pours a flat white — the espresso swirl in the milk 
captures perfectly. Overhead angle. Camera: slightly elevated, tilt down to flat overhead.
Natural light from a window right. Clean wooden café surface.
Fast, clean generation for high-volume social content.
Duration: 5 seconds. Loop-friendly — begin and end on similar frame composition.

Negative prompt: blurry, motion artifacts, hands with extra fingers, poor lighting.
```

**Annotation:** For UGC/social: use Standard tier for speed and cost efficiency. 9:16 aspect ratio. Keep motion simple and loop-friendly. Kling 2.5 Turbo is the cost-optimized choice for high-volume social content batches.

---

### Genre 12: Product Video / E-Commerce

**Recommended:** Kling 3.0 Pro | I2V (product on white/neutral BG) | Start+End Frame for 360° | 5–10s

```
[Start Frame: product facing 0°]
[End Frame: same product at ~120° rotation]

Prompt: A premium wireless headphone slowly rotates 120 degrees on a clean white surface.
The camera holds static. Studio lighting — soft box from upper left, white fill from 
right. As the product rotates, we see the hinge mechanism, the ear cushion texture, 
the brand mark on the earcup.
Motion: smooth mechanical rotation, no wobble.
Style: Apple/Sony product photography — clinical perfection, tactile texture.
Audio: silent (or very light ambient: barely perceptible room tone).

Negative prompt: reflections on background, shadows pooling, extra products in frame.
```

**Annotation:** Product video is where I2V + Start/End Frame genuinely excels. Generate a clean product image in Midjourney or Flux, then animate. The rotation interpolation between two keyframes produces very clean results.

---

### Genre 13: Explainer / Corporate

**Recommended:** Kling 3.0 Std | T2V | 1:1 or 16:9 | Simple motion

```
An abstract visualization of a data network: nodes of light connected by thin lines, 
slowly pulsing and shifting like a living organism. The camera gently orbits the 
network cluster. Each node glows briefly as data flows through it. 
Clean, professional. Blue and white palette, dark background.
Style: Salesforce / McKinsey motion graphics aesthetic — clear, trustworthy, 
not overwrought.
No characters. Purely abstract technical visualization.
Duration: 8 seconds. Loop-friendly.
Audio: gentle synthetic ambient chime sequence, corporate but not cheesy.
```

**Annotation:** Abstract data visualizations are a strong Kling use case — no anatomy risk, no character consistency requirement. Native audio handles the ambient layer. Keep corporate prompts simple; complexity introduces visual noise.

---

### Genre 14: Animation — 2D/3D/Stop-Motion

**2D Cel Animation:**
```
2D traditional animation style — hand-drawn line quality, slight line wobble, 
painted cel backgrounds in flat color. A young girl runs through a sunflower field, 
hair trailing, feet barely touching the ground. Saturated warm palette. 
Style: Don Bluth / Secret of NIMH — expressive character, rich color, not Disney-sanitized.
Camera: medium wide tracking shot, camera pans to follow.
Duration: 7 seconds. 24fps.
```

**3D Animation:**
```
3D CGI animation — Pixar quality rendering, subsurface scattering on character skin, 
ambient occlusion, studio key light. A small robot character sits on the edge of a 
cliff, swinging its legs, watching the sunset. Melancholy but hopeful expression.
Camera: medium shot from slightly below, looking up at the character.
Style: WALL-E emotional grammar.
```

**Stop-Motion:**
```
Stop-motion animation — visible clay texture, slight frame jitter inherent to the 
medium, handmade quality. A clay rabbit hops across a miniature forest set made of 
real moss, twigs, and painted backgrounds. 
Camera: tracking medium shot. Natural warm lighting.
Style: Aardman Animations — warmth, crafted texture.
```

**[All recommended: Kling 3.0 Pro | T2V | 24fps setting]**

---

### Genre 15: Anime / Japanese Animation

**Recommended:** Kling 3.0 Pro | T2V or I2V | 24fps

```
Japanese anime style — 2D hand-painted backgrounds in classic Ghibli tradition, 
detailed foreground characters with large expressive eyes, soft cel animation quality. 
A young woman stands at a train station platform as the last evening train departs.
Wind from the passing train moves her skirt and hair. She watches it leave.
Camera: medium wide, static, eye level.
Color: muted evening palette — dusty rose and deep indigo sky, warm station lights.
Reference: Makoto Shinkai Your Name / weathering with You — hyper-detailed backgrounds, 
emotionally resonant atmosphere, bittersweet longing.
Audio: piano motif, soft, unresolved chord at the end.
```

**Annotation:** Specifying Studio Ghibli or Makoto Shinkai is very effective in Kling — these aesthetic references are strongly represented in training data and produce consistent anime quality.

---

### Genre 16: Experimental / Art Film

**Recommended:** Kling 3.0 Pro or O3 | T2V | Unusual framing + color

```
An abstract study of time: a single red apple sitting on a white table. The camera is 
completely static. Over the duration of the clip, the apple very slowly begins to bruise 
— dark patches spreading across the skin like ink in water, almost imperceptible. 
The light source (a single window) slowly shifts position as if hours are passing in 
seconds. No sound except the deepening hum of refrigerator that becomes slowly musical.

The composition: centered, Kubrickian symmetry. The space around the apple is 
meaningful — negative space as intentional.
Style: Chantal Akerman / Michael Snow — duration, stillness, transformation as subject.
```

**Annotation:** Experimental film is where Kling's physics simulation becomes art. The bruising apple is a genuine physics transformation the model handles elegantly. Kubrick symmetry + stillness + single object = pure Kling strength.

---

### Genre 17: Sports Highlight

**Recommended:** Kling 3.0 Pro | T2V | High motion intensity | 10s

```
A basketball player drives through two defenders in the paint, rises to the basket.
Ultra-slow-motion — 240fps equivalent. The moment of the layup: fingers spread on the 
ball, backboard impact, the net snapping back. Camera: low angle tracking shot from 
court level, rising as the player rises.
Lighting: arena multi-source overhead, single dramatic follow-spot from above.
Color: high contrast, vivid team colors. 
Reference: ESPN E:60 sports cinematography — heroic, mythic.
Audio: crowd ambient, gradually muting under slow-motion effect.
```

**Annotation:** Kling 3.0 at high-FPS slow-motion is genuinely cinematic. Basketball, running, diving, gymnastics — where a single hero body is in frame — all work well. Team contact sports are harder due to multi-body physics interaction.

---

### Genre 18: Found Footage / Mockumentary

**Recommended:** Kling 2.5 Std or 3.0 Std | T2V | Handheld | 720p + grain

```
Home video quality — VHS transfer, slight tracking artifacts, timecode visible 
lower-right corner. Year: 1997 overlaid. A birthday party in a backyard.
Someone is filming handheld — the camera shakes, zooms in and out awkwardly, 
catches faces mid-motion. Then the camera swings to the far end of the yard 
where a door stands open. One child stands there, alone, staring into the 
camera with an expression completely inconsistent with a birthday party.
The camera freezes on her face for 3 seconds, then someone off-camera laughs 
and the camera swings away.

VHS grain, chromatic aberration, warm color shift from old tape transfer.
Resolution: 480p look (upscaled from lower quality).
```

**Annotation:** Found footage is where Kling's "imperfect" visual outputs become a feature. Request VHS/degraded aesthetic deliberately. The 720p Standard tier with grain prompt actually produces better results here than high-res Pro.

---

### Genre 19: Trailer / Teaser

**Recommended:** Kling 3.0 Pro | Multi-shot | Rhythmic cut structure | 15s

```
Shot 1 (2s): EWS of a burning city skyline at night. Static aerial, no sound.
Shot 2 (2s): CU — a pair of boots stepping through broken glass. Sound: crunch.
Shot 3 (2s): ECU — eyes opening suddenly. Sound: sharp breath.
Shot 4 (3s): A crowd running in panic through a city street. Camera: handheld in the crowd.
Shot 5 (3s): @Hero stands alone on a hilltop, back to camera, watching the city below.
Shot 6 (3s): Extreme close-up — @Hero's hand gripping a weapon. Title card implied.
Audio: silence for shots 1–3, then a rising drone, then thunderous percussion hit on shot 4.
Pace: rapid, each shot shorter than the last. The classic trailer rhythm.
```

**Annotation:** Trailers require the fastest multi-shot cadence. 6 shots in 15s = minimum 2.5s average. Each shot must be self-contained. Avoid complex actions in short duration shots — iconic visuals and micro-moments only.

---

### Genre 20: Lip-Synced Character Dialogue

**Recommended:** Kling 3.0 O3 | Multi-shot with native audio | Elements for character voice

*This is one of Kling's definitive strengths in the current landscape.*

```
[Preparation: Create @Detective element with face photos (4 angles) and audio 
reference recording (15-second clip of the voice actor speaking). 
The system extracts visual DNA + voice tone into the element.]

Shot 1 (7s): Interrogation room. Fluorescent overhead. @Detective sits across the table, 
leaning forward. He places a folder on the table, eyes fixed on the suspect off-camera.

[Detective, controlled, low, slightly threatening voice]: "Every story has a beginning.
I want yours."

He doesn't blink. Silence for 2 beats.

[Detective, same tone, quieter]: "From the beginning."

Shot 2 (8s): The detective stands, moves to the window. He speaks without turning.
[Detective, measured]: "I've heard a lot of stories in this room. Some of them were even true."
He turns. Pause.
[Detective]: "How about yours?"

Camera: Shot 1 — MCU static. Shot 2 — medium shot from behind, then slow turn to reveal face.
Audio: fluorescent hum, detective's bound voice, chair shift, no music.
```

**Annotation:** O3 voice cloning enables a custom voice that stays consistent across all shots. The character bracket syntax `[Detective, tone]` is the documented O3 audio notation. Plan the dialogue to be performable in the shot duration — leave pauses for the model to render micro-expressions.

---

### Genre 21: Cinemagraph / Subtle Motion

**Recommended:** Kling 1.6 Std or 2.5 Std | I2V | Motion Brush | 5s loop

```
[Input: a stylized photo of a woman at a rainy café window]

Motion Brush: mask the raindrops on the window glass only
Motion direction: downward streaks on the glass surface
Motion intensity: slow, naturalistic

Prompt: rain on the window glass runs slowly downward. 
The woman is completely still. Nothing else moves. 
Loop-friendly beginning and end.

Duration: 5 seconds, loop.
Negative prompt: face movement, body movement, hair movement, background movement.
```

**Annotation:** Cinemagraphs require Motion Brush precision — isolate ONLY the elements that should move. Negative prompting the subject still is critical. Standard tier is sufficient for this use case; save credits. Loop-friendly framing: start and end on the same visual state.

---

### Genre 22: Slow-Motion Hero Moment

**Recommended:** Kling 3.0 Pro | T2V | 10–15s | **KLING'S DEFINITIVE STRENGTH**

```
Ultra slow-motion — 240fps equivalent capture of a single extraordinary moment.
A glass of red wine falls from a table edge. At the moment it tips past the point of no 
return: the glass begins to fall, the wine separates from the glass — a perfect elliptical 
arc of deep burgundy, catching the late afternoon window light.
The glass rotates slowly. The wine holds its shape for a fraction of a second — crystalline, 
backlit, every droplet visible as a suspended world.
Camera: macro 100mm equivalent, tracking the fall. Ultra shallow depth of field.
Lighting: hard backlight from window, direct front fill is almost absent — 
the wine is lit from inside.
Duration: 8 seconds covering the 0.3 real-time seconds of the fall.
Style: Zack Snyder slow-motion aesthetic, but with natural physics.
Color: rich burgundy, warm amber light, dark background.
Audio: slowed ambient — the beginning of the break, stretched.
```

**Annotation:** This is where Kling separates from all competitors. Its physics engine produces extraordinary slow-motion liquid, fabric, and particle behavior. Generate at maximum duration and framerate. The "sustained physical moment" — one action stretched over 8+ seconds — is Kling's signature.

---

### Genre 23: Talking-Head / Avatar Video

**Recommended:** Kling Avatar 2.0 OR Kling 3.0 I2V + Lip Sync | Front-facing portrait | 10s

```
[Method A — Avatar 2.0 interface:]
Upload clean, well-lit portrait photo of subject (front-facing, 1080p, neutral expression, 
professional clothing). Input script text. Select voice (TTS with emotion preset OR 
custom ElevenLabs audio). Generate 30–60 second avatar video.

[Method B — 3.0 I2V + Lip Sync:]
Generate base video: "professional spokesperson, front-facing, slight natural head movement, 
speaking naturally, clean studio backdrop, soft key light, professional attire.
Subtle hand gesture occasionally enters lower frame. Static camera, MCU."
Then apply Lip Sync with custom audio.

Best for: corporate training, product demos, explainer videos, news anchor format.
Style note: resist the urge to over-complicate. Clean, direct, believable is the goal.
```

---

*[Continued: Advanced Techniques, Parameter Tables, Failure Modes, Cost Optimization, Bibliography, Glossary, Appendix...]*


---

## 9. ADVANCED TECHNIQUES

### 9.1 Character Consistency Across Multiple Generations (Elements Workflow)

**Step-by-step O3 character consistency pipeline:**

1. **Source images:** Gather or generate 4 images of your character — front, 3/4 left, 3/4 right, side profile. Consistent lighting preferred. Consistent wardrobe if the character wears the same outfit across the piece.

2. **Create Element:** In Element Library → New Element → upload 4 images → name (e.g., "ArthurKing") → system creates visual DNA reference.

3. **Optional voice cloning (O3 only):** Upload 3–8 second clean audio of the character speaking naturally. Or upload 5–30 second audio for voice binding. System extracts and locks voice tone.

4. **Reference in prompts:** Use `@ArthurKing` in every shot prompt that includes this character. The model will attempt to match the stored element.

5. **Consistency maintenance tips:**
   - Provide directional context in each prompt ("@ArthurKing faces camera, three-quarter view")
   - Use consistent lighting descriptors across shots
   - Don't change wardrobe description mid-sequence (introduce wardrobe changes only with explicit transition context)
   - Use negative prompts per shot: `changing hairstyle, different clothing, aging`

**Known failure: off-angle coverage.** Single-image elements fail when the character turns to an angle not represented in the reference. Multi-angle element sets (3–4 images) solve this. If a specific angle keeps drifting, add an additional reference image from that angle.

### 9.2 Style Consistency Across a Sequence

For non-character visual style consistency (color grade, production design, lighting) across multiple generations:

- **LUT Reference image:** Generate a "master frame" with perfect aesthetics → use it as I2V start frame for all subsequent generations → the model inherits the base visual palette
- **Style anchor prompt:** Begin every prompt with identical style descriptor: "Roger Deakins Blade Runner 2049 cinematography — amber dust tones, deep cobalt shadows, anamorphic scope, 2.40:1" before any shot-specific content
- **Consistent camera descriptor:** Same lens reference, same aperture description across all shots

### 9.3 Reference-Driven Prompting (Multi-Tool Pipeline)

**Recommended input image generation workflow:**

| Tool | Strength | Use Case in Kling Pipeline |
|---|---|---|
| Midjourney v7 | Artistic quality, painterly | Fantasy, cinematic character portraits, art-film aesthetics |
| Flux 1.1 Pro | Photorealistic, prompt-faithful | Commercial, corporate, product photography input frames |
| Grok Imagine / Aurora | Fast, accessible | Quick test frames, social content |
| Adobe Firefly | Clean commercial aesthetic | Advertising, brand-safe content |

**Best practice:** Generate the input frame at the exact aspect ratio of your target Kling output (16:9 for landscape, 9:16 for portrait). This prevents letterboxing or cropping in I2V.

### 9.4 Image-to-Video Input Preparation Checklist

- [ ] Resolution ≥ 720p; ideally 1080p for Pro/3.0 generation
- [ ] File under 10MB (JPG/PNG preferred)
- [ ] Aspect ratio matches target output
- [ ] Subject clearly visible and logically frameable
- [ ] No extreme backlighting (confuses face detection)
- [ ] Simple-to-moderate background (busy backgrounds increase drift risk)
- [ ] For face/character: front-facing or near-front preferred for lip sync
- [ ] For product: clean neutral background for I2V product reveal
- [ ] For landscape/establishing: ensure there's room in the frame for camera movement to operate

### 9.5 Video-to-Video Restyle Workflow

**Complete pipeline:**
1. Source video: ideally 3–6 seconds of clean footage or previously generated clip
2. In Kling O3 → Reference Video mode: upload source as motion reference
3. Toggle "Keep Original Audio" if source audio should carry through
4. Upload Reference Images (optional): general visual style direction
5. Upload Element Images (optional): subject-specific consistency
6. Write prompt: `[Target style]. [Subject in target style]. [Environment in target style]. Preserve camera motion and movement timing from reference video.`
7. Set duration to match or be slightly shorter than source (avoid extending a restyle)
8. Generate; compare motion fidelity

**Common issue:** Restyle changes subject identity along with aesthetics. Solution: use Element binding for subject, restyle only the environment/lighting via prompt.

### 9.6 Extend Chains for Longer-Form Content

**Practical workflow for a 30-second piece:**

```
Clip 1 (base): T2V or I2V → 10–15 second master shot. Must end on a 
visually stable, non-transitory moment (not mid-jump, mid-explosion).

Clip 2 (Extend 1): Uses final frames of Clip 1 as context. Prompt advances 
action by 5–10 seconds. Keep environment descriptors identical.

Clip 3 (Extend 2): Uses final frames of Clip 2. If visual drift is visible,
STOP extending. Instead: screenshot the last frame of Clip 2 → 
generate fresh I2V from that frame → stitch in editing.

Assembly: Bring all clips into Premiere / DaVinci Resolve. Cut on action or 
at matched holds. Color grade consistently across all clips.
```

**Chain limit recommendation:** Maximum 3–4 extensions before quality degradation requires the "last-frame restart" method.

### 9.7 Storyboard → Keyframe Pair → Start/End Frame Pipeline

```
PRE-PRODUCTION:
1. Draw or describe storyboard panels (can be rough sketches)
2. For each key story beat, generate a single "hero frame" image using 
   Midjourney / Flux at the target aspect ratio
3. Verify the hero frames create a logical spatial and temporal sequence

PRODUCTION:
4. Pair consecutive hero frames as Start Frame + End Frame in Kling
5. Write interpolation prompt for each pair
6. Generate and review — usually 3–4 iterations per pair for best result

POST:
7. Sequence all clips in edit; use match cuts on hold moments
8. Add audio (ElevenLabs + Suno + MMAudio) for final delivery
```

### 9.8 Combining Kling with Audio Tools

| Need | Recommended Tool | Notes |
|---|---|---|
| Dialogue / voice | ElevenLabs v3 | Expressive, 32 emotion styles, 29 languages |
| Music underscore | Suno v4, Udio | 30–180 second stems; input mood/genre |
| Sound effects / foley | MMAudio, Freesound | MMAudio generates context-aware SFX from video |
| Spatial audio mix | DaVinci Resolve Fairlight | Free professional audio tool |
| Voice clone (post-only) | ElevenLabs Voice Clone | Clone from 30s sample for consistent character voice |
| Lip sync on existing clip | Kling Lip Sync feature | Or HeyGen for avatar-specific workflows |

### 9.9 Cost Optimization

**When to use Standard vs. Pro vs. Master:**

| Use Case | Recommended Tier | Reasoning |
|---|---|---|
| Concept testing / iterations | Standard (2.5 or 3.0) | Cost 20–36 cr; throw away most results |
| Social content (high volume) | 2.5 Turbo Standard | Fastest + cheapest; 30fps 1080p |
| Client-facing final output | Pro (3.0 or O3) | 1080p; proper quality |
| Character consistency pieces | O3 Standard or Pro | Elements system; worth the credit premium |
| Slow-motion hero shots | 3.0 Pro | Physics simulation needs Pro fidelity |
| Cinemagraph / subtle motion | 1.6 Standard or 2.5 Standard | Simple motion; Standard is sufficient |
| Product video | 3.0 Pro or O3 Standard | Clean output; Start/End Frame precision |

**Batch generation strategies:**
- Generate all Standard-tier concept tests first ($0.03–0.05/s equivalent)
- Identify 2–3 winning directions
- Generate Pro-tier final versions only on selected directions
- For multi-shot pieces: test single shots in Standard before committing to 6-shot Pro generation

### 9.10 Content Moderation: Working Legitimately Around Refusals

**What Kling blocks (international platform):**
- Explicit sexual content (zero tolerance; no workaround)
- Graphic gore / extreme violence
- Political content related to Chinese leadership / sensitive historical events
- Specific named real individuals in compromising scenarios
- Certain drug depictions

**Legitimate strategies for commercial edge cases:**

| Commercial Need | Refusal Risk | Legitimate Solution |
|---|---|---|
| Alcohol product (beer, whisky) | Low-medium | Frame as "amber liquid," "artisan distillery product" |
| Fight choreography | Medium | "martial arts demonstration," "stage combat rehearsal," explicit stylized context |
| Medical procedures | Medium | "clinical simulation," "anatomical illustration" |
| War/conflict imagery | High | Historical documentary framing; "archival footage aesthetic" |
| Gothic/horror religion | Medium | "theatrical horror set design," avoid specific real religious iconography |

**Language-switching technique (COMMUNITY-VERIFIED):** When an English prompt triggers a false positive filter, the same content in Chinese sometimes passes because the content filter has different sensitivity patterns per language. Not a workaround for genuinely prohibited content — only for false positives.

**IMPORTANT DISCLAIMER:** Do not attempt to circumvent genuine content policies. The strategies above are for navigating legitimate commercial production scenarios within Kling's published terms of service.

---

## 10. PARAMETER & SETTINGS REFERENCE TABLES

### 10.1 Model Selection Quick Reference

| Goal | Best Model | Tier |
|---|---|---|
| Maximum video quality | Kling 3.0 or O3 | Pro |
| Maximum character consistency | O3 | Standard or Pro |
| Native 5-language audio | Kling 3.0 / O3 | Any |
| Fastest generation | Kling 2.5 Turbo | Standard |
| Cheapest viable output | Kling 2.5 Turbo | Standard |
| Multi-shot narrative | Kling 3.0 | Pro |
| Start+End frame precision | O1 or 3.0 | Pro |
| Video-to-video restyle | O3 | Standard |
| Virtual Try-On | Kling 1.5 Kolors | — |
| 4K image output | Image 3.0 Omni | — |

### 10.2 Aspect Ratio by Platform Target

| Platform | Aspect Ratio | Kling Setting |
|---|---|---|
| YouTube / TV broadcast | 16:9 | 1920×1080 |
| TikTok / Instagram Reels | 9:16 | 1080×1920 |
| Instagram feed / square | 1:1 | 1080×1080 (or 960×960) |
| Cinema scope (implied) | 2.39:1 | Use 16:9; crop in post with letterbox |
| LinkedIn / Twitter | 16:9 or 1:1 | Both supported |

### 10.3 Negative Prompt Standard Library

**Universal baseline (copy-paste):**
```
blurry, low quality, low resolution, watermark, text overlay, logo, 
extra limbs, extra fingers, distorted hands, deformed anatomy, morphing face, 
flickering, ghosting, motion artifacts, jello effect, chromatic noise
```

**For photorealistic human subjects, add:**
```
changing hairstyle, shifting clothing, de-aging, aging, inconsistent eye color,
anime style, cartoon style, painted style
```

**For product shots, add:**
```
competing products, busy background, lens distortion, chromatic aberration,
motion blur on product, extra products in frame
```

**For cinematic output, add:**
```
TV commercial feel, overlit, overexposed, flat lighting, instagram filter, 
oversaturated, HDR processing look, phone camera quality
```

### 10.4 Audio Tag Syntax for Kling 3.0 / O3

**Single speaker:**
```
[CharacterName, emotion/tone description]: "Dialogue line"
```

**Multi-speaker (sequential):**
```
[CharA, controlled voice]: "Line 1."
Immediately,
[CharB, sharp defensive voice]: "Response."
Pause.
[CharA, softly]: "Closing line."
```

**Voice list for O3 multi-character:**
```
voice_list: [@ElementA, @ElementB]
```

**Audio environment tags:**
```
ambient: [environment description — e.g., "rain on glass, distant traffic"]
music: [description — e.g., "slow piano, melancholy, unresolved"]
sfx: [specific sounds — e.g., "ceramic mug set down hard"]
```

---

## 11. FAILURE MODES & DIAGNOSTIC FRAMEWORK

### 11.1 Anatomy and Hand Errors

| Error Type | Current State (3.0, May 2026) | Mitigation |
|---|---|---|
| Extra fingers | Significantly reduced in 3.0 vs prior versions | Negative: "extra fingers, distorted hands"; frame wider |
| Fused fingers | Occasional in close-up hand shots | Avoid ECU hand shots with specific grip requirements |
| Phantom limbs | Rare in 3.0 | Negative: "extra limbs" |
| Face morphing | Less common with Elements binding | Use Elements + consistent angle refs; negative: "morphing features" |
| Unrealistic joint bend | Occasionally on fast motion | Avoid prompting extreme gymnastics/contortion |
| Complex grip (writing, instruments) | Still unreliable | Frame wide; focus on body/environment; don't require fine motor accuracy |

**HONEST ASSESSMENT:** Kling 3.0 hand anatomy is "much improved" — standard walking, reaching, waving, pointing, holding an object at a normal distance — all largely reliable. Close-up hand interaction with instruments, keyboards, pens, or other hand remains risky. Plan shot design around this limitation.

### 11.2 Physics Violations

- **Gravity inconsistency:** Objects float, fall incorrectly, or pass through surfaces in complex multi-object scenes
- **Water/liquid:** Kling is excellent at single liquid source; two liquids mixing or splashing in a complex impact remain challenging
- **Extreme velocity:** Objects faster than ~60 mph equivalent tend to produce blur artifacts or spatial jumps
- **Cloth:** Simple fabric drape and movement excellent; complex folding/origami-like manipulation may fail

**Mitigation:** Prompt for single-physics-action per shot. "The rain falls" is better than "the rain falls, the puddles splash, and the water runs along the gutter." One physics interaction per generation.

### 11.3 Identity Drift Across Extends

**Symptoms:** Character's face gradually changes over 3+ extensions; hair color or clothing shifts.

**Diagnosis:** Insufficient subject anchoring in initial generation; element binding not used; prompt description drift across extensions.

**Solution:**
- Use Elements binding from the start
- Keep subject description word-for-word identical in every prompt
- Don't extend more than 2× without the "last-frame restart" method
- Strong negative prompts for identity drift: `changing hairstyle, different clothing, aging, de-aging`

### 11.4 Motion Artifacts

| Artifact | Description | Cause | Fix |
|---|---|---|---|
| Warping | Background or subject surface bends/distorts | Complex motion + low-contrast area | Increase background detail specificity; use Pro tier |
| Melting | Character features blend/merge | Extreme close-up + high motion | Wider framing; slower motion prompt |
| Ghosting | Semi-transparent double of subject | Fast motion + high contrast | Slow down described motion; avoid "rapid" |
| Jello effect | Rolling shutter-like wave in background | Conflict between Camera Control + other settings | Check for Motion Brush / End Frame conflict |
| Background drift | Background slowly changes aesthetic | Long generation without strong scene anchoring | Add explicit background description in prompt |

### 11.5 Prompt Collapse Symptoms

"Prompt collapse" is when the model ignores key instructions and outputs a generic result:

- **Symptoms:** Generic cinematic scene instead of your specific scene; camera movement not reflected; character description ignored
- **Causes:** Prompt overlong; conflicting instructions; too many competing priorities; content filter edge case
- **Diagnosis:** Strip prompt to bare minimum (subject + one action + one camera move). Does that work? Then add back one element at a time.

### 11.6 When to Abandon vs. Iterate

| Situation | Recommendation |
|---|---|
| 3+ generations all miss the same specific element | Change the prompt approach; the model may not support that specific output reliably |
| Generation looks 80% correct | Iterate — small prompt tweak or negative prompt addition |
| Consistent anatomy failure in close-up | Change shot design (frame wider); don't fight it |
| Native audio out of sync | Re-generate with audio; check voice tag syntax |
| Content filter refusal | Rephrase; check for inadvertent trigger words; try Chinese-language prompt |
| Physics impossibility | Redesign the action to be physically plausible |

### 11.7 When to Switch Tiers or Features

| Problem | Switch From | Switch To |
|---|---|---|
| Character drifts across shots | 3.0 T2V | O3 + Elements |
| Wanted specific end state | T2V | I2V with Start+End Frame |
| Specific motion path needed | Text prompt only | Motion Brush |
| Output too generic for style | Standard | Pro |
| Credits too expensive for testing | Pro | Standard for testing only |
| Need 6-shot in one generation | Single-shot generation | 3.0 Custom Multi-Shot |

---

## 12. COST & WORKFLOW OPTIMIZATION

### 12.1 Practical Per-Project Budget Framework

For a 30-second branded short film (Kling 3.0 Pro with audio):

| Phase | Action | Credits Used | Notes |
|---|---|---|---|
| Pre-production | Input image generation (external) | 0 | Midjourney / Flux |
| Concept testing | 6 Standard-tier 5s generations | ~180 cr | Test different directions |
| Shot development | 10 Pro-tier 5–10s generations | ~700 cr | Develop winning direction |
| Multi-shot production | 3 × 15s O3 Pro generations | ~1,050 cr | Final shots |
| Extend passes | 4 × 5s extends | ~140 cr | Continuity extends |
| Lip sync / audio | 5 lip sync applications | ~50 cr | Post-lip-sync |
| **Total** | | **~2,120 credits** | ~$25–30 at Pro plan rates |

### 12.2 API vs. Web Cost Comparison

For high-volume production (100+ clips/month):
- fal.ai API at $0.14/s Pro = $1.40 per 10s clip
- Web Pro plan: ~$0.70–1.00 per 10s clip at amortized plan pricing
- **Web plan wins** for consistent high-volume; API preferred for programmatic/automation workflows

### 12.3 Third-Party Platform Premium

Pollo, Higgsfield, RunDiffusion typically charge 20–50% premium over direct web pricing for the convenience of their workflows. Justified for teams that need integrated collaboration features.

---

## 13. SOURCE BIBLIOGRAPHY

*Format: [Source Name] — [URL] — [Access Date] — [Language]*

1. Kuaishou IR Press Release: "Kling AI Launches 3.0 Model" — https://ir.kuaishou.com/news-releases/news-release-details/kling-ai-launches-30-model-ushering-era-where-everyone-can-be — Feb 5, 2026 — [EN]

2. Wikipedia: Kling AI — https://en.wikipedia.org/wiki/Kling_AI — Accessed May 2026 — [EN]

3. fal.ai Kling 3.0 Prompting Guide — https://blog.fal.ai/kling-3-0-prompting-guide/ — Feb 4, 2026 — [EN]

4. DataCamp: Kling 3.0 Comprehensive Guide — https://www.datacamp.com/tutorial/kling-3-0 — Feb 11, 2026 — [EN]

5. invideo.io: Kling 3.0 Complete Guide — https://invideo.io/blog/kling-3-0-complete-guide/ — Feb 24, 2026 — [EN]

6. seavidgen.com: Kling 3.0 Prompt Complete Guide 2026 — https://seavidgen.com/blog/kling-3-0-prompt-complete-guide — Mar 2, 2026 — [EN]

7. vo3ai.com: Kling AI Pricing 2026 — https://www.vo3ai.com/kling-ai-pricing — May 10, 2026 — [EN]

8. voiceoverstudioai.com: Kling AI Pricing 2026 — https://voiceoverstudioai.com/blog/kling-ai-pricing-2026 — May 8, 2026 — [EN]

9. Official Kling AI Camera Control Guide — https://kling.ai/quickstart/ai-camera-control-guide — Nov 23, 2025 — [EN]

10. Official Kling AI Image-to-Video Guide — https://kling.ai/quickstart/image-to-video-guide — Nov 23, 2025 — [EN]

11. kling.ai: Kling Video 3.0 Omni Audio Guide — https://kling.ai/blog/kling-video-3-omni-native-lip-sync-audio-guide — Mar 16, 2026 — [EN]

12. kling.ai: Style Emulation Guide — https://kling.ai/blog/kling-ai-video-style-emulation-guide — Feb 1, 2026 — [EN]

13. kling.ai: Horror AI Video Prompts Guide — https://kling.ai/blog/horror-ai-video-prompts-color-grading-sound — Apr 24, 2026 — [EN]

14. pixverse.ai: Kling O3 and 3.0 Review — https://pixverse.ai/en/blog/kling-o3-and-3-0-now-available-on-pixverse — Apr 12, 2026 — [EN]

15. atlascloud.ai: Solving Character Inconsistency in Kling 3.0 — https://www.atlascloud.ai/blog/guides/solving-character-inconsistency-a-guide-to-kling-3.0-image-to-video-mode — Mar 25, 2026 — [EN]

16. curiousrefuge.com: Kling 3.0 Review — https://curiousrefuge.com/blog/kling-30-review — Feb 4, 2026 — [EN]

17. higgsfield.ai: Kling Start & End Frames — https://higgsfield.ai/blog/Kling-Start-End-Frames — Sep 2, 2025 — [EN]

18. pollo.ai: Camera Movement Guide — https://pollo.ai/hub/how-to-use-kling-ai-camera-movement — Jan 19, 2025 — [EN]

19. pollo.ai: Best Negative Prompts — https://pollo.ai/hub/kling-ai-best-negative-prompts — Jan 22, 2025 — [EN]

20. magiclight.ai: Kling AI Censorship — https://magiclight.ai/academy/kling-ai-censorship/ — May 13, 2026 — [EN]

21. chinatalk.media: Seedance, Kling and the Chinese AI Video Ecosystem — https://www.chinatalk.media/p/seedance-kling-and-the-chinese-ai — Feb 12, 2026 — [EN]

22. fal.ai: Kling O1 Image-to-Video API — https://fal.ai/models/fal-ai/kling-video/o1/image-to-video — Accessed May 2026 — [EN]

23. fal.ai: Kling 2.6 Pro Developer Guide — https://fal.ai/learn/devs/kling-2-6-pro-developer-guide — Dec 3, 2025 — [EN]

24. Scribd: Kling AI Video Creation Guide / Prompt Structure — https://www.scribd.com/document/978960962/Kling-Prompt-Guide — Jan 12, 2026 — [EN]

25. getimg.ai: Kling 1.6 vs 2.0 Master Comparison — https://getimg.ai/blog/what-is-kling-ai-comparing-kling-1-6-standard-pro-and-2-0-master — May 28, 2025 — [EN]

26. imagine.art: Kling 2.1 Start & End Frame Overview — https://www.imagine.art/blogs/kling-2-1-start-and-end-frame-overview — Aug 26, 2025 — [EN]

27. capcut.com: Kling AI Lip Sync Beginner's Guide — https://www.capcut.com/resource/kling-ai-lip-sync — Jul 31, 2025 — [EN]

28. Kuaishou PR Newswire: Original Kling Launch — https://www.prnewswire.com/news-releases/kuaishou-unveils-proprietary-video-generation-model-kling — Jun 9, 2024 — [EN]

29. GlobeNewswire: Kling AI 2.0 Era Launch — https://www.globenewswire.com/news-release/2025/04/15/3062142/ — Apr 14, 2025 — [EN]

30. pixflow.net: Best AI Video Generator 2026 — https://pixflow.net/blog/best-ai-video-generator/ — Apr 20, 2026 — [EN]

31. mindstudio.ai: Kling O3 Model — https://www.mindstudio.ai/blog/what-is-kling-o3-latest-video-model/ — Feb 12, 2026 — [EN]

32. SCMP: Kuaishou Kling 2.0 Launch — https://www.scmp.com/tech/big-tech/article/3306631/ — Apr 15, 2025 — [EN]

33. vidguru.ai: Kling 3.0 Omni Guide — https://www.vidguru.ai/blog/kling-3.0-omni-guide.html — Feb 15, 2026 — [EN]

34. tryonr.com: Kling 3.0 vs Omni Comparison — https://tryonr.com/blog/kling-3-0-omni-vs-kling-3-comparison — Mar 5, 2026 — [EN]

35. videoai.me: Access Kling AI Outside China — https://videoai.me/blog/how-to-access-kling-ai — Apr 11, 2026 — [EN]

36. veed.io: Kling AI 3.0 User Guide — https://www.veed.io/learn/kling-3-0-guide — Mar 1, 2026 — [EN]

37. YouTube (How to Use Motion Brush, Kling AI): https://www.youtube.com/watch?v=s7AcTNH01d8 — Sep 21, 2024 — [EN]

38. YouTube (EVERY Camera Movement Prompt in Kling 2.5): https://www.youtube.com/watch?v=cHpgSf7LKEE — Jan 1, 2025 — [EN]

39. YouTube (Kling 3.0 and Omni FULL guide 2026): https://www.youtube.com/watch?v=tEdHJohIUlM — Apr 3, 2026 — [EN]

40. YouTube (Kling 3.0 vs Kling O3 — Multi-Shot, Native Dialogue): https://www.youtube.com/watch?v=-bAZTGbpgKk — Mar 16, 2026 — [EN]

41. Bilibili (可灵AI): Multiple tutorials sourced via search — [ZH] — Note: Chinese community frequently publishes Kling technique guides 2–4 weeks ahead of English coverage. Specific prompting techniques in ZH community include: context-window anchoring, spatial navigation via image references, dialect-specific audio prompts.

42. kling.ai Release History (official changelog): https://kling.ai/release-note/release-history — Accessed May 2026 — [EN]

---

## 14. GLOSSARY

| Term | Definition | Chinese Equivalent |
|---|---|---|
| T2V | Text-to-Video | 文生视频 |
| I2V | Image-to-Video | 图生视频 |
| V2V | Video-to-Video (style transfer/restyle) | 视频转视频 |
| Elements | Multi-reference system for character/object/scene consistency | 元素 (Yuánsù) |
| Extend | Feature that continues an existing clip by generating additional frames | 延展 |
| Motion Brush | Mask-based motion vector control tool | 运动笔刷 |
| Start Frame | First keyframe for interpolation — defines the beginning of the clip | 首帧 |
| End Frame | Last keyframe for interpolation — defines the end of the clip | 尾帧 |
| Lip Sync | Feature synchronizing face/mouth animation to audio input | 对口型 / 唇形同步 |
| DiT | Diffusion Transformer — architecture type used in Kling | 扩散变换器 |
| 3D VAE | 3D Variational Autoencoder — Kuaishou's spatiotemporal compression module | 三维变分自编码器 |
| MVL | Multi-modal Visual Language — Kuaishou's unified input framework (v2.0+) | 多模态视觉语言框架 |
| MMW | Multi-modal-document as a Word — sub-concept of MVL for rich input | 多模态文档 |
| Omni / O3 | Video 3.0 Omni model — advanced multi-reference, voice cloning version | 全模态版 |
| Standard tier | Fastest, cheapest quality setting within a model | 标准模式 |
| Pro tier | Higher fidelity, higher credit cost | 专业模式 |
| Master tier | Highest quality (available in 2.0, 2.1) | 大师模式 |
| Negative prompt | Field specifying what to exclude from the generation | 反向提示词 |
| Multi-shot | Native generation of up to 6 distinct camera shots in a single 15s clip | 多镜头 |
| Smart Storyboard | Auto-segmentation mode where AI creates shot structure from single prompt | 智能分镜 |
| Custom Multi-Shot | Manual mode where user defines each shot's prompt and duration | 自定义多镜头 |
| Element Library | Storage for created Elements (characters, objects, scenes) | 元素库 |
| Voice cloning | O3 feature extracting and replicating a speaker's voice from reference audio | 音色克隆 |
| Credit | Kling's generation currency unit | 灵感值 (Línggǎn zhí) |
| klingai.com | International platform | 国际版 |
| kling.kuaishou.com | China domestic platform | 国内版 |
| CAC | Cyberspace Administration of China — regulates content policies | 网络安全管理局 |
| @ElementName | Prompt syntax for referencing a named element in generation | @元素名称 |
| DOP / DP | Director of Photography / Cinematographer | 摄影指导 |
| DoF | Depth of Field | 景深 |
| HFR | High Frame Rate | 高帧率 |
| T/S | Tilt-Shift | 移轴 |
| Bokeh | Out-of-focus background blur quality | 虚化 |
| Halation | Film exposure glow around bright highlights | 光晕 |
| Chiaroscuro | Extreme light/shadow contrast | 明暗对比法 |
| LUT | Look-Up Table (color grade preset) | 色彩查找表 |

---

## 15. APPENDIX: 40+ REUSABLE PROMPT TEMPLATES

### A. Opening Shots / Establishing

```
TEMPLATE A1 — City Establishing (T2V, 3.0 Pro)
A [time of day] establishing shot of [city/location]. The camera [movement]. 
[Atmosphere: weather/light]. [Color palette]. [Style reference].
Duration: 10s.
```

```
TEMPLATE A2 — Nature Establishing (T2V, 3.0 Std)
[Landscape type] at [time of day]. The camera [slow crane/drone movement].
[Atmospheric element: fog/mist/rain/snow]. No subjects. Pure environment.
Duration: 10–15s.
```

```
TEMPLATE A3 — Interior Reveal (I2V + Start Frame, 3.0 Pro)
[Starting frame: exterior of building/door]
The door opens slowly — revealing [interior description]. 
Camera pushes forward through the doorway as the interior is revealed.
Lighting: [interior source]. Duration: 7s.
```

### B. Character Introduction

```
TEMPLATE B1 — Classic Hero Introduction (T2V/I2V, 3.0 Pro + Elements)
@[CharName] walks toward camera through [environment]. [Time of day], [lighting].
Camera: slow tracking push-in, MCU becoming CU as character approaches.
Character: [brief description]. Expression: [confidence/determination/resignation].
Duration: 8s.
```

```
TEMPLATE B2 — Mystery Figure Reveal (T2V, 3.0 Pro)
[Environment description]. A figure in [descriptive silhouette] stands at [position].
Their face is [in shadow/not visible/obscured]. Camera: slow push-in from EWS to MWS.
The face is never fully revealed. Duration: 7s.
```

### C. Dialogue Scenes

```
TEMPLATE C1 — Two-Character Dialogue (3.0 O3 Multi-shot + Elements)
Shot 1 (5s): OTS on @CharA — looking at @CharB off-frame right. 
[CharA, tone]: "Dialogue line."
Shot 2 (5s): Reverse OTS on @CharB — looking at @CharA off-frame left.
[CharB, tone]: "Response line."
Shot 3 (5s): Two-shot — both characters visible. Silence for 3s. 
One beats, turns away. Camera static.
```

### D. Action/Tension

```
TEMPLATE D1 — Pursuit (T2V, 3.0 Pro)
[Subject] runs through [environment] at speed. Camera: handheld tracking shot 
at waist height, maintaining distance. [Atmospheric condition]. 
[Lighting conditions]. Duration: 8–10s. 
Negative prompt: physics violations, extra limbs, background morphing.
```

```
TEMPLATE D2 — Confrontation Hold (T2V, 3.0 Pro)
Two figures face each other across [distance] in [environment]. Neither moves.
Camera: static wide shot. [Lighting — split between the two]. 
Duration: 7s. Silence. Just before the clip ends, one figure [small action].
```

### E. Emotional Moments

```
TEMPLATE E1 — Grief (I2V, 3.0 Pro)
[Input: portrait of character in neutral expression]
Motion prompt: the character's expression subtly transitions from neutral to 
grief — slight tremor in the lip, eyes growing wet. No dramatic sobbing. 
Camera static MCU. Duration: 7s.
```

```
TEMPLATE E2 — Joy Reaction (I2V, 3.0 Std)
[Input: portrait of character looking slightly downward]
Motion prompt: they receive news (off-frame). Their head comes up slowly. 
Eyes widen, then a real laugh breaks through. Duration: 5s.
```

### F. Product Showcases

```
TEMPLATE F1 — 360° Product Reveal (I2V, Start+End Frame, 3.0 Pro)
[Start: product facing 0°] [End: product at 120°]
[Product name] rotates smoothly on a clean [white/dark/textured] surface.
Studio lighting — soft box from [direction]. The [material detail] catches the light
as it rotates. Camera static. Duration: 5s.
```

```
TEMPLATE F2 — Product in Context (T2V, 3.0 Pro)
A [product] is [used/worn/opened] in a [lifestyle context — kitchen, office, outdoors].
The focus is on the product interaction. [User hand] interacts with [product feature].
Camera: MCU, slight push-in as interaction completes. 
Style: [brand aesthetic — Apple minimalist / outdoor rugged / luxury warm].
```

### G. Atmosphere / Ambient

```
TEMPLATE G1 — Rain Scene (T2V, 3.0 Std)
[Interior/exterior location]. Rain falls [light/heavy] outside [on window/on pavement].
Camera: static, medium. No subjects. Pure atmosphere.
Audio: rain sound, [secondary ambient — café sounds, distant traffic].
Duration: 10s. Loop-friendly.
```

```
TEMPLATE G2 — Fire/Candle (I2V, 2.5 Std or 3.0 Std)
[Input: still image of candle or fireplace]
Motion: flame flickers naturally in a slight draft. Warm light pulses gently 
on the surrounding surfaces. No other movement.
Duration: 5s loop.
```

### H. Slow-Motion Specialties

```
TEMPLATE H1 — Liquid Hero (T2V, 3.0 Pro)
Ultra slow-motion — [240fps equivalent] — [liquid action: wine poured/glass falls/
splash impact]. Camera: [macro/close-up], static or very slow drift.
Backlit from [direction]. [Color of liquid]. Duration: 8–10s.
```

```
TEMPLATE H2 — Fabric in Wind (I2V, 3.0 Pro)
[Input: image of fabric/dress/cape in still position]
Motion: wind catches the fabric and it rises and billows dramatically in slow motion.
Ultra slow — fabric folds visible, fibers catching backlight.
Duration: 8s.
```

### I. Stylized / Non-Realistic

```
TEMPLATE I1 — Anime Style (T2V, 3.0 Pro)
[Scene description] in Studio Ghibli / Makoto Shinkai anime style.
2D hand-painted backgrounds, cel animation quality, [specific aesthetic elements].
Color: [palette reference]. Camera: [movement].
Duration: [8–15s].
```

```
TEMPLATE I2 — Noir (T2V, 3.0 Pro)
[1940s–50s setting]. [Character] in [noir environment — rain, shadows, venetian blinds].
Chiaroscuro lighting — high contrast, deep shadow. Black and white or 
near-monochromatic with one warm source. Camera: [static/slow dolly].
Style: Carol Reed The Third Man visual grammar.
```

### J. Social/Vertical

```
TEMPLATE J1 — Vertical Lifestyle (T2V, 3.0 Std, 9:16)
Portrait 9:16 format. [Subject activity in lifestyle context].
Camera: medium shot, slight camera rise (pedestal up).
Natural light. Warm, relatable, real. Duration: 5–7s.
No text. No logos. Clean for social use.
```

```
TEMPLATE J2 — Product UGC (I2V, 2.5 Std, 9:16)
Portrait 9:16. [Product] sits in a natural environment context.
[Subject] picks it up / uses it naturally. Camera: handheld presence, real.
Lighting: natural window light. NOT commercial — feels user-generated.
Duration: 5s.
```

### K. Multi-Character Native Audio

```
TEMPLATE K1 — Argument Scene (3.0 O3 Multi-shot + Elements + Audio)
[Environment]. 
Shot 1: @CharA — MCU — speaks.
[CharA, upset voice]: "Line 1."
Shot 2: @CharB — MCU — responds.
[CharB, defensive voice]: "Response."
Shot 3: Two-shot — silence — both breathing hard.
Audio: ambient [environment sound]. No music.
```

### L. Transitions / Bridges

```
TEMPLATE L1 — Time Lapse Feel (T2V, 3.0 Pro)
[Scene at a specific time of day]. The scene plays normally. Then the light 
begins to change — [morning to noon / noon to dusk / dusk to night]. 
The transition takes the entire 10-second clip.
Camera: static wide. Duration: 10s.
```

```
TEMPLATE L2 — Match Cut Bridge (I2V Start+End Frame, O1 or 3.0 Pro)
[Start frame: object/shape in Scene A at specific position]
[End frame: visually similar object/shape in Scene B at similar position]
Prompt: camera holds as the scene transforms from [A] to [B].
The matching shapes/objects provide the visual link.
Duration: 5s.
```

---

*End of kling-ai-research.md*
*Verified: May 25, 2026 | Kuaishou Kling AI current state*

