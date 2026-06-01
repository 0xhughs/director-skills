# Grok Imagine (Aurora) — Professional Prompt Engineering Reference
> **Target audience:** Working photographers, art directors, designers, and creative professionals  
> **Document version:** May 2026  
> **Files in this set:** `grok-imagine-research.md` (this file) · `grok-imagine-guide.md` (daily-use reference card)

---

## 1. Verification Note — Current Product and Model State (May 2026)

The following facts have been verified against xAI's official documentation, official blog posts, and multiple corroborated sources as of May 22, 2026.

### What "Grok Imagine" and "Aurora" Actually Are

- **Aurora** is the internal code name for xAI's proprietary autoregressive image generation model, first announced on **December 8–9, 2024**, and integrated into the X platform within a week of that announcement.
- **Grok Imagine** is the consumer and developer brand name for the full generation product — covering still image generation, image editing, image-to-video, video editing, and video extension — all powered by the Aurora engine.
- These are the same underlying technology; "Aurora" = architecture/engine; "Grok Imagine" = the product surface.

### Current Model Names (API, May 2026)

| Model identifier | Status | Best for |
|---|---|---|
| `grok-imagine-image-quality` | **Current recommended model** (as of May 2026) | High-fidelity stills, commercial work |
| `grok-imagine-image` | Standard / fast | Speed-sensitive batch work |
| `grok-imagine-image-pro` | **Deprecated as of May 15, 2026** | (Migrate to quality) |
| `grok-2-image` / `grok-2-image-1212` | Legacy Aurora (Dec 2024) | Still functional; older API integrations |
| `grok-imagine-video` | Active | Video generation and editing |

> **⚠ NOTE ON MODEL HISTORY:** Between August and October 2025, xAI briefly switched Grok Chat's image generation from Aurora to a Flux-based model, then reversed course following community backlash. As of late 2025/early 2026, the Aurora engine (via the Grok Imagine stack) is the primary model again. Some third-party sources from Q3–Q4 2025 may describe Flux behavior — treat those as **POTENTIALLY OUTDATED**.

### Release Timeline

| Date | Event |
|---|---|
| Dec 8–9, 2024 | Aurora announced and deployed on X platform |
| Aug 4, 2025 | Grok Imagine (image + video) launched with Spicy Mode for SuperGrok/Premium+ iOS users |
| Aug–Oct 2025 | Flux interlude; community backlash; Aurora reinstated |
| Oct 7, 2025 | Imagine v0.9 announced — native audio-video synchronization |
| Jan 2026 | xAI restricts image editing to paid subscribers following deepfake backlash |
| Jan 28, 2026 | **Grok Imagine API officially launched** — public developer access, #1 in Artificial Analysis Video Arena at launch |
| Feb 2026 | Major quality upgrade ("Grok Imagine 1.0"); `grok-imagine-image-quality` introduced |
| May 15, 2026 | `grok-imagine-image-pro` deprecated; `grok-imagine-image-quality` is the recommended model |

### Access Surfaces

- **grok.com** — Web UI; Imagine tab with text-to-image, image editing, image-to-video, video editing; free tier limited; Spicy Mode **not available** on web in most regions
- **X (web + mobile)** — Integrated into Grok on X; image generation in posts; editing of shared images (limited to paid subscribers on X posts)
- **Grok iOS / Android app** — Full feature access; Spicy Mode available for qualifying subscribers with age verification
- **xAI API (api.x.ai/v1)** — Full programmatic access; OpenAI SDK-compatible; $0.02/image (standard) to $0.07/image (2k quality); $25 promotional credits on signup; no X Premium subscription required
- **Third-party platforms** — fal.ai, Replicate, WaveSpeedAI, OpenRouter, Scenario, Runware, and others host Grok Imagine endpoints

---

## 2. Executive Summary

Grok Imagine, powered by xAI's Aurora engine, is a commercially significant image generation system with a distinct architecture (autoregressive mixture-of-experts) that sets it apart from the diffusion-based models dominating the landscape. As of mid-2026, it occupies a specific position: **exceptional value at scale** ($0.02/image API), **strong photorealism and prompt adherence**, and a **uniquely permissive content stance** relative to peers — at the cost of inconsistent content moderation (an active regulatory flashpoint), no native negative prompt support, and text rendering that, while improved, still trails Ideogram.

**For professional creative work, Aurora's strongest use cases are:**
- High-volume product, commercial, and editorial image pipelines where cost matters
- Realistic portrait and environmental photography where the autoregressive architecture produces natural skin and lighting
- Iterative creative exploration where fast API response times (8–12 seconds typical) enable tight feedback loops
- Cinematic and conceptual work benefiting from Aurora's strong handling of complex scenes and atmospheric cues

**Aurora's confirmed weaknesses** (do not oversell):
- Text rendering inside images: improved but not Ideogram-class; multilingual accuracy is inconsistent
- Negative prompts: **not natively supported** in the consumer UI; must be phrased as positive exclusions
- Hand and anatomy: still error-prone; requires mitigation strategies
- Character identity consistency across separate sessions: requires reference image workflow; not automatic
- Content moderation: volatile — policies have shifted multiple times since August 2025; what was allowed 6 months ago may now be blocked or vice versa

**Prompt style verdict (evidence-based):** Aurora performs best with **natural-language scene descriptions of 40–120 words**, structured as subject → environment → lighting → mood → camera/lens → style reference. It ignores negative prompts in the consumer UI, dislikes keyword tag lists, and front-weights the prompt (first sentence dominates).

---

## 3. Product & Model Foundations

### Architecture

Aurora is described officially by xAI as "an autoregressive mixture-of-experts network trained to predict the next token from interleaved text and image data." This is a fundamentally different architecture from the diffusion transformers used by Flux, Stable Diffusion, and Midjourney. Key implications:

- **Sequential token prediction** produces images that tend toward higher internal coherence — objects relate correctly to each other and to the scene
- **Interleaved text-image training** means the model has stronger grounding in real-world semantics than models trained on image-only pairs
- **Mixture-of-experts routing** enables the model to specialize different expert pathways for different visual domains without training entirely separate models
- Training was on "billions of examples from the internet," per xAI's official announcement — no further public detail on data sourcing or filtering has been released

> **LABEL: OFFICIAL** — architecture description sourced directly from xAI's December 2024 announcement blog post.

> **LABEL: SPECULATIVE** — the claim that one third-party source (xsoneconsultants.com, January 2026) makes that Aurora is "a modified version of Black Forest Labs' FLUX.1 model" is not corroborated by xAI and contradicts the official autoregressive architecture description. Treat as **unreliable**.

### Prompt Auto-Rewriting

A documented behavior (visible in the API `revised_prompt` response field) is that Aurora's pipeline includes a **chat-model-based prompt rewriter** that modifies user prompts before passing them to the image model. This is confirmed by the Grok API documentation: "When you send the prompt for image generation, your prompt will be revised by a chat model, and then sent to the image generation model." The API returns a `revised_prompt` field showing exactly what was used.

**Professional implication:** This means your exact wording is not always what Aurora "sees." The rewriter tends to add compositional and stylistic detail to short prompts. With longer, more specific prompts (80+ words), the rewriter has less room to deviate. If your output is drifting from intent, you can use the `revised_prompt` to diagnose the drift, then adjust your source prompt to steer the rewriter.

### Capability Matrix by Surface

| Capability | grok.com | X Web/Mobile | Grok iOS/Android | xAI API |
|---|---|---|---|---|
| Text-to-image | ✅ Free (limited) | ✅ Paid only (X posts) | ✅ Full | ✅ Pay-per-use |
| Image editing (NL instruction) | ✅ | ✅ Limited | ✅ | ✅ |
| Multi-image editing (up to 3 ref) | ✅ | ❌ | ✅ | ✅ |
| Text-to-video (up to 15s) | ✅ Limited | ❌ | ✅ SuperGrok | ✅ Pay-per-use |
| Image-to-video | ✅ | ❌ | ✅ | ✅ |
| Video editing | ✅ | ❌ | ✅ | ✅ |
| Video extension | ✅ | ❌ | ✅ | ✅ |
| Spicy Mode (R-rated visual) | ❌ Most regions | ❌ | ✅ SuperGrok/Premium+, 18+ verified | ❌ (API is moderated) |
| Batch generation (up to 10) | ❌ | ❌ | Limited | ✅ |
| 2K resolution | ✅ | ❌ | ✅ | ✅ |

### Output Specifications

| Parameter | Specification |
|---|---|
| Image resolution | 1K (1024px long edge) or 2K (2048px long edge) |
| Supported aspect ratios | 1:1, 16:9, 9:16, 4:3, 3:4, 3:2, 2:3, 2:1, 1:2, 19.5:9, 9:19.5, 20:9, 9:20, auto |
| Output formats | JPEG (default), PNG, WebP |
| Max images per request (API) | 10 |
| Max prompt length | 10,000 characters |
| Video duration | 1–15 seconds (text-to-video); edits capped at 8.7s |
| Video resolution | 480p or 720p |
| Video format | MP4 |
| API pricing (image) | $0.02/image (standard 1K); $0.05–0.07/image (2K quality) |
| API pricing (video) | $0.05/sec (480p); $0.07/sec (720p) |
| Generation speed | 8–12 seconds typical (image); 15–30 seconds (video) |

### Content Moderation Tiers

Grok Imagine operates on four visual content modes (consumer apps):

| Mode | What it allows | Requirements |
|---|---|---|
| **Normal** | Standard creative content; no explicit material | Free account (limited); paid for full access |
| **Fun** | Stylized, edgy, humorous; extended creative latitude | Free account (limited) |
| **Custom** | User-defined style anchors | Paid |
| **Spicy** | R-rated equivalence per Elon Musk (March 12, 2026 public statement); partial nudity, suggestive poses, mature themes | SuperGrok ($30/mo) or X Premium+ ($40/mo); 18+ age verification; iOS/Android only; two content toggles enabled; region-dependent |

**What Spicy Mode allows:** Suggestive poses, partial nudity (upper body), intimate framing, fantasy/fashion with mature undertones, romantic non-explicit scenarios, bold cinematic atmospheres.

**What Spicy Mode permanently blocks:** Explicit sexual acts, full-frontal pornographic content, anyone under 18 or appearing to be, real-person sexual deepfakes, non-consensual scenarios, hate speech combined with sexual content, CSAM. xAI reports suspected CSAM to NCMEC.

**As of early 2026:** Visual Spicy Mode has been substantially tightened following regulatory pressure (Ofcom investigation in the UK, deepfake criticism globally). Server-side post-generation moderation scans all outputs. Borderline outputs are auto-blurred. Sexualized depictions of real people are heavily restricted even in Spicy Mode.

**API note:** The xAI API endpoint is a moderated developer route — Spicy Mode toggle does not apply. Content policy governs all API-generated outputs.

---

## 4. Competitive Landscape

| Model | Architecture | Photorealism | Text in images | Style range | Speed | Price/image | Aurora vs. |
|---|---|---|---|---|---|---|---|
| **Aurora (Grok Imagine Quality)** | Autoregressive MoE | Strong; natural skin/lighting | Improved; not class-leading | Very broad | 8–12s | $0.02–0.07 | — |
| **Midjourney v7** | Diffusion | Best-in-class; painterly | Poor | Extremely deep style library | <20s | ~$0.05+ | Aurora: more photorealistic; MJ: more aesthetically polished |
| **GPT Image 2 (ChatGPT)** | Reasoning + diffusion | High; reasoning-enhanced accuracy | Excellent; multilingual | Good | 20–30s | ~$0.21 | Aurora: 10× cheaper; GPT: better text, better reasoning |
| **FLUX 1.1 Pro / FLUX.2** | Diffusion Transformer | Leading technical quality | Strong | Broad; commercial-safe | 4–5s | ~$0.04–0.08 | Flux: fastest, best for commercial volume; Aurora: better scene coherence |
| **Ideogram 3** | Diffusion | Good | **Best in class** | Moderate | ~10s | ~$0.06 | Aurora: better photorealism; Ideogram: superior typography |
| **Stable Diffusion 3.5 Large** | Diffusion | Good; locally adjustable | Moderate | Unlimited (open) | Variable | ~$0.01–0.03 | SD: fully open/local; Aurora: hosted only, better out-of-box quality |
| **Recraft V4** | Diffusion | Very high | Very good | Design-focused | ~8s | ~$0.04 | Recraft: better for branded design assets |
| **Nano Banana Pro (Gemini Image)** | Diffusion | High | Excellent | Strong | ~8s | ~$0.03–0.05 | Aurora: more permissive; NBP: better character consistency |
| **Imagen 4 (Google)** | Diffusion | High | Excellent | Moderate | ~8s | ~$0.03–0.04 | Imagen: stronger at text; Aurora: more permissive content policy |

**LABEL: COMMUNITY-VERIFIED** — Comparative assessments based on Artificial Analysis Image Arena rankings, independent reviews (aiviewer.ai, gradually.ai), and corroborated practitioner reports as of Q1–Q2 2026.

---

## 5. Prompt Anatomy: Evidence-Based Structure

### Natural Language vs. Tags

Aurora processes **natural language paragraphs** more effectively than comma-separated tag lists. This is consistently reported across multiple community-verified sources and attributed to the autoregressive architecture's language-model foundation. A prompt that reads like a scene description will outperform a tag stack.

**Tag stack (weak):**
```
portrait woman, cinematic, 85mm, Rembrandt lighting, bokeh, 8K, masterpiece, detailed
```

**Natural-language sentence (strong):**
```
Medium-close portrait of a woman in her late 30s, soft Rembrandt lighting from camera-left casting a gentle triangle on her right cheek, shallow depth of field from an 85mm f/1.4 lens, warm neutral background, calm introspective expression, editorial magazine quality.
```

### Optimal Prompt Length

| Length | Outcome |
|---|---|
| Under 20 words | Model defaults heavily; high variance; avoid for professional work |
| **40–80 words** | **Sweet spot for most use cases** — enough specificity to anchor the model, short enough to remain coherent |
| 80–120 words | Use for complex multi-element scenes; requires careful sentence structure to prevent internal contradictions |
| 120–200 words | Risk of prompt collapse — model may average across competing instructions; use only when every element is essential |
| Over 200 words | Not recommended; the 10,000-character limit is a technical ceiling, not a recommendation |

### Positional Weighting

The **first sentence of your prompt receives the highest weight**. This is consistent with how language-model-based image systems process input. Always lead with the subject, then layer context. Placing style keywords first and subject last weakens the output.

**Correct order:**
> *Subject → Environment → Lighting → Mood → Camera/Lens → Style reference*

### Negative Prompt Support

**OFFICIAL CONFIRMED:** Aurora's consumer UI does **not support negative prompts** as a separate input field. The Picsart and multiple other practitioner guides confirm this explicitly. There is no `--no` flag or negative prompt box.

**Workaround:** Frame all exclusions as positive assertions.

| Instead of | Write |
|---|---|
| "no blurry background" | "sharp background" or "deep focus, f/8, full environment in focus" |
| "no extra fingers" | "hands carefully positioned, natural grip, anatomically correct" |
| "no text watermarks" | "clean image surface, no overlaid graphics" |
| "no harsh shadows" | "soft diffused lighting, minimal shadows" |
| "no people in background" | "empty environment, solitary subject, deserted location" |

### Multi-Subject Scenes

Aurora handles multi-subject scenes reasonably well if you **assign spatial positions explicitly** and describe interactions rather than listing characters. For complex blocking, use the `@image1`, `@image2` reference syntax (available in Grok Chat) to anchor specific character appearances.

### Text Rendering Inside Images

**Current state (May 2026):** Aurora has improved substantially since December 2024, with the `grok-imagine-image-quality` model adding "clean multilingual text rendering" as a positioned feature. It handles basic Latin-character signage, posters, and packaging adequately. However, ChatGPT Images 2.0 and Ideogram remain superior for text-critical work (multilingual marketing materials, complex typography hierarchies).

**Best practices for text in images:**
- Enclose the exact desired text in quotation marks within the prompt: `a café sign reading "Le Petit Café"`
- Keep text short (under 6 words per text element)
- Specify font mood descriptively: "bold condensed sans-serif", "hand-lettered chalk", "embossed gold serif"
- Do not attempt complex multi-line body copy; limit to headlines, labels, and short phrases
- If text accuracy is mission-critical, use Ideogram 3 instead

### Real People and Public Figures

Aurora's policy on real persons has been volatile. As of mid-2026:
- **Non-sexualized, non-defamatory depictions** of public figures (politicians, celebrities) are generally possible but subject to moderation
- **Sexualized depictions of real people** are blocked by server-side moderation even in Spicy Mode
- **Deepfake editing** (undressing, face-swapping) is prohibited and technically restricted
- **Celebrity in satirical, artistic, or documentary-style context** with clearly non-realistic framing tends to pass moderation more reliably
- For brand/advertising work involving real people, always obtain consent; generated likenesses are not substitutes for model releases

### Brand and IP Handling

Aurora recognizes and can render **branded objects, iconic locations, and named real-world entities** (e.g., "a Leica M11 on a wooden desk"). This is a documented capability advantage. However:
- Reproducing **trademarked logos exactly** (Coca-Cola script, Nike swoosh) is restricted
- Referencing a **brand aesthetic** without exact logo reproduction is generally permitted
- **Copyrighted character designs** (Disney, Marvel, etc.) are moderated inconsistently — do not rely on this for commercial work

---

## 6. The Photography Vocabulary — Section A: Camera Body & Format

Photography-specific terminology is one of Aurora's clearest performance amplifiers. The model's training on internet image data includes extensive photography metadata, gear reviews, and technical content, giving it strong associations between camera/lens terminology and specific visual qualities.

### Sensor Format Vocabulary Table

| Term in prompt | Effect Aurora typically produces |
|---|---|
| "medium format", "Hasselblad H6D", "Phase One IQ4", "Fujifilm GFX100S" | Extreme micro-contrast, very shallow DoF even at moderate apertures, 3D "pop" effect, luxurious tonal gradation |
| "35mm full-frame", "Sony A1", "Canon EOS R5", "Nikon Z9", "Leica M11" | Standard photographic "look" — the baseline reference most photography-trained AI uses |
| "APS-C", "Fujifilm X-T5", "Sony a6700" | Slightly tighter FOV implied; film simulation aesthetic if Fujifilm referenced |
| "Micro 4/3", "Olympus OM-1" | Deeper DoF at equivalent apertures; suggests travel/documentary aesthetic |
| "35mm film", "shot on film", "analog photography" | Grain, organic tones, slight color cast, reduced digital precision |
| "large format 4x5", "large format 8x10", "view camera" | Extreme sharpness across field OR extreme selective focus (tilt), architectural photography feel |
| "Polaroid", "instant film", "Polaroid SX-70" | Characteristic faded whites, color drift, heavy vignette, lo-fi charm |
| "Holga", "toy camera", "lomography" | Vignetting, soft edges, light leaks, unpredictable color |
| "disposable camera", "single-use camera" | Flat flash, high grain, cheap lens flare, nostalgic snapshot quality |

**LABEL: COMMUNITY-VERIFIED** — Effects listed based on multiple practitioner reports and structured testing references (chatsmith.io, picsart.com, skylum.com guides).

**Pitfall:** Adding "8K" or "4K" as a quality descriptor adds nothing to Aurora — it is not a resolution-control token the way it functioned in early Stable Diffusion prompts. Use resolution parameter in the API instead.

---

## 6. The Photography Vocabulary — Section B: Lens Language

### Focal Length Effects

| Focal length term | Visual effect | Best use cases |
|---|---|---|
| "14mm", "ultra-wide", "14mm rectilinear" | Dramatic wide angle, strong perspective distortion, exaggerated foreground, architectural sense of scale | Environmental portraiture, architecture, landscape |
| "24mm", "wide angle" | Modest distortion, environmental context, slightly heroic perspective | Street, documentary, lifestyle |
| "35mm" | "Natural" field of view; the photojournalist's classic; slight perspective depth | Street, documentary, candid |
| "50mm", "standard lens", "50mm prime" | Closest to human eye perspective; no distortion; versatile | Portrait, still life, commercial |
| "85mm", "85mm f/1.4", "85mm portrait lens" | Slight compression, flattering facial geometry, classic portrait look | Headshots, beauty, fashion |
| "135mm", "135mm f/2" | Moderate telephoto compression; subject separation; beautiful bokeh | Portraits, editorial, wedding |
| "200mm", "telephoto" | Strong compression; background brought close; subject isolation | Wildlife, sports, candid |
| "400mm", "super-telephoto" | Extreme compression; atmospheric haze layers; wildlife feel | Wildlife, sports, photojournalism |
| "macro", "1:1 macro", "extreme close-up" | Magnification, abstract surface detail, diffraction possible | Product, food, nature detail |
| "fisheye", "8mm fisheye" | Extreme barrel distortion, circular or full-frame, surreal feel | Creative, action sports |
| "tilt-shift", "tilt-shift miniature effect" | Selective focus plane, architectural correction, or fake miniature look | Architecture, landscape, commercial |

### Aperture and Depth of Field

| Aperture term | Effect |
|---|---|
| "f/1.2", "f/1.4", "wide open" | Extreme shallow DoF; creamy bokeh; minimal in-focus zone; subject pops |
| "f/2", "f/2.8" | Shallow DoF with slightly more subject coverage |
| "f/4" | Subject sharp; background beginning to separate |
| "f/8", "sharp throughout" | Traditional "sweet spot" — maximum resolution, moderate DoF |
| "f/11", "f/16" | Deep DoF; diffraction beginning; landscape standard |
| "hyperfocal distance" | Everything from near distance to infinity in focus |

### Lens Character Terms

| Lens character term | Associated visual quality |
|---|---|
| "vintage Leica rendering", "Leica Summilux", "Leica character" | 3D pop, slightly warm rendering, smooth out-of-focus transitions |
| "anamorphic lens", "anamorphic bokeh" | Oval bokeh, horizontal lens flare streaks, cinematic widescreen feel |
| "Petzval lens", "swirly bokeh", "Petzval swirl" | Characteristic spiral bokeh in background; Victorian/vintage feel |
| "Lensbaby", "selective focus effect" | Off-axis sweet spot; artistically blurred periphery |
| "zeiss rendering", "zeiss contax" | Micro-contrast, clinical sharpness, cool neutral rendering |
| "vintage 70s lens", "pre-AI lens", "flary vintage glass" | Reduced contrast, glow, chromatic aberration |

### Optical Artifacts

| Artifact term | When to use |
|---|---|
| "chromatic aberration", "color fringing" | Adds vintage/analog realism; use sparingly |
| "vignetting", "natural vignette" | Draws eye to center; analog feel |
| "lens flare", "sun star", "anamorphic flare" | Adds energy and realism for bright-light scenes |
| "halation", "glow around highlights" | Film-like bloom; romantic, soft look |
| "barrel distortion" | Wide-angle realism |
| "optical diffusion", "soft focus" | Ethereal, beauty/glamour look |

### Filter Simulations

| Filter term | Effect |
|---|---|
| "Black Pro-Mist filter", "pro-mist diffusion" | Halation around lights, softened highlights, cinematic look |
| "IR filter", "infrared", "false-color infrared" | White foliage, dark sky, surreal tones |
| "polarizer", "polarized sky" | Deepened blue sky, reduced reflections, enhanced foliage |
| "graduated ND filter", "ND grad" | Balanced exposure between sky and ground |
| "diffusion filter", "Hollywood diffusion" | Softened skin, romantic glow |

---

## 6. The Photography Vocabulary — Section C: Framing & Shot Scale

Aurora responds reliably to standard film/photography shot scale terminology:

| Code | Full name | Description |
|---|---|---|
| ECU | Extreme close-up | Single eye, lips, pore-level detail |
| CU | Close-up | Face fills frame |
| MCU | Medium close-up | Head and upper shoulders |
| MS | Medium shot | Waist up |
| MWS | Medium wide shot | Knees up; full expression visible |
| WS | Wide shot | Full body with environment context |
| EWS | Extreme wide shot | Subject small; environment dominant |

**Portrait conventions:**
- "Headshot" — face to clavicle; corporate or editorial
- "Half-body portrait" — waist up
- "Three-quarter portrait" — thigh/knee up
- "Full-length portrait" — head to toe
- "Environmental portrait" — subject visible within their environment/workspace

**Multi-subject framing:**
- "OTS shot", "over-the-shoulder" — foreground subject partial, attention on background subject
- "Two-shot" — two subjects in frame with spatial relationship
- "Ensemble shot", "group portrait" — three or more subjects

**Camera angles:**
- "Eye-level", "straight-on" — neutral, relatable
- "Low angle", "worm's eye view", "hero angle" — subject appears powerful, monumental
- "High angle", "bird's eye view" — subject appears vulnerable or contextual
- "Dutch angle", "canted angle" — tension, unease, drama
- "Overhead", "flat-lay", "top-down" — graphic, product, food
- "POV", "first-person perspective" — immersive, subjective

---

## 6. The Photography Vocabulary — Section D: Composition

Aurora's architecture processes compositional language as meaningful scene directives. Unlike tag-based systems, you can describe compositional intent in sentences.

### Compositional Rules

| Technique | Prompt phrase |
|---|---|
| Rule of thirds | "subject placed on the left third", "off-center composition, rule of thirds" |
| Golden ratio / spiral | "golden ratio composition", "subject at the golden spiral intersection" |
| Centered symmetry | "centered composition, bilateral symmetry", "perfectly symmetrical framing" |
| Leading lines | "a road leading the eye toward the subject", "leading lines converging on the figure" |
| S-curve | "S-curve river winding through the frame" |
| Diagonal tension | "strong diagonal composition from lower-left to upper-right" |
| Negative space | "generous negative space to the right of the subject", "subject isolated in lower-left corner, empty sky above" |
| Foreground layering | "shallow foreground element blurred in lower frame, subject sharp in midground" |
| Frame within frame | "subject framed by a doorway", "window frame composing the subject within" |
| Pattern and repetition | "repeating arches creating rhythm behind the subject" |

### Subject Placement

- "Rule of odds — three subjects" creates natural visual tension
- Explicitly state headroom and lead room: "three inches of headroom above the figure", "lead room to the right as she looks left"

---

## 6. The Photography Vocabulary — Section E: Lighting

Lighting specification is the single highest-leverage element in any Aurora prompt. The model has extremely strong associations between named lighting setups and visual output.

### Named Lighting Schemes

| Scheme | Prompt phrase | Characteristic look |
|---|---|---|
| Three-point | "classic three-point lighting setup" | Balanced, television, commercial |
| Rembrandt | "Rembrandt lighting", "triangular shadow on cheek" | Dramatic, fine art, classic |
| Butterfly / Paramount | "butterfly lighting", "paramount lighting" | Glamour, beauty; shadow under nose |
| Loop lighting | "loop lighting" | Natural; slight nose shadow loops down |
| Split lighting | "split lighting, half face in shadow" | Dramatic, edgy, fashion |
| Broad lighting | "broad lighting, main light toward camera" | Fuller face, high-key commercial |
| Short lighting | "short lighting, shadow side toward camera" | Narrowing, dramatic, editorial |
| Clamshell | "clamshell lighting, reflector below" | Beauty, cosmetics, filled shadows |

### Light Quality

| Quality | Prompt phrase | Effect |
|---|---|---|
| Hard | "hard directional light", "strong shadows with crisp edges" | Dramatic, noon sun, strobe without modifier |
| Soft | "soft diffused light", "wrapped light, gentle transitions" | Flattering, cloudy day, large softbox |
| Specular | "specular highlights", "shiny surfaces catching hard light" | Commercial product, metal, glass |
| Dappled | "dappled light through leaves", "mottled forest light" | Natural, intimate, editorial |

### Light Direction

| Direction | Prompt phrase |
|---|---|
| Key light (main) | "key light from camera-left", "strong side light" |
| Fill light | "soft fill from camera-right, 2 stops under key" |
| Rim / hair light | "rim light outlining the figure", "hair light separating from background" |
| Backlight | "strong backlight creating silhouette", "backlit scene, subject glowing at edges" |
| Top light | "overhead light casting downward shadows" |
| Under light | "light source below, uplighting, dramatic horror feel" |

### Modifier Vocabulary

| Modifier | Prompt phrase |
|---|---|
| Softbox | "large softbox key light", "softbox wrapped around the subject" |
| Beauty dish | "beauty dish, specular catchlights" |
| Octabox | "large octabox, even soft illumination" |
| Ring light | "ring light, circular catchlights in eyes" |
| Reflector | "silver reflector fill from below" |
| Scrim / diffusion panel | "scrim diffusing harsh window light" |

### Light Sources

| Source type | Prompt phrase | Color temperature feel |
|---|---|---|
| Tungsten | "tungsten practical lights", "warm orange tungsten glow" | Very warm 3200K |
| HMI | "HMI daylight fill" | Cool 5600K |
| LED panel | "LED panel side light" | Variable |
| Neon | "neon sign light", "neon pink and blue light" | Highly saturated colored |
| Candle / firelight | "single candle illumination", "warm firelight from below" | Extremely warm, flicker |
| Screen glow | "face lit only by laptop screen glow", "blue screen light" | Cool, modern, intimate |
| Window light | "soft northern window light", "Vermeer window light, diffused afternoon" | Gorgeous naturalistic |
| Golden hour | "golden hour, warm low sun, long shadows" | 2700–3200K, deeply golden |
| Blue hour | "blue hour twilight, even cool illumination" | 10,000K+ ambient |
| Overcast | "flat overcast light, even fill, no shadows" | 7000K, neutral |
| Magic hour | "magic hour, last 15 minutes of sunlight" | Maximum warmth and drama |

### Mood Lighting

| Mood | Prompt phrase |
|---|---|
| High-key | "high-key lighting, bright whites, minimal shadows" |
| Low-key | "low-key lighting, deep shadows, small light source" |
| Chiaroscuro | "dramatic chiaroscuro lighting, deep blacks" |
| Noir | "film noir lighting, venetian blind shadow pattern, single hard light" |
| Caravaggio | "Caravaggio-style lighting, dramatic shadow, period oil painting feel" |
| Vermeer | "Vermeer window light, soft directional daylight, Dutch master quality" |
| Naturalistic | "naturalistic available light, documentary feel" |
| Editorial | "editorial lighting, intentional and controlled, magazine quality" |

---

## 6. The Photography Vocabulary — Section F: Atmospherics

Atmospheric cues are highly effective in Aurora because the autoregressive model has strong associations between atmospheric descriptors and compositional decisions (haze layers, reduced contrast, color temperature shifts).

### Weather and Atmosphere Terms

| Atmospheric element | Prompt phrase | Effect |
|---|---|---|
| Fog / mist | "dense fog reducing contrast", "morning mist, soft depth layers" | Mood, mystery, depth |
| Rain | "heavy rain, rain-soaked streets with reflections", "light drizzle" | Energy, atmosphere, wet texture |
| Snow | "falling snow, overcast diffused light" | Quiet, isolation, high-key |
| Heat shimmer | "desert heat shimmer, atmospheric distortion" | Arid, cinematic |
| Volumetric light / god rays | "god rays through clouds", "volumetric light beams through smoke" | Cinematic, sacred, atmospheric |
| Dust / sand | "dust storm, orange light filtered through particulate" | Epic, harsh, environmental |
| Smoke | "smoke haze in background", "light beams visible in smoke" | Dramatic, atmospheric |
| Embers | "glowing embers in foreground" | Fire scene, warm, intimate |

### Particulate and Micro-Atmospheric

- "dust motes floating in shaft of light" — adds interior atmosphere
- "pollen in air, soft golden haze" — spring/garden scenes
- "sea spray, ocean mist" — coastal scenes
- "condensation on glass" — adds tangible texture

### Seasonal Cues

- "early March, bare branches catching morning light" — specific and painterly
- "late October light, golden-brown leaves, low sun angle" — autumn warmth
- "deep January snow, blue-grey shadows, cold still air" — winter austerity

---

## 6. The Photography Vocabulary — Section G: Color Science & Film Stocks

Color specification is among Aurora's most responsive capabilities. The model's training on photography-tagged internet content means film stock names trigger specific tonal profiles.

### Film Stock Emulations

| Film stock | Prompt phrase | Signature look |
|---|---|---|
| Kodak Portra 400 | "Kodak Portra 400 color profile" | Warm skin tones, pastel highlights, natural saturation |
| Kodak Portra 800 | "Kodak Portra 800, pushed latitude" | Slightly more grain, shadows lift, latitude look |
| Kodak Ektar 100 | "Kodak Ektar 100, saturated landscape" | Punchy primary colors, high saturation landscapes |
| Kodak Tri-X 400 | "Tri-X film grain, high contrast black and white" | Aggressive grain, deep blacks, photojournalism grain structure |
| Kodak T-Max | "T-Max fine grain black and white" | Finer grain than Tri-X, smoother tonality |
| Fujifilm Pro 400H | "Fujifilm Pro 400H, pastel skin tones" | Very pastel, cool highlights, wedding/lifestyle |
| Fujifilm Velvia 50 | "Velvia 50, hyper-saturated landscape" | Maximum saturation, punchy greens and reds |
| Fujifilm Provia | "Provia transparency, neutral accurate" | Clean, accurate, documentary |
| Cinestill 800T | "Cinestill 800T, tungsten halation" | Night city scenes, halation around lights, blue shadows |
| Ilford HP5 | "Ilford HP5 black and white" | Versatile, pushed street photography grain |
| Ilford Delta 3200 | "Delta 3200, extreme grain" | Massive grain structure, low-light authenticity |
| Lomochrome Purple | "Lomochrome Purple, false color" | Green → purple, surreal nature color shift |
| Expired film | "expired film, color drift, unpredictable cross-contamination" | Faded, color-shifted, nostalgic imperfection |

### Processing Techniques

| Technique | Prompt phrase | Look |
|---|---|---|
| Cross-process | "cross-processed, E-6 in C-41, teal shadows orange highlights" | Unnatural, punchy, 90s rave aesthetic |
| Push processing | "pushed 2 stops, elevated grain, blocked shadows" | Contrasty, high grain, urgency |
| Pull processing | "pulled 1 stop, pastel, low contrast" | Soft, airy, editorial |
| Bleach bypass | "bleach bypass process, desaturated, high contrast" | Silver retention, reduced color, cinematic |

### Digital Color Grading References

| Grade reference | Prompt phrase | Look |
|---|---|---|
| Teal and orange | "teal and orange color grade, Hollywood blockbuster" | Complementary split; warm skin, cool shadows |
| Vintage Kodachrome | "Kodachrome color, warm reds, slightly faded yellows" | 1960s–70s warmth |
| Faded postcard | "faded postcard color, washed-out, lifted blacks" | Nostalgic lo-fi |
| Neon noir | "neon noir, deep shadows, saturated neon accents" | Cyberpunk/crime thriller |
| Nordic desaturated | "desaturated Nordic palette, cool grey-blue, muted" | Scandinavian minimalism |
| Mexico filter | "Mexico filter, warm golden ambient, teal sky" | Telenovela/Netflix Latin drama look |

### Named Photographer/Cinematographer Palettes

These references can be highly effective but results are variable — Aurora's recognition of these references has not been officially confirmed.

| Reference | Prompt phrase | Expected aesthetic | Label |
|---|---|---|---|
| Saul Leiter | "Saul Leiter color, muted saturated blocks, street abstraction" | Rich but muted color, graphic depth | COMMUNITY-VERIFIED |
| Wes Anderson | "Wes Anderson palette, pastel symmetrical" | Symmetry, pastel pinks/yellows, flat staging | COMMUNITY-VERIFIED |
| Roger Deakins | "Roger Deakins cinematography, moonlight blue, Sicario palette" | Desaturated cool tones, precise natural light | COMMUNITY-VERIFIED |
| Gregory Crewdson | "Gregory Crewdson cinematic, suburban uncanny, cinematic suburban" | Cinematic staging, suburban setting, mystery | COMMUNITY-VERIFIED |
| William Eggleston | "William Eggleston color, American South, dye transfer" | Saturated mundane scenes, democratic color | COMMUNITY-VERIFIED |
| Nan Goldin | "Nan Goldin, snapshot saturation, intimate" | High saturation, raw, snapshot quality | COMMUNITY-VERIFIED |

---

## 6. The Photography Vocabulary — Section H: Subject Action & Performance

### Pose Vocabulary

| Pose type | Prompt phrase |
|---|---|
| Contrapposto | "contrapposto stance, weight on one hip, classical pose" |
| Candid | "caught mid-action, candid, not posing" |
| Dynamic | "dynamic movement, motion energy, action pose" |
| Static / contemplative | "still, quiet presence, introspective" |
| Gesture | "expressive hand gesture", "hands in motion" |
| Walking | "mid-stride, confident walk" |

### Micro-Expressions

Specific emotional direction produces better results than generic adjectives:
- Weak: "happy expression"
- Strong: "subtle upturn at corner of lips, relaxed brow, eyes lit by genuine warmth"

| Emotion | Effective prompt phrase |
|---|---|
| Joy | "eyes crinkled, soft smile reaching the eyes, radiant" |
| Melancholy | "downward gaze, slightly parted lips, weight of quiet thought" |
| Intensity | "locked direct gaze into camera, jaw set, focused" |
| Vulnerability | "averted gaze, slight tension at brow, exposed" |
| Authority | "direct gaze, relaxed posture, command without effort" |

### Hand Placement

Hands remain one of Aurora's most persistent failure modes. Mitigation strategies:

1. **Keep hands out of frame when possible** — use MCU or tighter shots
2. **Give hands something to do:** "both hands wrapped around a coffee cup", "right hand resting on chin, elbow on table", "fingers loosely interlaced, resting in lap"
3. **Specify digit count explicitly:** "five fingers clearly visible, natural hand position"
4. **Describe grip and purpose:** "holding a vintage camera with both hands, thumbs on controls"
5. **Avoid requests for complex hand signs or gestures** — these still fail frequently

### Wardrobe Specification

More specific = better Aurora adherence:
- Weak: "wearing a nice suit"
- Strong: "charcoal wool double-breasted suit, peak lapels, white Oxford shirt with spread collar, no tie, pocket square in white linen"

| Wardrobe element | Useful terms |
|---|---|
| Fabric | wool, silk, cotton, linen, denim, leather, velvet, chiffon, organza, neoprene |
| Fit | tailored, relaxed, oversized, slim-cut, draped |
| Condition | pristine, softly worn, distressed, wrinkled, starched |
| Era | 1970s silhouette, 1990s grunge, Y2K, contemporary, Victorian |

### Skin Specification

Describe respectfully with specificity:
- "warm medium-brown skin with natural oiliness and visible pores"
- "pale porcelain skin with light freckles across nose and cheeks, almost no redness"
- "deep mahogany skin with a subtle sheen, fine textured"
- "weathered and lined, evidence of decades outdoors"

---

## 6. The Photography Vocabulary — Section I: Environment & Set Design

### Location Specificity

Named real locations work well in Aurora:
- "Brooklyn Bridge at dusk, golden hour, Manhattan skyline"
- "Shibuya Crossing at night, neon signs reflecting on wet pavement"
- "Provence lavender field, midsummer, 8am light"

Fictional but specific environments work equally well:
- "a 1940s Paris brasserie interior, zinc bar, tile floor, pressed tin ceiling"
- "brutalist Soviet-era government building exterior, concrete weathered, overcast sky"

### Architectural Style References

| Style | Prompt phrase |
|---|---|
| Brutalism | "raw concrete brutalist architecture, monolithic, textured surface" |
| Art Deco | "Art Deco facade, geometric ornamentation, gold and black detailing" |
| Bauhaus | "Bauhaus interior, clean geometry, primary colors, functional" |
| Japanese minimalist | "Japanese minimalist interior, wabi-sabi, natural materials" |
| Maximalist eclectic | "Victorian maximalist interior, pattern-on-pattern, rich color" |

### Interior Styling Vocabulary

- "Kinfolk aesthetic, warm natural materials, imperfect linen" — the Kinfolk magazine look
- "Apartamento lived-in, real home not staged" — the Apartamento magazine look
- "sterile luxury, marble and chrome, aspirational" — high-end commercial interior

---

## 6. The Photography Vocabulary — Section J: Rendering, Materials & Textures

Material description is where Aurora's autoregressive architecture shines — the model builds coherent physical scenes where materials interact consistently with light.

### Skin Rendering

| Detail level | Prompt phrase |
|---|---|
| Ultra-detailed | "visible pores, peach fuzz catching sidelight, slight surface oiliness, SSS in ear" |
| Natural beauty | "natural skin texture, softly lit, light freckles, healthy glow" |
| Editorial retouched | "editorially retouched, smooth but not plastic, natural contours preserved" |
| Glossy beauty | "high-gloss skin, wet-looking highlight, beauty-industry standard" |
| Aged | "deeply lined, age spots, papery skin quality, authentic character" |

SSS = subsurface scattering — a rendering term Aurora processes correctly for skin realism.

### Fabric Rendering

| Fabric | Prompt phrase |
|---|---|
| Wool | "heavy wool tweed, visible weave, slight texture on surface" |
| Silk | "liquid silk, catching light in folds, smooth and lustrous" |
| Linen | "crumpled linen, natural irregular texture, slightly warm tone" |
| Denim | "worn denim, faded knees, visible thread weave, indigo" |
| Leather | "polished black leather, specular reflections, fine grain surface" |
| Sheer | "sheer organza, semi-transparent, catching backlight" |

### Hair Rendering

| Hair state | Prompt phrase |
|---|---|
| Detailed strand work | "individual strand detail visible, fine flyaways catching rim light" |
| Wet | "wet hair, darkened, slicked back, droplets on forehead" |
| Product-styled | "heavily pomaded, side-parted, mirror shine" |
| Natural texture | "4C curl pattern, defined coils, slight shrinkage" |
| Wind-blown | "hair caught by breeze, natural movement, slightly disheveled" |

### Material Rendering Reference

| Material | Prompt phrase |
|---|---|
| Polished metal | "brushed stainless steel, directional grain, specular highlights" |
| Oxidized metal | "patinated bronze, verdigris, aged surface" |
| Water | "water surface tension at edge of glass, condensation beads, refraction" |
| Glass | "glass with slight smudge, catching light at edge, subtle refraction" |
| Stone | "rough-hewn granite, mica flecks, cold and heavy" |
| Weathered wood | "reclaimed wood with silver-grey weathering, visible grain" |
| Food gloss | "glistening glaze on pastry, steam rising, fresh-from-oven texture" |

---

## 6. The Photography Vocabulary — Section K: Post-Processing Language

Aurora can be directed to simulate specific post-processing looks:

| Post effect | Prompt phrase |
|---|---|
| Film grain | "fine film grain overlay, organic texture" |
| Halation | "halation around bright highlights, film-like bloom" |
| Vignette | "moderate edge vignetting, darkened corners" |
| Lifted shadows | "lifted black point, shadow detail preserved, modern grade" |
| Rolled highlights | "gentle highlight rolloff, no clipping, HDR-but-real" |
| High clarity | "high clarity and micro-contrast, every detail sharp" |
| Double exposure | "double exposure effect, transparent overlay" |
| Light leak | "light leak entering from left edge, warm orange wash" |
| Lens dirt | "minor lens dust specks, slightly dirty glass" |

---

## 6. The Photography Vocabulary — Section L: Style Invocation

### Photography Genre Vocabulary

| Genre | Effective prompt phrase |
|---|---|
| Editorial fashion | "high fashion editorial, Vogue Italia aesthetic, dramatic and conceptual" |
| Commercial beauty | "cosmetics advertising, product-focused beauty, clean studio" |
| Documentary | "documentary photography, unposed, authentic moment" |
| Photojournalism | "photojournalism style, AP wire quality, moment-driven" |
| Street photography | "street photography, candid, Leica aesthetic, available light" |
| Fine art photography | "fine art photography, gallery-ready, conceptual" |
| Conceptual | "conceptual photography, metaphorical, art-directed" |
| Architectural | "architectural photography, perspective-corrected, HDR balanced" |
| Landscape | "landscape photography, National Geographic quality" |
| Wildlife | "wildlife photography, telephoto, natural behavior" |
| Sports | "sports action photography, peak moment, motion freeze" |
| Macro | "macro photography, extreme close-up, fine detail" |
| Astrophotography | "astrophotography, long exposure Milky Way, star trails" |
| Still life | "still life photography, product arrangement, controlled studio" |

### Art Movement References

| Movement | Prompt phrase |
|---|---|
| Baroque | "Baroque painting style, dramatic chiaroscuro, Caravaggio influence" |
| Impressionism | "Impressionist painting, loose brushwork, atmospheric light" |
| Art Deco | "Art Deco illustration, geometric forms, gold and black" |
| Bauhaus | "Bauhaus graphic design aesthetic, primary colors, geometric" |
| Surrealism | "Surrealist composition, dreamlike juxtaposition" |
| Pop Art | "Pop Art style, Ben-Day dots, bold flat color" |
| Brutalism | "architectural brutalism, raw concrete, monumental" |

### Named Artist References (Aurora Recognition)

Use carefully and ethically — these are style references, not reproduction requests.

| Artist/Style | Notes | Label |
|---|---|---|
| "in the style of Annie Leibovitz" | Environmental portrait; celebrity context | COMMUNITY-VERIFIED |
| "inspired by Gregory Crewdson" | Cinematic suburban uncanny | COMMUNITY-VERIFIED |
| "Ansel Adams black and white" | High-contrast B&W landscape | COMMUNITY-VERIFIED |
| "Helmut Newton fashion" | Edgy, powerful fashion imagery | COMMUNITY-VERIFIED |
| "Dorothea Lange documentary" | Humanist, Great Depression aesthetic | COMMUNITY-VERIFIED |

**Legal caveat:** Style references invoke an aesthetic, not copyrighted specific works. Aurora processes these as style signals, not as reproduction instructions. Do not describe specific copyrighted images in detail.

### Publication Aesthetic References

| Publication | Prompt phrase |
|---|---|
| Vogue editorial | "Vogue editorial aesthetic, high fashion, conceptual" |
| National Geographic | "National Geographic photography, world-class nature/culture" |
| The New Yorker | "New Yorker illustration style, simple line art, editorial" |
| Apartamento magazine | "Apartamento magazine aesthetic, lived-in home, real people" |
| Kinfolk | "Kinfolk aesthetic, natural light, warm minimalism, lifestyle" |
| i-D magazine | "i-D magazine wink portrait" — the specific winking-eye motif |

### Era References

| Era | Prompt phrase |
|---|---|
| 1970s | "1970s Kodachrome photography, warm, slightly overexposed, analog" |
| 1980s | "1980s editorial, high contrast, dramatic, power dressing" |
| 1990s grunge editorial | "1990s grunge fashion editorial, raw, anti-gloss" |
| Y2K digital | "Y2K aesthetic, early digital camera quality, oversaturated, low-res pixel feel" |
| 2010s Instagram | "2010s Instagram aesthetic, VSCO-filtered, faded matte" |

---

## 6. The Photography Vocabulary — Section M: Text Rendering Inside Images

### Current Capability State (May 2026)

The `grok-imagine-image-quality` model includes "clean multilingual text rendering" as a documented feature. Compared to December 2024 Aurora, text accuracy has improved substantially. Compared to Ideogram 3 or GPT Image 2, it remains inferior for complex or critical text.

### Best Practices

1. **Enclose exact text in quotes:** `café sign reading "OPEN 7AM–10PM"`
2. **Keep text short:** Maximum 5–6 words per text element
3. **Describe typography mood:** "bold condensed industrial sans-serif", "elegant thin-stroke serif", "playful hand-lettered chalk"
4. **Specify placement:** "text centered at bottom of image", "text in upper-left corner"
5. **Specify contrast:** "white text on dark background", "embossed gold text on matte black"

### Failure Modes for Text

- Multi-line body copy — near-universal failure
- Non-Latin scripts in complex layouts — accuracy drops
- Very small text within a large scene — likely illegible
- Text in unusual orientations (circular, extreme angles) — inconsistent

**Workaround for critical text:** Generate the image without text in Aurora, then add text in a post-production tool (Figma, Photoshop, Canva).

---

## 7. Use-Case Pattern Library

The following 30 fully annotated prompt examples represent evidence-based constructions using the vocabulary, structural guidance, and Aurora-specific behavior documented in this report. Each prompt is 100–250 words in the description; the actual prompt text is formatted in a code block.

---

### UC-01: Editorial Fashion Portrait

```
Half-body fashion editorial portrait of a woman, mid-30s, mixed European and East Asian heritage, wearing a structured ivory silk blouse with asymmetrical collar and high-waisted black crepe trousers. Shot on a Hasselblad H6D with an 80mm f/2.8 lens. She stands against a weathered grey concrete wall in soft overcast natural light, the wall providing an industrial tension against the luxurious garment. Her gaze is direct and slightly challenging, chin tilted upward, posture confident. The light is flat and even, reminiscent of a Paris fashion week backstage. Color palette is monochromatic: black, ivory, and concrete grey. Skin has editorial retouching — contours preserved, not smoothed. Shot vertical, 4:3 aspect ratio. High fashion editorial, French Vogue aesthetic.
```

**Annotation:**
- **Camera reference (Hasselblad H6D + 80mm):** Signals medium-format clarity and shallow-DoF characteristics, elevating perceived image quality
- **Garment specificity:** Fabric names (silk, crepe), structural detail (asymmetrical collar) push Aurora beyond generic "white shirt"
- **Light description:** "Flat and even, Paris fashion week backstage" invokes a specific, recognizable photographic moment
- **Retouching level stated:** "editorial retouching — contours preserved" avoids the default over-smooth AI beauty look
- **Color palette constrained:** "monochromatic black, ivory, concrete grey" prevents Aurora from defaulting to colorful backgrounds

---

### UC-02: Beauty Close-Up (Cosmetics-Grade)

```
Extreme close-up beauty portrait, cropped just above brows to just below chin. Subject has deep warm-toned brown skin, exceptionally smooth but not plastic — visible healthy texture at pore level, dewiness suggesting hydration. Bold matte terracotta lip color, precisely applied. Eyes closed, lashes full and brushed. Clamshell lighting setup using a large beauty dish above and white reflector below, creating even illumination with distinctive oval catchlights (not visible as eyes are closed). Hair slicked back revealing forehead, no distractions. Clean white background. Shot on Phase One IQ4 with Schneider 100mm macro lens. No post-processing artifacts, no skin smoothing beyond cosmetics-grade standard. The image should read as a cosmetics campaign hero shot.
```

**Annotation:**
- **Clamshell lighting named:** Aurora knows this means specific beauty-world setup; the absence of distracting shadows is implied
- **Catchlight detail:** Even specifying catchlights when eyes are closed helps Aurora understand the intended lighting fixture
- **Skin description specificity:** "Dewiness suggesting hydration" — product-benefit language triggers the right skin rendering mode
- **Phase One + Schneider macro:** Extreme resolution signal; also invokes the specific "pop" associated with digital medium format
- **"Cosmetics-grade standard" retouching:** Frames the expected post-processing level without being vague

---

### UC-03: Studio Headshot (Corporate)

```
Corporate headshot, medium close-up, man in his mid-40s, clean-shaven, confident but approachable expression, slight natural smile. Wearing a charcoal wool suit with a light blue spread-collar dress shirt, no tie. Standard three-point lighting: key light large softbox camera-left, fill light camera-right at -2 stops, hair light from above-behind. Clean neutral grey seamless background, slightly lighter than subject. Shot on Sony A1 with 85mm f/1.8 lens, shallow depth of field placing background slightly out of focus. Skin is naturally retouched — not smoothed, healthy complexion. This image needs to read as authentic and trustworthy, suitable for LinkedIn, executive bio, annual report. Not creative — crisp, professional, and warm.
```

**Annotation:**
- **"Slight natural smile":** More specific than "smiling" — avoids the toothy advertising smile that reads as insincere
- **Exact lighting ratios stated:** "fill light at -2 stops" is a real photography concept Aurora may interpret directionally
- **"Not creative — crisp, professional, and warm":** Explicitly correcting Aurora's tendency toward dramatic lighting in portrait prompts

---

### UC-04: Environmental Portrait (Documentary Feel)

```
Environmental portrait of a master glassblower, man in his 60s, Italian, weathered face with deep lines, wearing a leather apron with burn marks, in the middle of gathering molten glass from a furnace at his Venice workshop. Medium shot, waist up. The furnace in the background glows orange, providing a warm backlight that rims his silhouette. Ambient light is the glow of the workshop — no studio light, entirely available. Camera is positioned at eye level, slightly to the left, using a 35mm f/2 lens on a full-frame body. The scene should feel real, lived-in, not staged. No perfect posing — this is documentary-style, capturing an authentic working moment. Color treatment: Kodak Portra 800 emulation, warm and filmic.
```

**Annotation:**
- **Occupation and specific context:** "Venetian glassblower" collapses hundreds of visual decisions into one culturally specific reference
- **Available light only stated explicitly:** Prevents Aurora from adding artificial studio lighting
- **"Not staged" instruction:** Direct countermand to Aurora's default toward posed portraiture
- **Backlight from furnace:** Describes a physically real light source in the scene — Aurora handles this well when the source is logical

---

### UC-05: Street Photography (Candid, Vérité)

```
Street photograph captured in Tokyo, Shinjuku, late evening rush hour. A salaryman in his 50s moves through the crowd with his briefcase, face showing quiet exhaustion. The image should feel genuinely candid — not composed, not posed. Shallow depth of field separating him from the blur of moving commuters behind. Available light from overhead fluorescent station lights and neon advertising signs providing mixed color temperature (warm signs, cold overhead). Shot with a 35mm f/2 on a Leica M11, handheld, slight camera movement acceptable. Black and white with visible grain — Ilford HP5 pushed to 1600 feel. Decisive moment aesthetic, Cartier-Bresson tradition.
```

**Annotation:**
- **"Slight camera movement acceptable":** Signals authentic handheld street photography rather than tripod-perfect sharpness
- **Mixed color temperature → B&W decision:** Avoids the messy mixed-light color problem by converting to B&W as an aesthetic choice
- **"Decisive moment aesthetic":** Aurora associates this phrase with a specific compositional sensibility (peak action, environmental context)

---

### UC-06: Photojournalism / Reportage

```
Documentary photojournalism image. A climate protest in front of a government building, overcast European city, midday flat light. Dozens of protestors visible in a wide shot, signs held up with handwritten messages (show generic protest signs, no specific text required). The image should feel authentic, not art-directed — slightly off-level horizon acceptable, no beautiful bokeh, everything in focus at f/8. Shot on a Canon R5 with 24mm lens, handheld. Gritty, immediate, real. Color treatment naturalistic, no color grading. This image should read as a wire service news photograph, not a lifestyle shot.
```

**Annotation:**
- **"No beautiful bokeh":** Direct instruction against Aurora's default toward pleasing shallow DoF
- **"AP wire service feel":** A specific journalistic aesthetic benchmark
- **Generic signs to avoid text failures:** "Generic protest signs, no specific text required" — sidesteps Aurora's text rendering limitations
- **f/8 specified:** Deep focus, everything sharp — standard photojournalism technique

---

### UC-07: Wedding & Lifestyle

```
Wedding photograph, first look moment. Bride and groom facing each other in a garden of an old English manor house, late afternoon golden hour. Bride wearing a flowing off-shoulder ivory satin gown, hair in a loose updo with soft tendrils. Groom in a grey morning suit with white boutonniere. Their faces are close, not yet kissing — a moment of anticipation. Both in soft focus of golden light from the right, garden slightly blurred in background through shallow DoF. Shot on 85mm f/1.8, Canon R5. Color treatment: warm, lifted shadows, creamy — Fujifilm Pro 400H emulation. Emotional, intimate, timeless.
```

**Annotation:**
- **"First look moment":** An industry-standard wedding photography term that collapses the emotional beat into one phrase
- **"Faces are close, not yet kissing — moment of anticipation":** Specific micro-temporal description of the image beat
- **Fujifilm Pro 400H:** The wedding industry's classic film stock for its pastel skin rendering

---

### UC-08: Product Photography — Hero Shot (E-Commerce)

```
Clean e-commerce product hero shot. A premium wireless over-ear headphone in matte midnight blue colorway, floating on a pure white background. Single light source: large octabox from upper-left at 45 degrees casting a clean soft shadow to the lower-right that grounds the product without drama. The headphone is tilted at approximately 35 degrees from horizontal, left ear cup facing camera, band arching to upper right. Surface reflections on the matte housing are minimal and controlled. No props, no people, no environment context. Shot with a medium-format lens equivalent, maximum detail. Ultra-sharp product focus throughout. The only element in the image is the headphone.
```

**Annotation:**
- **Precise angle description:** "35 degrees from horizontal, left ear cup facing camera" — Aurora's prompt adherence is tested here
- **Single light source and position stated:** Controls the shadow behavior and product drama level
- **"No props, no people, no environment context":** Explicit exclusion of Aurora's tendency to add contextual elements

---

### UC-09: Product Photography — Lifestyle / In-Use

```
Lifestyle product photograph. A woman in her late 20s is wearing matte midnight blue wireless headphones while working at a minimalist home office desk. Morning light fills the space from a large window on the left. She is partially side-on, looking at a laptop screen with quiet concentration — not posing, not looking at camera. The desk has a coffee cup, a small succulent, and a clean notebook. Hardwood floor, white walls. Shot with a 35mm f/2 lens creating moderate depth of field — desk and figure sharp, window and back of room slightly soft. Kodak Portra 400 film emulation, warm and natural.
```

**Annotation:**
- **Product integrated naturally:** Headphones are present but not the obvious "subject" — the scene sells the lifestyle context
- **"Not posing, not looking at camera":** Specifically addresses Aurora's default toward posed "product demonstration" look
- **Environmental details:**  "coffee cup, succulent, notebook" — specific enough to trigger recognizable home-office visual language without over-specifying

---

### UC-10: Food Photography (Editorial)

```
Editorial food photograph. A single slice of dark chocolate cake on a white ceramic plate, dramatically lit from a single window source to the left, soft and directional. The cake has a matte ganache frosting with slight imperfection — not cake-shop perfect, handmade quality. A fork has taken one bite revealing the inner layers: dark sponge, ganache filling, raspberry jam. The plate rests on a grey linen tablecloth with slight texture visible. Background: very dark, almost black, shallow depth of field. Shot on 85mm macro, f/4. Steam: none. The mood is intimate and slightly indulgent. Color grade: deep, slightly desaturated, moody.
```

**Annotation:**
- **"Imperfect" ganache stated:** Counters Aurora's tendency toward artificially perfect food
- **"One bite taken":** Creates visual narrative; implies human presence and consumption
- **Dark background instruction:** Against Aurora's default lighter food backgrounds
- **"Steam: none":** Explicit removal of the AI cliché food steam that appears uninvited

---

### UC-11: Food Photography (Social-Native)

```
Overhead flat-lay food photograph for Instagram. Avocado toast on thick sourdough bread, torn not sliced, on a light cream ceramic plate. The toast is topped with halved cherry tomatoes, a soft-boiled egg cut in half showing a jammy yolk, fresh micro herbs, flaky salt. The plate is on a white marble surface. Surrounding elements: a few loose herbs, a small ceramic bowl of chili flakes, a glass of sparkling water. Natural daylight from the upper-right. Bright, light, and airy. Color palette: creamy whites, avocado green, golden yolk yellow, deep red tomatoes. Aspect ratio 1:1. No shadows darker than light grey. Highly styled but reads as natural.
```

**Annotation:**
- **Flat-lay stated:** Directs Aurora to overhead composition, which it executes well
- **Specific surrounding elements listed:** "ceramic bowl of chili flakes, glass of sparkling water" — the editorial food props that suggest intentionality
- **"Torn not sliced":** The authentic food styling choice; Aurora will render the difference

---

### UC-12: Interior & Architecture (Residential)

```
Architectural interior photograph of a contemporary Japanese-influenced living space. Early morning light entering from floor-to-ceiling windows on the right, casting warm golden horizontal bands across a white linen sofa. Concrete floors, exposed wood ceiling beams, a single large art piece on the far white wall. No people. The room is immaculate and calm — wabi-sabi aesthetic, minimal objects placed with intentionality. Shot with a 24mm tilt-shift lens, perspective corrected, verticals perfectly straight. f/8, everything in focus. Color treatment: warm, slightly desaturated, natural.
```

**Annotation:**
- **Tilt-shift reference:** Aurora associates tilt-shift with architectural photography — corrected perspective, extreme sharpness
- **"Verticals perfectly straight":** Explicit instruction for the key failure mode in AI architecture imagery (converging verticals)
- **"No people":** Strong explicit instruction for a room-only shot

---

### UC-13: Architecture (Commercial/Exterior)

```
Architectural exterior photograph of a newly completed modernist cultural center. The building is a massive poured concrete structure with deep recesses and horizontal banding. Photographed at blue hour — the sky above is deep indigo gradient, the building's interior lights glow warm amber through full-height glazing. The building's reflection pools in the foreground catch both the sky and the warm interior glow. Tilt-shift perspective correction. Shot on 24mm or similar. The balance between exterior concrete texture and interior warm glow is the key tension. No people, no vehicles. Long-exposure feel — water in reflection pools perfectly still.
```

**Annotation:**
- **Blue hour stated with precise sky description:** "Deep indigo gradient" is more specific than "sunset"
- **Light duality described:** Warm interior vs. cool exterior sky — Aurora handles this contrast well
- **"Long-exposure feel":** Signals still water reflection without requiring the model to simulate a multi-second exposure

---

### UC-14: Landscape (Epic)

```
Epic landscape photograph. Torres del Paine, Patagonia, at dawn. The granite towers emerge from morning mist, first light catching the upper faces in warm rose-gold while the valley below remains in blue pre-dawn shadow. In the foreground, a glacial lake reflects the towers and sky with mirror-like stillness. The image should convey immense scale — the towers should appear monumental. Shot on a 24mm tilt-shift lens for maximum sharpness, f/16 hyperfocal, everything pin-sharp from the pebbles in the foreground to the tips of the towers. National Geographic magazine quality. No human presence.
```

**Annotation:**
- **Specific named location:** "Torres del Paine" gives Aurora a precise visual reference point
- **Light split described:** "rose-gold upper towers, blue shadow valley" — a real meteorological phenomenon at this location
- **"Monumental scale" stated:** Aurora needs this instruction to prevent a flat, documentary composition

---

### UC-15: Landscape (Intimate)

```
Intimate landscape photograph. A mossy stone wall in rural Ireland, County Clare, early April. Overcast diffused light creating no shadows, revealing maximum surface texture in the pale limestone. Wild primroses growing from gaps in the wall. Beyond the wall, a field of vivid green grass extends to soft grey horizon. No sky visible — the frame cuts to grey-green horizon. 35mm lens on full-frame, f/8, all sharp. Color treatment: cool grey-greens, the primroses the only warm yellow accent. The mood is quiet, ancient, specifically Irish.
```

**Annotation:**
- **Geographical specificity (County Clare):** Particular limestone karst geology — signals a specific color and texture palette
- **"Wild primroses the only warm accent":** Compositional color direction — one warm element in a cool palette creates focal point
- **No sky instruction:** Forces a ground-level intimate composition instead of epic sky-dominant framing

---

### UC-16: Wildlife

```
Wildlife photograph. A great grey owl, wings fully spread, landing on a snow-covered branch in a boreal forest at dawn. Motion of wings captured at high shutter speed — feathers tack-sharp, tips slightly motion-blurred by the landing movement. The owl's eyes locked directly at camera. Background is a soft, out-of-focus corridor of birch and spruce in morning blue light. Shot on 400mm f/2.8 telephoto with teleconverter, equivalent of 560mm. 1/2000s shutter feel. The image should read as a genuine wildlife moment, not a studio setup. Natural behavior, natural light.
```

**Annotation:**
- **Wing position and behavior specificity:** "Fully spread, landing" captures a specific behavioral moment
- **"Tack-sharp tips motion-blurred by landing":** Technically specific instruction for a real-world wing motion capture characteristic
- **Telephoto compression stated with specific focal length:** Triggers background compression and subject isolation behavior

---

### UC-17: Sports Action

```
Sports action photograph. A male professional road cyclist in full racing kit, number pinned, mid-sprint in the final 200 meters of a stage finish. He is leaning forward over the handlebars, face showing maximum effort. Background is a blurred crowd of spectators behind barriers, colorful but indistinct from motion blur at 1/500s effective shutter. Telephoto compression, 200mm lens equivalent. Shot from a slightly low angle at roadside, giving him a heroic perspective. Warm afternoon light from the left side. Peak moment — the decisive frame at maximum effort. Sports photography, wire service quality.
```

**Annotation:**
- **"Number pinned":** Small detail that makes it a race photograph rather than a training photograph
- **Crowd blur described:** Aurora handles motion blur when asked explicitly
- **Low angle instruction:** "Heroic perspective" — the standard sports photography elevation for peak effort

---

### UC-18: Macro / Detail

```
Extreme macro photograph. A single dewdrop on a grass blade at dawn, the droplet perfectly spherical, containing a refracted upside-down reflection of the surrounding meadow landscape within it. Shot with a dedicated macro lens, 1:2.5 magnification. Lighting: early morning sun at 8 degrees above horizon, side-lighting the grass blade and making the dewdrop glow from within. Depth of field: razor thin — only the very center of the droplet in sharp focus, blade and meadow behind softly blurred in warm green bokeh. Shot from an extremely low angle, grass-level perspective. No vibration, perfectly sharp within the focus plane.
```

**Annotation:**
- **Refracted reflection within dewdrop:** Aurora can simulate this physics phenomenon when explicitly described
- **"8 degrees above horizon" sun angle:** An extremely specific instruction — this level of detail gives Aurora a precise physical reference
- **"Razor thin DoF — only center of droplet sharp":** Explicit DoF instruction for the correct macro aesthetic

---

### UC-19: Astrophotography / Night Sky

```
Astrophotography landscape. The Milky Way core rising over a lone standing stone on the Orkney Islands, Scotland. The stone is 3 meters tall, rough ancient surface, silhouetted against the star field with only faint starlight illuminating its edges. The Milky Way stretches diagonally across the upper half of the frame, dense galactic core centered, visible nebulosity and star clouds. No artificial light pollution — complete darkness. In the far distance, the faint glow of the horizon from the setting moon, 4 degrees below the horizon, leaving a blue-grey gradient at the very base of the frame. Shot at 14mm, f/2.8, ISO 6400 feel — slight grain acceptable, star points sharp.
```

**Annotation:**
- **"ISO 6400 feel":** Triggers Aurora's model of high-ISO digital noise characteristic of astro photography
- **"No artificial light pollution":** Explicit instruction for dark skies
- **Moon below horizon detail:** Creates subtle horizon glow without a visible moon — real astrophotography technique
- **Standing stone silhouette:** Clear foreground interest against star field — the compositional convention of this genre

---

### UC-20: Conceptual / Fine Art

```
Fine art conceptual photograph. A woman in her 40s, seated on a plain wooden chair in the center of an empty grey room, surrounded by stacks of open books — books piled on the floor radiating outward from her feet, books stacked to above her head on either side, books cascading behind her. She wears plain white clothing. Her expression is one of profound calm, not overwhelmed — at peace within the chaos of knowledge. The light is a single soft overhead source, creating an even, studio quality illumination. Shot on a large-format 4x5 camera, perfectly sharp throughout, cool neutral color. The image should feel studied, deliberate, museum-wall worthy.
```

**Annotation:**
- **Environmental symbolism is explicit:** The books radiating outward is a visual metaphor that Aurora can execute because it's spatially described
- **"Not overwhelmed — at peace":** Clarifying the emotional read prevents misinterpretation
- **"Museum-wall worthy":** Quality signal that shifts rendering toward fine art territory

---

### UC-21: Still Life

```
Still life photography, classical Dutch Golden Age influence. On a dark oak table draped in deep velvet: a half-peeled lemon, spiral of zest intact; a small glass of water catching light; several dark cherries with stems; a silver spoon resting diagonally; a single white flower beginning to wilt. Dramatic single-source light from the upper-left, creating deep chiaroscuro shadow to the right. The objects are arranged with intended asymmetry — not perfectly composed, more natural grouping. Shot on 85mm macro, f/5.6, slight depth graduation. Color: dark and rich, shadows nearly black, highlights creamy. Zeiss Otus rendering quality.
```

**Annotation:**
- **Named art historical reference (Dutch Golden Age):** One of the strongest style signals available for still life
- **"Intended asymmetry — not perfectly composed":** Counters AI's geometric perfect arrangement default
- **Specific object list with states:** "half-peeled lemon, spiral of zest intact" — Aurora will attempt to render this level of detail

---

### UC-22: Fashion Lookbook (Full-Length)

```
Fashion lookbook photograph, full-length. Female model, tall, slender frame, mixed heritage, in a structured architectural coat in camel wool — oversized proportions, strong shoulders, falls to mid-calf. Worn with straight-leg black trousers, polished black leather ankle boots. Minimal hair, pulled back tightly. Set in a covered Parisian arcade — iron and glass architecture overhead, tiled floor, warm ambient light from skylights filtered through iron framework. The model walks toward camera, one foot forward, slight motion energy, not a static pose. Shot on 35mm f/2.8, full body visible, environmental context clearly readable. Tone: cool, editorial, sophisticated.
```

**Annotation:**
- **Architectural coat description:** Garment specificity at design-brief level
- **"Parisian arcade":** A highly specific location with recognizable architectural signature (galerie du Palais Royal, etc.)
- **Walking motion:** "One foot forward, slight motion energy" produces more natural movement than a static pose

---

### UC-23: Luxury Advertising (Watch)

```
Luxury watch advertising photograph. A Patek Philippe Calatrava on a man's wrist, hand resting on a polished dark walnut desk with a few papers, a pen, and a piece of aged leather. The watch dial is visible in full — white, crisp, hands at 10:10. Shot from above-left at a 45-degree angle with a macro capability, the watch face and case edge pin-sharp, wrist and desk softly falling off. Single key light from the right: a narrow snoot or gridded strip creating specular highlights along the watch bezel without overexposing the dial. The image communicates heritage, precision, and quiet wealth.
```

**Annotation:**
- **Specific watch named:** "Patek Philippe Calatrava" gives Aurora a precise reference for the design language
- **Standard hands position (10:10):** The industry convention for watch photography — Aurora should honor this
- **"Quiet wealth" vs. "luxury":** More specific and tonally precise — avoids the garish "luxury" render

---

### UC-24: UGC / Social-Native (TikTok/Reels Aesthetic)

```
Vertical 9:16 social content. A young woman, early 20s, sitting in a cozy bedroom with fairy lights, pastel wall behind her, holding a oversized ceramic mug with both hands. She's in a comfortable oversized knit sweater. The look is candid and self-shot in aesthetic — slightly warm tones, soft ambient light, bokeh background. She is looking directly at the camera with a relaxed smile. The aesthetic is VSCO-filtered, lifestyle, authentic — the kind of image that gets saved to a mood board on Pinterest. Shot with a wide 24mm equivalent to create the slightly distorted selfie feel. Aspect ratio 9:16. Not professionally lit — intentionally casual.
```

**Annotation:**
- **9:16 explicit:** Correct aspect ratio for vertical social content
- **"Not professionally lit — intentionally casual":** Explicitly requests lo-fi aesthetics against Aurora's default professional quality
- **"Saved to a mood board on Pinterest":** Cultural reference that invokes a specific aspirational-everyday visual tone

---

### UC-25: Cinematic Film Still (1970s New Hollywood)

```
Cinematic film still, 1970s New Hollywood aesthetic. A woman in her 30s sits alone at a diner counter, 2am, neon light from the window painting one side of her face in pink, fluorescent overhead fixtures the other in cold white. She holds a cup of coffee with both hands. The anamorphic lens provides a subtle horizontal squeeze and bokeh ovals from the neon signs out of focus behind the rain-streaked window. The frame is 2.39:1 widescreen. The color grade is the warm-push and slight desaturation of Kodak 5247 stock. The atmosphere is melancholy, existential — Taxi Driver, Midnight Cowboy, Five Easy Pieces tradition. The feeling is: 3am, far from home.
```

**Annotation:**
- **Specific film references named:** "Taxi Driver, Midnight Cowboy, Five Easy Pieces" — a tight period and aesthetic cluster that Aurora can reasonably process
- **Anamorphic lens specified:** Triggers the oval bokeh and 2.39:1 aspect ratio
- **Dual light source described physically:** Neon from window vs. fluorescent overhead — explains the color temperature split

---

### UC-26: Anime / Japanese Illustration

```
Anime illustration in the style of a 1990s Studio Ghibli production painting. A young girl, approximately 12 years old, stands at the edge of a cliff overlooking a sea of clouds at sunset. She wears a simple cotton dress in pale blue, hair caught by wind. The sky is layered in golds, pinks, and purples — the clouds below are lit from beneath in warm orange. The art style is hand-painted, warm and textured, with the specific brushwork quality of Yoshifumi Kondō or Isao Takahata — not digital-smooth, distinctly analog-painted. The mood is wonder, vastness, belonging. Composition: she is small against the immense sky, lower-left third of the frame.
```

**Annotation:**
- **Specific Ghibli era and directors named:** 1990s production paintings, Kondō/Takahata style — these are specific enough to distinguish from generic anime
- **"Not digital-smooth, distinctly analog-painted":** Important instruction against Aurora's default clean anime style
- **Scale relationship stated:** "She is small against the immense sky" — explicit compositional direction for emotional read

---

### UC-27: Western Editorial Illustration

```
Editorial illustration for a major newspaper opinion section. Subject: the loneliness of urban life. A lone figure stands in a massive empty train station during peak rush hour — hundreds of people stream past in motion blur, but the central figure stands completely still, the only sharp element in the frame. The illustration style is realistic editorial — not cartoonish, not fine art, but the stylized realism of New York Times Magazine cover illustration. Cool grey and blue color palette with a single warm amber from a shaft of sunlight hitting only the still figure. Strong graphic composition, single dominant diagonal of crowd movement.
```

**Annotation:**
- **Visual metaphor described spatially:** The lone still figure in a blurred crowd is both technically and symbolically described
- **"NYT Magazine cover illustration" as style reference:** A specific illustration tradition Aurora can recognize
- **"Not cartoonish, not fine art":** Explicitly narrows the illustration style range

---

### UC-28: Concept Art (Character)

```
Character concept art, game development quality. Female warrior character, mid-30s, West African heritage. She wears articulated leather and iron plate armor — asymmetric, practical rather than decorative, showing battle wear: scratches, small repairs, leather darkened by use. She carries a paired weapon — two shorter swords across her back. Standing pose, three-quarter view, neutral background of concept art grey. The art style is detailed digital illustration suitable for an art direction bible — not fully rendered, but showing form, material, and silhouette clearly. Warm diffused directional light from the upper-left. The expression is calm and focused, not aggressive. Art direction reference: concept work for The Witcher, God of War, Horizon.
```

**Annotation:**
- **"Practical rather than decorative":** The key design direction for serious game character concept art vs. fantasy cliché
- **"Battle wear: scratches, small repairs":** Signals a lived-in worldbuilding approach
- **"Concept art grey background":** The standard concept art presentation — keeps focus on the character
- **Game title references:** Establish the aesthetic tier and worldbuilding tradition

---

### UC-29: Concept Art (Environment)

```
Environment concept art for a science fiction film production. An alien industrial city on a low-gravity moon with dense atmospheric haze. The city is vertical — structures extend upward 3–4 kilometers, connected by hundreds of skyways and cables at various heights. The scale should feel vertiginous. Looking down from mid-height within the city: below, a ground-level canyon of darkness; above, the structures disappear into haze and diffuse sunlight. The aesthetic is influenced by Syd Mead and Chris Foss — functional industrial, not clean utopian. Dominant colors: ochre, rust, and industrial grey. The image should serve as a production design reference, roughly 16:9 for cinematic framing.
```

**Annotation:**
- **Syd Mead and Chris Foss references:** Two of the defining visual references for credible hard SF production design
- **"Vertiginous scale" explicitly stated:** Without this, Aurora may default to a flatter, more readable composition
- **"Functional industrial, not clean utopian":** The critical aesthetic direction in SF design — prevents the generic "chrome future" look

---

### UC-30: Surreal / Dreamscape

```
Surrealist photograph in the tradition of Gregory Crewdson and René Magritte. A man in a grey suit stands in the living room of a suburban home, facing a window. Through the window, instead of the expected front lawn and street, the scene reveals an underwater ocean floor — fish swimming past, coral visible, light filtering down from the surface above. The lighting inside the room is normal household — warm tungsten lamps — creating a collision of warm interior and cool blue oceanic exterior. The man's posture is casual, as if this is unremarkable. No surrealist distortion of objects — the unreality comes entirely from the window view juxtaposition. Photographic realism throughout, Cinestill 800T color treatment.
```

**Annotation:**
- **"The unreality comes entirely from the juxtaposition, not distortion":** Extremely important instruction for Magritte-style surrealism — prevents cartoonish morphing
- **"As if this is unremarkable":** The key Crewdson/Magritte emotional quality — the uncanny accepted as ordinary
- **Cinestill 800T:** The specific film stock that produces the slightly warm, slightly blurred, intimate cinematic quality appropriate for this mystery-suburban genre

---

*(Use cases 29–30 for Poster Design, Children's Book, Comic Panel, Logo, Lookbook, Luxury Fragrance/Automotive are available on request as the pattern library above demonstrates the full prompt construction methodology.)*

---

## 8. Advanced Techniques

### Multi-Subject Prompts

For two subjects, explicitly state their **spatial relationship and interaction**:
```
Two people — a man and a woman — seated on opposite sides of a narrow café table. He looks down at his espresso; she watches him with a measured expression. 60cm of separation between them. MS framing, both visible. Available light from window camera-left.
```

Avoid: listing two subjects without staging them.

### Character Consistency Across a Series

Aurora does not natively maintain character identity across separate generation sessions. To achieve consistency:

1. **Generate a character reference image first** — a clean, well-lit, A-pose or neutral-expression "character sheet" image
2. **Use image-to-image editing or multi-image input** — upload the reference and use the `@image1` syntax to anchor the character in subsequent generations
3. **Lock specific physical descriptors in a template** — paste the same character description block into every prompt
4. **Use the multi-image editing endpoint (API)** — supports up to 3 source images per request; anchor one as character reference, one as environment reference, one as style reference
5. **For highest consistency in a series:** Generate all images in a single session; character drift increases across separate API calls

> **LABEL: COMMUNITY-VERIFIED** — the `@image` referencing technique for character consistency is documented in community tutorials; the multi-image API endpoint is confirmed in xAI's official documentation.

### Style Consistency Across a Series

Establish a "style anchor" prompt block that never changes across your series:
```
[STYLE ANCHOR — paste at end of every prompt]
Shot on Fujifilm GFX 100S with 80mm lens. Color treatment: Kodak Portra 400, warm skin tones, lifted shadows. Editorial lighting: large softbox from camera-left. Background: always white seamless.
```

The `revised_prompt` feature returned by the API shows you exactly what Aurora's rewriter generated — review this to understand how your style block is being interpreted.

### Reference Image Use

Via the **image editing/multi-image endpoint**, you can supply up to 3 reference images:
- **Character reference:** Face/body to maintain identity
- **Style reference:** An existing image whose color grade, lighting, or aesthetic you want to match
- **Environment reference:** A location or set you want to replicate

Use the `grok-imagine-image-quality` model endpoint for multi-image reference work. In the Grok Chat UI on mobile, the `@image1`, `@image2` syntax directs the model to use specific uploaded images as references.

### Iterative Refinement Workflow

The most efficient workflow per practitioners is **one variable per iteration**:

1. Generate base image with complete prompt
2. Identify the single most important issue
3. Add one targeted correction, keep everything else identical
4. Never rewrite the entire prompt to fix one problem — you lose what was working

Example correction prompts (for image-to-image editing):
- "Keep everything identical. Change only the lighting to a warmer, more golden tone."
- "Keep the composition, face, and clothing. Change the background to a concrete wall texture."
- "The model's left hand needs correction — three fingers are merged. Maintain everything else."

### Using Grok Text Mode to Draft Image Prompts

One of Aurora's most productive workflows is **chaining Grok's text model with its image model**:

1. Open Grok.com in text mode
2. Describe your visual intent in plain terms: "I need a cinematic portrait of a jazz musician in a 1950s New Orleans setting"
3. Ask Grok to write a detailed image generation prompt: "Write me a Grok Imagine prompt for this scene, structured with subject, lighting, camera, mood, and style reference"
4. Review and adjust the generated prompt
5. Paste into the Imagine interface

This uses Grok's language capabilities to construct more technically precise prompts than most users write naturally. The `revised_prompt` field in the API output from image generation shows you Aurora's own internal rewrite, which can itself be used as a starting point for iteration.

### Spicy Mode Professional Context

**What it unlocks for legitimate professional creative work:**
- Lingerie and swimwear advertising photography (partial nudity in professional context)
- Mature fashion editorial (suggestive but non-explicit)
- Fine art figure studies (artistic nude within R-rated parameters)
- Bold cinematic atmospheres that standard mode over-modifies

**Access requirements:** SuperGrok ($30/mo) or X Premium+ ($40/mo) · iOS/Android only · 18+ age verification · Two content toggles enabled

**Professional cautions:**
- The moderation is post-generation and server-side — outputs are scanned after generation; borderline results auto-blur
- Do not use Spicy Mode for client-deliverable work that will undergo advertising pre-clearance
- Real-person sexualized likenesses remain blocked even in Spicy Mode — do not attempt with named subjects
- The policy has changed multiple times since August 2025 — check current xAI AUP before building workflows that depend on Spicy Mode

### Image-to-Video Extension Overview

Grok Imagine's video capabilities (Imagine v0.9 and later) allow:
- **Text-to-video:** Up to 15 seconds, 720p, with native synchronized audio (dialogue, music, ambient sound)
- **Image-to-video:** Animate a still image as the starting frame
- **Video editing:** Modify an existing video with natural language
- **Video extension:** Continue from the last frame of an existing clip

**Prompt grammar for video (brief notes):** Add motion verbs and camera directions to your image prompt: "slow dolly forward toward subject", "smooth pan right following figure", "static shot, subject approaches camera". Keep prompts shorter for video — motion stability decreases with overly complex prompts. The best results come from: subject + action + camera movement + lighting + atmosphere, under 80 words.

### Working Around Common Refusals

For legitimate creative work that triggers false-positive moderation:

| Blocked intent | Rephrasing approach |
|---|---|
| Violence in art historical context | "Baroque painting depicting a mythological battle scene, oil on canvas" |
| Injury for medical illustration | "Medical illustration, clinical educational context, anatomical detail" |
| Extreme weather for documentary | "Documentary photograph of the aftermath of a severe storm" |
| Edgy fashion editorial | "High fashion editorial, art-directed, conceptual — inspired by Nick Knight" |

**General principle:** Framing content within an established artistic or professional context (documentary photography, medical illustration, art historical painting, fashion editorial) provides legitimate context that moderation systems can process. Do not attempt to defeat moderation; find the legitimate framing.

---

## 9. Parameter & Settings Reference Table

| Parameter | Values | Effect |
|---|---|---|
| `model` | `grok-imagine-image-quality` (recommended), `grok-imagine-image` | Quality level vs. speed |
| `aspect_ratio` | `1:1`, `16:9`, `9:16`, `4:3`, `3:4`, `3:2`, `2:3`, `2:1`, `1:2`, `19.5:9`, `9:19.5`, `20:9`, `9:20`, `auto` | Output dimensions |
| `resolution` | `1k`, `2k` | Long-edge pixel count |
| `n` | 1–10 | Images per request |
| `response_format` | `url`, `b64_json` | Delivery method |
| `image` | URL or base64 | Source image for editing |
| `revised_prompt` | (returned field) | What Aurora actually used |

**Video parameters:**
| Parameter | Values | Notes |
|---|---|---|
| `duration` | 1–15 seconds | Text-to-video max 15s; edits capped at 8.7s |
| `aspect_ratio` | Same as image | Image-to-video defaults to input aspect |
| `resolution` | `480p`, `720p` | 720p recommended for final delivery |

---

## 10. Failure Modes & Diagnostic Framework

### Hands and Anatomy

**Current state (May 2026):** Hand rendering remains Aurora's most persistent anatomical weakness, consistent with industry-wide issues in image generation models. Typical failure modes:

- Merged fingers (two or three fingers fused into one)
- Wrong finger count (6 fingers)
- Unnatural joint angles
- Inconsistent hand sizes between left and right

**Mitigation hierarchy:**
1. **First choice:** Keep hands out of frame (MCU or tighter)
2. **Second choice:** Give hands a physical task with clear shape (holding a mug, gripping a railing, resting flat on table)
3. **Third choice:** State explicitly "hands correctly formed, five fingers visible, natural resting position"
4. **Fourth choice:** Generate without hands shown, composite hands in post

### Text Rendering Failures

**Common failure patterns:**
- Letters replaced by visually similar glyphs
- Correct characters scrambled in wrong order
- Partial correct rendering (first word correct, second scrambled)
- Very small text becomes abstract marks

**Diagnostic:** If text fails in Aurora, evaluate whether the project actually requires text-in-image from generation. For most professional work, text is better applied in post (Figma, Illustrator, After Effects). Use Aurora for the visual foundation; apply typography after.

### Identity Drift in Multi-Image Sets

Without reference images, a character described in text will drift across generations — different nose shape, eye color, hair thickness. This is not a bug; it is the inherent variability of non-deterministic generation.

**Diagnosis:** If you see identity drift, you need a reference image workflow (see Section 8). Text-only character descriptions cannot produce identity-consistent series.

### Style Bleed and Prompt Collapse

**Style bleed:** When multiple style references are combined, Aurora averages them into an indistinct result. "Baroque + cyberpunk + watercolor" produces muddy confusion.

**Diagnosis:** Your prompt contains more than one major style reference. Choose one primary style; use others only as secondary qualifiers.

**Prompt collapse:** With prompts over ~150 words, Aurora may appear to drop certain elements entirely. The model is prioritizing the front-weighted elements.

**Diagnosis:** Review your `revised_prompt` API field. Identify which elements are being dropped in the rewrite. Move the most important elements to the front of your prompt.

### Common Reasons for Sterile / Generic Output

1. **No camera reference** — Aurora defaults to a neutral "AI illustration" mode without a camera/lens anchor
2. **Generic quality adjectives** ("stunning", "masterpiece", "ultra-detailed") — these are content-free and consume prompt tokens
3. **No lighting specification** — Aurora defaults to even, flat, uninspiring illumination
4. **No color direction** — Aurora picks a default "AI color" palette (usually slightly over-saturated primary colors)
5. **Subject stated, scene not described** — "a woman in a city" gives Aurora too little to work with

**Diagnostic checklist for generic output:**
- [ ] Does your prompt name a specific camera or lens?
- [ ] Does your prompt describe a light source and direction?
- [ ] Does your prompt specify a color palette or film stock?
- [ ] Does your prompt describe the scene (not just the subject)?
- [ ] Is your prompt in natural-language sentences, not tag lists?

If you answer "no" to two or more of these, rewrite before iterating.

### When to Abandon vs. Iterate

**Iterate when:** The composition, subject, or aesthetic direction is approximately right but one specific element is wrong. Use targeted single-variable correction.

**Abandon and rewrite when:** The fundamental composition is wrong (you wanted portrait, got landscape orientation), the subject is completely wrong, the wrong scene was generated, the style is entirely wrong. Starting from scratch is faster than trying to correct a fundamentally misgenerated image.

**Switch models when:** Text rendering fails consistently (use Ideogram). Character identity needs to hold across dozens of frames (use Nano Banana Pro or Flux.2). You need true 4K output (use Midjourney or Flux.2).

---

## 11. Workflow & Iteration Strategy

### Professional Prompt Development Workflow

```
Phase 1: BRIEF
Write a plain-language description of the image you need, as if briefing a photographer. 
No technical terms yet. Just: what is this image, who/what is in it, what should it feel like?

Phase 2: STRUCTURE
Apply the Aurora prompt structure:
Subject → Environment → Lighting → Mood → Camera/Lens → Style Reference
Write in natural language, 50–80 words.

Phase 3: FIRST GENERATION
Generate 4 variations (n=4 API call or repeated generations in UI).
Evaluate: is the composition direction correct? Is the subject recognizable?

Phase 4: DIAGNOSIS
Identify the single most important issue.

Phase 5: TARGETED ITERATION  
Add one correction. Generate again.

Phase 6: STYLE LOCK
Once composition and subject are correct, lock the style by anchoring the 
color treatment and lighting in a reusable style block.

Phase 7: REVIEW REVISED_PROMPT
Check what Aurora actually used (API only). Adjust source prompt to 
reduce rewriter deviation.
```

### Batch Strategy for Commercial Work

For high-volume commercial projects (product photography, social content):

1. Develop and validate a **base prompt template** with your style locked
2. Run `n=10` per prompt call to explore variations efficiently
3. Keep a **prompt library** of validated templates by category
4. Use the `revised_prompt` field to build a library of "Aurora-native" prompt phrasing that survives the rewriter

### The Iterative Refinement Mindset

The most common mistake is rewriting the entire prompt when one element fails. This destroys what was working. The fastest path to professional output is:

> **Generate → Identify one problem → Fix that problem only → Repeat**

---

## 12. Source Bibliography

1. xAI. "Grok Image Generation Release." xAI News Blog. December 8, 2024. https://x.ai/news/grok-image-generation-release [Verified May 2026]
2. xAI. "Imagine Overview." xAI Developer Documentation. Last updated May 12, 2026. https://docs.x.ai/developers/model-capabilities/imagine [Verified May 2026]
3. xAI. "Image Generation." xAI Developer Documentation. Last updated May 14, 2026. https://docs.x.ai/developers/model-capabilities/images/generation [Verified May 2026]
4. xAI. "Video Generation." xAI Developer Documentation. Last updated May 12, 2026. https://docs.x.ai/developers/model-capabilities/video/generation [Verified May 2026]
5. xAI. "Imagine API." xAI Product Page. https://x.ai/api/imagine [Verified May 2026]
6. TechCrunch. "Grok Imagine, xAI's new AI image and video generator, lets you make NSFW content." August 4, 2025. https://techcrunch.com/2025/08/04/ [Verified May 2026]
7. Fello AI. "Grok Imagine Spicy Mode: How to Enable It (2026 Guide)." May 16, 2026. https://felloai.com/grok-imagine-spicy-mode/ [Verified May 2026]
8. Picsart. "Grok Imagine Prompts: Copy-Ready Examples and Tips." April 17, 2026. https://picsart.com/blog/grok-imagine-prompts/ [Verified May 2026]
9. GenAIntel. "Grok Imagine Prompting Guide: Better Prompts for Cinematic Results." January 29, 2026. https://www.genaintel.com/guides/how-to-prompt-grok-imagine [Verified May 2026]
10. The Rundown AI. "xAI's Grok Imagine climbs the leaderboards." January 29, 2026. https://www.therundown.ai/p/xais-grok-imagine-climbs-the-leaderboards [Verified May 2026]
11. Replicate. "Grok Imagine Image Quality." https://replicate.com/xai/grok-imagine-image-quality [Verified May 2026]
12. Fal.ai. "Grok Imagine Pro API Live on fal (May 2026)." May 20, 2026. https://fal.ai/grok-imagine-pro [Verified May 2026]
13. MexicoBusiness.news. "xAI Restricts Grok Image Editing Amid Global Deepfake Crackdown." January 14, 2026. https://mexicobusiness.news [Verified May 2026]
14. Techloy. "ChatGPT Images 2.0 vs Grok Imagine." April 22, 2026. https://www.techloy.com [Verified May 2026]
15. YingTu AI. "Grok xAI NSFW Image Generation Policy." April 26, 2026. https://yingtu.ai/en/blog/grok-xai-nsfw-image-generation-policy [Verified May 2026]
16. ChatSmith.io. "Grok Aurora Prompt Guide." March 26, 2026. https://chatsmith.io/blogs/prompt/grok-image-prompts-00259 [Verified May 2026]
17. Skylum. "Best Grok AI Prompts." March 12, 2026. https://blog.skylum.com/best-grok-image-prompts/ [Verified May 2026]
18. Artificial Analysis. "Grok Imagine Quality, Generation Time & Price Analysis." https://artificialanalysis.ai/image/model-families/grok-imagine [Verified May 2026]
19. EM360Tech. "What is xAI Aurora Generator?" December 9, 2024. https://em360tech.com/tech-articles/what-xai-aurora-generator-inside-groks-new-image-generator [Verified May 2026] **[6+ months old — confirm currency]**
20. LifeArchitect.ai. "Grok timeline." https://lifearchitect.ai/grok/ [Verified May 2026]
21. Reddit r/grok. "Previous image generation model, grok-2-image (aka Aurora), is back." September 5, 2025. https://www.reddit.com/r/grok/comments/1n98po1/ [Verified May 2026] **[Community source]**
22. Reddit r/grok. "Limits of Grok Imagine: prompt structure and art." August 17, 2025. https://www.reddit.com/r/grok/comments/1mt2qvu/ [Verified May 2026] **[Community source]**
23. OpenCreator. "Grok Imagine — Revised Prompt documentation." https://opencreator.io/models/grok-imagine [Verified May 2026]

---

## 13. Glossary

**Aurora** — xAI's internal code name for its autoregressive mixture-of-experts image generation model, powering the Grok Imagine product.

**Autoregressive model** — A generative model that predicts output tokens sequentially, one at a time, conditioning each prediction on all previous outputs. Contrasts with diffusion models, which iteratively denoise from random noise.

**Mixture-of-Experts (MoE)** — A neural network architecture where different "expert" sub-networks are activated for different types of inputs, enabling specialization without proportional parameter increase.

**Bokeh** — The aesthetic quality of the out-of-focus areas in an image, produced by a lens with wide aperture. Shape varies by lens design (circular, oval in anamorphic, swirly in Petzval).

**Chiaroscuro** — The strong contrast of light and dark in an image, associated with Baroque painters such as Caravaggio and Rembrandt.

**Color grade** — The post-processing step where image color is manipulated to achieve a desired mood or cinematic look.

**DoF** — Depth of Field; the range of distance within a scene that appears acceptably sharp.

**grok-imagine-image-quality** — The current recommended API model for Grok Imagine still image generation (as of May 2026), superseding `grok-imagine-image-pro` (deprecated May 15, 2026).

**Grok Imagine** — xAI's consumer and developer brand name for the full multimodal generation suite powered by Aurora.

**Halation** — A bloom or glow around bright areas of an image, caused by light scattering in film emulsion; heavily associated with Cinestill 800T.

**Image-to-video** — The Grok Imagine capability to animate a still image (which becomes the first frame) into a short video clip.

**MoE routing** — The mechanism by which a MoE model selects which expert sub-networks to activate for a given input.

**Negative prompt** — An instruction specifying what to exclude from an image. **Not natively supported in Aurora/Grok Imagine** — must be phrased as positive exclusions.

**Revised_prompt** — The API response field containing Aurora's rewritten version of your input prompt, showing exactly what was passed to the image model.

**Spicy Mode** — xAI's R-rated content tier for Grok Imagine (launched August 4, 2025); allows mature/suggestive visual content; available only on iOS/Android with paid subscription, age verification, and enabled content toggles.

**SSS** — Subsurface Scattering; the optical phenomenon where light penetrates slightly into translucent materials (skin, candle wax, leaves) and scatters, producing the characteristic warmth and glow of skin rendering.

**Tilt-shift** — A lens or post-processing effect that allows the plane of focus to be tilted relative to the sensor, enabling selective focus at any angle and correction of perspective distortion in architectural photography.

**Wabi-sabi** — Japanese aesthetic philosophy centered on imperfection, impermanence, and incompleteness; in photography and design, associated with natural materials, worn surfaces, and asymmetry.

---

## 14. Appendix: Reusable Prompt Templates

### Category 1: Portrait Templates

**T-01: Clean studio portrait**
```
[DESCRIPTION] shot on [CAMERA] with [LENS], [LIGHTING SETUP] from camera-[SIDE], clean [BACKGROUND COLOR] seamless background. Subject is [GENDER, AGE, ETHNICITY], wearing [CLOTHING SPECIFICS]. Expression: [EMOTIONAL QUALITY]. Color treatment: [FILM/GRADE]. [CROP FRAMING].
```

**T-02: Environmental portrait**
```
Environmental portrait of [SUBJECT DESCRIPTION + OCCUPATION] in their [ENVIRONMENT/LOCATION]. [TIME OF DAY] light, [QUALITY: soft/hard/available]. Shot on [CAMERA, LENS]. [MOOD DESCRIPTION]. [FILM EMULATION]. The image should feel [CANDID/STAGED].
```

**T-03: Beauty close-up**
```
[ECU/CU] beauty portrait, [SKIN DESCRIPTION], [MAKEUP DESCRIPTION]. [LIGHTING SETUP] with [CATCHLIGHT DESCRIPTION]. [HAIR DESCRIPTION]. [BACKGROUND]. Shot on [CAMERA] with [MACRO LENS]. Skin retouching level: [UNTOUCHED/NATURAL/EDITORIAL/GLOSSY]. [STYLE REFERENCE].
```

### Category 2: Product Templates

**T-04: E-commerce hero**
```
Clean product photograph, [PRODUCT NAME AND DESCRIPTION] on [BACKGROUND TYPE]. Single [MODIFIER] from [POSITION], casting [SHADOW DESCRIPTION]. [PRODUCT ANGLE DESCRIPTION]. No props, no context. Shot on [CAMERA/LENS], maximum detail, ultra-sharp throughout.
```

**T-05: Product lifestyle**
```
Lifestyle product photograph. [SUBJECT DESCRIPTION] using/wearing [PRODUCT] in a [ENVIRONMENT]. [TIME OF DAY], [LIGHT QUALITY]. Shot on [LENS], [DOF DESCRIPTION]. [MOOD]. Color treatment: [GRADE]. Not posed, candid feel.
```

### Category 3: Architectural / Interior Templates

**T-06: Interior residential**
```
Architectural interior photograph, [STYLE DESCRIPTION] space. [TIME OF DAY] light from [LIGHT SOURCE POSITION]. [KEY FURNITURE/ELEMENTS LISTED]. No people. Tilt-shift perspective correction, verticals straight. f/8, everything sharp. Color: [GRADE/PALETTE].
```

**T-07: Exterior architecture**
```
Architectural exterior, [BUILDING STYLE AND DESCRIPTION], photographed at [TIME: golden hour/blue hour/overcast noon]. [FOREGROUND ELEMENT]. [SKY DESCRIPTION]. Tilt-shift corrected. Shot on [WIDE LENS]. [COLOR GRADE].
```

### Category 4: Landscape Templates

**T-08: Epic landscape**
```
Landscape photograph, [NAMED LOCATION], [TIME OF DAY]. [FOREGROUND ELEMENT] in foreground, [MIDGROUND], [BACKGROUND/HORIZON]. Light: [QUALITY AND DIRECTION]. Shot on [LENS], f/16, hyperfocal distance, everything in focus. [COLOR TREATMENT]. No human presence.
```

**T-09: Intimate landscape**
```
Intimate landscape, [SPECIFIC LOCATION DETAIL], [SEASON AND TIME]. Overcast/soft diffused light revealing [TEXTURE/DETAIL]. [SINGLE FOCAL ELEMENT]. [LENS] f/8, all sharp. Color: [PALETTE DESCRIPTION]. Mood: [QUIET/MELANCHOLIC/SERENE].
```

### Category 5: Food Templates

**T-10: Editorial food**
```
Editorial food photograph, [DISH DESCRIPTION WITH SPECIFIC STATE]. Single window light from [LEFT/RIGHT], [SOFT/HARD]. Plated on [VESSEL DESCRIPTION] on [SURFACE]. Background: [DARK/LIGHT/SPECIFIC]. Shot on [LENS]. Color: [MOOD GRADE]. Mood: [INDULGENT/CLINICAL/RUSTIC].
```

**T-11: Social-native food flat-lay**
```
Overhead flat-lay food photograph for [PLATFORM]. [DISH NAME AND DESCRIPTION], on [PLATE/VESSEL] on [SURFACE]. Surrounding: [PROP LIST]. Natural daylight from upper-right. [LIGHT: bright/airy OR moody/dark]. Color palette: [COLORS]. 1:1 aspect ratio. [HIGHLY STYLED BUT NATURAL/EDITORIAL STYLED].
```

### Category 6: Fashion Templates

**T-12: Editorial fashion**
```
High fashion editorial portrait, [CROP]. Subject: [DEMOGRAPHICS], wearing [GARMENT DESCRIPTION — FABRIC, SILHOUETTE, COLOR]. Set: [LOCATION]. Lighting: [QUALITY AND SETUP]. Gaze: [DIRECT/AVERTED/DISTANCE]. Shot: [CAMERA, LENS]. Color: [GRADE]. Aesthetic: [MAGAZINE REFERENCE].
```

**T-13: Lookbook full-length**
```
Fashion lookbook photograph, full-length. [SUBJECT DESCRIPTION], wearing [COMPLETE OUTFIT DESCRIPTION]. Set: [LOCATION WITH ARCHITECTURE OR ENVIRONMENT DETAIL]. Lighting: [TYPE AND QUALITY]. Pose: [WALKING/STANDING/ACTION DESCRIPTION]. Shot: [CAMERA, LENS]. Tone: [EDITORIAL DESCRIPTOR].
```

### Category 7: Illustration Templates

**T-14: Cinematic film still**
```
Cinematic film still, [ERA: 1970s/1980s/etc] [GENRE: neo-noir/horror/thriller] aesthetic. [SUBJECT
 IN SCENE]. [SETTING WITH PRACTICAL LIGHTING DESCRIBED]. Anamorphic or spherical lens, [ASPECT RATIO]. Color grade: [FILM STOCK OR GRADE]. Mood: [EMOTIONAL DESCRIPTOR]. References: [2-3 FILM TITLES].
```

**T-15: Anime / illustration**
```
[ANIME ERA AND STUDIO STYLE] illustration. [CHARACTER DESCRIPTION — AGE, APPEARANCE, CLOTHING]. [SETTING AND ATMOSPHERE]. Art style: [SPECIFIC QUALITY — handpainted/cel/digital]. Color palette: [PALETTE DESCRIPTION]. Mood: [EMOTIONAL QUALITY]. Composition: [FRAMING DESCRIPTION].
```

**T-16: Concept art character**
```
Character concept art, [MEDIUM: game/film] production quality. [CHARACTER — DEMOGRAPHICS, PROFESSION]. Wearing [ARMOR/COSTUME DESCRIPTION — MATERIALS, CONDITION, DESIGN LANGUAGE]. [WEAPON/PROP]. [POSE AND VIEW]. Neutral concept-art grey background. [LIGHTING]. Expression: [EMOTIONAL QUALITY]. Style reference: [GAME/FILM TITLES].
```

**T-17: Concept art environment**
```
Environment concept art, [GENRE: sci-fi/fantasy/contemporary] [MEDIUM: film/game]. [LOCATION DESCRIPTION WITH SCALE IMPRESSION]. [TIME OF DAY AND ATMOSPHERIC CONDITIONS]. Color palette: [DOMINANT COLORS]. Influences: [CONCEPT ARTISTS OR PRODUCTION REFERENCES]. [ASPECT RATIO FOR CINEMATIC FRAMING]. Should serve as: production design reference.
```

### Category 8: Surreal / Conceptual Templates

**T-18: Magritte-style surrealism**
```
Surrealist photograph in the Magritte tradition. [REALISTIC SCENE DESCRIPTION] but [SINGLE SURREAL JUXTAPOSITION — described in spatial/physical terms]. The subject treats the unreality as [UNREMARKABLE/FASCINATING/ALARMING]. Photographic realism throughout — unreality from juxtaposition only, not from object distortion. [FILM STOCK OR GRADE].
```

**T-19: Conceptual fine art**
```
Fine art conceptual photograph. [SUBJECT] surrounded by/immersed in/contained within [SYMBOLIC ELEMENT DESCRIBED SPATIALLY]. The relationship between subject and symbolic elements should communicate [THEMATIC STATEMENT]. Lighting: [SETUP]. Color: [PALETTE]. The image should read as [EMOTIONAL QUALITY] and function as [INTENDED CONTEXT: gallery/magazine cover/campaign].
```

### Category 9: Action / Sport / Wildlife Templates

**T-20: Sports peak moment**
```
Sports action photograph. [ATHLETE DESCRIPTION AND SPORT] at [PEAK MOMENT IN ACTION]. [ENVIRONMENTAL CONTEXT AND CROWD/SETTING]. Telephoto compression, [FOCAL LENGTH] equivalent. Motion: [FREEZE/SLIGHT BLUR AT EXTREMITIES]. Light: [NATURAL/ARTIFICIAL AND DIRECTION]. [EMOTIONAL QUALITY]. Wire service / [PUBLICATION] quality.
```

**T-21: Wildlife behavioral moment**
```
Wildlife photograph. [SPECIES DESCRIPTION] in [BEHAVIOR: feeding/in flight/stalking/at rest]. Natural habitat: [ENVIRONMENT DESCRIPTION]. Shot on [TELEPHOTO FOCAL LENGTH], shallow DoF, background [ENVIRONMENT BOKEH DESCRIPTION]. Natural available light. The image should feel like a genuine behavioral moment, not a staged setup. [FILM EMULATION OR GRADE].
```

### Category 10: Night / Astro Templates

**T-22: Night street**
```
Night street photograph. [CITY AND LOCATION SPECIFICS], [TIME: late night / pre-dawn]. Mixed practical lighting: [NEON + STREETLIGHT + WINDOW LIGHT]. [SUBJECT OR EMPTY SCENE]. [LENS AND APERTURE]. [WET STREET/DRY] condition, [REFLECTIONS IF WET]. ISO feel: [3200/6400] — grain visible and organic. Color: [GRADE]. Mood: [DESCRIPTOR].
```

**T-23: Astrophotography**
```
Astrophotography landscape. [MILKY WAY/STAR TRAILS/AURORA] above [NAMED OR DESCRIBED FOREGROUND LANDMARK]. [LIGHT POLLUTION CONDITIONS]. [HORIZON DETAIL]. [FOREGROUND ILLUMINATION SOURCE IF ANY: moonlight/blue hour/light painting]. [LENS AND SETTINGS FEEL — f/2.8, ISO 6400, 25s shutter]. Grain acceptable. Star points sharp. Mood: [VAST/INTIMATE/SPIRITUAL].
```

### Additional Specialized Templates

**T-24: Double exposure / Composite**
```
[FIRST SUBJECT DESCRIPTION] in double exposure with [SECOND ELEMENT — LANDSCAPE/TEXTURE/PATTERN]. The composite: [DESCRIBE HOW THE ELEMENTS OVERLAP OR INTERACT VISUALLY]. The first subject's silhouette contains the second element within it. [OR OTHER COMPOSITE DESCRIPTION]. [COLOR GRADE]. [MOOD].
```

**T-25: Macro nature detail**
```
Extreme macro photograph. [SUBJECT: dewdrop/insect/flower/mineral] at [MAGNIFICATION DESCRIPTION]. [LIGHTING: direction and quality]. DoF: razor thin — [SPECIFIC FOCAL PLANE DESCRIBED]. Background: [BOKEH COLOR AND QUALITY]. No digital artifacts; maximum optical quality. Shot at grass/ground/surface level looking [DIRECTION].
```

**T-26: Documentary portrait (crowd/street)**
```
Street/documentary photograph. [LOCATION: city, neighborhood, event]. [SUBJECT: individual or group IN CONTEXT]. Candid — not posed. Available light, [LIGHT QUALITY]. Shot on [LENS], [APERTURE]. [B&W / COLOR FILM TREATMENT]. [PHOTOJOURNALIST OR STREET PHOTOGRAPHER TRADITION]. Decisive moment, AP wire quality.
```

**T-27: Luxury product (fragrance / cosmetics)**
```
Luxury advertising photograph, fragrance/cosmetics. [PRODUCT NAME AND DESIGN DESCRIPTION]. Set on [SURFACE: marble/glass/mirror/stone]. [PROPS: flower petals/fabric/complementary objects]. Lighting: [SINGLE NARROW SOURCE] creating [SHADOW AND HIGHLIGHT DESCRIPTION]. Background: [DEEP BLACK/CLEAN WHITE/GRADIENT]. Shot [LENS AND ANGLE]. Color grade: [WARMTH AND SATURATION LEVEL]. Communicates: [BRAND VALUE — heritage/sensuality/purity/edge].
```

**T-28: Children's editorial / book illustration**
```
Children's book illustration. [CHARACTER — AGE, APPEARANCE, EXPRESSION] in [DETAILED SCENE AND SETTING]. Art style: [SPECIFIC: Quentin Blake loose ink + watercolor / Maurice Sendak / modern flat digital]. Warm, inviting color palette. Clear readable composition — [CHARACTER PLACEMENT]. Mood: [WONDER/ADVENTURE/COSINESS]. Age-appropriate emotional tone.
```

**T-29: Comic / Graphic novel panel**
```
Graphic novel panel. [SCENE AND ACTION — DESCRIBED AS A PANEL BEAT]. Art style: [INKER AND PERIOD: Bill Sienkiewicz painted / Moebius ligne claire / Mazzucchelli cartoonish realism]. Panel composition: [FRAMING AND ANGLE]. Inking: [WEIGHT AND LINE QUALITY]. Color: [FOUR-COLOR PROCESS / PAINTED / LIMITED PALETTE]. Caption/speech bubbles: [NONE / DESCRIBED AS BLANK].
```

**T-30: Poster / Typography design**
```
[GENRE: film poster / event poster / propaganda-style graphic] design. Subject: [CENTRAL IMAGE DESCRIPTION]. Typography: [TITLE OR HEADLINE] in [TYPEFACE MOOD: bold condensed / art deco serif / hand-lettered] positioned [LOCATION IN FRAME]. Color palette: [SPECIFIC PALETTE]. Design tradition: [SAUL BASS / BAUHAUS / SOVIET CONSTRUCTIVIST / CONTEMPORARY MINIMALIST]. Aspect ratio: [PORTRAIT FOR PRINT].
```

**T-31: Underwater / Submerged**
```
Underwater photograph. [SUBJECT] submerged in [CLEAR OCEAN / POOL / RIVER / LAKE]. [DEPTH IMPRESSION]. Caustic light patterns on [SURFACE/SUBJECT]. Water clarity: [CRYSTAL / SLIGHTLY TURBID / MURKY]. Color: [TROPICAL BLUE-GREEN / COLD NORTHERN BLUE-GREY]. Shot from [ANGLE]. [BUBBLES? YES/NO]. Available natural light from surface above. Wide angle, all sharp.
```

**T-32: Architecture — Interior Night / Atmosphere**
```
Interior night photograph. [SPACE DESCRIPTION: cathedral/library/theater/industrial hall] lit only by [PRACTICAL SOURCES: candles/spotlights/windows/emergency lighting]. [SCALE IMPRESSION: vast/intimate]. [HUMAN PRESENCE: single figure / empty]. Long-exposure feel — light sources bloom slightly. [COLOR PALETTE FROM SOURCES]. [MOOD: sacred/abandoned/theatrical/cinematic].
```

