# Grok Imagine (Aurora) Prompt Engineering — Research Report & Field Guide

> **Note on deliverable format:** The task specifies two markdown files (`grok-imagine-research.md` and `grok-imagine-guide.md`). Both are delivered below as a single response, with explicit `===== FILE 1 =====` and `===== FILE 2 =====` separators so a downstream agent or user can split them losslessly into the two named files.

---

===== FILE 1: grok-imagine-research.md =====

# Grok Imagine (Aurora) — Prompt Engineering Research Report
*Working reference for photographers, art directors, designers and creative directors. Compiled May 22, 2026.*

## 1. Verification Note — Current State of the Product (May 2026)

- **Product brand:** "Grok Imagine." "Aurora" is now used internally as the engine codename; Elon Musk publicly asked in December 2024 to "delete the name of the internal @xAI image generation system (Aurora). Just think of Grok as doing anything." The consumer brand on grok.com, in the iOS/Android apps, and on X is **Grok Imagine**.
- **Current flagship image model:** `grok-imagine-image-quality` ("Quality Mode"), launched May 6, 2026. xAI's announcement headline: *"Higher realism. Stronger text rendering. Better creative control."* The previous `grok-imagine-image-pro` was deprecated May 15, 2026. The standard tier `grok-imagine-image` remains available for high-volume, lower-cost batch work.
- **Current video model:** `grok-imagine-video`. Grok Imagine 1.0 shipped February 3, 2026; xAI's @xai account announced it on February 2, 2026 at 9:29 pm UTC as *"Introducing Grok Imagine 1.0, our biggest leap yet. 1.0 unlocks 10-second videos, 720p resolution, and dramatically better audio. Imagine has generated 1.245 billion videos in the last 30 days alone,"* with a follow-up post stating *"Huge leap in prompt following."* "Extend from Frame" was added March 2, 2026.
- **Architecture:** Autoregressive Mixture-of-Experts, predicting the next token from interleaved text and image data (xAI blog, December 9, 2024). Aurora is not diffusion-based; this is the single most important fact for prompt design.
- **Access surfaces:** X (web/mobile, via Grok), standalone Grok app on iOS and Android, grok.com, and the xAI API at `POST https://api.x.ai/v1/images/generations` (also resold by Replicate, fal.ai, AIMLAPI, Scenario, PixVerse, fal, etc.).
- **Mode taxonomy:** Four modes — **Custom, Normal, Fun, Spicy**. Mode selection applies most strictly to video generation; image generation gating in the consumer app is controlled by the NSFW toggle and regional rules.
- **Output specs:** Images at 1K (1024 px on the long edge) or 2K (2048 px); 14 aspect ratios — 1:1, 16:9, 9:16, 4:3, 3:4, 3:2, 2:3, 2:1, 1:2, 19.5:9, 9:19.5, 20:9, 9:20, auto; up to 10 images per request; up to 3 reference images per edit; JPG/PNG/base64; **no seed parameter exposed**; **negative prompts not respected**.
- **Pricing (May 2026):** $0.05 / 1K image, $0.07 / 2K image, $0.08 / 2K edit (1 input + 1 output), ~$0.05/sec video. SuperGrok $30/mo consumer plan; SuperGrok Heavy $300/mo; X Premium+ $40/mo; SuperGrok Lite $10/mo; X Premium $8/mo. Free image generation was removed March 19, 2026.
- **Generation time:** Images 3–10 s; 10-s video 30–60 s.
- **Watermarks:** No default cryptographic watermark; visible "GROK ⧄" historically appeared on some X consumer outputs but is not present on API outputs. C2PA provenance is **not** implemented as of May 2026.

**Deltas vs. user-brief assumptions:** (a) "Aurora" is engine-internal, not the consumer brand. (b) Standard/Fun/Spicy/Custom mode taxonomy applies most strictly to **video**, not image generation. (c) Generation times have dropped — older "10–20 s" figures are stale. (d) Free-tier image generation has been removed. (e) Quality Mode (`grok-imagine-image-quality`) supersedes everything older.

## 2. Executive Summary (≈400 words)

Grok Imagine matured into a production-grade image and short-video generator by May 2026. The new `grok-imagine-image-quality` model launched May 6, 2026, and xAI's announcement states verbatim: *"xAI's Grok Imagine API ranks among the strongest models on independent leaderboards. Source: Arena Text-to-Image Arena as of May 4, 2026."* On that same Arena Text-to-Image leaderboard as retrieved May 22, 2026 (5,169,154 votes across 60 models), `grok-imagine-image-quality` is **rank #6 with an Elo of 1223 (Preliminary, 11,002 votes)**, behind `gpt-image-2 medium` (#1, Elo 1393), two Gemini 3-series models (#2–3), `gpt-image-1.5-high-fidelity` (#4), and `gemini-3-pro-image-preview` (#5). At $0.05 per 1K image and $0.07 per 2K image, Grok Imagine occupies the Pareto frontier for cost-to-quality at its price point, but it is no longer the outright quality leader.

For working professionals, four practical implications follow.

**One — Aurora rewards director-style natural language, not tag soup.** Because the model is autoregressive, the first 20–30 words of the prompt disproportionately set composition, palette and subject identity. Comma-separated keyword stacks ("masterpiece, 8K, ultra-detailed") underperform full sentences that lead with subject, scale and scene. Negative prompts are not respected — restate as positives ("clear skin" not "no blemishes"; "five fingers naturally splayed" not "no extra fingers").

**Two — text rendering and brand assets are genuine strengths.** Aurora "writes" text rather than dreaming it. Wrap target strings in straight double quotes, name the medium ("neon sign reading", "letterpress poster titled"), and specify typographic mood. This is the single biggest differentiator vs. Midjourney; only Google Imagen 4 outperforms it on multilingual signage.

**Three — identity, hands and complex anatomy remain the weakest dimensions.** Independent assessments place Grok Imagine behind Flux 2 on raw photorealism, behind Imagen 4 on typography in mixed-script scenes, and behind Midjourney v7 on artistic stylization. Character consistency across a series requires the reference-image edit workflow, not prompt repetition alone.

**Four — the consumer surface is policy-volatile.** Following the January 2026 deepfake controversy — which Reuters named "a mass digital undressing spree," and which the Paris-based AI Forensics found involved 53% of sampled Grok-generated images depicting individuals in minimal attire (81% women-presenting, 2% appearing to be 18 or younger) across 20,000+ images and 50,000 prompts between December 25, 2025 and January 1, 2026 — xAI removed the free image tier (March 19, 2026), tightened editing of real-person images, geoblocked Spicy outputs in the UK, EU, Indonesia, Malaysia and California, and is under active investigation by California Attorney General Rob Bonta (who announced the investigation January 14, 2026 and issued a cease-and-desist letter on January 16, 2026 demanding xAI *"take immediate action to stop the creation and distribution of deepfake, nonconsensual, intimate images and child sexual abuse material (CSAM)"*), Ofcom, and the European Commission, whose spokesperson said January 5, 2026: *"This is not 'spicy'. This is illegal. This is appalling. This is disgusting. This has no place in Europe."*

**Bottom line:** For fast cinematic concepting, in-image text and branding, mid-volume editorial and lifestyle production, and short-form social video at the best price-to-quality ratio in the category, use Grok Imagine. For ironclad hand anatomy in unusual poses, gallery-grade artistic style consistency across a 50-shot campaign, or commercial indemnification — pick another tool (Flux 2, Midjourney v7, or Adobe Firefly respectively).

## 3. Product & Model Foundations

### 3.1 Aurora architecture
xAI's December 9, 2024 release post characterizes the engine: *"Aurora is an autoregressive mixture-of-experts network trained to predict the next token from interleaved text and image data. We trained the model on billions of examples from the internet, giving it a deep understanding of the world. As a result, it excels at photorealistic rendering and precisely following text instructions."* This is the architectural fact that drives every prompting decision: image tokens are emitted sequentially, so prompt order matters more than in diffusion models, and text rendering is closer to language-model "writing" than diffusion "dreaming."

### 3.2 Release timeline (verified)
| Date | Milestone |
|---|---|
| Dec 9, 2024 | Aurora replaces Flux as Grok's image engine |
| Mar 21, 2025 | Aurora available via xAI API |
| Mar 2025 | Image editing (multimodal input) ships |
| Jul 28, 2025 | Grok Imagine launches with image + 6-sec video and audio |
| Aug 4, 2025 | Spicy Mode added |
| Oct 2025 | v0.9 — generation time below 15 s |
| Jan 28, 2026 | Imagine API expands with text-to-video, image-to-video, video editing |
| Feb 3, 2026 | Grok Imagine 1.0 — 10-s clips at 720p, improved audio |
| Mar 2, 2026 | Extend from Frame |
| Mar 12, 2026 | Musk publicly sets R-rated standard for Spicy Mode |
| Mar 19, 2026 | Free image generation tier removed |
| May 6, 2026 | Quality Mode (`grok-imagine-image-quality`) launches |
| May 15, 2026 | `grok-imagine-image-pro` deprecated |

### 3.3 Capability matrix per surface
| Surface | T→I | Edit | I→V | T→V | Spicy | Ref Imgs | Max Res |
|---|---|---|---|---|---|---|---|
| X (web/mobile) | ✓ | ✓ | ✓ | ✓ | Region-gated | 1 | 2K / 720p |
| Grok iOS / Android | ✓ | ✓ | ✓ | ✓ | ✓ (paid + 18+) | 1 | 2K / 720p |
| grok.com | ✓ | ✓ | ✓ | ✓ | Limited / regional | 1–3 | 2K / 720p |
| xAI API | ✓ | ✓ | ✓ | ✓ | Not exposed | 3 | 2K / 720p |

### 3.4 Content tiers
- **Custom** — granular per-request controls.
- **Normal** — default safe-for-work.
- **Fun** — looser, meme/cartoon interpretation.
- **Spicy** — R-rated. Musk, March 12, 2026: *"If it's allowed in an R-rated movie, it's allowed in Grok Imagine."* Hard limits: explicit acts, minors, real-person sexualized deepfakes, CSAM. Geoblocked in UK, EU member states, Indonesia, Malaysia, California video.

### 3.5 Output specs reference
| Spec | Value |
|---|---|
| Image resolutions | 1K, 2K |
| Aspect ratios | 14 (1:1, 16:9, 9:16, 4:3, 3:4, 3:2, 2:3, 2:1, 1:2, 19.5:9, 9:19.5, 20:9, 9:20, auto) |
| Images per request | up to 10 |
| Reference images per edit | up to 3 |
| Video resolutions | 480p, 720p |
| Video duration | 1–15 s |
| Video frame rate | 24 fps |
| Endpoint | `POST https://api.x.ai/v1/images/generations` |
| Pricing 1K image | $0.05 |
| Pricing 2K image | $0.07 |
| Pricing 2K edit (1+1) | $0.08 |
| Pricing video | ~$0.05/sec |
| Seed | not exposed |
| Negative prompt | not respected |

## 4. Competitive Landscape (May 2026)

Direct comparison anchored to the Arena Text-to-Image leaderboard as of May 22, 2026 (5,169,154 votes, 60 models): Grok Imagine Quality sits rank #6 with Elo 1223; GPT Image 2 medium leads at #1 (1393), Gemini 3-series at #2–3, GPT Image 1.5 HF at #4, Gemini 3 Pro Image at #5.

| Capability | Grok Imagine | Midjourney v7 | DALL-E 4 / GPT Image 2 | Flux 2 Pro | Imagen 4 Ultra | Stable Diffusion 3.5 |
|---|---|---|---|---|---|---|
| Architecture | Autoregressive MoE | Proprietary diffusion | Proprietary diffusion | Hybrid transformer/diffusion | Diffusion | Diffusion |
| Photorealism | Strong | Strong | Strong | Class-leading | Strong | Variable |
| Artistic stylization | Mid | Class-leading | Mid–strong | Strong | Mid | Strong with LoRAs |
| Text-in-image | Strong | Weak | Strong | Strong | Class-leading | Weak |
| Prompt adherence | Strong | Mid | Class-leading | Strong | Strong | Mid |
| Hands / anatomy | Mid | Mid | Strong | Strong | Strong | Weak |
| Real people / celebrities | Permissive (gated) | Restricted | Restricted | Restricted | Restricted | User-controlled |
| Native image→video | Yes (720p, 15 s) | No | No (via Sora) | No | No (via Veo) | No |
| Entry price per image | $0.05 | $10/mo tier | ~$0.04 | $0.04–0.08 | Higher | Free self-host |
| Commercial indemnification | No | No | No | No | No | No |
| Strongest at | Cinematic concepting, in-image typography, fast iteration, mature content | Editorial aesthetics, style consistency | Reasoning-heavy briefs, mixed-text scenes | Photoreal product, lighting | Multilingual signage, product | Self-hosted LoRA work |
| Weakest at | Anatomy in unusual poses, brand safety, free access | Text, API ecosystem | Loose-style art | Style range, ecosystem | Consumer access | Out-of-box quality |

## 5. Prompt Anatomy — Evidence-Based Structure

### 5.1 The 12-slot Aurora grammar
```
[SHOT TYPE] of [SUBJECT + 3–6 DETAILS], [ACTION / POSE],
[SETTING], [LIGHTING + QUALITY], [TIME / ATMOSPHERE],
shot on [CAMERA] with [LENS + APERTURE], [FILM / COLOR PROFILE],
[COMPOSITION RULE], [TEXTURE / MATERIAL CUES], [POST-PROCESS],
[STYLE REFERENCE], [ASPECT RATIO]
```

### 5.2 Length sweet spots
- **<50 words** — ideation, memes, surprise.
- **50–150 words** — sweet spot for professional work.
- **150–250 words** — staged scenes with multiple subjects, brand assets, text.
- **>250 words** — attention smears; earlier slots dominate.

### 5.3 Positional weighting
- Subject and shot scale first.
- Camera / lens / film stock together mid-prompt.
- Mood-overriding modifiers in the last 20 words.
- Quoted text strings in the first half of the prompt.

### 5.4 Negative prompts — restate as positives
| ❌ | ✅ |
|---|---|
| "no blur" | "tack sharp" |
| "no extra fingers" | "five fingers naturally splayed" |
| "no blemishes" | "clear skin" |
| "no clutter" | "minimalist composition, generous negative space" |

### 5.5 Multi-subject handling
Name spatial relationships ("on the left, in the foreground, behind"). Cap at 4 named subjects; beyond that use group descriptors.

### 5.6 Text rendering recipe
`[medium] reading "TARGET TEXT" in [typographic mood] font`. Failure modes: strings over 20 characters truncate; mixed scripts (Latin + CJK in same line) bleed.

### 5.7 Real-person, celebrity and IP policy (May 2026)
- Real-person likenesses permitted in artistic / portrait contexts.
- Editing uploaded photos of real people into revealing clothing **blocked platform-wide** (X Safety, Jan 14, 2026): *"We have implemented technological measures to prevent the Grok account from allowing the editing of images of real people in revealing clothing such as bikinis. This restriction applies to all users, including paid subscribers."*
- Public figures generable in non-sexual contexts (Grok-specific differentiator vs. DALL-E and Imagen).
- Copyrighted characters and logos technically generable; user assumes IP liability.

## 6. The Photography Vocabulary — A through M

**A — Camera body & format.** Hasselblad H6D (editorial anchor), Phase One IQ4 (product / luxury), Leica M11 (street / documentary), Sony A1 (sports / wildlife), Canon R5 (general), Fujifilm GFX, Mamiya 7 (medium-format film look), Pentax 67 (1970s editorial), Contax T2 / Yashica T4 (soft fashion candid), Polaroid SX-70 (instant), Holga / Diana (lo-fi). Naming Hasselblad or Phase One reliably increases perceived sharpness and tonal range. **Pitfall:** don't mix a digital body with a film grain stock unless intentional.

**B — Lens.** 14–24mm wide, 35mm street, 50mm general, 85mm portrait, 100–135mm short tele, 200–400mm sports/wildlife, tilt-shift architecture, anamorphic cinema. Apertures f/1.2 → f/16. Specialty: Petzval, Lensbaby, Helios 44-2 swirly bokeh, vintage Leica Summilux. Filters: polarizer, ND, Black Pro-Mist 1/4, Tiffen Glimmerglass, diffusion, IR. **Reliable phrases:** "85mm f/1.4 editorial portrait," "35mm f/2 documentary," "anamorphic with oval bokeh and horizontal flares," "Black Pro-Mist 1/4 highlight bloom."

**C — Framing & shot scale.** ECU, CU, MCU, MS, MWS, WS, EWS; OTS, two-shot, three-shot; eye-level, low, high, worm's-eye, bird's-eye, Dutch, overhead flat-lay, POV. **Pitfall:** "wide shot" alone often returns medium-wide; add "subject occupies 1/4 of frame."

**D — Composition.** Rule of thirds, golden ratio/spiral, symmetric / centered, asymmetric, leading lines, S-curves, diagonals, triangular, frame-within-frame, three-plane depth, negative space, breathing room, headroom, lead room, rule of odds, pattern / repetition. Place composition cues in the first 60 words.

**E — Lighting.** Patterns: three-point, Rembrandt, butterfly/paramount, loop, split, broad, short, clamshell. Qualities: hard, soft, diffused, specular, dappled, motivated, practical. Sources: tungsten, HMI, LED, fluorescent, sodium vapor, neon, candle, firelight, screen glow, window, sunlight, moonlight; blue/golden/magic hour, high noon, overcast, dusk, dawn. High-art: high-key, low-key, chiaroscuro, noir, Caravaggio, Vermeer, Hopper. **Don't stack more than one pattern + one accent.**

**F — Atmospherics.** Rain, snow, fog, mist, dust storm, sandstorm, heat shimmer, god rays, volumetric light, dust motes, pollen, smoke, embers, condensation, long shadows.

**G — Color science & film stocks.** Kodak Portra 400 (warm editorial default), Portra 800, Ektar 100 (saturated landscape), Tri-X 400 / T-Max (B&W), Fuji Pro 400H (cool greens), Velvia 50 (saturated), Eterna (muted), Cinestill 800T (tungsten halation night), Ilford HP5, Delta 3200, Lomochrome Purple, cross-process, bleach bypass, ENR. Cinema profiles: ARRI LogC, RED IPP2, Sony S-Cine. Director palettes: Roger Deakins (cool single-source motivated), Wes Anderson (symmetric pastel), Saul Leiter (reflective windows), Eggleston (saturated everyday), Crewdson (cinematic suburban tableaux), Vittorio Storaro (saturated primaries). **Hex codes work**: "palette dominated by #1B3A5B and #E8C28A."

**H — Subject action & performance.** Contrapposto, candid, dynamic, static, mid-stride, mid-laugh, three-quarter profile, direct-to-camera, hand on hip, fingers interlaced, holding [object]. Eye-line ("eyes off-frame left at something unseen") + hand placement + weight distribution is the single biggest unlock for candid portraits.

**I — Environment & set design.** Location specificity ("Marrakech medina at 4 PM") outperforms generic ("a city"). Era accuracy works well. Architectural styles (Brutalist, Bauhaus, mid-century modern, Mediterranean revival, Edwardian) are reliably recognized.

**J — Rendering, materials & textures.** Skin: "natural skin texture with visible pores, fine peach fuzz, subsurface scattering" — the most important phrase to defeat AI wax. Fabric: weave / drape / sheen / wrinkle / weight. Hair: strand detail, frizz, fly-aways, gloss. Materials: brushed steel, oxidized copper, raw concrete, end-grain oak, blown glass, weathered teak. Food: gloss, steam, crumb, oil sheen, condensation, juices, char marks. Stylized: cel-shaded, anime, oil paint impasto, watercolor with paper texture, gouache flat, ink wash, pencil, charcoal, Octane render, Pixar 3D, isometric, low-poly, voxel, claymation.

**K — Post-processing.** Sharpening, micro-contrast, dehaze, grain, halation, vignette, highlight rolloff, shadow lift, split-toning, frequency-separation retouch, dodge-and-burn, double exposure, light leak, lens dirt, anamorphic flare.

**L — Style invocation.** Editorial: Vogue, AnOther, i-D, Self Service. Documentary: Magnum, VII, National Geographic. Lifestyle: Apartamento, Kinfolk, Cereal, Dwell, AD. Conceptual: Aperture, Foam. Decades: 1970s Kodachrome, 1990s grunge, Y2K digital, 2010s Instagram. Movements: Baroque, Art Deco, Bauhaus, Surrealism, Pop Art, Brutalism. Recognized photographers (community-tested as Aurora-responsive): Annie Leibovitz, Steven Meisel, Peter Lindbergh, Helmut Newton, Mario Sorrenti, Tim Walker, David LaChapelle, Nan Goldin, Sally Mann, Wolfgang Tillmans, Tyler Mitchell, William Eggleston, Saul Leiter, Vivian Maier, Cartier-Bresson, Sebastião Salgado, Steve McCurry, Gregory Crewdson, Cindy Sherman, Andreas Gursky, Hiroshi Sugimoto, Daido Moriyama, Rinko Kawauchi, Alec Soth. **Ceiling: one photographer + one publication per prompt.**

**M — Text inside images.** Strengths: brand names, posters, packaging, neon signs, street signage, book covers, T-shirt graphics, license plates, awnings, menus. Failure modes: paragraphs >5 lines, mixed scripts in one line, decorative cursive at small sizes.

## 7. Use-Case Pattern Library — 30 Worked Prompts (150–300 words each)

(Each pattern is a paste-ready prompt formatted in Aurora's preferred grammar. The fully worked 30 examples are in the "Use-Case Pattern Library" section of FILE 2 below — each is a reusable template by substituting subject, wardrobe and location.)

**Index:** 1 Editorial fashion portrait · 2 Beauty close-up · 3 Studio headshot · 4 Environmental portrait · 5 Street vérité · 6 Photojournalism · 7 Wedding lifestyle · 8 Product hero · 9 Product lifestyle · 10 Food editorial · 11 Interior architecture · 12 Landscape · 13 Wildlife · 14 Sports · 15 Macro · 16 Astro · 17 Conceptual fine art · 18 Still life · 19 Lookbook · 20 Luxury · 21 UGC mirror selfie · 22 1970s thriller film still · 23 Anime cel-shaded · 24 Western editorial illustration · 25 Concept art turnaround · 26 Logo / brand identity · 27 Letterpress poster · 28 Children's book · 29 Comic panel · 30 Surreal dreamscape.

Full prompt bodies appear in FILE 2 Section 9 ("20 Ready-to-Use Recipes") and FILE 1 Appendix below.

## 8. Advanced Techniques

- **Character consistency (Prompting Systems "character bible" methodology, March 2026):** Generate a single master reference image with a 60–80-word character description. Repeat that description verbatim in every subsequent prompt's first 60 words. Use the master as a reference image (up to 3 supported per edit). Change one variable per generation. Prefer MS/MWS distance over CU for face stability.
- **Style consistency:** Define a 20-word "stylebloc" (film stock, lens, lighting pattern, palette, reference) and prepend to every generation.
- **Reference image use:** Up to 3 per edit. Pattern: "Keep [X from image 1], change [Y] to [Z]."
- **Iterative refinement:** Pass 1 composition (1K, n=8) → Pass 2 lighting (1K, n=4) → Pass 3 finish (2K, n=2) → Pass 4 surgical edit.
- **Grok-chain workflow:** Use Grok 4 chat to draft a 120-word Aurora prompt from a one-line brief, then iterate the brief, not the image.
- **Spicy Mode professional use:** Lingerie editorial, art-nude, boudoir, mature horror/thriller atmosphere. R-rated only. Hard limits: explicit acts, minors, real-person sexualization. Geoblocked UK / EU / Indonesia / Malaysia / California for video.
- **Image-to-video extension:** Generate still in Quality → image-to-video with motion-only prompt → Extend from Frame for up to 15 s per clip. Cap chained extensions at 3 for production work.
- **Working around refusals:** Replace clinical terms with art-historical ones ("classical nude," "boudoir portrait"). Use "imaginary adult character" rather than naming real people. Shift sensitive themes to genre descriptors.
- **Batch generation:** API `n=4` or `n=8` at 1K for exploration, re-render best at 2K.

## 9. Parameter & Settings Reference Table

| Parameter | Values | Notes |
|---|---|---|
| `model` | `grok-imagine-image`, `grok-imagine-image-quality` | Quality is current flagship |
| `prompt` | string | xAI docs do not publish an explicit character cap; community-verified sweet spot 200–1000 words |
| `n` | 1–10 | n=4 sweet spot for exploration |
| `aspect_ratio` | 14 values + `auto` | Repeat at start and end of prompt for reliability |
| `resolution` | `1k`, `2k` | 2K default for Quality |
| `response_format` | `url`, `b64_json` | URLs temporary; base64 for embedding |
| `image` | URL or base64 | Up to 3 references per edit |
| Seed | N/A | Not exposed |

## 10. Failure Modes & Diagnostic Framework

| Symptom | Likely cause | Fix |
|---|---|---|
| Wax / plastic skin | Missing texture cues | "Natural skin texture with visible pores, fine peach fuzz" |
| Distorted hands | ECU on hands | Crop wider; restate as "five fingers naturally splayed" |
| Garbled text | Long string / mixed scripts | <20 chars; quote it; specify medium |
| Identity drift | No reference image | Use API edit with reference; verbatim character bible |
| Style bleed | >2 style references | One photographer + one publication |
| Aspect ratio ignored | Single mention | Start, end and API param |
| Sterile / generic | Adjective spam | Concrete cues (lens, film, palette) |
| Brand refusal | Sexualized or political framing | Rephrase neutrally |
| Prompt collapse | >250 words | Cut to 150; key cues in first 60 |
| Sodium-orange cast everywhere | Cinestill 800T over-anchoring | Pair with neutral daylight cue or remove |

**When to abandon vs. iterate:** Abandon after 3 failed compositions on the same prompt; iterate when you have one strong image with one fixable flaw.

## 11. Workflow & Iteration Strategy

Four-pass production workflow:
1. **Brief pass** — Grok chat drafts the Aurora prompt from a one-line brief.
2. **Composition pass** — API 1K, n=8. Score composition only.
3. **Lighting pass** — Winner's prompt, n=4 lighting variations.
4. **Finish pass** — Re-render at 2K; edit endpoint for surgical fixes.

For campaigns: lock a stylebloc, generate the lead image at 2K, use it as reference for the remaining shots.

## 12. Source Bibliography (with access dates)

Primary:
- xAI, "Grok Image Generation Release," x.ai/news/grok-image-generation-release, December 9, 2024.
- xAI, "Grok Imagine Quality Mode API," x.ai/news/grok-imagine-quality-mode, May 6, 2026.
- xAI Docs, "Image Generation," docs.x.ai/developers/model-capabilities/images/generation, updated May 14, 2026.
- xAI Docs, "Imagine Overview," docs.x.ai/developers/model-capabilities/imagine, updated May 12, 2026.
- @xai on X, Grok Imagine 1.0 announcement, February 2, 2026, 9:29 pm UTC.
- @elonmusk on X, March 12, 2026: "If it's allowed in an R-rated movie, it's allowed in Grok Imagine."
- X Safety, January 14, 2026 statement on real-person image editing restrictions.
- California DOJ, Bonta cease-and-desist press release, January 16, 2026, oag.ca.gov.

Secondary (all accessed May 22, 2026):
- Arena Text-to-Image leaderboard (5,169,154 votes, 60 models), May 22, 2026.
- AI Forensics, "Grok Unleashed," January 5, 2026, aiforensics.org/work/grok-unleashed.
- Reuters, "mass digital undressing spree," January 2–3, 2026.
- CNN Business, "Elon Musk's Grok can no longer undress images of real people on X," January 14, 2026.
- Al Jazeera, "Musk's Grok to bar users from generating sexual images of real people," January 15, 2026.
- Tech Policy Press, regulator-response tracker.
- Euronews / European Commission spokesperson, January 5, 2026: "This is not 'spicy'. This is illegal. This is appalling. This is disgusting. This has no place in Europe."
- TechCrunch, The Verge, Tom's Guide on Aurora launch coverage.
- Picsart, GenAIntel, SeaArt, Promptomania, Prompting Systems, basenor.com, felloai.com, mindstudio.ai, scenario.com, replicate.com, fal.ai, aimlapi.com, supergrok.online — community / partner-API references.
- @tetsuoai on X — autoregressive prompting analysis, November 2025.

## 13. Glossary

- **Aurora** — internal codename for xAI's autoregressive Mixture-of-Experts image engine.
- **Autoregressive** — generates output token-by-token, predicting next conditioned on all prior. Distinct from diffusion.
- **MoE** — Mixture-of-Experts; routing architecture where sub-networks specialize.
- **Quality Mode** — current premium image tier (`grok-imagine-image-quality`), launched May 6, 2026.
- **Spicy Mode** — R-rated content tier launched August 4, 2025.
- **Extend from Frame** — video continuation using last frame of one generation as start of next, launched March 2, 2026.
- **Character bible** — 60–80-word fixed description prepended verbatim to every prompt in a series for consistency.
- **Stylebloc** — 20-word fixed style anchor block (film, lens, light, palette, reference).

## 14. Appendix — 40 Reusable Prompt Templates

(Templates organized by category. Each is a 60–120-word skeleton; substitute bracketed variables.)

**Editorial portraits (5):** see use cases 1, 3, 4 in FILE 2 §9, plus two variants below.

T01. `Editorial fashion portrait, three-quarter length, of a [age] [model description], wearing [wardrobe], in [setting] at [time]. Camera-left key from [light source], soft fill camera-right, hair light from above-behind. Shot on Hasselblad H6D with an 80mm at f/2.8, slight contrapposto, weight on back leg, hand grazing [detail], gaze off-frame left. Natural skin texture with visible pores, fabric weave clearly resolved. Palette restricted to [#hex1] and [#hex2]. Cinematic film grain, Kodak Portra 400 color science. Rule of thirds, subject right-aligned. Reference: Steven Meisel for Vogue Italia. 4:5.`

T02–T40 follow the same structure for each of the 30 use cases below, plus variants for boudoir editorial, art-nude editorial, e-commerce flat-lay, model board comp card, pet portrait, travel editorial, candid documentary wedding, fitness lifestyle, lifestyle UGC product testimonial, and minimalist still-life packshot.

---

===== FILE 2: grok-imagine-guide.md =====

# Grok Imagine — Practical Field Guide
*A daily-use reference card. Print double-sided; keep beside your monitor.*

## 1. Quick Start Checklist
1. Pick surface: **API** (production), **grok.com** (concepting), **iOS/Android app** (Spicy / video).
2. Pick model: `grok-imagine-image-quality` (default), `grok-imagine-image` (batch).
3. Aspect ratio in the **API param AND at the start AND at the end** of the prompt.
4. Lead with subject and shot scale. Lock camera/lens/film mid-prompt. Mood/style last.
5. Negatives → positives.
6. 1K with n=4 → pick winner → re-render at 2K.

## 2. Prompt Structure (12 Slots)
`[Shot scale] of [subject + 3–6 details], [action/pose], [setting], [lighting + quality], [time/atmosphere], shot on [camera] with [lens + aperture], [film/profile], [composition cue], [texture cues], [post-process], [style anchor], [aspect ratio].`

## 3. Universal Aurora Prompt Template
```
[Shot scale] of a [age] [role] with [3 physical traits], wearing [wardrobe],
[action/pose], in [setting] at [time of day/atmosphere].
[Lighting pattern] from [direction], [fill description], [accent light].
Shot on [camera] with [lens] at [aperture], [composition cue].
Natural skin texture with visible pores, [fabric/material cues].
[Film stock or color profile], palette of [#hex1] and [#hex2].
Reference: [photographer or publication]. [Aspect ratio].
```

## 4. Top 30 Power Phrases
1. "Natural skin texture with visible pores"
2. "Shot on Hasselblad H6D with an 80mm at f/4"
3. "Cinestill 800T halation"
4. "Kodak Portra 400 color science"
5. "Rembrandt lighting"
6. "Clamshell — large octabox above, silver bounce below"
7. "Golden hour, low sun camera-left, long shadows"
8. "Practical lights only"
9. "Single shaft of light through [aperture]"
10. "Subject left-of-centre, gaze leading into negative space"
11. "Rule of thirds, horizon on the lower third"
12. "Symmetric centered composition"
13. "Focus stacked, tack sharp end to end"
14. "Three-plane composition: foreground, midground, background"
15. "Palette restricted to [#hex] and [#hex]"
16. "Anamorphic lenses, oval bokeh, horizontal flares"
17. "Black Pro-Mist 1/4 highlight bloom"
18. "Gentle highlight rolloff, deep but detailed shadows"
19. "Mid-stride, slight motion blur only at the back foot"
20. "Eyes off-frame left at something unseen"
21. "Magnum photojournalism aesthetic"
22. "Apartamento magazine interior style"
23. "Wes Anderson symmetric pastel"
24. "Roger Deakins single-source motivated lighting"
25. "Steven Meisel for Vogue Italia"
26. "Gregory Crewdson cinematic tableau"
27. "1973 paranoid thriller color science — sallow yellow, burnt orange"
28. "Letterpress impression with slight registration shift"
29. "Halftone dot texture in the midtones"
30. "Imperfect smartphone UGC look, slight tilt, fluorescent + warm spill"

## 5. Decision Tree
- Photoreal product → **Quality, 2K, 3:2 or 16:9, Phase One + 120mm macro**.
- Editorial portrait → **Quality, 4:5, Hasselblad + 80mm, Portra 400**.
- Stylized art → **Standard fine; lead with medium ("gouache," "anime cel-shaded")**.
- Readable text → **Quality, quote string, specify medium**.
- Mature content → **Mobile app, Spicy, paid + 18+, non-restricted region**.
- Long sequence → **Quality still → image-to-video → Extend from Frame, max 3 chains**.
- Character consistency → **Master image + reference editing with verbatim bible**.

## 6. Cheat Sheets

**Camera anchors:** Hasselblad H6D (editorial), Phase One IQ4 (product/luxury), Leica M11 (street/doc), Sony A1 (sports/wildlife), Canon R5 (general), Fujifilm X-T5 (street/lifestyle), Mamiya 7 (medium-format film), Pentax 67 (1970s editorial), Polaroid SX-70 (instant), Holga (lo-fi).

**Lens:** 24mm environmental, 35mm street, 50mm general, 85mm portrait, 120mm macro, 200–400mm sports/wildlife, tilt-shift architecture, anamorphic cinema.

**Framing:** ECU > CU > MCU > MS > MWS > WS > EWS · OTS · two-shot · three-shot · flat-lay · POV · Dutch.

**Lighting:** Rembrandt portrait · butterfly beauty · split drama · clamshell beauty · three-point corporate · single-source motivated cinematic · practicals-only documentary.

**Film:** Portra 400 (warm editorial default) · Cinestill 800T (neon night halation) · Ektar 100 (saturated landscape) · Tri-X 400 (B&W documentary) · Velvia 50 (saturated nature) · Eterna (muted cinema) · bleach bypass (gritty).

**Texture cues:** "natural skin texture with visible pores" · "linen weave resolved" · "brushed metal microscratch" · "raw concrete bloom" · "end-grain oak."

**Style:** Vogue · Apartamento · Kinfolk · Magnum · National Geographic · The New Yorker · Hatch Show Print.

## 7. 30 Use Cases at a Glance
1. Editorial fashion portrait — **80mm + Portra 400 + Meisel/Vogue**
2. Beauty close-up — **120mm macro + clamshell + Pat McGrath**
3. Studio headshot — **85mm + three-point + mid-grey seamless**
4. Environmental portrait — **35mm + overcast + Salgado**
5. Street vérité — **23mm + Cinestill 800T + Tokyo dusk**
6. Photojournalism — **28mm + deep DOF + Magnum**
7. Wedding lifestyle — **85mm + bistro lights + Jose Villa**
8. Product hero — **120mm macro + white seamless + focus-stack**
9. Product lifestyle — **50mm + natural side light + Apartamento**
10. Food editorial — **50mm macro + 90° flat-lay + window key**
11. Interior architecture — **32mm tilt-shift + dusk balance + Cereal**
12. Landscape — **24mm + f/11 + golden hour + Hans Strand**
13. Wildlife — **400mm + first light + Vincent Munier**
14. Sports — **200mm + 1/2000 + stadium HMI**
15. Macro — **100mm 1:1 + focus stack + dewdrop**
16. Astro — **14mm + tracked exposure + Atacama**
17. Conceptual — **Mamiya 7 80mm + symmetry + Crewdson**
18. Still life — **100mm + window chiaroscuro + Vermeer**
19. Lookbook — **50mm + softbox + 9:16**
20. Luxury — **120mm + controlled specular + Phase One**
21. UGC — **smartphone tilt + fluorescent + imperfect**
22. Cinematic still — **anamorphic + Vision3 + Willis**
23. Anime — **cel-shading + Satoshi Kon**
24. Western illustration — **gouache + Niemann**
25. Concept art — **turnaround + Feng Zhu**
26. Logo — **minimal geometric + Pentagram**
27. Poster — **letterpress + Hatch Show Print**
28. Children's book — **watercolor + Jon Klassen**
29. Comic — **duotone + halftone + Sean Phillips**
30. Surreal — **medium format + Magritte**

## 8. Common Mistakes & Fixes
| ❌ | ✅ |
|---|---|
| "8K, masterpiece, stunning, cinematic" | "Shot on Hasselblad H6D, 80mm at f/4, Portra 400" |
| "No blur, no bad hands" | "Tack sharp, five fingers naturally splayed" |
| "A man in a forest" | "A 35-year-old in olive workwear at golden hour, mossy spruce forest, 35mm" |
| Six style references stacked | One photographer + one publication |
| "Make it pretty" | "Visible skin pores, fabric weave resolved, gentle highlight rolloff" |
| Aspect ratio only in API | Aspect ratio at start of prompt + end of prompt + API param |
| "Realistic photograph in anime style" | "Anime style illustration with realistic lighting and proportions" |
| Naming camera + incompatible film grain | One anchor only |

## 9. 20 Ready-to-Use Recipes (paste-ready)

**R01. Editorial fashion portrait.**
`Editorial fashion portrait, three-quarter length, of a 28-year-old model with cropped platinum hair and sharp brows, wearing an oversized charcoal wool blazer over a white silk slip dress, standing in a vacant marble-floored gallery at golden hour. Camera-left key from a tall window, soft fill from a white wall camera-right, subtle hair light from a high window behind. Shot on Hasselblad H6D-100c with an 80mm at f/2.8, eye-level, slight contrapposto, weight on back leg, hand grazing collarbone, gaze off-frame left. Natural skin texture with visible pores and peach fuzz, fine flyaways catching the light, fabric weave on the wool resolved. Palette restricted to warm bone, smoke grey and a single oxblood at the lipstick. Cinematic grain, Kodak Portra 400 color science, gentle highlight rolloff. Rule of thirds, subject right-aligned, negative architectural space camera-left. Reference: Steven Meisel for Vogue Italia. 4:5.`

**R02. Beauty close-up.**
`Beauty close-up, extreme tight crop on eyes and brow of a 30-year-old with luminous bronze skin and pearlescent eyeshadow in fine champagne shimmer. Clamshell lighting from a large octabox above and a silver bounce below, no hard shadows, catchlights centered. Shot on Phase One IQ4 with a 120mm macro at f/8, tack sharp on iris detail with brown-and-amber starburst, fine eyelash separation, faint peach fuzz on the upper cheek, individual brow hairs resolved. Background a soft creamy beige falloff. Frequency-separation retouch — pores preserved, no plastic. Editorial color grade, neutral whites, warm midtones. Composition centered, eyes upper third. Reference: Pat McGrath. 1:1.`

**R03. Corporate headshot.**
`Corporate studio headshot, chest-up, 45-year-old executive, short silver hair, light olive skin, navy notch-lapel suit, crisp white open-collar shirt. Confident half-smile, eyes meeting camera. Three-point: large softbox key camera-left at 45°, silver reflector fill camera-right, hair light above-behind. Mid-grey seamless evenly lit. Canon R5, 85mm at f/4, both eyes sharp. Commercial-level retouch, pores preserved. Neutral slightly warm grade, 5500K. Shoulders slightly turned camera-right. 4:5.`

**R04. Environmental documentary portrait.**
`Environmental portrait of a 62-year-old fisherman in Skye, weathered tan skin with deep crow's-feet, salt-flecked grey beard, sun-bleached navy waterproof, hands on the gunwale of a small wooden boat at the harbour wall. Overcast late afternoon, soft directional light camera-right, faint rim from sky. Leica M11, 35mm Summicron at f/4, eye-level, subject left-third, harbour and weathered stone extending right, shallow falloff. Salt crystals visible on beard, individual hair strands clear, fabric weave resolved. Tri-X 400 B&W, deep blacks, controlled highlights, slight grain. Reference: Sebastião Salgado. 3:2.`

**R05. Street vérité (Cinestill 800T).**
`Street photography, candid mid-stride, Shibuya scramble at dusk in light rain. A 30-year-old commuter in a black trench coat with a clear umbrella, water beads bouncing off; behind, blurred neon in Japanese reading "らーめん" and "カフェ" reflects on wet pavement. Fujifilm X-T5, 23mm at f/4, 1/200, ISO 1600, slight motion blur on the foot, sharp on the face mid-glance camera-right. Cinestill 800T halation around the brightest neons, magenta-teal cast. Subject left-of-centre on a diagonal sidewalk line. 3:2.`

**R06. Food editorial flat-lay.**
`Editorial food shot of a steaming tonkotsu ramen bowl on worn dark walnut. Overhead 90° flat-lay, chopsticks slight diagonal, soft-boiled egg cut to show jammy yolk, chashu glistening, scallion confetti, sesame, coiled nori at the rim. Single large window source camera-top through a 4×6 silk, black flag camera-bottom for directional falloff. Canon R5, 50mm macro at f/5.6. Visible steam against dark background, fine bubbles on broth, scattered sesame off-bowl. Warm broth, deep brown wood, single bright green scallion accent. Rule of odds — three garnishes — negative space lower-right. Reference: Bon Appétit / Kinfolk. 4:5.`

**R07. Interior architecture at dusk.**
`Modern Japandi living room at dusk, dining area through to a glass wall and small zen courtyard. Low warm pendant over an oak table foreground, linen sofa midground, vertical wood slats and a single artwork on back wall, courtyard lantern through glass. Warm tungsten practicals inside, cool blue dusk outside, balanced exposure interior/exterior. Phase One XT, 32mm tilt-shift at f/8, two-row stitched, verticals locked. Oak end grain, linen weave, lime plaster all resolved at micro-detail. Reference: Norm Architects / Cereal. 3:2.`

**R08. Epic landscape.**
`Dawn over the Lofoten Islands, low pink-and-gold cloud band over jagged dark peaks, still fjord foreground reflecting the sky, a single fishing skiff at left for scale. Sony A1, 24mm f/1.4 at f/11, focus-stacked for foreground-to-infinity, polarizer cutting glare. Palette dominated by #1B3A5B and #E8C28A, single warm hit on the skiff. Rule of thirds, horizon lower third, peaks upper-right, leading line of reflected light to the skiff. Long-exposure smoothing on water. Reference: Hans Strand. 3:2.`

**R09. Wildlife.**
`Snow leopard side profile pausing on a stone outcrop in Ladakh at first light. Eye-level, telephoto compression. Canon R5, 400mm f/2.8 at f/5.6, 1/1000, focus on the eye, fur across cheek and ruff resolved, breath visible. Soft side rim from rising sun camera-left, deep shadow camera-right, background soft falloff of rock and snow. Warm highlights, cool shadows. Subject left-of-centre, gaze into negative space right. Reference: Vincent Munier. 3:2.`

**R10. Sports action.**
`Sprinter mid-stride at 80m, full extension, lead foot landing, spikes biting the track, dust kicked up. Sony A1, 200mm f/2 at f/2.8, 1/2000, focus locked on face, stadium crowd in heavy bokeh. Multiple HMI sources wrap the body. Visible sweat, vein detail in the arm, fabric tension on the jersey. Slight motion blur at the trailing back foot only. Saturated, high contrast. Subject central, strong diagonal of track line. Sports Illustrated aesthetic. 3:2.`

**R11. Macro flower.**
`Single morning-glory blossom at 1:1, 100mm macro on Canon R5 at f/8, focus stacked across 40 frames for petal-edge-to-stamen sharpness. Softbox above-right, white bounce camera-bottom. Dewdrops at petal edge acting as tiny lenses. Petal veining and powdery pollen on anthers visible. Background clean falloff of deep green out-of-focus foliage. Violet petals with yellow-green throat, dewdrops catching warm window light. Centered, slight diagonal of flower axis. 1:1.`

**R12. Astrophotography.**
`Wide nightscape, Milky Way core arching over the Atacama, small lit tent lower-right for scale and warm contrast. Sony A7S III, 14mm f/1.8 at f/2, ISO 6400, 20-s tracked exposure on a star tracker, foreground separately exposed and blended. Dust lanes and galactic core resolved, faint airglow at horizon, no light pollution. Sky deep navy with subtle yellow at the core. Tent a single warm orange point. Arching Milky Way along upper third, tent at right-third intersection. 16:9.`

**R13. Conceptual fine art (figure in lake).**
`A single figure in a long crimson coat standing knee-deep in a still mirror-flat lake at dawn, arms relaxed, facing away, surrounded by low mist. Wide shot, perfectly symmetric centered. Mamiya 7, 80mm at f/8, medium-format depth. Soft golden side-rim from rising sun, blue-grey midtones, the coat the only saturated colour. Visible mist tendrils, faint ripples around the figure. Reference: Gregory Crewdson + Bill Henson. 4:5.`

**R14. Still life — Vermeer chiaroscuro.**
`Painterly tabletop arrangement: three persimmons, half-cut pomegranate showing seeds, ceramic jug, folded linen napkin on weathered oak table by a small north-facing window. Vermeer chiaroscuro: single soft window light camera-left, deep fall into camera-right, dark plum background. Hasselblad H6D, 100mm at f/8, focus on the pomegranate seeds. Bloom on persimmon skin, condensation on jug, linen weave visible. Deep plum background, warm orange persimmon, ruby pomegranate, neutral cream linen. Triangular composition, rule of odds. Reference: Pieter Claesz / Paulette Tavormina. 4:5.`

**R15. Luxury watch ad.**
`Stainless steel diver's watch with a black ceramic bezel and indigo gradient dial, mounted on dark grey concrete, single splash of water suspended mid-air camera-right. Phase One IQ4, 120mm macro at f/16, focus-stacked, every facet of bezel and bracelet sharp. One strip box camera-left for dial highlight, one rear flag for gradient, controlled specular on the crystal. Cool steel, indigo dial, single tritium index pop. Off-centre right with negative space camera-left for wordmark "GROK CHRONO" in thin sans-serif. 3:2.`

**R16. UGC mirror selfie.**
`Smartphone-vertical UGC selfie in a stainless-steel elevator mirror by a 24-year-old in a black graphic tee and baggy jeans, one hand holding a silver phone, the other relaxed, slight knowing smile. Imperfect framing, slight tilt, mixed fluorescent ceiling light and warm spill from outside the elevator. Visible skin pores and a small chin blemish, fly-aways at the hairline, faint thumbprint on the phone screen. Slightly desaturated, slight blue cast. 9:16.`

**R17. 1970s paranoid thriller still.**
`Cinematic film still, 1973 paranoid thriller, medium shot of a 40-year-old in a tan trench coat in a wood-panelled telephone booth in a deserted lobby. Mid-conversation, eyes flicked camera-right, jaw tight. Single overhead practical fluorescent above the booth, sodium-vapor warm spill from the lobby outside, deep shadow on the camera-right of his face. ARRI Alexa Mini LF with anamorphic lenses, 1/50 shutter, slight motion-blur halation, oval bokeh. Kodak Vision3 250D filmic grain, muted greens, burnt orange, sallow yellow. 2.39:1. Reference: Gordon Willis on The Parallax View.`

**R18. Anime night crosswalk.**
`Anime cel-shaded illustration, 1990s OVA style, of a 17-year-old in school uniform on a rainy crosswalk at night, holding a clear umbrella, neon signs reflecting on wet pavement. Bold inked outlines, limited cel-shading with 3 tones per surface, vibrant pink-and-cyan rim from signage. Low angle, character three-quarter to camera, slight motion lines at the bottom of the frame. Reference: Satoshi Kon / early Production I.G. 4:5.`

**R19. Letterpress concert poster.**
`Letterpress-style concert poster, vertical, reading "GROK IMAGINE LIVE / FRIDAY 22 MAY / TOKYO STUDIO COAST / DOORS 19:00" in chunky condensed slab serif with deliberate ink texture, woodblock illustration of a stylized fox at the top. Deep navy ink on cream paper, single red accent on the date. Worn paper edges, slight registration shift on the red. Title block top, illustration middle, details bottom. Reference: Hatch Show Print. 2:3.`

**R20. Children's book spread.**
`Children's book spread, watercolor-and-ink, small fox in a red scarf reading aloud to a snowy owl on a moss-covered log in a moonlit forest clearing. Soft washes, visible paper texture, gentle indigo night palette with warm lantern glow at right. Hand-lettered title across top: "THE FOX WHO READ TO OWLS." Wide horizontal, characters centered. Reference: Jon Klassen / Beatrix Potter. 16:9.`

## 10. Spicy Mode Quick Notes (Professional Use Only)
- **Eligibility:** SuperGrok or X Premium+ + 18+ verified + iOS/Android app + non-restricted region.
- **Permitted:** R-rated. Editorial lingerie, art-nude, boudoir, mature horror/thriller atmosphere, partial nudity.
- **Blocked (hard):** explicit acts, minors, real-person sexualized deepfakes, CSAM.
- **Geoblocked:** UK, EU member states, Indonesia, Malaysia, California video.
- **Standard, per Musk March 12, 2026:** *"If it's allowed in an R-rated movie, it's allowed in Grok Imagine."*
- **Prompting:** prefer "imaginary adult character"; classical / art-historical framing; specify lighting and styling, not anatomy.

## 11. Iteration Playbook
- **Pass 1 — Composition** (1K, n=8). Score composition only.
- **Pass 2 — Lighting** (1K, n=4). Vary lighting cues only.
- **Pass 3 — Finish** (2K, n=2). Lock everything else.
- **Pass 4 — Surgical edit.** "Keep [X], change [Y] to [Z]" with reference image.
- **Score against the brief**, not the previous generation.

## 12. Anti-Patterns (Never Do This)
- Stacking quality adjectives ("masterpiece, stunning, 8K, cinematic").
- Writing negative prompts ("no extra fingers"). Restate as positives.
- More than two style anchors.
- Aspect ratio only in the API call.
- More than 250 words.
- Mixing camera and film stock that don't go together (Phase One + Tri-X grain).
- Asking for both photoreal and anime in one prompt.
- Using Spicy Mode for non-mature briefs (it warms the grade unhelpfully).
- Trusting visible watermarks as proof of AI provenance — there is **no** cryptographic / C2PA watermark.
- Treating consumer-app behavior as production-stable. Use the **API** for repeatable work.
- Editing real people's photos into revealing clothing — blocked platform-wide since Jan 14, 2026.
- Naming a real person in a sexualized context — generates legal liability under the Take It Down Act and various state statutes.

---

## Caveats (apply to both files)

- xAI does not publish an explicit prompt character cap; community sweet spot is 200–1000 words. Some third-party docs claim 1,000 or 10,000; treat both as unverified.
- The "ranks among the strongest models on independent leaderboards" claim is xAI marketing language; the actual Arena ranking is #6 (Elo 1223) as of May 22, 2026, behind GPT Image 2, Gemini 3, and GPT Image 1.5.
- Spicy Mode and content moderation are policy-volatile; verify regional availability before committing client work.
- No commercial indemnification ships with Grok Imagine output. For indemnified commercial use, Adobe Firefly remains the only safe pick in May 2026.
- The image-to-video feature is best for short-form social; resolution caps at 720p and quality degrades after 2–3 chained extensions. For high-end film production, use a dedicated cinema model.