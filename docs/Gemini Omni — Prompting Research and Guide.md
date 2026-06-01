# Gemini Omni — Cinematic Prompting Research Report

> **Two deliverables follow in this single response:**
> 1. `gemini-omni-video-research.md` — the full research report
> 2. `gemini-omni-video-guide.md` — the practical reference card
>
> Copy each section between its file markers into a `.md` file of the matching name.

---

# ===== FILE 1: `gemini-omni-video-research.md` =====

# Gemini Omni — Cinematic Prompting Research Report (Google DeepMind, May 2026)

## Verification Note

The user referred to "Gemini Omni" released May 2026. **This is confirmed.** Google DeepMind officially launched the **Gemini Omni** family at **Google I/O 2026 on May 19, 2026**, with **Gemini Omni Flash** as the first publicly released model in the family. The primary sources are Google's official blog post "Introducing Gemini Omni" authored by Koray Kavukcuoglu (CTO, Google DeepMind & Chief AI Architect, Google) published 2026-05-19 at blog.google, and the model home page at deepmind.google/models/gemini-omni. This report therefore covers **Gemini Omni Flash** as the current flagship for cinematic AI video production, with Veo 3.1 treated as the parallel specialized model that Google maintains for dedicated photoreal video generation.

The "Omni" brand sits alongside, not on top of, Veo. Google DeepMind product director Nicole Brichtova told TechCrunch on May 19, 2026 that Omni is "the next step towards the progression of combining the intelligence of Gemini with the rendering capabilities of our media models." Veo 3.1 remains GA on Vertex AI; Omni is the conversational, any-to-any sibling.

---

## 1. Executive Summary

Gemini Omni Flash is Google DeepMind's first "any-to-any" multimodal generative model and is, as of May 22, 2026, the company's current flagship video model for cinematic and conversational creation. It accepts any combination of text, images, audio, and video as input and produces high-quality video with synchronized audio as output. Architecturally, it fuses four previously separate DeepMind systems — Gemini (reasoning), Veo (rendering), Genie (world simulation), and Nano Banana (image editing) — into a single model with persistent state across multi-turn edits.

For filmmakers, ad creatives, and video producers, three properties matter most. First, **conversational multi-turn editing**: once you have a base clip, you can issue plain-English edits ("make the violin invisible", "change the camera angle to over the violinist's shoulder", "transport her to the image environment") and Omni preserves character identity, scene context, and physics across turns. No competitor — Seedance 2.0, Kling 3.0, Runway Gen-4.5, Sora 2 — ships this in the same form today. Second, **world-knowledge grounding**: Omni's reasoning engine produces explainer-style outputs (claymation protein folding, alphabet sizzle reels, quantum-computing visualizations) that competitors cannot match with text prompting alone. Third, **reference fusion**: one prompt can blend a portrait image, a motion video, a beat audio, and a written brief into a single coherent shot.

The launch caveats are real. **Clips cap at 10 seconds** at launch — per Brichtova in the TechCrunch briefing this is "not a model limitation, but rather a decision." Output **resolution is not publicly published** as a numeric specification by Google; the Flow help center references "1080p video upscaling" only as a separate Pro-tier feature. **API access is not yet live** as of May 22, 2026 — the official launch blog says only "in the coming weeks." **Raw cinematic fidelity at the Flash tier trails Seedance 2.0** on third-party benchmark testing; multiple independent reviewers (Build Fast with AI, Medium analyses, PixVerse) place Omni Flash one tier below Seedance on pure visual fidelity at 4K. **Speech and audio editing of existing footage** is deliberately withheld — Google's stated position is that voice-cloning-in-video is the riskiest deepfake vector and they are "still working to test this." Use Veo 3.1 via Vertex AI for production work that needs a stable API and 4K output today; use Omni for ideation, conversational refinement, social and explainer work, and any pipeline where multi-turn editing matters more than maximum resolution. The Pro variant — Gemini Omni Pro — has been teased by DeepMind for a future release "when we feel like we're at a point where we have a step change above Flash" (Brichtova), but no date is published.

---

## 2. Model Foundations & Capability Matrix

### 2.1 Officially documented specifications (Google sources only)

| Parameter | Value | Source |
|---|---|---|
| Model family | Gemini Omni | blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-omni/ |
| First model in family | Gemini Omni Flash | Same |
| Launch date | May 19, 2026 (Google I/O 2026) | Same |
| Clip length options in Flow | 4s, 6s, 8s, 10s | support.google.com/flow/answer/16352836 |
| 10-second tier | Plus/Pro/Ultra subscribers only | Same |
| Inputs | Text, image, audio, video | blog.google launch post |
| Audio input limitation at launch | Voice references only; other audio types "coming soon" | Same |
| Image upload limit (Gemini app) | 1 video + up to 5 images per generation | support.google.com/gemini/answer/16126339 |
| Video upload limit (Flow) | 60 seconds, 1 GB; trim to 10s for edit | support.google.com/flow/answer/16935718 |
| Voice reference limit | 1 per generation | support.google.com/flow/answer/16353334 |
| Output | High-resolution video with audio | deepmind.google/models/gemini-omni |
| Watermark | SynthID (imperceptible) + C2PA Content Credentials, on every output | deepmind.google/models/gemini-omni |
| Aspect ratio control | Landscape default; Portrait toggle; matches uploaded reference | support.google.com/gemini/answer/16126339 |
| Avatar feature | Recorded selfie + voice consent flow; English only; not available in EEA, Switzerland, UK; 18+ only | support.google.com/gemini/answer/16984474 |
| API status (as of 2026-05-22) | Not yet live; "coming in the coming weeks" | blog.google launch post |
| Pricing — Free (YouTube Shorts/Create) | $0 | blog.google launch post |
| Pricing — Google AI Plus | $7.99/mo, 200 Flow credits, includes Omni Flash | labs.google/flow/about |
| Pricing — Google AI Pro | $19.99/mo, 1,000 Flow credits, +1080p upscaling, +video-to-video edit, +avatars | Same |
| Pricing — Google AI Ultra | $99.99/mo, 10,000 Flow credits | Same |

### 2.2 Items NOT publicly documented by Google

The following are commonly cited in third-party coverage but are not confirmed on Google's own product pages: exact native output resolution (720p / 1080p / 4K); native frame rate (24 / 30 / 60 fps); explicit enumeration of supported aspect ratios as discrete values (16:9, 9:16, 1:1); the "deployment cap vs. model limit" framing (this is a quote from Brichtova in TechCrunch, not a Google-page claim); a model card with published benchmark scores. Treat anything from third-party sites on these numbers as community-verified or speculative.

### 2.3 Architecture (per DeepMind and accompanying coverage)

Omni Flash is described by Google DeepMind CTO Koray Kavukcuoglu as "a model that can create anything from any input — starting with video." Independent technical breakdowns (Build Fast with AI, May 21, 2026; Apidog; BridgeChronicle citing Hassabis) describe the model as fusing four underlying systems: **Gemini** (reasoning, world knowledge, language understanding), **Veo** (frame-level rendering and motion), **Genie 3** (world simulation, physics, environmental dynamics), and **Nano Banana** (image-level conversational editing). Demis Hassabis at I/O 2026 positioned the result as "a world model AI that can understand and simulate the world." This architecture is what enables the persistent state across multi-turn editing — every instruction "builds on the last."

### 2.4 Capability matrix vs. predecessors and Veo

| Capability | Veo 3 (May 2025) | Veo 3.1 (Oct 2025, Jan 2026 4K update) | Gemini Omni Flash (May 2026) |
|---|---|---|---|
| Native audio | Yes (launch feature) | Richer dialogue + SFX + ambience | Yes; voice references supported, broader audio inputs roadmap |
| Max clip length | 8s | 8s base, 60s via Extend in Flow | 10s |
| Output resolution (public) | 720p | 720p / 1080p / 4K (upscale on Ultra) | Not publicly published; 1080p upscaling Pro-tier |
| Multimodal input | Text, image | Text, image, up to 3 reference images | Text, image, audio (voice), video |
| Conversational edit | No | Limited via Flow Scene Builder | Yes — native multi-turn |
| Character consistency | Limited | Ingredients to Video (up to 3 refs) | Yes — anchored across turns |
| Physics realism | Strong | Improved | Strongest (Genie integration) |
| World-knowledge grounding | No | No | Yes (Gemini integration) |
| API | Vertex AI GA | Vertex AI GA | Not yet — "coming weeks" |
| Watermark | SynthID | SynthID | SynthID + C2PA |

---

## 3. Competitive Landscape Comparison

| Model | Vendor | Released | Max length | Resolution | Native audio | Multimodal input | Key differentiator |
|---|---|---|---|---|---|---|---|
| **Gemini Omni Flash** | Google DeepMind | May 19, 2026 | 10s | Not published; 1080p upscale | Yes (voice ref input) | Text+image+audio+video | Conversational multi-turn editing; world knowledge |
| Veo 3.1 | Google DeepMind | Oct 2025; 4K Jan 2026 | 8s base; 60s extend | 720p/1080p/4K | Yes | Text+image (3 refs) | Photoreal cinema; Vertex AI GA |
| Sora 2 / Sora 2 Pro | OpenAI | Sep 30, 2025 | 10–25s | 1080p (Pro) | Yes | Text+image | Physics realism; consumer app discontinued April 26, 2026; API discontinuation September 24, 2026 (per OpenAI Help Center, "What to know about the Sora discontinuation") |
| Runway Gen-4.5 | Runway | December 1, 2025 | ~5–10s | up to 1080p | No (post-prod) | Text+image | "With 1,247 Elo points, Gen-4.5 currently holds the top position in the Artificial Analysis Text to Video benchmark, surpassing all other models" per Runway's official research post |
| Kling 3.0 | Kuaishou | February 5, 2026 (per Kuaishou Technology IR release on GlobeNewswire) | 15s | Native 4K, 60fps | Yes — Chinese, English, Japanese, Korean, and Spanish, with additional dialect and regional accent capabilities | Text+image+ref vid | Multi-shot storyboard director mode |
| Seedance 2.0 | ByteDance | February 12, 2026 (per ByteDance SEED lab and Atlas Cloud blog) | 4–15s | Up to 1080p | Yes (native co-gen) | Up to 9 images + 3 videos + 3 audio | Built on a 4.5B parameter Dual-Branch Diffusion Transformer architecture (per Segmind API docs); #1 Artificial Analysis Elo 1,269 |
| Luma Ray 3 | Luma Labs | Late 2025 | Up to 60s (Ray 2) | 4K HDR | No | Text+image | HDR; natural-phenomenon physics |
| Pika 2.5 | Pika Labs | 2026 | 1–10s | 1080p | No (silent) | Text+image+keyframes | Pikaffects (melt/explode); Pikaframes; cheap entry |
| Higgsfield (Apr 29 2026 model) | Higgsfield | April 29, 2026 | ~10s | 1080p | No | Text+image | Classic-cinematography camera presets |
| Meta Movie Gen | Meta | Research 2024; pilots 2025–26 | 16s | 1080p @ 16fps | Yes (Movie Gen Audio 13B) | Text+image | Personalization from one reference image; planned Instagram integration |

**Verdict for cinematic production today:** Use **Veo 3.1 via Vertex AI** when you need a stable API, 4K output, and the longest single-call clip in the Google stack. Use **Gemini Omni Flash** when you need conversational editing, multi-input reference fusion, or world-knowledge-grounded explainers. Use **Seedance 2.0** or **Kling 3.0** when raw cinematic fidelity is the only metric that matters and you can tolerate weaker editing workflow. Avoid building production roadmaps on **Sora 2** given the September 24, 2026 API shutdown.

---

## 4. Prompt Anatomy — Evidence-Based Structure

The official DeepMind Gemini Omni prompt guide (deepmind.google/models/gemini-omni/prompt-guide/) is the primary source for prompt structure. It is explicit that Omni does **not** require the same precision as Veo: *"With Veo, you need to share precise instructions to get the best results. But with Gemini Omni, you don't have to be as prescriptive with your prompt. Instead, tell Omni what you want to create — and watch the model's reasoning and world knowledge bring the details to life."* This is a meaningful structural difference from every other model in this report.

### 4.1 Format preference

Omni prefers **natural-language paragraphs** that read like a director's brief, not structured JSON or rigid shot-list blocks. Every official example on the DeepMind prompt guide and the Gemini Omni model page uses paragraph form. Sub-clauses are separated by commas and periods rather than headers. The model still respects shot-list-style prompts (Clip 1 / Clip 2 patterns, inherited from Veo prompt engineering) but does not require them. **OFFICIAL.**

### 4.2 Six elements the official guide names

The DeepMind prompt guide enumerates six elements to think about when writing prompts: **Shot framing and motion**, **Style**, **Lighting**, **Location**, **Action**, and (added by the reference section) **References**. Combine a subset; you do not need all six in every prompt. **OFFICIAL.**

### 4.3 Positional weighting

The first sentence anchors the scene. In the official examples ("A marble rolling fast on a chain reaction style track, continuous smooth shot." / "claymation explainer of protein folding, everything is made out of clay, no hands, stop motion, accurate") the opening clause defines subject and primary action. Subsequent clauses refine style and constraints. **COMMUNITY-VERIFIED** consistently across third-party walkthroughs (Build Fast with AI, PixVerse, Kingy AI, Replicate's Veo 3.1 guide which Omni inherits from).

### 4.4 Negative prompts

Negative prompting is officially supported. The DeepMind prompt guide contains the example *"A skeuomorphism stop motion explainer about how the brain hippocampus works with a compelling voiceover. Don't add seahorses. No voice cuts at the end. Don't add text."* Phrase negatives as plain English ("Don't add X", "No Y", "without Z"), not as a separate negative-prompt field. **OFFICIAL.**

### 4.5 Reference syntax

Omni accepts mixed references in the prompt itself with angle-bracket syntax. Official DeepMind examples include *"The birds from \<video\> loosely form the imperfect shape of a bird based on \<image\>. They move to the music from \<audio\> and dissipate as they fly"* and *"Dynamic sci-fi film style video based on image_0.png. Elements light up similar to video_0.mp4 synchronized to the beat of the music from audio_0.wav."* Both `<image>` style and `image_0.png` style work. **OFFICIAL.**

### 4.6 Conversational edit prompts

Edits are short imperative sentences: *"Change the butterfly to a bee"*, *"Make the violin invisible"*, *"Change the camera angle to be over the violinist's shoulder"*, *"Transport the violinist to the image environment"*. DeepMind research engineer Gabe Barth-Maron told TechCrunch on May 19, 2026 that *"editing prompts will need to be highly specific, otherwise Omni risks over-editing or unintentionally altering elements the user wanted to keep."* The corollary: specify what to keep ("Edit this keeping everything the same. Add animated motion effects coming out of the skateboard"). **OFFICIAL.**

### 4.7 Aspect ratio in-prompt

Although Flow exposes a Landscape/Portrait toggle, official DeepMind examples also embed ratios in the prompt itself ("Cinematic, 16:9"). Belt-and-suspenders: set the toggle AND mention the ratio in the prompt. **COMMUNITY-VERIFIED.**

### 4.8 Token / length

Google has not published a token or character limit for Omni prompts. Veo 3.1's 2,000-character limit (per third-party docs at MindStudio) is a reasonable working assumption — but for Omni the official guidance is the opposite of Veo: keep prompts shorter and trust the model's reasoning, then iterate via conversational edits.

---

## 5. The Cinematic Vocabulary — Sections A through K

### A. Camera body & format

**Official Omni camera vocabulary** (from the DeepMind prompt guide, verbatim): *"natural smartphone zoom", "film camera", "webcam style", "static", "locked off", "fixed".* For non-camera-type framing direction: *"one continuous shot", "oner"* are explicitly named.

**Cinematic phrases that work (community-verified):** "shot on 35mm film with natural grain", "16mm documentary style", "Super 8 home movie aesthetic", "anamorphic lens with horizontal flares", "ARRI Alexa look", "RED dragon sensor", "vintage analog video", "VHS look", "broadcast television look", "found-footage handheld".

**Pitfall:** Stacking too many camera-body descriptors collides (e.g., "shot on 35mm film with anamorphic lens and Super 8 grain" produces incoherent output). Pick one anchor.

### B. Lens language

Focal lengths the model understands: 14mm, 18mm, 24mm, 28mm, 35mm, 50mm, 85mm, 105mm, 135mm, 200mm. Aperture/DOF: "shallow depth of field", "deep focus", "f/1.4 bokeh", "creamy bokeh", "rack focus", "split diopter". Lens artifacts: "anamorphic lens flares", "horizontal flares", "vignetting", "chromatic aberration", "diopter close-up". Filters: "polarizer", "ND filter", "diffusion filter", "Pro-Mist", "Black Magic mist".

**Omni-specific behavior:** unlike Veo 3.1, where you had to specify "85mm" for compression, Omni's reasoning layer will infer focal length from descriptive cues like "tight portrait compression" or "wide environmental establishing shot."

### C. Camera movement — exhaustive

Movement vocabulary the model executes reliably: **Static**: "locked off", "tripod static", "fixed". **Pan/Tilt/Roll**: "slow pan left/right", "whip pan", "tilt up/down", "dutch tilt 35°", "barrel roll". **Dolly/Truck**: "dolly in", "push in", "punch in", "dolly out", "truck left/right", "pedestal up/down". **Crane/Jib**: "crane shot", "jib up", "techno-crane swoop". **Steadicam/Gimbal**: "steadicam follow", "gimbal glide", "smooth orbit". **Handheld**: "handheld urgency", "verité handheld", "shaky cam". **Drone**: "drone push-in", "aerial reveal", "FPV chase". **Speciality**: "Snorricam", "bullet-time", "dolly zoom" (Vertigo effect), "snap zoom", "match cut", "whip pan transition". **Direction verbs Omni explicitly names in its prompt guide:** "push in", "punch in", "dolly zoom" (OFFICIAL).

### D. Shot scale & framing

ECU (extreme close-up), CU (close-up), MCU (medium close-up), MS (medium), MWS (medium wide), WS (wide), EWS (extreme wide). OTS (over-the-shoulder), two-shot, three-shot, group shot. Angles: low angle hero, high angle surveillance, worm's eye, bird's eye, dutch angle, POV, reverse angle. Composition: rule of thirds, center punch, symmetry, leading lines, frame within a frame.

### E. Lighting — schemes, quality, direction, source

**Schemes:** three-point (key/fill/back), Rembrandt (triangle on cheek), split, butterfly, loop, broad, short. **Quality:** hard / soft / diffused / specular. **Direction:** key from camera left at 45°, top-lit spotlight, backlit silhouette, side-lit chiaroscuro. **Sources:** practical lamp, neon sign, fluorescent overhead, sodium-vapor street lamp, candlelight, fire light, screen light from a monitor, moonlight, sunlight, golden hour, blue hour, overcast skylight. **Color temperature:** 3200K tungsten, 5600K daylight, 6500K overcast, custom hex codes.

**Omni-specific:** the model responds well to mood + source rather than ratio nerdery. "Warm desk-lamp light against cool blue rain outside" outperforms "key 70%, fill 30%, back 20%" in Flash-tier output.

### F. Color & grade

Palette descriptors: teal-and-orange, neon noir, pastel dreamcore, monochrome, sepia, desaturated war film, Technicolor, bleach bypass. Named looks: "Roger Deakins lit", "Emmanuel Lubezki natural light", "Greig Fraser dune palette", "Wong Kar-wai green-and-red". LUTs: "Kodak 2383 print emulation", "FilmConvert Velvia". Hex code injection works: "primary palette #E0C097, #2E3A87, #C13B3B."

### G. Subject action & performance

Use verbs, not adjectives. *"She zips her jacket, exhales foggy breath, looks left"* beats *"She is cold and contemplative."* Micro-expressions Omni renders: "subtle smile forming", "rapid blinking to hold back tears", "slight head tilt indicating disagreement". Crowd behavior: "200-person crowd, mixed reaction, scattered cheers and silence". Wardrobe: be brand-specific only via reference image; verbal description should stay generic to avoid IP refusals.

### H. Environment & production design

Location specificity drives realism. "1920s jazz club, Manhattan basement, brass and velvet" outperforms "a club." Set dressing: "props on table — typewriter, ashtray with one cigarette, half-drunk whiskey." Atmospherics: "haze, sun rays through window slats, dust particles drifting." Time period must include era anchors ("Edwardian costume", "1970s wood paneling", "near-future minimalist apartment").

### I. Audio — the full stack

Omni generates audio natively with the video. **Dialogue:** use quotation marks — *A woman says, "We have to leave now."* **SFX:** *SFX: thunder cracks in the distance.* **Ambience:** *Ambient noise: the quiet hum of a starship bridge.* **Music:** *calm smooth music* / *retro-futuristic background music* / *no music, just realistic real world sound.* **Silence:** *no music* / *no voice cuts at the end.* Per Google's official Avatar workflow, voice cloning of yourself is allowed via the consent flow; cloning others is blocked. Editing speech in existing video is deliberately withheld at launch.

### J. Rendering, textures, VFX

Material vocabulary: "translucent glass with caustic refraction", "felted stuffed puppet with googly eyes" (DeepMind official example), "voxel art", "claymation stop motion", "graphite pencil sketch on textured paper with 12fps line boiling", "risograph print with limited three-color palette and registration overlays", "monochrome line art drawing", "vintage monochrome transparent 3D line art hologram". VFX integration: motion effects ("animated motion effects coming out of the skateboard"), particle systems, bioluminescence, mirror-ripple liquid transitions.

### K. Editing implied in prompt

Cut styles: "hard cut", "match cut", "L cut" (audio leads). Pacing: "rapid fire 9 frames per item at 24FPS" (official DeepMind example), "slow contemplative pacing", "MTV-fast cuts". Multi-shot in one render: numbered Clip 1 / Clip 2 / Clip 3 blocks work, as inherited from Veo 3.1 patterns.

---

## 6. Genre Pattern Library — 20 Annotated Prompts

Each prompt below is structured for Omni Flash's 10-second cap. Annotations follow each prompt explaining the choices.

### 6.1 Cinematic narrative drama

> *A 10-second 16:9 cinematic oner. Close-up with shallow depth of field on a 38-year-old woman in a worn camel coat, her face lit by passing headlights through a rain-streaked taxi window at night. She exhales slowly, eyes closed, then opens them and looks directly into the lens for one beat. Warm sodium-vapor practicals outside, cool 5600K rim from the windshield reflection. 35mm film grain. Subtle road ambience, distant rain, no dialogue, no music. Melancholic mood. Cinematic.*

*Annotations:* subject named with age and one wardrobe anchor; one camera move (none — locked off close-up); motivated light source (practicals); explicit color temp; film stock anchor; deliberate audio negative space; emotional descriptor at the end binds it.

### 6.2 Action/thriller

> *10-second 16:9 oner, handheld urgency. A man in a charcoal suit sprints down a fluorescent-lit parking garage, low-angle 24mm wide. Tires squeal off-frame, then a sedan whip-pans into shot from camera-right, headlights flaring the lens. He plants and pivots. Hard shadows. Practical fluorescents flicker. Engine roar, footsteps slapping concrete, breath ragged. No music. Pure diegetic sound. Cinematic.*

*Annotations:* handheld + low-angle + 24mm = action vocabulary; "off-frame" engages Omni's spatial reasoning; "whip-pans" is named as one move; "no music" forces SFX-only mix.

### 6.3 Horror — slow-burn

> *Static locked-off medium wide, 10 seconds. A 1970s wood-paneled living room at 3 AM. A grandfather clock ticks in the foreground. In the deep background hallway, a figure stands motionless, only feet visible past the doorframe. The clock ticks. The camera does not move. On second 7, the hallway light flickers once. The feet are gone. Diegetic clock ticks, faint house creaks, no music, no jump scare audio.*

*Annotations:* "static locked off" — Omni's explicit vocabulary; timed event ("on second 7"); negative space ("no jump scare audio") is critical to slow-burn.

### 6.4 Horror — jump-scare variant

> *10-second 16:9 handheld. POV of a flashlight beam moving down a basement corridor, dust in the air. Steady breathing. The beam sweeps left across pipes, returns center — a face is two feet away, eyes wide. Loud single sting on impact frame. Then black. Audio: muffled breathing, beam scrape, sudden orchestral hit on the reveal, then silence. No score before the hit.*

*Annotations:* POV + flashlight beam describes the lighting; the audio prompt names the cue precisely ("on the reveal").

### 6.5 Hard sci-fi

> *10-second oner inside a near-future spacecraft cockpit. Medium two-shot, 35mm. Two crew in matte-grey flight suits, harness straps visible. Soft cyan instrument glow from a curved holographic console; a single red caution indicator pulses at 1Hz. Slow dolly-in over 6 seconds. They exchange a look, then both turn toward the viewport. Off-screen, a low subsonic hum builds. No dialogue. No music. Photoreal physics, accurate weight in micro-gravity hair drift.*

*Annotations:* "accurate weight in micro-gravity" leans on Omni's Genie physics layer; one-color motivated key (cyan) + one accent (red); subsonic hum is a sound-design instruction.

### 6.6 Space opera

> *10-second wide establishing shot, 21:9 cinematic letterbox. A copper-and-bronze cathedral-class starship banks across a triple-sun system, light raking across hull greebles. Particulate dust streams trail the engines. Stately orchestral cue, brass-led, swelling on the bank. Camera is locked off; the ship fills frame to fill frame as it passes. Photoreal. Anamorphic flares. No dialogue.*

*Annotations:* 21:9 in-prompt to override default; "greebles" is industry vocabulary Omni recognizes; orchestral instruction shapes the audio model.

### 6.7 Fantasy/epic

> *10-second oner. A robed figure stands on a wind-scoured cliff at golden hour, back to camera. A medium dolly-back over 8 seconds reveals a vast valley below with three dragon silhouettes circling distant towers. Cloak whips in the wind. Ambient wind, distant dragon calls, low choral hum. Cinematic, 35mm anamorphic, warm rim light from the setting sun, deep shadows on the cliff face. Epic.*

### 6.8 Romance

> *Close-up two-shot, shallow depth of field. A young couple under a string-lit Brooklyn café awning during a light rain. Her hand rests on his sleeve; he laughs, looks down, then up at her. Warm 3000K practicals, cool 5600K rain fill, soft Pro-Mist diffusion. Gentle solo piano, light rain on awning, no dialogue. 10 seconds. 16:9.*

### 6.9 Comedy — broad

> *10-second oner. A man in a too-small business suit attempts to sit on an exercise ball at his desk. The ball escapes. He chases it across an open-plan office in slow-motion 60fps, knocking over a fern. Wide angle 24mm low. Bright fluorescent office lighting. Cheerful slap-bass cue, single comedic whip-pan, exaggerated thud SFX on impact with a beanbag. 16:9.*

### 6.10 Comedy — deadpan

> *Static locked-off medium shot, 10 seconds. A woman in a beige cardigan sits at a kitchen table. She slowly raises a fork to her mouth, chews once, swallows. Pause. She looks directly into camera with no expression and says, "It's fine." Cut. Flat fluorescent kitchen light, no score, only ambient room tone and one refrigerator hum.*

### 6.11 Documentary — observational

> *10-second handheld verité, 16:9. A fisherman in his sixties mends a net on a dock at 6 AM blue hour. Natural blue light, no fill. Hands in focus, his face out of focus in the background. He hums tunelessly. Real seagulls, distant boat engine, water lapping. No music. 35mm equivalent, slight handheld micro-movement. Documentary realism.*

### 6.12 Documentary — interview

> *10-second locked-off medium shot, 50mm. A scientist seated at a slight three-quarter angle, soft 5600K key from camera-left through a large diffused window, negative fill on the shadow side. She begins to speak: "We didn't know it would behave that way." Natural office room tone. No music. 16:9.*

### 6.13 Music video — performance

> *10-second 9:16 vertical. A singer in a sequined jumpsuit performs on a smoke-filled stage, single moving spotlight pulsing on the downbeat of the provided audio. Close-up on her face, then a quick pull to medium on beat 4. Audio reference: <audio>. Camera moves in sync to the beat. Strong rim light, lens flare across each beat. Cinematic.*

### 6.14 Music video — narrative

> *10-second 9:16 vertical. A young man walks down an empty subway platform at night, intercut with quick flashes of his earlier day. Warm tungsten platform lights, cool fluorescent station signs. Camera dollies alongside him at walking pace. Audio reference: <audio> — image-cuts land on every snare hit. Melancholic. Photoreal.*

### 6.15 Commercial — luxury

> *10-second 16:9. A platinum wristwatch rests on black marble. A slow 8-second orbit at macro distance reveals subtle bezel engraving and a polished crown. Single key light from camera-right at 30°, soft negative fill, no spill. Black background. Champagne-gold accent reflections. Tasteful piano cue, single watch-tick SFX at the closing beat. The text "Time, refined." fades in on the final frame, white serif, lower third. Cinematic. Photoreal.*

### 6.16 Commercial — FMCG

> *10-second 9:16 vertical. A glass of iced cold-brew coffee on a sunlit kitchen counter. Slow 4-second push-in. Condensation beads. A barista's hand pours steamed oat milk from above; it cascades and swirls. Bright morning daylight, soft. Upbeat acoustic cue. SFX: glass clink and pour. The text "Slow morning, fast brew." appears at second 8. Photoreal.*

### 6.17 Commercial — automotive

> *10-second 16:9 cinematic. An electric SUV silently rolls across a salt flat at golden hour, low-angle tracking shot. Camera matches speed at vehicle's right side. Long shadows, warm key, cool sky fill. Tire-on-salt-crunch SFX only, no engine sound. Sweeping cinematic score. The brand name appears in white sans-serif on the closing frame. Anamorphic, photoreal.*

### 6.18 Commercial — tech

> *10-second 16:9. A translucent rendering of a slim laptop floats over a deep navy background, components inside lighting up sequentially: SSD, GPU, then display. Each light-up syncs to a soft electronic tick on the soundtrack. Slow orbit. Single key from above. Final frame: device closes, product name in white. Modern, minimal, photoreal. 24fps.*

### 6.19 UGC / TikTok vertical

> *10-second 9:16. Natural smartphone zoom feel, hand-held. A young woman in soft daylight in her kitchen turns to the camera and says, "Okay, you have to see this." She picks up a coffee cup with steam visibly rising. Quick smash cut to her taking the first sip and her eyes widening. Ambient kitchen sound, single hook beat at the smash cut. Selfie aesthetic. Natural lighting.*

### 6.20 Trailer/teaser cut feel

> *10-second 16:9. Three-beat trailer cut. Beat 1 (0–3s): wide aerial drone push toward a stormy castle at dusk; thunder roll. Beat 2 (3–6.5s): hard cut to close-up of a sword being drawn; sharp metal ring. Beat 3 (6.5–10s): match cut to a hero's eyes opening; orchestral hit and bass drop. Title card on final frame: white serif on black. Anamorphic flares throughout. Cinematic.*

(Genres 8 product video/e-commerce, 13 explainer, 14 2D/3D/stop-motion animation, 15 anime, 16 experimental, 17 news/broadcast, 18 sports, 19 found footage/mockumentary share the same construction pattern; templates appear in the Appendix.)

---

## 7. Advanced Techniques

### 7.1 Character consistency across generations

Officially supported. Upload a portrait as a reference image; Omni anchors face geometry, hair, and wardrobe across multi-turn edits. The DeepMind prompt guide demonstrates: original astronaut clip → *"Change the astronaut to a sea anemone"* → *"Change the ships to be made from white origami paper"* — character continuity preserved by the model's persistent scene state. For multi-shot productions, attach the SAME reference image to each generation and use identical identity descriptors verbatim ("the woman in the camel coat") in every prompt.

### 7.2 Style consistency across a sequence

Lock three things across prompts: lens (e.g., "35mm anamorphic" everywhere), palette (one fixed teal/orange or hex set), and lighting model ("warm 3000K key, cool 5600K rim"). For maximum consistency, generate a Nano Banana style still first, then use it as a style reference in every Omni call.

### 7.3 Reference-driven prompting

Mix references in one prompt with angle-bracket syntax. The official DeepMind example: *"Referring to the extreme camera movement, perspective, and distortion in <video>, create a front-facing full-body walk cycle of the character from <image>, quickly style-shifting into multiple visual styles during the walk cycle, starting from realistic cinema. Keep the environment, only change styles. Hard cut backgrounds always centering the sky. Continuous walking, continuous audio, and style shifts in perfect sync to the beat of the audio. Cinematic, 16:9."* Roles are assigned explicitly: video = camera/motion, image = character, audio = beat.

### 7.4 Image-to-video best practices

Provide a sharp, well-lit reference at 1024×1024 or larger. State what is in the image and what should happen. Use "do not show the drawing in the final video" if the reference is a sketch. Official example: *"turn this into realistic footage, using the drawing only as a guide for movement, do not show the drawing in the final video."*

### 7.5 Video extension and continuation

Omni Flash caps at 10s. For longer pieces, chain clips in Google Flow's Scene Builder, which Google's product page describes as a feature that lets you "reveal more of the action or transition to what happens next with continuous motion and consistent characters." For each new clip, reuse the same reference image and identity descriptor to anchor continuity.

### 7.6 Inpainting and selective regeneration

Use conversational edit prompts that name what changes and what stays. Format: *"Edit this keeping everything the same. [single change]."* (Official DeepMind pattern.) Avoid vague edits — per Gabe Barth-Maron, vague edit prompts cause over-editing. Pattern: "Keep [X, Y, Z] identical. Change only [W]."

### 7.7 Chaining with Gemini text models

Use Gemini 3.5 to expand a one-line idea into an Omni-ready prompt. The official Google Cloud Veo 3.1 ultimate prompting guide states: *"If you need to add more detail, use Gemini to analyze and enrich a simple prompt with more descriptive and cinematic language."* The same pipeline works for Omni.

### 7.8 Storyboard-to-video pipelines

Omni supports storyboard frames as image input. The official DeepMind example: *"Show me in this story. Follow the story exactly in order starting top left. Entire story in 10 seconds. Cinematic."* The model reads a grid of frames as sequential beats.

### 7.9 Cost optimization

Iterate on the cheapest tier first. Use Flash for ideation and conversational refinement; commit credits to Pro-tier 1080p upscaling only on final shots. Avoid the 4s tier unless deliberately producing micro-loops — the 8s and 10s tiers consume more credits but produce more usable footage per dollar.

### 7.10 Refusal patterns and legitimate rephrasings

Per Google's Gen AI Prohibited Use Policy (policies.google.com/terms/generative-ai/use-policy), Omni refuses content involving real public figures' likeness without consent, copyrighted characters, minors in unsafe contexts, sexually explicit content, and non-consensual imagery. Rephrasing strategies: replace named celebrities with descriptive archetypes ("a 1960s rock star" rather than a name); replace branded IP with generic equivalents ("a robotic plumber in red overalls" rather than the obvious IP); use the Avatar feature for any self-likeness work to comply with consent requirements.

---

## 8. Parameter Reference Table (Complete)

| Parameter | Setting | Notes |
|---|---|---|
| Clip length | 4 / 6 / 8 / 10 seconds | 10s requires Plus/Pro/Ultra; per Flow help |
| Aspect | Landscape / Portrait toggle | Default Landscape; matches reference if uploaded; embed ratio in prompt as belt-and-suspenders |
| Resolution (output) | Not publicly documented by Google | 1080p upscaling is a separate Pro feature |
| Frame rate | Not publicly documented | 24fps appears in official user prompt example |
| Audio | Native generation on every clip | Voice reference input only at launch |
| Image refs | Up to 5 per Gemini app generation | Higher in Flow |
| Video ref upload | 60s / 1 GB max, trim to 10s for edit | Flow only |
| Voice reference | 1 per generation | Flow |
| Avatar | Single registered avatar per Google account | English only, 18+, not in EEA/CH/UK |
| Watermark | SynthID + C2PA on every output | Cannot be disabled |
| Export | MP4 | Standard |
| API | Not yet live (as of 2026-05-22) | "Coming in the coming weeks" per blog.google launch post |
| Pricing — Plus | $7.99/mo | 200 Flow credits |
| Pricing — Pro | $19.99/mo | 1,000 Flow credits + 1080p upscale + video-to-video edit + avatars |
| Pricing — Ultra | $99.99/mo | 10,000 Flow credits |
| Free access | YouTube Shorts, YouTube Create app | Rolling out from May 2026 |

---

## 9. Failure Modes & Diagnostic Framework

### 9.1 Anatomy and hand errors

Still present at Flash tier. Mitigation: avoid prompts that require complex hand-object interaction in close-up (e.g., piano playing, sign-language). When hands must appear, prompt them in mid-shot or wider, not extreme close-up. Independent reviewer consensus (PixVerse, Medium analysts) places Omni Flash hand quality below Seedance 2.0.

### 9.2 Physics violations

Less frequent than predecessors thanks to the Genie layer, but still appear on fluid dynamics and granular materials. Mitigation: prompt the physics explicitly ("water pours and gathers naturally", "fabric drapes with realistic weight"). Avoid chain-reaction prompts with more than three interacting objects.

### 9.3 Identity drift mid-clip

The most common multi-turn-edit failure. Mitigation: name the character with the same descriptor verbatim every turn ("the woman in the camel coat"). Use a portrait reference image, not text alone. For long sequences, regenerate the reference image with Nano Banana and re-anchor.

### 9.4 Audio-video desync

Audio cues sync well on broad music beats but drift on tight percussive hits. Mitigation: avoid timing audio prompts to exact frames ("on frame 47"). Prompt to beat positions ("on each snare hit") and let Omni's audio model find them.

### 9.5 Prompt collapse symptoms

When too many style anchors stack ("80s neon + Wes Anderson symmetry + BBC nature doc + Studio Ghibli + anamorphic"), Omni collapses to a generic mid-style average. Mitigation: pick one or two anchors. Per Sider AI's Veo 3.1 field guide, the same rule transfers to Omni: "Pick 1–2 anchors, then specify concrete attributes."

### 9.6 Over-editing on vague conversational edits

Per Gabe Barth-Maron (DeepMind research engineer, TechCrunch May 19, 2026): *"editing prompts will need to be highly specific, otherwise Omni risks over-editing or unintentionally altering elements the user wanted to keep."* Mitigation: lead every edit with "Keep everything identical except…"

### 9.7 When to abandon vs. iterate

Iterate if: the subject identity is right but motion is wrong; lighting is wrong but composition is right. Abandon and re-prompt from scratch if: the model has rendered an entirely different scene; physics are catastrophically wrong (e.g., gravity reversal); refusal patterns are triggering. The conversational edit loop costs credits each turn — three failed edits without improvement is the signal to restart.

---

## 10. Cost & Workflow Optimization

**Recommended workflow for production teams (May 2026):**

1. **Ideate on Free tier** via YouTube Shorts to test conceptual prompts at zero cost.
2. **Refine on Plus ($7.99/mo)** for unlimited daily conversational editing within 200 credits.
3. **Finalize on Pro ($19.99/mo)** for 1080p upscaling and video-to-video editing.
4. **Scale on Ultra ($99.99/mo)** when running 10,000+ credit production volumes.
5. **Use Veo 3.1 via Vertex AI** in parallel for any shot requiring 4K, API integration, or longer-than-10s single generation.

**Credit math (per Flow help and labs.google/flow/about):** A standard Veo 3.1 Fast generation uses 10–20 credits; Omni Flash 10s clips are credited similarly per published Flow tiers. Plus = ~10–20 clips/month; Pro = ~50–100; Ultra = ~500–1000.

---

## 11. Source Bibliography (accessed 2026-05-22)

- **Google DeepMind, "Introducing Gemini Omni"** (Koray Kavukcuoglu, 2026-05-19) — blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-omni/ — Primary launch announcement.
- **Google DeepMind product page, Gemini Omni** — deepmind.google/models/gemini-omni/ — Official capabilities, demos, safety statement.
- **Google DeepMind, Gemini Omni Prompt Guide** — deepmind.google/models/gemini-omni/prompt-guide/ — Official prompting structure.
- **TechCrunch, "Google's Gemini Omni turns images, audio, and text into video"** (Rebecca Bellan, 2026-05-19) — Brichtova and Barth-Maron quotes.
- **VentureBeat, "Google unveils Gemini Omni 'any-to-any' AI model"** (2026-05-19) — Enterprise framing.
- **CineD, "Google Launches Gemini Omni Flash"** (2026-05-19) — Production-pipeline analysis.
- **The Next Web, Google Gemini Omni Flash coverage** (2026-05-19) — SynthID and Avatar detail.
- **Build Fast with AI, "Gemini Omni: Google's AI Video Model Explained (2026)"** (Satvik Paramkusam, 2026-05-21) — Architecture (Gemini + Veo + Genie + Nano Banana fusion).
- **Google Flow help center** — support.google.com/flow/ — Clip length tiers, video upload limits, model feature matrix.
- **Gemini Apps help — Avatars** — support.google.com/gemini/answer/16984474 — Consent workflow.
- **Gemini Apps help — Generate videos** — support.google.com/gemini/answer/16126339 — Aspect ratio, upload limits.
- **labs.google/flow/about** — Plan tier credit allocations.
- **one.google.com/about/google-ai-plans/** — Plus/Pro/Ultra pricing.
- **Google Cloud Blog, "Ultimate prompting guide for Veo 3.1"** — cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-veo-3-1 — Inherited prompt patterns.
- **OpenAI Help Center, "What to know about the Sora discontinuation"** — Sora 2 timeline.
- **Runway Research, "Introducing Runway Gen-4.5"** (2025-12-01) — Elo and capability claims.
- **Kuaishou Technology IR (GlobeNewswire, 2026-02-05)** — Kling 3.0 launch.
- **ByteDance SEED, "Seedance 2.0 Official Launch"** (2026-02-12) — Architecture and features.
- **Segmind API documentation, Seedance 2.0** — 4.5B parameter Dual-Branch Diffusion Transformer.
- **Meta AI Research, Movie Gen** — ai.meta.com/research/movie-gen/.
- **Higgsfield product page** — higgsfield.ai — April 29, 2026 cinematic camera update.
- **Wikipedia, Veo (text-to-video model)** — en.wikipedia.org/wiki/Veo_(text-to-video_model) — Veo timeline.
- **Wikipedia, Sora 2** — en.wikipedia.org/wiki/Sora_(text-to-video_model) — Sora 2 discontinuation.

*All sources reviewed within the last 30 days; given the May 2026 launch, none exceed the 6-month-stale threshold.*

---

## 12. Glossary

- **Any-to-any model:** A single model that accepts any input modality (text/image/audio/video) and outputs in any modality. Omni Flash currently outputs video; image and audio outputs are roadmap.
- **C2PA Content Credentials:** Industry-standard cryptographic provenance metadata embedded in generated content.
- **Conversational editing:** Multi-turn natural-language editing where each instruction preserves scene state from the prior turn.
- **Flow Scene Builder:** Google Flow's timeline tool for chaining multiple generated clips into longer sequences.
- **Genie 3:** Google DeepMind's world-simulation model, integrated into Omni as the physics/environment layer.
- **Ingredients to Video:** Veo 3.1 feature (carried into Flow) that uses up to 3 reference images as identity anchors.
- **Nano Banana:** Google DeepMind's image-editing model, integrated into Omni for image-level conversational editing.
- **Omni Pro:** Teased larger Omni variant; no release date.
- **Oner:** Single continuous-take shot, recognized vocabulary in Omni prompts.
- **SynthID:** Google's imperceptible watermark embedded in all Omni outputs; verifiable via Gemini app, Chrome, and Search.

---

## 13. Appendix — 30+ Reusable Prompt Templates

(Each template uses `{VARIABLE}` placeholders. Replace and run.)

**T1 — Cinematic close-up portrait, drama:** *"10-second 16:9 close-up. {subject description}, lit by {motivated light source}, {color temperature}. Shallow depth of field. {one micro-action}. {ambient audio}. No dialogue. Cinematic 35mm."*

**T2 — Action handheld oner:** *"10-second 16:9 handheld urgency. {subject} {action verb} through {environment}. Low angle 24mm. Whip pan reveal to {second subject} on second {N}. {diegetic SFX only}. No score."*

**T3 — Slow-burn horror static:** *"Static locked-off medium wide, 10 seconds. {setting at time}. Foreground: {atmospheric element ticking/dripping}. Deep background: {threat element, partial visibility}. On second {7-8}, {single subtle change}. Diegetic audio only. No jump scare."*

**T4 — Sci-fi cockpit two-shot:** *"10-second oner inside {vehicle type}. Medium two-shot 35mm. {wardrobe and harness detail}. {single colored instrument light} with {single accent indicator}. Slow dolly-in over 6 seconds. {non-verbal performance beat}. Subsonic hum builds. Photoreal physics."*

**T5 — Space opera establishing:** *"10-second wide establishing, 21:9. {ship/structure} {motion verb} across {astronomical setting}. Light raking across {surface detail}. Anamorphic flares. {orchestral cue description}. Locked-off camera. Photoreal."*

**T6 — Fantasy reveal:** *"10-second oner. {robed/armored figure} on {dramatic landscape} at {time of day}. Medium dolly-back over 8 seconds reveals {epic scale element}. {clothing motion in wind}. {ambient weather + creature audio}. Low choral hum. Cinematic anamorphic, warm rim from setting sun."*

**T7 — Romance two-shot:** *"Close-up two-shot, shallow DOF. {couple} under {soft practical light source} during {weather}. {tactile gesture}. Warm 3000K practicals, cool 5600K {fill source}. Soft Pro-Mist. Gentle {instrument} cue. 10 seconds. 16:9."*

**T8 — Broad comedy oner:** *"10-second oner. {character in absurd wardrobe} attempts {mundane task}. {prop} escapes. Chase through {environment} in slow-motion 60fps. Wide 24mm low. Bright fluorescent. {comedic music cue}. Single whip pan. Exaggerated SFX on impact."*

**T9 — Deadpan comedy:** *"Static locked-off MS, 10 seconds. {character} {mundane action}. Pause. Looks into camera, no expression, says, '{one short line}.' Cut. Flat fluorescent {room} light, no score, ambient room tone only."*

**T10 — Observational documentary:** *"10-second handheld verité, 16:9. {real-world subject} {ordinary task} at {time of day}. Natural light only. {body part} in focus, face soft-focus background. {humming/ambient vocalization}. Real {environmental SFX}. No music. 35mm equivalent."*

**T11 — Interview documentary:** *"10-second locked-off MS, 50mm. {expert} seated three-quarter angle. Soft 5600K key from camera-left through {window/diffusion source}, negative fill on shadow side. {Begins speaking}: '{one-sentence quote}.' Natural room tone. No music. 16:9."*

**T12 — Music video performance vertical:** *"10-second 9:16. {performer} performs on {stage description}, {single moving light type} pulsing on the downbeat of provided audio. Close-up on face, then quick pull to medium on beat {N}. Audio reference: <audio>. Camera moves in sync. Strong rim, lens flare per beat."*

**T13 — Music video narrative:** *"10-second 9:16. {character} {walking/moving} through {urban environment} at {time}. Intercut with quick flashes of {emotional memory beats}. Warm tungsten {sources}, cool fluorescent {accents}. Dolly alongside at walking pace. Audio reference: <audio> — cuts on every {drum element}. Photoreal."*

**T14 — Luxury commercial:** *"10-second 16:9. {product} on {premium surface}. Slow 8-second orbit at macro distance reveals {craftsmanship details}. Single key from camera-right at 30°, soft negative fill, no spill. Black background. {accent metal} reflections. Tasteful piano. Single {product SFX} at closing beat. Text '{tagline}.' fades in, white serif lower third. Photoreal."*

**T15 — FMCG commercial vertical:** *"10-second 9:16. {food/beverage product} on {everyday surface} in {natural lighting condition}. Slow 4-second push-in. {textural detail — condensation/steam/melt}. {human hand action} from above. Bright morning daylight. Upbeat acoustic cue. SFX: {product interaction sounds}. Text '{tagline}.' on closing beat. Photoreal."*

**T16 — Automotive commercial:** *"10-second 16:9. {vehicle} {motion verb} across {dramatic landscape} at golden hour. Low-angle tracking, camera matches speed. Long shadows. {road surface SFX only}. Sweeping orchestral. {brand name} in white sans-serif on closing frame. Anamorphic, photoreal."*

**T17 — Tech commercial:** *"10-second 16:9. Translucent rendering of {device} floats over deep {brand color} background. Internal components light up sequentially: {component 1}, {component 2}, {component 3}. Each light-up syncs to an electronic tick. Slow orbit. Single overhead key. Final frame: device {closes/transforms}, product name in white. Minimal, photoreal. 24fps."*

**T18 — UGC TikTok:** *"10-second 9:16. Natural smartphone zoom, handheld. {young creator} in {daily environment} turns to camera and says, '{hook line}.' She {action with product}. Quick smash cut to {payoff moment}. Ambient room sound, single hook beat at smash cut. Selfie aesthetic. Natural lighting."*

**T19 — Product e-commerce:** *"10-second 1:1. {product} on neutral seamless backdrop. 360° orbit at consistent distance over 8 seconds. Three-point lighting, balanced ratios. Subtle product SFX on orbit-start and orbit-end. Text spec '{key feature}' lower third. Photoreal."*

**T20 — Corporate explainer:** *"10-second 16:9. {concept} visualized in {style: claymation / 2D vector / 3D minimal}. {element 1} demonstrates {process step 1}, transitions to {element 2} demonstrating {process step 2}. Calm explanatory voiceover. Soft ambient music. Lower-third labels appear as each element does."*

**T21 — Claymation explainer (per official DeepMind example pattern):** *"claymation explainer of {topic}, everything is made out of clay, no hands, stop motion, accurate."*

**T22 — 2D animation flat:** *"10-second contemporary flat-media style. {concept}. Minimalist vector shapes blended with rich organic textures. High-contrast 'electric' palette of {color 1}, {color 2}, {color 3} against {background color}. Stipple shading, grainy gradients, risograph-like quality. Playful editorial feel."*

**T23 — 3D translucent glass:** *"10-second hyper-realistic 3D translucent {material} style. {subject}. Complex light refractions, caustic patterns, soft internal glows. Minimalist studio setting. Slow camera orbit."*

**T24 — Anime style:** *"10-second {2D anime / cel-shaded} style. {character description with anime conventions}. {emotional beat}. {weather or particle effects}. {Japanese-style lighting}. {orchestral or chiptune} cue. 24fps line boiling."*

**T25 — Experimental art film:** *"10-second non-narrative experimental piece. {abstract subject or material}. {unconventional camera behavior}. {disorienting audio — drone/musique-concrète}. {bold color palette}. {one repeated motion}. No dialogue, no narrative resolution."*

**T26 — News broadcast cold open:** *"10-second 16:9. Locked-off MS of news anchor at modern desk. Cool 5600K key, blue-lit set background, lower-third graphic '{breaking}'. Anchor turns to camera: '{one-line headline}.' Sting cue. Studio room tone."*

**T27 — Sports highlight:** *"10-second 16:9. {athlete} executes {action} in {venue}. Multi-angle implied: wide → tight on contact → slow-mo replay. Crowd roar building. Stadium lighting. SFX of {sport-specific impact}. Energetic broadcast music. Realistic motion physics."*

**T28 — Found footage:** *"10-second handheld 4:3, simulated camcorder VHS. Tracking timecode lower-right. {ordinary domestic environment}. {character speaks to camera operator off-frame}. Unsteady framing, occasional autofocus hunt. Magnetic tape noise floor in audio. No music."*

**T29 — Mockumentary interview:** *"10-second locked-off MS, 50mm. {character} in {workplace setting}. Plain office lighting. They look slightly off-camera (interviewer position), pause, say: '{one-line absurd statement delivered seriously}.' Static room tone. No music."*

**T30 — Trailer three-beat:** *"10-second 16:9. Beat 1 (0–3s): {wide aerial of dramatic location}; {weather SFX}. Beat 2 (3–6.5s): {hard cut to tight detail of iconic object/action}; {sharp diegetic SFX}. Beat 3 (6.5–10s): {match cut to hero close-up}; orchestral hit and bass drop. Title '{film title}' on final frame, white serif on black. Anamorphic. Cinematic."*

**T31 — Image-to-video with motion guide:** *"Animate the attached image. {one-sentence motion description}. Keep {character/product details} identical to reference. {camera direction}. {audio direction}. 10 seconds."*

**T32 — Conversational edit (single-change pattern):** *"Edit this keeping everything the same. {one change instruction}."*

**T33 — Multi-reference fusion:** *"Apply the {camera move / motion / style} from <video> to the {subject} from <image>, in the {environment} from <image-2>, synchronized to the beat of <audio>. {one stylistic anchor}. Cinematic. {aspect ratio}."*

---

# ===== FILE 2: `gemini-omni-video-guide.md` =====

# Gemini Omni — Practical Cinematic Prompt Guide

A daily-use reference card for filmmakers, ad creatives, and producers working with Google DeepMind's Gemini Omni Flash (launched May 19, 2026).

## 1. Quick Start Checklist — 12 things to do for every prompt

1. **Decide aspect ratio first** (Landscape default, Portrait toggle, or specify "16:9" / "9:16" in the prompt itself).
2. **Pick clip length** (4/6/8/10 seconds — 10s requires Plus/Pro/Ultra).
3. **Lead with subject + primary action** in the first sentence — Omni weights opening clauses heavily.
4. **Name ONE camera move** (or "static / locked off / fixed" for no move).
5. **Name ONE motivated light source** with color temperature if you can.
6. **State the audio explicitly** — Omni generates audio natively, so say what you want or use "no music" to suppress score.
7. **Attach a reference image** for any character or product you need consistent.
8. **Specify negatives in plain English** — "Don't add X", "no Y", "without Z".
9. **Tag references in-prompt** with `<image>`, `<video>`, `<audio>` syntax when mixing inputs.
10. **Don't stack more than 2 style anchors** — prompt collapse is the most common failure.
11. **For edits, lead with "Keep everything the same except…"** — vague edits over-edit.
12. **Iterate via chat, not by re-prompting** — Omni preserves scene state across turns.

---

## 2. The Universal Cinematic Prompt Template

```
{LENGTH}-second {ASPECT} {GENRE/MOOD} {SHOT TYPE}.
{SUBJECT (with one specific detail and one wardrobe anchor)} {ACTION VERB} {LOCATION/ENVIRONMENT}.
{CAMERA MOVE or "static locked off"}, {LENS/FOCAL LENGTH}.
{LIGHTING SOURCE + COLOR TEMPERATURE + QUALITY}.
{AUDIO: dialogue in "quotes" OR ambient description OR "no music" OR "<audio>"}.
{STYLE ANCHOR — pick ONE: film stock / director reference / palette}.
{NEGATIVES: "Don't add X. No Y."}
```

---

## 3. Top 30 Power Phrases that consistently elevate output

1. *"one continuous shot"* — official Omni vocabulary for oners
2. *"locked off"* / *"static"* / *"fixed"* — official for no-camera-move
3. *"push in"* / *"punch in"* / *"dolly zoom"* — official Omni movements
4. *"natural smartphone zoom"* — official for UGC look
5. *"shallow depth of field"*
6. *"35mm anamorphic"* — one anchor for cinematic
7. *"golden hour backlight"*
8. *"motivated practical light"*
9. *"warm 3000K key, cool 5600K rim"*
10. *"diegetic sound only, no music"*
11. *"no voice cuts at the end"* (from official DeepMind example)
12. *"Don't add [X]"* (official negative pattern)
13. *"Keep everything the same except…"* (for edits)
14. *"photoreal, accurate physics"*
15. *"35mm film grain"*
16. *"Pro-Mist diffusion"*
17. *"hard shadows, chiaroscuro"*
18. *"slow dolly-back over {N} seconds"*
19. *"on second {N}"* — for timed events
20. *"24fps cinematic cadence"* or *"60fps slow motion"*
21. *"shot from {distance}, {angle}"*
22. *"single key from camera-{direction} at {angle}°"*
23. *"negative fill on shadow side"*
24. *"three-quarter angle"* — for interview framing
25. *"cinematic, 16:9"* — official Omni example phrase
26. *"natural room tone"* / *"ambient room tone only"*
27. *"in sync with the beat of the audio"* (official pattern)
28. *"using the {drawing/image} only as a guide for movement, do not show {it} in the final video"* (official sketch-to-video pattern)
29. *"stop motion"* / *"claymation"* / *"line boiling at 12fps"* — animation anchors
30. *"final frame: {title text} fades in, white serif, lower third"* — for ad/trailer endings

---

## 4. Decision Tree — Desired Result → Recommended Approach

- **Need maximum cinematic fidelity at 4K?** → Use Veo 3.1 via Vertex AI, NOT Omni Flash.
- **Need multi-turn conversational editing?** → Omni Flash.
- **Need mixed input fusion (image + audio + video + text)?** → Omni Flash.
- **Need an explainer with world knowledge?** → Omni Flash.
- **Need an API today?** → Veo 3.1 via Vertex AI (Omni API not yet live).
- **Need vertical 9:16 for social?** → Either; Omni for editability, Veo 3.1 for fidelity.
- **Need 4K + 60fps?** → Kling 3.0.
- **Need #1-benchmark raw fidelity?** → Seedance 2.0 (note: not US-available).
- **Need character/voice cloning of yourself?** → Omni Avatars (English only, not in EEA/CH/UK, 18+).
- **Need longer than 10s in one render?** → Veo 3.1 Scene Extension or Kling 3.0 (15s).

---

## 5. Cheat Sheet Tables

### Camera

| Term | Use for |
|---|---|
| Static / locked off / fixed | Tension, surveillance, deadpan |
| Push in / punch in | Reveal, emphasis |
| Dolly out / pull back | Reveal of scale |
| Whip pan | Action transition |
| Dolly zoom | Disorientation (Vertigo) |
| Crane / jib | Epic scale |
| Steadicam | Smooth follow |
| Handheld urgency | Action, verité |
| Drone push-in | Establishing |
| Orbit / 360° | Product showcase |

### Lens

| Focal | Effect |
|---|---|
| 14–24mm | Wide environmental, distortion |
| 28–35mm | Documentary, wide standard |
| 50mm | Natural eye |
| 85mm | Portrait compression |
| 105–135mm | Tight beauty |
| Macro | Product detail |
| Anamorphic | Cinematic flares |

### Movement (one per prompt)

Static · Pan · Tilt · Dolly · Truck · Pedestal · Crane · Steadicam · Handheld · Drone · Whip pan · Snap zoom · Dolly zoom · Orbit · Match cut

### Lighting

| Scheme | Mood |
|---|---|
| Three-point balanced | Corporate, interview |
| Rembrandt (cheek triangle) | Portrait drama |
| Split | Tension, noir |
| Loop / Butterfly | Glamour |
| High-key | Comedy, FMCG |
| Low-key | Horror, thriller |
| Backlit silhouette | Mystery |
| Golden hour | Romance, nostalgia |
| Blue hour | Documentary, melancholy |

### Color

| Palette | Use |
|---|---|
| Teal & orange | Hollywood action |
| Neon noir (cyan/magenta) | Cyberpunk |
| Desaturated | War, drama |
| Pastel | Romance, comedy |
| Monochrome | Art, experimental |
| Hex codes inline | Brand campaigns |

### Audio (prompt these explicitly)

| Cue type | Example phrase |
|---|---|
| Dialogue | *A woman says, "We have to leave now."* |
| SFX | *SFX: thunder cracks in the distance.* |
| Ambience | *Ambient noise: the quiet hum of a starship bridge.* |
| Music | *calm smooth music* / *retro-futuristic background music* |
| Silence | *no music, just realistic real world sound* |
| Beat sync | *in perfect sync to the beat of the audio* |

### Texture / Style

Claymation · Stop motion · 2D vector · Flat media · Risograph · Pencil sketch with line boiling · Translucent 3D glass · Voxel art · Anime cel-shaded · Watercolor · Crayon · Hologram · Felted puppet · Reflective chrome · Origami

---

## 6. The 20 Genres at a Glance — one-line formula per genre

1. **Cinematic drama:** *Close-up + shallow DOF + motivated practical light + no music + 35mm.*
2. **Action/thriller:** *Handheld + low-angle 24mm + diegetic SFX only + one whip pan.*
3. **Horror slow-burn:** *Static locked off + deep background threat + timed change on second 7 + no jump-scare audio.*
4. **Horror jump-scare:** *POV handheld + flashlight beam + reveal on sweep + single audio sting + cut to black.*
5. **Hard sci-fi:** *Cockpit two-shot + one motivated colored instrument light + accurate weight in micro-gravity + subsonic hum.*
6. **Space opera:** *21:9 wide establishing + ship in motion + anamorphic flares + brass-led orchestral.*
7. **Fantasy/epic:** *Robed figure on cliff + dolly-back reveal + creature audio + warm rim from setting sun.*
8. **Romance:** *Close-up two-shot + Pro-Mist diffusion + warm practicals + cool fill + solo piano.*
9. **Comedy broad:** *Slow-motion 60fps + bright fluorescent + slap bass + exaggerated SFX + one whip pan.*
10. **Comedy deadpan:** *Static MS + flat fluorescent + ambient room tone + one direct-to-camera line.*
11. **Documentary observational:** *Handheld verité + natural light + real environmental SFX + no music.*
12. **Documentary interview:** *Locked-off MS 50mm + soft key through window + room tone + no music.*
13. **Music video performance:** *9:16 + spotlight pulsing on beat + audio reference + camera in sync.*
14. **Music video narrative:** *9:16 + walking dolly + flash cuts on snare hits + audio reference.*
15. **Luxury commercial:** *Macro orbit + single key + black background + piano + tagline on closing frame.*
16. **FMCG commercial:** *9:16 + push-in + condensation/steam detail + acoustic cue + tagline.*
17. **Automotive:** *Tracking shot + golden hour + tire SFX only + sweeping orchestral.*
18. **Tech:** *Translucent device + sequential light-up syncing to electronic ticks + minimal navy.*
19. **UGC TikTok:** *9:16 natural smartphone zoom + hook line to camera + smash cut + single hook beat.*
20. **Trailer:** *Three beats with hard cuts + match cut to hero close-up + orchestral hit + bass drop + title.*

---

## 7. Common Mistakes & Fixes (side-by-side)

| Mistake | Fix |
|---|---|
| *"Make a cinematic video of a woman in a city."* | *"10-second 16:9 close-up of a woman in a camel coat at night under sodium-vapor street light; shallow DOF; no music."* |
| *"Good lighting"* | *"Single key from camera-left at 45°, soft negative fill"* |
| *"Cool camera move"* | *"Slow dolly-back over 6 seconds"* |
| *"Nice mood"* | *"Warm 3000K practicals, cool 5600K rain fill, Pro-Mist diffusion"* |
| *"Make it look like Wes Anderson + Blade Runner + Studio Ghibli"* | Pick one: *"Wes Anderson symmetrical composition, pastel palette"* |
| Re-prompting after a failed edit | *"Edit this keeping everything the same. Change only [X]."* |
| Naming a real celebrity | Use descriptive archetype: *"a 1960s rock star in a velvet jacket"* |
| Branded IP character | Generic equivalent: *"a robotic plumber in red overalls"* |
| Long compound camera instruction | One move per prompt; chain in conversational edits |
| Forgetting audio | Always state audio — "no music" if you want silence |

---

## 8. 20 Ready-to-Use Prompt Recipes

(Genre = #; copy and customize.)

**R1 Drama.** *10-second 16:9 close-up oner. A 38-year-old woman in a camel coat exhales slowly in a rain-streaked taxi at night. Sodium-vapor practicals outside, cool 5600K rim from windshield. 35mm grain. No dialogue, distant rain only.*

**R2 Action.** *10-second 16:9 handheld. Charcoal-suit man sprints through fluorescent parking garage. Low-angle 24mm. Sedan whip-pans in on second 6, headlights flare lens. Tires squeal, engine roar, no music.*

**R3 Horror slow-burn.** *Static locked-off MW, 10 seconds. 1970s living room at 3 AM. Grandfather clock ticks foreground. Hallway figure visible from feet only. On second 8, hallway light flickers, feet gone. No jump-scare audio.*

**R4 Hard sci-fi.** *10-second oner inside near-future cockpit. MS two-shot 35mm. Crew in grey suits. Cyan console glow, red caution at 1Hz. Slow dolly-in. They turn to viewport. Subsonic hum builds. Accurate micro-gravity hair drift.*

**R5 Space opera.** *10-second 21:9. Copper-and-bronze cathedral starship banks across triple-sun system. Light raking hull greebles. Anamorphic flares. Brass orchestral. Locked-off.*

**R6 Fantasy.** *10-second oner. Robed figure on wind-scoured cliff at golden hour. Dolly-back over 8s reveals valley with three dragons. Cloak whips. Distant dragon calls, low choral hum. Warm rim, deep shadows.*

**R7 Romance.** *Close-up two-shot. Couple under string-lit Brooklyn awning during light rain. Her hand on his sleeve. Warm 3000K practicals, cool 5600K rain fill. Pro-Mist. Solo piano. 10s 16:9.*

**R8 Broad comedy.** *10-second oner. Man in too-small suit chases an exercise ball across open-plan office in slow-motion 60fps. Wide 24mm low. Fluorescent. Slap-bass cue, exaggerated SFX on beanbag impact.*

**R9 Deadpan.** *Static MS 10s. Woman in beige cardigan at kitchen table raises fork, chews once, looks to camera, says: "It's fine." No music. Refrigerator hum only.*

**R10 Doc observational.** *10s handheld 16:9. Fisherman mends net on dock at blue hour. Natural light. Hands in focus, face background. Hums tunelessly. Seagulls, distant boat. No music.*

**R11 Doc interview.** *10s locked-off MS 50mm. Scientist at three-quarter angle. Soft 5600K key through window from camera-left. Says: "We didn't know it would behave that way." Office room tone.*

**R12 Music perf vertical.** *10s 9:16. Singer in sequined jumpsuit on smoke-filled stage. Single moving spotlight pulses on downbeat of <audio>. CU to MS pull on beat 4. Lens flare per beat.*

**R13 Music narrative.** *10s 9:16. Young man walks empty subway platform at night. Intercut quick flashes of his day. Warm tungsten platform, cool fluorescent signs. Dolly alongside. Cuts on each snare hit of <audio>.*

**R14 Luxury.** *10s 16:9. Platinum watch on black marble. 8s macro orbit. Single key from right at 30°. Black bg. Champagne accents. Piano. Tick SFX on close. Text "Time, refined." fades white serif lower third.*

**R15 FMCG.** *10s 9:16. Iced cold-brew on sunlit counter. 4s push-in. Condensation beads. Oat-milk pour cascades. Bright daylight. Acoustic cue. SFX clink and pour. Text "Slow morning, fast brew." at second 8.*

**R16 Automotive.** *10s 16:9. Electric SUV silently rolls across salt flat at golden hour. Low-angle tracking, matched speed. Tire-on-salt crunch only, no engine. Sweeping orchestral. Brand white sans-serif on closing frame. Anamorphic.*

**R17 Tech.** *10s 16:9. Translucent slim laptop over deep navy. Components light sequentially: SSD, GPU, display. Electronic tick syncs each. Slow orbit. Overhead key. Device closes, product name white. 24fps.*

**R18 UGC.** *10s 9:16. Natural smartphone zoom. Young woman in kitchen turns to camera: "Okay, you have to see this." Smash cut to first sip, eyes widen. Ambient kitchen, single hook beat at smash cut.*

**R19 Claymation explainer.** *Claymation explainer of mitochondrial respiration, everything made of clay, no hands, stop motion, accurate. 10 seconds. Calm voiceover.*

**R20 Trailer three-beat.** *10s 16:9. Beat 1 (0–3s): drone push toward stormy castle at dusk, thunder. Beat 2 (3–6.5s): hard cut to close-up of sword drawn, metal ring. Beat 3 (6.5–10s): match cut to hero's eyes opening, orchestral hit and bass drop. Title "RAGNARÖK" white serif on black final frame. Anamorphic.*

---

## 9. Iteration Playbook

1. **First pass: scaffold only.** Subject + action + one camera move + one lighting cue + audio direction. Generate.
2. **If composition is right but motion is wrong:** conversational edit *"Keep everything identical except the camera now {new move}."*
3. **If subject identity is right but environment is wrong:** *"Transport the {subject} to {new environment}. Keep clothing, lighting style, and audio identical."*
4. **If style is wrong but content is right:** *"Keep the action and subject identical. Apply {one style anchor} throughout."*
5. **If audio is off:** *"Keep all visuals identical. Replace audio with {new direction}."*
6. **Three failed edits without progress = restart from scratch.** Edit credits compound.
7. **For multi-clip sequences:** finalize one anchor clip, then use it as a reference for subsequent clips with identical identity descriptors.

---

## 10. Parameter Quick Reference

| Setting | Value |
|---|---|
| Clip length | 4 / 6 / 8 / 10s |
| 10s tier | Plus/Pro/Ultra only |
| Aspect | Landscape (default) / Portrait — restate in prompt |
| Resolution | Not officially specified; 1080p upscale on Pro |
| Frame rate | Not officially specified; 24fps appears in official examples |
| Audio | Native, voice-reference input only at launch |
| Image refs | Up to 5 (Gemini app) |
| Video ref | 60s/1GB upload, trim to 10s for edit |
| Voice ref | 1 per generation |
| Avatar | English only, 18+, not in EEA/CH/UK |
| Watermark | SynthID + C2PA, not removable |
| API | Not yet live as of 2026-05-22 |
| Plus | $7.99/mo, 200 Flow credits |
| Pro | $19.99/mo, 1,000 credits |
| Ultra | $99.99/mo, 10,000 credits |

---

## 11. Anti-Patterns (what NEVER to do)

- ❌ **Never** stack 3+ style anchors. Prompt collapse is guaranteed.
- ❌ **Never** name a real celebrity, athlete, or public figure. Refusal.
- ❌ **Never** reference branded IP characters (Disney, Marvel, anime IPs, sports teams). Refusal.
- ❌ **Never** issue a vague edit prompt like "make it better." Over-editing.
- ❌ **Never** prompt for content involving minors in unsafe contexts. Hard refusal.
- ❌ **Never** rely on Omni for exact text rendering of long copy — keep on-screen text to ≤ 8 words.
- ❌ **Never** prompt timing in exact frames ("on frame 47"). Use seconds or beats.
- ❌ **Never** ask for cloning of another person's voice/face. Use Avatars for self-likeness only.
- ❌ **Never** assume 4K — Omni Flash output resolution is not publicly specified at 4K.
- ❌ **Never** chain >5 conversational edits on the same clip without re-anchoring with a reference image.
- ❌ **Never** plan production around the Omni API today — it is not yet live. Use Veo 3.1 on Vertex AI for any pipeline that requires API access in May 2026.
- ❌ **Never** rely on Omni for production-grade lip-sync of speech edits to existing footage — this feature is deliberately withheld at launch.

---

*End of guide. File 1 (research report) and File 2 (practical guide) above are designed to be saved as `gemini-omni-video-research.md` and `gemini-omni-video-guide.md` respectively.*