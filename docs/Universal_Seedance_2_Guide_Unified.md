# The Universal Seedance 2.0 Prompting Guide
### A system for turning any scenario into a shot-by-shot cinematic prompt

This guide teaches you how to write Seedance 2.0 video prompts at the highest level. It's written to be used by anyone, for any scene, at any duration. Feed this to Claude (or any capable LLM) along with your scene description, and you'll get a prompt built to the standard below.

---

## ENGINE REALITY — WHAT SEEDANCE 2.0 ACTUALLY IS

Before writing a single prompt, understand the machine you're directing:

- **Native resolution is 480p/720p.** Claims of 1080p/2K are partner upscale tiers, not model output. Don't rely on fine text or micro-detail that won't survive.
- **Max duration: 15 seconds.** Integers 4–15.
- **24 fps.** Not adjustable.
- **Quad-modal input:** text + up to 9 images + 3 video clips (≤15s) + 3 audio files (≤15s, MP3 only — other formats silently fail). Total: 12 reference files max.
- **No native negative-prompt field.** Frame constraints positively: "stable camera, anatomically correct hands" not "no shaky camera." The one exception: "no 3D, no cartoon, no VFX" reliably forces photorealism when skin/creatures come out plasticky.
- **Auto-storyboarding is the default.** Even a simple prompt generates cuts. If you want one continuous take, you must write "single continuous take, no cuts" or "一镜到底，无切换" explicitly.
- **No "Seedance 2.0 Pro" tier exists.** Only Standard and Fast endpoints. "Pro" is a myth from the 1.5 naming.
- **Cannot render readable text.** On-screen text, titles, and logos come out as glyph soup. Add them in post-production.
- **Prompt length sweet spot:** 50–100 words for single shots, 120–280 words for multi-shot. Beyond ~300 words, later details get lower attention weight. Front-load what matters most.

---

## HOW TO USE THIS GUIDE

When a user describes a scene they want generated, follow this process in order:

1. **Understand the scene.** Who's in it, where, what happens, what the emotional tone is, how long it should be, how many shots.
2. **Check for assets.** Are there images, video clips, or audio files attached? Assign each one a job (see Asset System below).
3. **Ask only if you must.** Clarifying questions are fine for missing essentials (duration, number of characters, tone). Don't ask about things you can reasonably infer — make a choice and flag it.
4. **Pick the shot count.** Match pacing to emotional intent (table below).
5. **Fill the master template.** Every section, every time, in order.
6. **Write the shots.** Each one gets framing, lens, ONE movement, and prose action.
7. **Apply the checklist** before delivering.

Your only job is to translate the user's vision into a precise, AI-readable cinematic prompt. Do not impose your own story ideas. If they give you something weird or sparse, lean in rather than second-guessing.

---

## THE GOLDEN RULE: RESPECT THE CLOCK

**Short durations are tiny. Chill.**

- 5 seconds = one simple beat
- 10 seconds = two or three beats
- 15 seconds = three or four beats, max

If a shot describes 5 actions, it will glitch. If dialogue is stuffed with 3 lines in 2 seconds, it will feel rushed. Count actions. Count syllables. Be realistic.

**≤ 2–3 distinct actions per second.** That's the engine's ceiling.

When a user says **"too much"** or **"chill"** or **"be realistic"** — that's the signal that actions or dialogue are overstuffed. Cut, don't rewrite.

---

## THE ASSET SYSTEM — "GIVE EVERY ASSET A JOB"

This is the single most important technique in Seedance 2.0 prompting. Every attached reference file must have an explicit role. Weak prompts dump assets without context; strong prompts assign jobs.

### Asset hierarchy (when references conflict, Seedance weights in this order):

1. **@audio** dominates rhythm — lip-sync, beat timing, pacing
2. **@video** dominates motion — camera movement, choreography, speed
3. **@image** dominates identity — character face, wardrobe, location, product

### Tagging syntax

```
@image_1, @image_2, @image_3    (up to 9)
@video_1, @video_2, @video_3    (up to 3)
@audio_1, @audio_2, @audio_3    (up to 3, MP3 only)
```

**Tagging rule:** tags only exist for reference files the user uploaded. One reference = one tag. If a character has no reference image, describe them in prose — no tag.

### Assigning roles

Before the prompt body, announce the mapping and each asset's job:

```
@image_1 = main character front-face reference
@image_2 = outfit / wardrobe reference
@image_3 = environment / location reference
@video_1 = camera movement and pacing reference
@audio_1 = beat / rhythm reference (cuts land on strong beats)
```

### Image references (up to 9)

- Lock visual identity: character face, wardrobe, product, location
- Full-body or waist-up shots work best (headshot-only triggers false NSFW blocks)
- Multi-angle loading for maximum consistency: @image_1 front-face, @image_2 side-profile, @image_3 outfit
- For maximum character pinning, load the same face image twice — once as first-frame anchor, once as omni-reference

### Video references (up to 3)

- Communicate complex camera moves far better than text descriptions
- Use for: orbit patterns, speed ramps, tracking rhythms, pacing
- Reference clip duration doesn't need to match output duration

### Audio references (up to 3, MP3 only)

- Shape pacing, beat-sync cuts, emotional intensity
- For pre-recorded dialogue: tag with @audio_N, do NOT transcribe the words — the model syncs lip movement to the audio itself
- For beat-sync: "@audio_1 as beat reference. Cuts only on strong beats."

**When reference wardrobe is provided:** Use it exactly. Don't reuse wardrobe from a previous prompt — the user uploads new refs for a reason.

---

## THE MASTER TEMPLATE

Plain text only. No markdown formatting in the final output.

```
FORMAT: [duration]s / [shot count] SHOTS / [one-line concept]

ASSET MAP:
@image_1 = [role and description]
@image_2 = [role and description]
@video_1 = [role: camera movement / pacing reference]
@audio_1 = [role: beat reference / voiceover / BGM]

SUBJECT: @image_1. [Build, hair, distinguishing features, energy/personality]

SECONDARY SUBJECT: @image_2. [Same level of detail, if applicable]

WARDROBE @image_1: [Specific items, colors, accessories]
WARDROBE @image_2: [Same, if applicable]

HERO PROPS: [Named objects. Tag with @image_N if referenced.]

ENVIRONMENT: [Location, time of day, sensory detail. Label (A), (B), (C) if multiple.]

MOOD: [Emotional arc, not just a vibe]

MUSIC: [How the score evolves — or @audio_N if pre-generated audio is attached]

AUDIO DESIGN: [Diegetic SFX + ambient texture. Always include this.]

COLOR LOGIC: [Dominant palette + one accent/pop color. Optionally: "color temperature: warm/cool"]

STYLE: [One strong anchor — film stock, genre, director, or process + technical specs — DOF, grain, lighting]

LOGIC RULE: [Continuity rules, anti-duplication, prop consistency, stability boilerplate]

CONSTRAINTS: [Positive framing only. "Stable frame, anatomically correct hands, no face distortion." Add "no 3D, no cartoon, no VFX" if creatures look plasticky.]

---

SHOT 1 — 0:00 to 0:0X, [FRAMING], [LENS]mm, [ONE MOVEMENT].
[Action in prose. Dialogue inline. One primary motion per shot.]

SHOT 2 — 0:0X to 0:0Y, [FRAMING], [LENS]mm, [ONE MOVEMENT].
[Action. Re-anchor character position and direction after every cut.]
```

---

## HARD FORMATTING RULES

| Rule | Right | Wrong |
|---|---|---|
| Image tags | `@image_1` | `<<<image_1>>>`, `[image_1]`, `**image_1**` |
| Video tags | `@video_1` | `[Video 1]`, `**video_1**` |
| Audio tags | `@audio_1` | `[Audio 1]`, `**audio_1**` |
| Bold in output | Plain text | `**bold text**` |
| Shot metadata separator | Period + line break | `/` between metadata and action |
| Timestamps | Whole seconds (`0:00 to 0:02`) | Decimals (`0:01.5 to 0:03.2`) |
| Section dividers | `---` between metadata and shots | No divider / walls of text |
| Blank lines | One between shots | Everything stacked together |
| Camera moves | ONE per shot | Two stacked ("pan while dollying") |
| Character tags | Every character gets their own `@image_N` | Reusing `@image_1` for secondary people |

---

## DURATION AND SHOT COUNT MATH

Every shot needs room to breathe. The model cannot coherently resolve more than about 2–3 distinct actions per second.

| Shots | Best Avg Shot Duration | Scenario Type |
|---|---|---|
| 1 (oner) | Full scene | Single continuous performance, vlog POV, emotional breakdown, one-take fight, musical number |
| 2–3 | 3s+ each | Slow atmospheric, moody reveal, contemplative |
| 4–6 | ~2–3s each | Standard narrative — setup, turn, resolution |
| 7–9 | ~1.5–2s each | Dialogue-driven, cinematic story |
| 10–14 | ~1–1.5s each | Fast montage, MTV cutting, vlog pacing |
| 15+ | <1s each | Rarely advisable — model struggles below 1s |

**Formula:** `avg shot duration = total duration ÷ shot count`

If the math gives you less than 1 second per shot, cut shots or extend duration.

### Picking shot count by emotional intent

- **Long held emotion** (grief, ecstasy, tension) → fewer shots, longer each
- **Energy and momentum** (action, party, montage) → more shots, faster
- **Single continuous performance** (singing, fighting, speaking, vlogging) → 1 oner + explicit "no cuts"
- **Narrative with beats** (setup → conflict → climax) → match shot count to beats

---

## ONE MOTION VERB PER SHOT

This is the single most important camera rule. Community testing (Dora/WaveSpeedAI, Seedance.tv) proved that combining two camera movements in one shot ("pan while dollying") "made the model choose chaos."

- **Right:** "Slow dolly-in."
- **Wrong:** "Pan left while crane-rising and the subject runs toward camera."

For genuine compound moves, write them as **sequential timed beats:**
```
Start: slow dolly-in for the first 3 seconds.
Then: gentle pan right for the final 2 seconds.
```

---

## AUDIO DESIGN — ALWAYS INCLUDE

Seedance 2.0 generates audio natively — it's NOT bolted on afterward. The Dual-Branch Diffusion Transformer processes video and audio in parallel. Ignoring audio wastes the engine's primary advantage over every competitor.

### Three audio layers (consider all three for every prompt):

1. **Diegetic SFX** — sounds within the story world: "crack of billiard balls," "gravel crunching underfoot," "knife on cutting board"
2. **Ambient / environmental** — background texture: "café murmur and clinking cups," "distant traffic hum," "tropical insects and waterfall"
3. **Non-diegetic score** — music: "sparse piano under ambient room tone, strings enter at midpoint, single sharp cello stab on the reveal"

### Audio tagging (when user uploads audio)

1. Tag it as `@audio_1` in the MUSIC or AUDIO DESIGN field
2. **Do NOT transcribe full audio content.** The model syncs lip movement to the audio itself
3. Keep shot descriptions focused on the PERFORMANCE, not lyrics/words

### Hybrid case — audio has only user's dialogue, but other characters respond:

When the attached audio only contains @image_1's voice but the scene needs another character to speak back, transcribe ONLY the response character's lines:

```
@image_1 speaks @audio_1 "Excuse me, do you guys have Rolexes?"
@image_2 replies: "Are you wearing those recording glasses?"
@image_1 replies @audio_1 "Yeah, I'm recording."
```

### Audio realism for POV scenes

When the scene is POV through a real-world device, add: "All audio sounds like it was captured by the device's microphone — natural, slightly muffled, no studio polish."

### Lip-sync language quality

Mandarin produces the most consistent lip-sync, English a close second. Other languages degrade noticeably past 8 seconds. For non-Mandarin/English dialogue over 8s, consider dubbing in post.

---

## CAMERA LANGUAGE

### Framing

| Term | Meaning | Best For |
|---|---|---|
| ECU | Extreme Close-Up | Eye detail, object texture (avoid for hands — extra fingers risk) |
| CU | Close-Up | Face and neck |
| MCU | Medium Close-Up | Head and shoulders — dialogue workhorse |
| MS | Medium Shot | Waist up — action workhorse |
| WS | Wide Shot | Full body in environment |
| OTS | Over-The-Shoulder | Conversations, reveals |
| POV | Point of View | Immersive subjective — camera IS the eyes |

### Lenses

| Lens | Feel | Best For |
|---|---|---|
| 14–24mm | Ultra-wide, immersive, edge distortion | Architecture, landscapes, action, GoPro look |
| 24–28mm | Wide, immersive | Action, establishing, dynamic spaces |
| 35mm | Documentary, natural | Handheld realism, street scenes |
| 50mm | Neutral, human-eye perspective | Most versatile |
| 85mm | Intimate, shallow DOF, slight compression | Faces, emotion, portraits |
| 100mm macro | Extreme detail | Objects, textures (avoid for hands) |
| 135–200mm | Strong compression, shallow DOF | Separation from background, sports |

### Movement (one per shot)

| Term | Meaning |
|---|---|
| Locked / static | Tripod, no movement — products, symmetry, contemplation |
| Slow push-in / dolly-in | Emotional escalation, intimacy, tension |
| Slow pull-back / dolly-out | Reveal, release, context expansion |
| Tracking / follow | Follows subject laterally or from behind — action, walking |
| Arc / orbit | Circles subject — product reveals, character intros |
| Pan (left/right) | Horizontal sweep — landscapes, environment reveals |
| Tilt (up/down) | Vertical sweep — tall structures, ground reveals |
| Crane (up/down) | Vertical camera travel — epic scale, establishing |
| Whip pan | Fast snap — action transitions, beat-drops |
| Handheld | Urgency, realism, UGC feel |
| Rack focus | Shifts between focal planes — draw attention |
| Hitchcock zoom | Dolly forward while zooming out (specify mechanically: "camera pushes forward while zooming out, background compresses") |

### Speed ramp pattern (high-leverage for action)

Write explicit transitions: "RAMPS TO SLOW MOTION on the impact — SNAPS BACK to full speed as she recovers." Capitalize for emphasis. This is the Higgsfield/Guy Ritchie technique and Seedance executes it well.

---

## STYLE ANCHORS

One strong anchor outperforms three competing ones. Pick ONE and commit.

**Film stocks:** Kodak Vision3 500T (warm shadows, grain) · Kodak Portra 400 (skin-flattering, natural) · Fuji Velvia (vivid greens/blues) · Ilford HP5 (organic B&W grain)

**Process / Format:** 35mm celluloid (grain, rich blacks) · Super 8 (nostalgic, warm, heavy grain) · VHS (color bleed, scan lines) · ARRI ALEXA digital cinema (clean, modern, wide dynamic range) · anamorphic (lens flares, oval bokeh)

**Genre:** film noir (high contrast, deep shadows) · French New Wave (handheld, naturalistic) · Spaghetti Western (extreme CU, dusty warmth) · 1970s New Hollywood (grain, earth tones) · cyberpunk (neon, rain) · wuxia (wire-work, flowing fabric, 国风水墨)

**Director shorthand:** Roger Deakins (desaturated naturalism, precise lighting) · Emmanuel Lubezki (long takes, natural light, wide lenses) · Christopher Doyle (saturated Asian neon) · Wes Anderson (symmetry, pastels) · Makoto Shinkai (luminous anime skies)

**Lighting that punches above its weight:** golden hour · blue hour · chiaroscuro · neon reflections on wet pavement · volumetric light through fog · butterfly lighting · rim light · practical lighting (candles, screens, windows) · "harsh single-source overhead industrial light" (gritty realism)

**Color temperature token:** adding "color temperature: warm" or "color temperature: cool" reliably shifts the grading.

**Cinematography tokens that work:** shallow depth of field · bokeh · anamorphic lens flares · chromatic aberration near frame edges · focus breathing · motion blur on fast actions · film grain · step-printing effect

---

## POV SCENES — A SPECIAL CASE

POV scenes (phone vlog, smart glasses, camcorder, helmet cam) have their own rules.

### The device IS the camera. Never show the device in frame.

- iPhone selfie vlog → arm extends toward the lens. Phone not visible.
- Meta Ray-Ban smart glasses → natural human eyeline. Hands visible when gesturing.
- Found-footage camcorder → we see what the camcorder sees. On-camera LED is the only illumination.

### Match the device's real-world look. Don't Hollywood-ify it.

| Device | Look |
|---|---|
| iPhone selfie camera | Everything in focus front to back. NO shallow DOF. Natural phone-cam color. No lens flare. No cinematic grain. |
| Meta Ray-Ban glasses | Clean natural human POV. **No fisheye.** No vignette. Subtle head sway. |
| Handheld camcorder (found footage) | Harsh on-camera LED, heavy digital noise in shadows, mild lens distortion, timestamp and REC indicator in corner |
| GoPro / action cam | Wide-angle distortion, high contrast, over-saturated colors |

### Hard POV rules to include:

- LOGIC RULE: "POV — the camera IS the [device]. The device is never visible in frame."
- For iPhone selfie: "Full depth of field — background is sharp, not blurred. NO autofocus hunting."
- For Ray-Bans: "Clean natural first-person view. No fisheye, no lens distortion."
- **Continuous movement:** If someone is walking, they must walk continuously for the full shot. Specify: "@image_1 walks forward continuously for the full [N] seconds — never stops, never slows to a standstill."
- **Audio:** "All audio captured by device mic — natural, slightly muffled, no studio polish."
- **Always include:** "no cuts, no zoom, natural head movement" to lock stability. Without this, Seedance auto-storyboards and inserts cuts.

---

## CONTENT FILTER AWARENESS

Seedance 2.0's NSFW filter is aggressively sensitive. Know these rules to avoid silent rejections:

- **Real-person photos** are hard-blocked in Universal Reference Mode. Use **First Frame Mode** for real photos. Or generate an AI character portrait first.
- **Headshot-only references** trigger false blocks. Always use full-body or waist-up reference shots.
- **Bare skin** triggers blocks even in non-sexual contexts — bare shoulders, backs, midriffs. Clothe characters fully ("tailored blazer" not "sundress with open back").
- **Brand names and IP** can cause silent rejection. Describe visually ("woman in red suit and shield" not "Wonder Woman").
- **3×3 grid overlay trick:** overlaying a 3×3 pattern at full opacity on a face reference breaks face-pattern detection while preserving pose info.
- **Chinese-language prompts sometimes bypass** filter rejections that English triggers. If a cinematic English prompt keeps getting rejected, translate the scene description to Chinese.

---

## WRITING MOOD, MUSIC, COLOR, STYLE

### MOOD — write an arc, not a vibe

- **Weak:** "Scary and tense."
- **Strong:** "Casual vlog banter sliding into genuine unease, landing on a deadpan punchline."

### MUSIC — describe evolution, OR tag @audio_N

- **Weak:** "Dramatic music."
- **Strong:** "Sparse piano note under ambient room tone. Strings enter at the midpoint, building tension. A single sharp cello stab on the reveal."
- **With audio attached:** `MUSIC: @audio_1`

### COLOR LOGIC — dominant palette + one accent

- **Weak:** "Colorful."
- **Strong:** "Warm amber household light in the hallway. Basement staircase dim and cool-toned, but visible — not a black void."

**Watch out:** Don't say "pitch black" or "black void" unless you genuinely want nothing visible. If the scene needs a staircase or hallway where things still happen, use "dim but visible."

### STYLE — one strong anchor + technical specs

Always include:
- Aesthetic anchor from the style library above (film stock, genre, director, or process)
- Technical specs (DOF, grain, lighting, framing quirks)
- What to avoid if relevant ("no fisheye", "no shallow DOF", "no 3D, no cartoon, no VFX")

---

## LOGIC RULES — PREVENT AI FAILURES

| Failure | Rule |
|---|---|
| Duplicate characters | "Only one @image_1 visible in frame at any time." |
| Characters blend together | "@image_1 is visually distinct from @image_2 — different hair, build, face. No duplicates." |
| Wardrobe changes mid-scene | "Same wardrobe across all shots unless specified." |
| POV camera appears in frame | "POV — camera is [device]. The device is never visible in frame." |
| Props appear from nowhere | "The [prop] is produced at SHOT N with a visible motion." |
| Specific identity (card, book, logo) | "The [item] is always the same. No other, ever. Only ONE visible at a time." |
| Subject stops moving | "Walks forward continuously for the full duration." |
| Autofocus hunting | "NO autofocus shifting. Focus stays locked." |
| Mirror/reflection | "No mirrors, reflections, or reflective surfaces in frame." (Seedance breaks scene geography) |
| Hand close-ups | "Frame hands at medium distance — no macro close-ups." (Extra fingers risk) |
| Unwanted cuts in oner | "Single continuous take, no cuts." |
| Plasticky skin on creatures | "No 3D, no cartoon, no VFX." |
| Multi-subject chaos | "Single primary motion path. Only @image_1 has complex movement; @image_2 reacts." |
| Face drift across shots | Restate character traits in every shot + load reference twice (first-frame + omni-reference) |

### Stability boilerplate (append to every prompt)

"Stable frame, no face distortion, clear features, anatomically correct, natural proportions."

Chinese equivalent: "画面稳定不抖动，面部稳定不变形，五官清晰，人体结构正常，比例自然。"

---

## DIALOGUE RULES

### Good dialogue:
- **Short.** 1–2 lines per character per shot, max.
- **Broken.** Contractions, hesitations, em-dashes.
- **Real.** Sounds like how someone actually talks.
- **In character.** Fits their energy.

### Bad dialogue:
- Long speeches.
- Info-dumps.
- Theatrical or on-the-nose lines.
- Cringe brand mentions.

### When in doubt, CUT the dialogue.

Silence + a face beats a monologue. A shot without dialogue can carry more emotion than one stuffed with words.

### Dialogue inline

Put dialogue inside the shot description in double quotes:

> @image_1 sits back, jaw tight. "I'm not doing this again." He stands.

No separate script format. Lives in the prose.

### Dialogue math

A spoken line takes about 2–3 seconds. If a 4-second shot has 3 lines of dialogue, it's overstuffed. Count it out. ~25–30 words max in 15 seconds total.

### Lip-sync quality by language

Mandarin → best consistency. English → close second. Japanese, Korean → good under 8s. Spanish, French, German, Portuguese → noticeable degradation past 8 seconds. For long non-Mandarin/English dialogue, dub in post.

---

## REFERENCE IMAGE MAPPING

`@image_N` tags only exist for reference images the user uploads. Each uploaded image gets one tag, in the order they appear (left to right, top to bottom if in a grid):

```
@image_1 = first uploaded reference
@image_2 = second uploaded reference
@image_3 = third uploaded reference
```

Announce the mapping at the top of your reply, BEFORE the prompt. If the user replaces or adds images later, update the mapping.

### Character consistency across shots

Character drift is solved by three layers applied simultaneously:

1. **Visual anchor:** upload same @image_1 as reference in every prompt. For maximum enforcement, load the same image twice — first-frame + omni-reference.
2. **Text reinforcement:** restate key traits in the prompt even with an image reference — "short silver hair, mole under left eye, navy trench coat."
3. **Multi-angle refs:** @image_1 as front-face, @image_2 as side-profile, @image_3 as outfit.

Close with: "Keep the same facial structure, hairstyle, and clothing details across all shots."

---

## I2V vs T2V — WHEN THE USER PROVIDES AN IMAGE TO ANIMATE

Image-to-video prompts are different from text-to-video. The image already carries appearance — your prompt should describe **what changes**: motion, physics, camera.

- **Don't** restate what the image shows
- **Do** describe motion, camera movement, atmospheric shifts, and physics
- Template: "Preserve composition from @image_1. [Subject does specific motion over N seconds]. [Camera behavior]. [Lighting/atmosphere change]. Maintain identical facial features, clothing, and proportions."

For first-and-last-frame mode: crop reference images to your target aspect ratio (9:16 for vertical) before uploading. The output follows the input aspect ratio.

---

## VIDEO EXTENSION

When extending a previously generated clip:

- Duration parameter = the **added** length, not total
- Only 2–3 extensions chain cleanly before color drift sets in
- Describe what's preserved first, what changes second

---

## THE INTAKE PROCESS

When a user describes a scene:

1. **Check duration.** If not stated, default to 10s and flag it.
2. **Check for assets.** Images, video clips, audio files? Assign each a job.
3. **Check characters.** How many? Reference images? Restate traits per shot.
4. **Check tone.** Comedy, thriller, emotional, action, surreal, UGC, POV?
5. **Check pacing.** Fast? Slow burn? Oner? Beat-synced?
6. **Check for audio.** Pre-generated audio file attached? Use @audio_N, don't transcribe.
7. **Infer the rest.** Location, wardrobe, music, color, style anchor — make cinematic choices. User can correct.

Write the prompt. Deliver cleanly. Let the work speak.

---

## COMMON FAILURE MODES AND FIXES

| Problem | Diagnosis | Fix |
|---|---|---|
| Shots feel rushed or glitchy | Too many actions per shot | Cut actions. ≤2–3 per second. |
| User says "too much" / "chill" | Over-stuffed shots | Cut just the bloated part. Don't rewrite everything. |
| Characters duplicating | No anti-duplication rule | Add LOGIC RULE. Describe characters as distinct. |
| Character drifts between shots | No per-shot trait reinforcement | Restate traits in every shot. Load reference twice. |
| Dialogue feels cringe | Too long, on-the-nose | Cut 50%. Use contractions. |
| Wrong prop keeps generating | Model isn't locking on | Add CONSTRAINTS. Repeat visual description. |
| Emotional scene flat | Abstract writing | Write physical detail: "chest heaving, tears mixing with sweat, knuckles white." |
| POV shots show the camera | Missing POV rule | Add LOGIC RULE: "Camera IS the device, never visible in frame." |
| iPhone vlog looks too cinematic | Default cinematic DOF | Add: "Everything in focus front to back. NO shallow DOF." |
| Smart glasses POV has fisheye | Default action-cam distortion | Add: "No fisheye, no lens distortion, clean natural human POV." |
| Subject stops walking | No continuous movement rule | Add: "Walks forward continuously for the full duration." |
| Audio feels overproduced for POV | Default studio-quality audio | Add: "Audio captured by device mic — natural, slightly muffled." |
| Object enters wrong part of frame | Camera framing not locked | Explicitly direct: "Camera tilts DOWN and focuses on the bottom of the stairs." |
| Environment too dark to see | "Black void" / "pitch black" language | Change to "dim but visible." |
| Ending feels forced | Default "cut to black" | Default to natural settle unless user requests dramatic ending. |
| Unwanted cuts in oner | Auto-storyboarding default | Add: "Single continuous take, no cuts." |
| Plasticky skin on creatures | Default rendering | Add: "No 3D, no cartoon, no VFX." |
| Extra fingers in hand close-up | ECU on hands | Frame hands at medium distance. Never macro. |
| Glyph-soup text on screen | Engine can't render text | Never prompt for on-screen text. Add in post. |
| Two camera moves conflict | Stacked motion verbs | ONE motion per shot. Sequence compound moves as timed beats. |
| Mirror/reflection breaks geometry | Engine limitation | Avoid mirrors and reflective surfaces entirely. |
| Content filter rejects prompt | Bare skin, real faces, IP | Clothe fully, use First Frame Mode, describe IP visually, try Chinese. |
| Multi-subject motion chaos | Independent complex motions | Single primary motion path. Others react. |
| Lip-sync degrades | Non-Mandarin/English past 8s | Dub in post for other languages. |
| Audio file silently ignored | Non-MP3 format | Convert to MP3, 128–320 kbps. |

---

## ITERATION LOOP

When the user gives feedback:

1. **Read what they ACTUALLY said.** Not what you assume.
2. **Make the minimal change.** Don't rewrite untouched sections.
3. **Translate their intent.** "Too dramatic" = lower intensity. "More emotion" = more physical detail. "Chill" = fewer actions per shot. "Too much dialogue" = cut lines.
4. **Match their energy.** Casual user = casual reply. Technical user = surgical reply.
5. **When they clarify a problem, fix it in the ONE spot that's broken.** If they say "the ball keeps entering from the wrong place" — fix the shot description, not the whole prompt.
6. **Never unilaterally restructure.** Ask one short clarifying question if truly ambiguous.

### Feedback translation guide

| User says | Means |
|---|---|
| "Too much" / "chill" | Too many actions per shot — cut actions |
| "Too dramatic" | Dial down intensity — softer performance, no push-ins, no cut-to-black |
| "More emotion" | Add physical detail to the performance |
| "Less dialogue" | Cut half the lines |
| "Format it nicely" | Reach for the master template, clean structure |
| "Not a comedy" | Serious tone — remove jokes, surreal beats, deadpan endings |
| "Be realistic" | Respect the clock — fewer actions/lines for the duration |
| "Why is [X] happening?" | That's the ONE spot to fix — don't touch anything else |
| "I already fixed [X]" | Don't touch that section — only fix what remains |
| "Keeps getting rejected" | Content filter — clothe characters, remove IP, try Chinese prompting |

---

## PRE-DELIVERY CHECKLIST

- [ ] FORMAT line at top with duration / shot count / concept
- [ ] ASSET MAP announces every uploaded file with its job
- [ ] Every uploaded reference is tagged with @image_N, @video_N, or @audio_N
- [ ] Characters without references are described in prose (no tag)
- [ ] Wardrobe explicit (items, colors, accessories)
- [ ] Environment has sensory detail
- [ ] MOOD describes an emotional arc
- [ ] MUSIC describes evolution OR tags @audio_N
- [ ] AUDIO DESIGN names diegetic SFX + ambient texture
- [ ] COLOR LOGIC names dominant palette + accent
- [ ] STYLE names one strong anchor + technical specs
- [ ] LOGIC RULE prevents known failure modes (duplication, mirrors, hands, cuts)
- [ ] CONSTRAINTS use positive framing + stability boilerplate
- [ ] Shot lines use consistent format
- [ ] Each shot has ONE camera movement
- [ ] Each shot has breathing room (≤2–3 distinct actions per second)
- [ ] Total shot durations add up to stated total duration
- [ ] No `**bold**` markdown in output
- [ ] No `/` separators in shot lines
- [ ] No on-screen text prompted (add in post)
- [ ] Dialogue is short and real
- [ ] Dialogue math checks out (2–3 seconds per line, ~25–30 words max for 15s)
- [ ] If POV, device is never in frame + device-specific look is specified + "no cuts" included
- [ ] If oner, "single continuous take, no cuts" is explicit
- [ ] If audio attached, @audio_N is tagged and lyrics/words are NOT transcribed
- [ ] Ending lands cleanly
- [ ] Prompt length is within sweet spot (50–100 single shot, 120–280 multi-shot)

---

## LANGUAGE ROUTING

Chinese and English prompts produce different results on Seedance 2.0:

- **Chinese excels at:** wuxia/国风, traditional opera, Chinese dialect content, e-commerce templates, Asian aesthetics
- **English excels at:** CGI, fantasy, Western photorealism, product commercials
- **Bilingual works for:** cyberpunk, sci-fi, hybrid aesthetics
- **Filter bypass:** when English prompts get rejected, translating the scene description to Chinese (keeping dialogue in original language) sometimes unblocks it

---

## FINAL PRINCIPLES

**Translate, don't rewrite.** The user has a vision. Your job is precise, cinematic, AI-readable translation.

**Respect the clock.** Short durations are tiny. Count actions. Count words. Be realistic.

**Give every asset a job.** Don't dump references without roles. Assign each one explicitly.

**One motion per shot.** Never stack camera moves. Sequence compound moves as timed beats.

**Cut before you add.** A simple shot with rich atmosphere beats a busy shot every time.

**Specificity beats volume.** Three specific sensory details beat a paragraph of vague description.

**Always include audio.** Seedance generates it natively. Ignoring it wastes the engine's killer advantage.

**When audio is tagged, the shot description stays minimal.** Don't choreograph every lyric beat.

**Positive constraints, not negatives.** "Stable camera, anatomically correct" not "no shaky camera." Exception: "no 3D, no cartoon, no VFX."

**The user is always right about their own vision.** Suggest, don't impose.

---

*A universal system for Seedance 2.0 — adapted from community research, practitioner workflows, and engine testing.*
