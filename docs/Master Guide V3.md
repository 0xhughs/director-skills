# The Ultimate AI Director's Guide: Mastering Grok Cinematic Prompt Engineering

---

## WHAT'S NEW IN v3.0

This edition merges the original 7-Pillar architecture with confirmed findings. Key upgrades:

- **Timestamp brackets replaced** with Grok-native prose sequencing and official `Camera switch.` / `Cut to:` triggers
- **Front-Loading Rule** added as a mandatory preamble discipline
- **Stability Constraint** added as a mandatory prompt closer
- **Anti-AI Guardrails expanded** with Aurora's slow-motion bias fix, hand/finger workarounds, and crowd collapse rules
- **Camera vocabulary expanded** with named glass (Cooke, Zeiss, Panavision), shutter angle, frame-rate ladder, and 5 new specialty moves
- **Audio expanded** with voice specification formula, default muzak override, lip-sync accuracy note, trans-diegetic sound, and composer proxy references
- **Workflow section added** with full Image-First Pipeline and Master Consistency Lock for video extension
- **Genre library expanded** from 13 to 22 genres with full per-genre blueprints (lighting, lens, color grade, DP/director reference, example prompt)
- **Unique contributions added**: 21:9 Cinematic Crop Hack, API reference block, competitive tool guidance, `Audio narration:` voiceover trigger

---

## I. The Method: Directing the Rendering Engine

AI video models do not natively understand physics, mass, or linear time — they understand pixel patterns and sequence. To achieve studio-quality cinematic results, stop writing descriptive "prompts" and start writing **directorial prose**.

### The Three Core Philosophies

**1. Sequential Narrative Flow (Replace Timestamps)**

Grok's Aurora engine does **not** parse bracket timestamps like `[0:00-0:05]`. If used, the model ignores the numbers and blends the entire prompt into a continuous blob, often hallucinating transitions. The fix: control time through **narrative sequence words**.

- Use: `"First... then... suddenly... at the moment of... afterward..."`
- For hard cuts: `Camera switch.` or `Cut to:` — these are officially documented transition triggers

> **Correct:** "The soldier slowly removes his helmet. Then the camera pushes in on his exhausted eyes. Camera switch. Wide shot of the artillery-scarred horizon."
>
> **Incorrect:** "[0:00-0:03] soldier removes helmet. [0:03-0:06] push in on eyes. [0:06-0:10] wide shot."

The 7-Pillar labels below are your internal planning scaffold — use them to organize your thinking. But when writing the final submitted prompt, convert them into flowing prose using the sequencing words above.

**2. Action & Consequence**

Never state an action without its physical consequence. If a character falls, they fall "with heavy physical momentum, displacing dust and dirt." This forces Aurora to simulate gravity rather than floaty, underwater movement.

**3. Anti-AI Guardrails (Positive Commands)**

Aurora has no negative prompt field — negative commands are silently ignored. Worse, mentioning a concept with a negative prefix forces the model's attention *toward* that concept. The fix: exhaustively describe what IS present to crowd out unwanted elements.

- Instead of: `"no blur"` → use: `"sharp focus"`
- Instead of: `"no extra characters"` → use: `"single subject only, empty frame background"`
- Instead of: `"no CGI smoothing"` → use: `"visible pores, translucent sub-surface scattering"`
- **Exception:** `"no music"` and `"no score"` work because they specify audio track contents, not negation.

### Prompt Economy (Token Discipline)

Strip all filler — Aurora doesn't need conversational English. Remove "We see a," "There is a," "The camera shows." Keep it declarative.

- *Instead of:* "We see a muscular man who is crying and there is heavy rain."
- *Use:* "Muscular man crying in heavy rain."

**Hard limits:** Optimal prompt length is 50–150 words. Above 200 words, detail dilutes and the model gets chaotic. Maximum prompt length: ~10,000 characters.

---

## II. The Front-Loading Rule (MANDATORY)

> **The first 20–30 words of your prompt carry approximately 30% of Aurora's total semantic weight.**

Subject-first ordering is mandatory. If your subject appears at word #80, Aurora will under-prioritize it. Front-load:

**`[Genre/Style anchor] + [Subject] + [Primary action] + [Scene/setting]`**

Everything else — camera, lighting, audio — follows after this core.

> **Correct:** "Cinematic cyberpunk thriller. A lone hacker in a translucent black raincoat steps out of a ramen stall in Neo-Kowloon at 2 AM, rain falling around her. Low-angle 24mm handheld push-in..."
>
> **Incorrect:** "Shot on ARRI Alexa with Cooke S7/i at T2.0 with anamorphic lens flares in a rainy neon city, a lone hacker in a translucent black raincoat, cyberpunk thriller..."

---

## III. The 7 Pillars of Grok Cinematography

Every strong prompt weaves these seven categories into a **single cohesive paragraph** (not modular brackets). Use them as your mental checklist:

1. **[Camera Specs]** — Camera body, lens, aspect ratio, frame rate, optical imperfections
2. **[Camera Movement]** — One movement per clip, shot type, transition trigger
3. **[Subject & Action]** — Identity lock, sequential staging, anatomical acting, dialogue
4. **[Setting & Depth]** — Location, depth of field, atmosphere, foreground framing
5. **[Micro-Textures]** — Organic skin, moisture, surfaces, particles — prevents "plastic doll" look
6. **[Physics & Motion]** — Weight, gravity, cloth, lip isolation, morphing guardrails
7. **[Lighting & Finish]** — Directional light source, color grade, film grain

> `+ AUDIO:` — appended as a dedicated final block
> `+ Stability Constraint` — mandatory closing clause

---

## IV. Deep Dive: The Comprehensive Toolkits

---

### Pillar 1: Camera Specs & Lenses

#### Camera Bodies & Formats

| Spec Category | AI Prompt Keyword | Visual Effect |
|---|---|---|
| High-End Cinema | `ARRI Alexa 65` / `ARRI Alexa Mini LF` | Natural skin tones, smooth highlight roll-off, cinematic warmth |
| Gritty & Sharp | `RED V-Raptor` / `RED Monstro 8K` | Hyper-detailed, ultra-sharp, high-contrast, punchy |
| Massive Scale | `IMAX 65mm` / `IMAX 70mm Film` | Breathtaking field of view, Nolan/Villeneuve scale |
| Indie / Vintage | `Shot on 16mm Film` / `Bolex H16` / `Aaton LTR` | Heavy film grain, muted colors, organic imperfection |
| Low-Light / Neon | `Sony Venice 2` / `Sony FX6` | Clean shadows, vibrant color in dark, skin tones |
| Slow Motion | `Phantom Flex 4K` | **The magic phrase** for cinematic slow-motion ramps |
| Retro / Horror | `VHS Camcorder` / `Found Footage` | Tracking lines, chromatic aberration, color bleeding |
| Classic Analog | `Kodak Portra 400 film look` | Warm, slightly soft, classic 35mm analog |
| Commercial | `Crystal-clear digital cinematography, 4K sharp` | Clean modern, no grain, maximum sharpness |
| Social / UGC | `iPhone 15 Pro front camera` | Handheld micro-pulses, ~26mm field, slight overexposure, selfie framing |
| Vintage Cinema | `Arriflex 35 BL` / `Mitchell BNC` | Gate flicker, period grain, classic optical rendering |
| Blackmagic | `Blackmagic URSA` / `BMPCC 6K` | Clean digital with slight filmic roll-off |

**Film formats that trigger period grain, color science, and gate flicker:** `35mm`, `Super 35mm`, `65mm`, `16mm`, `Super 16`, `Super 8mm`, `VHS`

**Most reliable phrasing:** `shot on [body] with [lens] at [aperture]`
> Example: `shot on ARRI Alexa Mini LF, Cooke S7/i 50mm at T2.0` — the two highest-leverage words you can paste into any cinematic prompt.

#### Named Lens Glass (Advanced)

Aurora reads these as bundled style references — combined prompts for color, contrast, falloff, and flare character. Always pair with focal length and T-stop.

| Lens | Character |
|---|---|
| `Cooke S4 / S7/i` | Warm, organic, "Cooke look" — subtle barrel distortion, creamy falloff |
| `Zeiss Master Prime / Ultra Prime` | Clinically sharp, high-contrast, neutral |
| `Zeiss Master Anamorphic` | Anamorphic with Zeiss clarity and horizontal flares |
| `Panavision Primo` | Warm, rounded, classic Hollywood premium |
| `Panavision C-Series / G-Series` | Vintage anamorphic character |
| `Canon K35` | Vintage warm, slightly soft, unique flare |
| `Hawk V-Lite anamorphic` | Distinct horizontal streak flares, oval bokeh |
| `Helios 44-2` | The swirly-bokeh classic — distinctive rotating background blur |
| `Atlas Orion anamorphic` | Modern anamorphic, clean flares |
| `Lomo Anamorphic` | Russian anamorphic — distinctive oval bokeh and color cast |
| `Petzval` | Swirly bokeh on edges, sharp center |
| `Super Baltar` | Vintage soft wide — warm and organic |
| `Laowa 24mm probe lens` | Bug's-eye perspective inside tight spaces |

#### Focal Lengths

| Lens Type | AI Prompt Keyword | Visual Effect |
|---|---|---|
| Ultra-Wide / Horror | `14mm` / `16mm` / `18mm lens` | Distorts edges, chaotic scale, claustrophobic |
| Wide | `24mm wide lens` / `28mm wide-angle` | Environment + subject, slight distortion |
| Documentary | `35mm lens` | Natural perspective — cinematic standard |
| The "Human Eye" | `50mm standard lens` | Grounded realism, minimal distortion |
| Portrait / Intimacy | `85mm portrait lens` | Shallow DoF, creamy bokeh — the romance lens |
| Medium Telephoto | `100mm lens` / `135mm telephoto` | Background compression, isolation |
| Long Telephoto | `200mm telephoto compressed` / `300mm telephoto` | Maximum compression, stacked planes, surveillance |
| Stylized Flare | `Panavision Anamorphic` / `anamorphic lens` | Horizontal flares, oval bokeh, 2.39:1 feel |
| Microscopic | `Macro lens` / `100mm macro` | Razor-thin extreme detail |
| Fisheye | `8mm fisheye` / `fisheye lens` | 180° field — found footage, hip-hop, extreme sports |
| Probe | `Laowa 24mm probe lens` | Bug's-eye perspective in tight spaces |
| Tilt-Shift | `tilt-shift lens` | Miniature/diorama effect |

> **Always pair focal length with the word "lens":** `"24mm wide lens"` outperforms bare `"24mm"`.

#### Aspect Ratios

| Format | Prompt | Use |
|---|---|---|
| Anamorphic Scope | `2.39:1` | Epic blockbuster, maximum cinematic feel |
| Classic Widescreen | `2.35:1` | Hollywood letterbox |
| Standard | `16:9` | YouTube, TV, cinema |
| Vertical / Social | `9:16` | TikTok, Reels, Shorts |
| Square | `1:1` | Instagram feed |
| Retro | `4:3` | Old film simulation, period drama |

> **21:9 Cinematic Crop Hack:** Generate at 16:9 with `"wide framing, extra headroom"` → apply black letterboxing in post-production to achieve a 2.39:1 anamorphic look. This also crops AI artifacts that frequently appear at the absolute top and bottom edges of the frame.

#### Frame Rate & Shutter Angle

Frame rate language is **aesthetic, not literal** — Aurora outputs at 24fps regardless. These tokens shift the motion *character*:

| Frame Rate | Effect |
|---|---|
| `24fps cinematic` | Classic cinematic motion — always close every prompt with `...24fps cinematic` |
| `30fps broadcast` | Slightly smoother, TV/news feel |
| `48–60fps` | Hyperreal, sports |
| `96–120fps slow motion` | Buttery slow-motion |
| `240fps super slow-mo` | Phantom-class slow-motion |
| `1000fps extreme slow-mo` | Ultra-Phantom, water droplets, impact |
| `time-lapse` | Compressed time (pair with `static camera`) |
| `hyperlapse` | Camera-in-motion compressed time |

**Cleanest slow-mo notation:** `120fps slow motion side-tracking shot, 24fps playback of 120fps footage`
**Cleanest cinematic ramp:** `real-time wind-up for 4 seconds, then 240fps slow-motion at the contact frame, snap back to real-time` + add `shot on Phantom Flex 4K`

**Shutter Angle:**

| Shutter Angle | Effect |
|---|---|
| `180° shutter angle` | Natural motion blur — cinematic standard |
| `45–90° shutter` | Staccato war-footage stutter (Saving Private Ryan) |
| `360° shutter` | Dreamy smear, impressionistic |

#### Optical Imperfections — Break the "AI Sterility"

| Effect | AI Prompt Keyword | Visual Result |
|---|---|---|
| Anamorphic Flare | `anamorphic lens flares` / `horizontal blue lens streaks` | **Highest-leverage single addition to any cinematic prompt** |
| JJ Abrams Flare | `JJ Abrams blue lens flare` | Circular bright artifact |
| Color Fringing | `chromatic aberration` / `subtle chromatic aberration on highlights` | Slight color split at edges |
| Dark Corners | `vignetting` / `dark vignette corners` | Directs eye to center |
| Edge Distortion | `barrel distortion` | Slight wide-angle curve |
| Soft Falloff | `soft lens falloff` | Organic feel |
| Focus Drift | `lens breathing` | Micro focus movement — raw realism |
| Oval Blur | `oval anamorphic bokeh` | Anamorphic bokeh characteristic |
| Bokeh Variants | `swirly Helios bokeh` / `soap-bubble Trioplan bokeh` / `creamy bokeh` / `cat's-eye bokeh` | Works when the lens itself is named |
| Soft Glow | `halation glow around highlights` / `bloom` | Filmic warmth — mimics Kodak halation |
| Diffusion | `Black Pro-Mist 1/4 filter` | Softens highlights, gentle glow |

> Lens dust registers weakly — describe as `"smudged glass filter, soft halation around highlights"` instead.

---

### Pillar 2: Camera Movement & Transitions

**Use exactly one camera move per clip.** Combining more than two produces morphing artifacts.

#### Camera Movement Vocabulary

| Category | Move | Prompt Keyword |
|---|---|---|
| Static | Locked off | `static camera` / `tripod-locked` / `static locked-off frame` |
| Pan/Tilt | Pan | `pan left` / `pan right` |
| | Tilt | `tilt up` / `tilt down` |
| | Whip Pan | `whip pan with extreme directional motion blur` |
| Dolly Family | Push in | `slow dolly in` / `slow camera push-in` |
| | Pull back | `camera pull back` / `dolly out` / `pull-back reveal` |
| | Crash zoom | `crash zoom` / `snap zoom` |
| | Dolly zoom | `dolly zoom` / `Vertigo effect` / `zolly` / `Hitchcock zoom` — all four synonyms work |
| Track/Truck | Lateral | `truck left` / `lateral slider` / `tracking shot` |
| | Follow | `follow shot` / `following shot` / `parallax tracking` |
| Crane/Jib | Crane | `crane up` / `crane down` / `jib reveal` |
| | Pedestal | `pedestal up` / `pedestal down` |
| Stabilized | Steadicam | `steadicam smooth follow` |
| | Gimbal | `gimbal tracking parallel` |
| | Handheld | `handheld with organic human jitters, slight instability, subtle breathing motion` ← **one of the most reliable phrases in the vocabulary** |
| Specialty | 360 Orbit | `360-degree orbit` / `360 orbit` |
| | Half Orbit | `half orbit 180` / `slow arc shot` |
| | FPV Drone | `FPV drone dive — fast aggressive agile` |
| | Aerial | `drone stabilized shot` / `top-down god's-eye drone, 90° slowly twisting` |
| | Snorricam | `Snorricam — body-mounted, face locked at center, background moves chaotically` |
| | Cosmic Zoom | `cosmic hyper-zoom (space to street)` — Aurora handles continuous-scale zooms well |
| Focus | Rack Focus | `rack focus from [A] to [B]` / `focus pull reveal` |
| | Split Diopter | `split diopter` |

#### Shot Type Vocabulary

| Shot Name | Prompt Term | Purpose |
|---|---|---|
| Extreme Wide | `extreme wide shot` / `establishing shot` | Scale, isolation, geography |
| Wide | `wide shot` / `full shot` | Subject in full environment |
| Medium Wide | `framed mid-thigh up` *(say this instead of "cowboy shot" — registers weakly)* | Action + character |
| Medium | `medium shot` / `waist-up shot` | Balanced subject + setting |
| MCU | `medium close-up` / `MCU` | Face + shoulders — dialogue |
| Close-Up | `close-up shot` / `CU` | Emotion |
| ECU | `extreme close-up` / `ECU` | Eyes, hands, suspense — **avoid on faces in motion** (Aurora's "waxy" failure mode) |
| OTS | `over-the-shoulder shot` / `OTS` | Conversation |
| POV | `first-person POV` / `subjective camera` | Immersion |
| Insert | `insert shot` | Object detail |
| Two-Shot | `two-shot` | Character relationship |
| Dutch Angle | `Dutch angle` / `canted frame` | Unease, horror, noir |
| Bird's Eye | `bird's-eye view` / `top-down shot` | God-like overview |
| Worm's Eye | `worm's-eye view` | Monumentality — pair with actual height: `"from sand level looking up"` |

> **Forcing wide shots:** Add `"a tiny silhouette"` to force Aurora to keep extreme wides from accidentally zooming in.
> **Full-body shots:** Describe `"boots and floor"` to prevent leg-cropping.

#### Transition Triggers (Official xAI Documented)

- `Camera switch.` — hard cut to a new angle (**most reliable**)
- `Cut to:` — editorial cut (both work; always describe the new shot explicitly — Aurora does not infer continuity)
- `Slow transition to` — soft scene change
- `Rack focus from A to B` — in-camera focus transition

**Multi-beat structure:** Describe 2 shots max per clip. For longer sequences, chain via Extend from Frame. Beyond 2 beats per clip, coherence collapses.

---

### Pillar 3: Subject & Action

#### Identity Lock System

Use the `@` tag system to lock character identity:
1. Generate your key frame still in Quality Mode
2. Drag and drop up to **7 reference images** into the Grok Imagine prompt field
3. Type `@` to bring up a menu of uploaded images (e.g., `@Image1`, `@Image2`)
4. Weave the tag directly into the narrative: `"A muscular man matching @Image1 sitting up in bed..."`

This guarantees near 1:1 character fidelity for the initial generation.

#### Character Description Formula

```
[Age range] + [physical feature] + [clothing with material detail] + [emotional state] + [body posture/stance]
```

*Example:* "Weathered male detective, 50s, salt-and-pepper stubble, rumpled brown trench coat, collar turned up, scanning the alley with quiet suspicion, shoulders hunched."

#### Cinematic Action Verbs — Replace Generic Language

| Generic | Cinematic Alternatives |
|---|---|
| moves | surges, drifts, lunges, glides, stumbles, hurtles |
| looks | scans, peers, glares, studies, stares wide-eyed |
| walks | strides, slinks, staggers, prowls, marches, tiptoes |
| runs | sprints, races, bolts, scrambles, charges, flees |
| falls | collapses, crumbles, tumbles, plummets, staggers backward |
| hits | strikes, slams, smashes, impacts, shatters |
| speaks | mutters, shouts, whispers urgently, gasps, screams |
| other motion | surges, unfurls, shatters, plunges, lunges, recoils, gazes, trembles, smirks, beams |

#### Motion Intensity Modifiers

- **Increase motion scale:** `"rapidly"`, `"violently"`, `"with large amplitude"`, `"powerfully"`, `"wildly"`, `"at high frequency"`
- **Reduce motion:** `"barely perceptibly"`, `"subtly"`, `"with micro-gestures"`, `"gently"`, `"slowly"`, `"deliberately"`
- **Temporal distortion:** `"in slow motion"` / `"bullet-time"`
- **Speed feel:** `"with motion blur"`, `"urgently"`, `"frantically"`, `"suddenly"`

**Without intensity language, Aurora defaults to subdued motion.** Always include an intensity modifier.

#### Dialogue & Vocal Texture System

Define the **texture of the voice** — it directly impacts physical acting, throat tension, and facial micro-expressions.

| Vocal Characteristic | AI Prompt Keyword | Visual Effect on Character |
|---|---|---|
| Raw / Damaged | `Deep raspy voice, voice breaking with emotion` | Bulging throat tendons, strained neck muscles, pained micro-expressions |
| Vulnerable / Weak | `Shaky and breathless, whispering, trembling lip` | Shallow rapid chest breathing, hesitant stuttering lip movements |
| Aggressive / Loud | `Sharp husky passion, booming roar, projected shout` | Mouth opens wider, jaw tenses, leans forward aggressively |
| Cold / Restrained | `Deadpan delivery, monotone, speaking through gritted teeth` | Locks jaw, tightens facial muscles, limits mouth movement |

*Instead of:* "He says 'Why did you lie?'"
*Use:* "He shouts back with sharp, husky passion, his voice breaking as he visibly forms the words: 'Why did you lie?!'"

**Voice Specification Formula** (for multi-clip dialogue consistency):
> `"Voice: [gender], [age], [dB volume], [wpm pace], [Hz pitch range], [articulation quality], [acoustic resonance]"`
> *Example:* `"Voice: Nigerian female, late-20s, 65 dB, 140 words per minute, 220 Hz pitch range, crisp articulation, dry acoustic resonance. She says calmly: 'I knew this would happen.'"`

This prevents Aurora from randomly shifting voice profiles between extension clips.

#### The Facial Acting Toolkit — Anatomy Over Emotion

Prompt the *physical symptoms* of the emotion. Aurora understands anatomy better than abstract feelings.

| Emotion | Weak Prompt (Avoid) | Master Trigger Keywords | Visual Effect |
|---|---|---|---|
| Crying / Grief | "He is crying very hard." | `Bloodshot sclera, damp eyelashes, slow subtle shedded tears, single glistening tear track, quivering chin, hollow glassy stare` | Prevents the "waterfall" CGI tear effect |
| Extreme Anger | "He looks super angry." | `Flared nostrils, clenched jaw muscles, bulging temple veins, tightly furrowed brow, twitching cheek muscle, heavy facial flushing` | Keeps anger grounded and dangerous |
| Shock / Betrayal | "He is shocked." | `Slack jaw, widened pupils, frozen facial muscles, sudden loss of color (pale skin), erratic eye darting` | Visceral psychological disbelief |
| Suppressed Emotion | "He is holding back tears." | `Biting inside of lip, rapid blinking, swallowing hard, prominent Adam's apple movement, tense neck tendons, forced stoicism` | The most cinematic acting style |

**The Director's Rule for Tears:** Never use "tears" alone. Anchor to physics of the face and lighting.

*Example:* `"slow, subtle shedded tears catching the harsh overhead light, a single wet trail tracing down his flushed cheekbone." or "subtle thin crystal-clear tears slowly well up in his bloodshot sclera and trace glistening paths down his flushed cheeks" or "subtle thin crystal-clear tears slowly well up in his bloodshot sclera and trace glistening paths down his flushed cheeks. His chin quivers faintly, he swallows hard with visible tense neck tendons, and his broad chest heaves with slow labored silent sobs.".`

**Other micro-expression vocabulary:**
- **Eye movement:** `darting eyes`, `fixed gaze`, `slow blink`, `eyes flicking left`, `eyes widening`, `narrowing eyes`, `looking off-frame`
- **Breath:** `sharp inhale`, `exhaled cloud of fogged breath`, `audible sigh`, `panting`, `ragged breaths`, `slow exhale through teeth`
- **Body language:** `defiant stance`, `slumped shoulders`, `coiled posture`, `weight on back foot`, `fists clenched`, `leaning forward`
- **Blocking:** `enters frame from left`, `crosses to a mug`, `turns toward camera`, `exits frame left`

#### Wardrobe & Physical Description

Always pair **material + finish + period**: `brushed wool overcoat`, `raw silk robe`, `riveted brass armor`, `weathered leather jacket`, `period-correct 1940s wool suit`, `distressed denim`, `mesh tactical vest`

Anchor periods with year and one specific garment detail to prevent era-drift.

---

### Pillar 4: Setting & Depth

| Technique | AI Prompt Keyword | Visual Effect |
|---|---|---|
| Isolation | `Extremely shallow cinematic depth of field, heavy bokeh` | Forces focus on subject emotion |
| Scale | `Deep depth of field, infinite focus` | Citizen Kane-style sharp from foreground to infinity |
| Voyeuristic | `Foreground framing, candid shoot-through` | Out-of-focus objects near lens — hidden, authentic |
| Atmospheric | `Volumetric lighting, god rays, atmospheric haze` | Gives air itself texture |
| Realism | `Lived-in environment, practical props, highly detailed set dressing` | Prevents the empty "AI void" |
| Focus Pull | `Rack focus from [A] to [B]` | Attention shifts mid-shot |

#### Atmosphere & Environmental Layers

- `"morning mist rising from the valley"` — mystery, beauty, horror
- `"heat haze shimmering above the asphalt"` — desert, western, intensity
- `"rain-soaked neon reflections on wet cobblestone"` — noir, cyberpunk, thriller
- `"dust motes floating in a shaft of light"` — period drama, warmth, stillness
- `"fog rolling through broken windows"` — horror, abandoned spaces
- `"smoke and particle debris drifting through the air"` — war, action, aftermath
- `"underwater caustics rippling across surfaces"` — fantasy, dreamlike
- `"snow falling softly in the background"` — winter drama, isolation, silence
- `"volumetric god rays piercing storm clouds"` — Aurora's flagship strength — renders almost too eagerly

---

### Pillar 5: Micro-Textures

The ultimate secret weapon against the "video game" or "plastic doll" aesthetic.

| Texture Category | AI Prompt Keyword | Visual Effect |
|---|---|---|
| Organic Skin | `Visible pores, translucent sub-surface scattering, flushed capillaries` | Faces catch light organically — not waxy |
| Moisture | `Glistening micro-sweat, tear trails, oily skin accumulation` | Realistic specular highlights that look alive |
| Textiles | `Individual fabric weave, frayed threads, heavy denim stiffness` | Clothing has physical weight |
| Decay | `Pitted rust, scuffed concrete, peeling paint, smeared glass` | Anchors in authentic physical space |
| Particles | `Suspended dust motes, drifting ash, microscopic lint` | Interacts beautifully with harsh light |
| Anti-AI Shield | `Absolutely no CGI smoothing, completely avoiding waxy skin` | Final safety net against computational smoothness |

**Advanced rendering terminology :**
- `subsurface scattering (SSS)` — light penetrates skin, scatters, exits at different point — prevents clay/plastic look
- `physically based rendering (PBR) textures` — materials react uniquely to light (rust vs silk vs wet asphalt)
- `global illumination` / `path tracing` — light bounces off secondary surfaces, colors bleed onto adjacent walls
- `ambient occlusion` — deepens shadows in crevices and intersecting geometry — prevents flat look
- `caustics` — web-like patterns of light through water or glass
- `bloom & halation` — bright sources bleed luminous glow over edges
- `Unreal Engine 5 aesthetic` — high-fidelity real-time cinematic visuals

#### Extended Surface Texture Library

- `"wet asphalt reflecting neon signs"` — rain city, noir, cyberpunk
- `"rough stone weathered by centuries"` — medieval, fantasy, ruins
- `"brushed aluminum with micro-scratches"` — sci-fi, tech, product
- `"worn leather cracked with age and use"` — western, period drama
- `"shattered glass catching ambient light"` — thriller, action aftermath
- `"concrete cratered from impact"` — war, action
- `"ice surface reflecting cold blue light"` — winter horror, sci-fi
- `"foliage with light filtering through overlapping leaves"` — forest, fantasy
- `"fabric rippling in wind with realistic cloth simulation"` — costume drama
- `"skin texture with visible pores and natural imperfection"` — photorealism anchor
- `"beads of sweat catching the rim light"` — physical exertion, drama
- `"peach fuzz catching backlight"` — intimate portraiture

**Particle effects:** `rain (light/heavy/sideways)`, `snow (flurries/blizzard)`, `dust kicking up backlit`, `sparks flying`, `glowing embers floating`, `fireflies`, `falling cherry blossoms`, `falling leaves`, `confetti`, `ash falling`. Density via words: `scattered`, `dense`, `swirling`, `gentle drift` — numeric particle counts are ignored.

---

### Pillar 6: Physics & Motion

The structural guardrails that force Aurora to obey the laws of physics.

| Physics Category | AI Prompt Keyword | Visual Effect |
|---|---|---|
| Weight & Mass | `Heavy physical weight, realistic gravity, grounded momentum` | Cures "floaty/underwater" AI movement |
| Friction / Contact | `Accurate weight displacement, realistic skin friction, firm grip` | Stops hands and objects from melting into each other |
| Facial Control | `Strict lip isolation, restrained micro-expressions, locked jaw` | Cures "soap opera" overacting |
| Fluid Dynamics | `Accurate fluid dynamics, dissipating smoke plumes, viscous dripping` | Smoke dissipates naturally, tears obey gravity |
| The Guardrail | `Strict object permanence, zero morphing, consistent skeletal anatomy` | Keeps backgrounds and body parts solid from frame 1 to end |
| Cloth Physics | `Realistic cloth simulation, fabric reacts to motion` | Clothes have weight and move with the body |
| Particle Physics | `Realistic particle simulation` | Particles obey gravity, wind, and heat |

#### Aurora's Slow-Motion Bias (Critical)

Aurora has a **default slow-motion bias** — a WAN-distillation artifact. The model naturally drifts toward slower motion.

- **To get full-speed action:** Always write `"real-time speed, no slow motion"` explicitly
- **For intentional cinematic slow-mo:** Use `"shot on Phantom Flex 4K"` + the dual notation: `"real-time wind-up for 4 seconds, then 240fps slow-motion at the contact frame, snap back to real-time"`

#### The Hand/Finger Problem

Hands and fingers are Aurora's most consistently documented failure mode. Six workarounds, in order of preference:

1. **Hide them** — `"hands in pockets"`, `"hands behind back"`, `"arms crossed"`
2. **Cover them** — `"wearing leather gloves"`, `"tactical gloves"`, `"wraps around the wrists"`
3. **Occupy them** — `"gripping a steering wheel"`, `"fingers wrapped around a sword hilt"`, `"holding a coffee mug"` (solid objects stabilize finger geometry)
4. **Crop them out** — `"framed from the chest up"`, `"hands out of frame"`
5. **Keep gestures slow and singular** — fast hand motion breaks first
6. **Lock the still in image-to-video** — generate the hand pose in a Quality Mode image, then animate without changing it

#### Crowd Collapse Rule

Crowds collapse past ~6 visible humans. Keep one hero in the foreground, render mass as `"silhouettes in fog"` or `"out-of-focus background combatants"`.

#### Multi-Character Lip Isolation

Aurora struggles to keep one mouth closed while another speaks in a single prompt. Solution: generate each character's dialogue as a separate clip and edit together.

```
Shot 1 — Character A Speaks:
"...ONLY [Character A]'s mouth moves. [Character B] has a firmly locked jaw, closed mouth, zero lip movement."

Shot 2 — Character B Replies:
"...ONLY [Character B]'s mouth moves. [Character A] has a firmly locked jaw, closed mouth, zero lip movement."
```

---

### Pillar 7: Lighting & Finish

**Lighting must be directional.** Never say "dramatic lighting" — tell Aurora where the light is coming from.

> `"hard rim light from the left"` outperforms `"dramatic lighting"` every single time.

#### Core Lighting Styles

| Lighting Style | AI Prompt Keyword | Visual Effect |
|---|---|---|
| Chiaroscuro | `Moody low-key lighting, harsh directional light, deep shadows` | Pitch-black shadows, massive 3D volume |
| Hollywood Blockbuster | `Teal and orange color grade, warm key light, cool blue shadows` | Pushes skin warm, shadows cold |
| Industrial / Sterile | `Harsh overhead fluorescent glare, desaturated cold tint` | Unforgiving, isolating, gritty |
| Natural | `Golden hour lighting, backlit silhouettes, soft window light` | Soft, forgiving glow with rim light halos |
| Practical | `Single motivated light source from above or side, deep shadows` | First-class concept in Aurora |
| Volumetric | `Volumetric lighting, god rays, shafts of light` | Aurora flagship strength |
| The Glue | `Subtle 35mm film grain, analog cross-processing` | Breaks digital sharpness, unifies the aesthetic |

#### Named Lighting Setups

| Scheme | Prompt Term | Visual Result | Genre |
|---|---|---|---|
| Three-Point | `three-point studio lighting` | Professional, clean | Drama, commercial |
| High-Key | `high-key bright lighting` | Low contrast, cheerful | Comedy, romance |
| Low-Key | `low-key dramatic lighting` | High contrast, shadows | Noir, thriller, horror |
| Rembrandt | `Rembrandt lighting` | Triangle of light on cheek | Drama, portrait, period |
| Split | `split lighting` | Half face lit, half shadow | Villain reveal, duality |
| Butterfly | `butterfly lighting` / `Paramount lighting` | Shadow below nose | Glamour, fashion |
| Clamshell | `clamshell lighting` | Even glow, eliminating shadow under chin | Fashion, beauty |
| Silhouette | `backlit silhouette` | Iconic mystery | Thriller, epic |
| Negative Fill | `negative fill` | Deepens shadows, increases contrast | Noir, thriller |
| Chiaroscuro | `chiaroscuro lighting, strong light-dark contrast` | Extreme shadow drama | Horror, noir, period |

#### Practical Light Sources Aurora Recognizes

- `sodium-vapor amber` — urban street light
- `cyan moonlight` — cool, ethereal
- `fluorescent green ballast` — industrial, horror
- `neon magenta-and-cyan` — cyberpunk
- `candlelight` / `firelight` — period drama, romance
- `CRT phosphor green` — tech, retro
- `warm tungsten interior` — practical indoor
- `cool blue moonlight bleeding through window` — mixed lighting

**Kelvin values register weakly.** Use descriptive language: `"warm tungsten"` beats `"3200K"`.

**Behavioral lighting** beats labels: `"warm raking side light at 3 pm, casting long diagonal shadows across the dock"` outperforms bare `"golden hour"`.

**Technical jargon that fails** (rewrite as consequences):

| Technical Term | Workaround |
|---|---|
| `cucoloris` | `"broken dappled shadow pattern across the wall like sunlight through leaves"` |
| `barn doors flagged off` | `"hard-edged pool of light with dark surrounding fall-off"` |
| `300D through diffusion` | `"soft diffused key light through sheer fabric"` |

**Color spaces and log profiles do not work:** `Rec.709`, `Rec.2020`, `S-Log3`, `ARRI Log C` are wasted tokens. Convert to behavioral consequence: instead of `ARRI Log C` write `"shot on ARRI Alexa, latitude in highlights, clean shadow detail"`.

#### Natural Light Sources

| Light Source | Prompt Terms | Mood | Genre |
|---|---|---|---|
| Golden Hour | `golden hour light`, `warm sunset glow` | Warmth, nostalgia, romance | Romance, western, drama |
| Magic Hour | `magic hour`, `soft pink twilight` | Dreamlike, Days of Heaven | Drama, romance |
| Blue Hour | `blue hour twilight`, `dusk light` | Melancholy, transition | Drama, noir |
| Overcast | `overcast diffused light`, `flat grey sky` | Neutral, clinical | Documentary, drama |
| Dawn | `soft dawn light`, `early morning mist` | Hope, fresh start | Drama, adventure |
| High Noon | `harsh overhead sunlight`, `midday sun` | Oppressive | Western, thriller |
| Moonlight | `cold moonlight`, `silver moonlight` | Ethereal, eerie | Horror, fantasy |

#### Director / Cinematographer References (DP Names Beat Director Names)

**Cinematographer tokens encode specific visual signatures — they are higher-yield than director names.**

| DP Name | Visual Signature |
|---|---|
| `Roger Deakins` | **Most reliable DP keyword** — naturalistic, doorways/windows as frames, golden hour, bleach bypass |
| `Emmanuel "Chivo" Lubezki` | `"Lubezki natural light"` is documented working syntax — fluid, organic, available light, long takes |
| `Christopher Doyle` | Hong Kong neon, swoony handheld, Wong Kar-wai saturated swelter |
| `Janusz Kamiński` | Bleach-bypass war footage, high-contrast |
| `Vittorio Storaro` | Bold expressive color symbolism |
| `Gordon Willis` | Top-light, deep shadows, "Prince of Darkness" |
| `Robert Richardson` | Hot overhead key with bright halos |
| `Greig Fraser` | Earthy, raw, large-format (Dune, Batman) |
| `Hoyte van Hoytema` | IMAX 65mm naturalism (Nolan) |
| `Bradford Young` | Underexposed atmospheric, soft fog, dim moody interiors |
| `Darius Khondji` | Painterly muted (Se7en, Midnight in Paris) |
| `Jarin Blaschke` | Eggers — Witch/Lighthouse candlelight, natural flame only |
| `Lol Crawley` | Muted earth tones, low-saturation skin |
| `Tonino Delli Colli` | Leone — saturated amber + cobalt sky, Technicolor |

**Director + Film references that function as full visual DNA bundles:**

| Reference | Visual Bundle |
|---|---|
| `Christopher Nolan + Hoyte van Hoytema` | Long lens, IMAX scale, desaturated tension |
| `David Fincher + Erik Messerschmidt` | Cool grade, low-key precision, lifted blacks |
| `Wes Anderson` | Symmetrical, pastel, deadpan centered composition |
| `Denis Villeneuve + Greig Fraser` | Brutalist, monumental, deliberate (Dune) |
| `Stanley Kubrick + John Alcott` | One-point perspective, candlelight period |
| `Wong Kar-wai + Christopher Doyle` | Saturated neon, smeary step-printed motion |
| `Robert Eggers + Jarin Blaschke` | Natural flame only, Witch/Lighthouse |

**Film titles:** `Blade Runner 2049`, `Mad Max: Fury Road`, `Dune`, `2001: A Space Odyssey`, `The Shining`, `Studio Ghibli`, `In the Mood for Love`, `The Matrix`, `Akira (1988)`, `No Country for Old Men`, `Sicario`, `The Brutalist`

> **IP safety note (post-January 2026):** Moderation sometimes filters explicit IP names. Stylistic homage language (`"Blade Runner mood"`, `"Wong Kar-wai-style saturated neon"`) is safer and generally just as effective.

#### Color Grades

| Grade | Effect | When to Use |
|---|---|---|
| `Teal and orange` | Skin pushed orange, shadows pushed teal | Action/thriller blockbuster default |
| `Bleach bypass` | Desaturated, metallic, high-contrast, retained silver | War, gritty thriller (Ryan, Se7en) |
| `Sepia / tobacco` | Warm brown monochrome | Period, nostalgic |
| `True black-and-white, no color, high-contrast film` | Greyscale, deep blacks | Classic noir — **must write this exact phrase** or Aurora renders desaturated color |
| `Cool blue` | Pushed blue | Sad, dystopian, Matrix |
| `Pink-and-blue duotone` | Refn signature | Drive, neon-noir |
| `Pastel high-key` | Bright, soft, low-contrast | Wes Anderson, romcom |
| `Magenta-cyan neon` / `Cyan and magenta neon` | Saturated complementary | Cyberpunk, hip-hop |
| `Crushed blacks + halation` | Rich shadow + warm highlight bleed | Filmic warmth, Kodak look |
| `Two-strip Technicolor` | Cyan-red palette only, no blue or yellow | Classic Hollywood period |
| `Cross-processed` | Shifted greens, magenta shadows, lifted blacks | Editorial, music video |
| `Kodachrome warmth` | Warm-shifted analog | 1970s nostalgia |

#### Film Stock References

Use only **one stock per prompt** — mixing confuses the model.

| Stock | Character |
|---|---|
| `Kodak Portra 400` | **The single most reliable stock token** — warm, slightly soft, pastel skin |
| `Kodak Vision3 500T` | Night/low-light king — Nolan, Tarantino |
| `Kodak Vision3 250D` | Daylight workhorse |
| `Kodak Ektar 100` | Vibrant, muted earth tones |
| `Fujifilm Velvia` | Saturated, high-contrast slide film |
| `Fujifilm Eterna 250D` | Warm cinematic skin tones |
| `CineStill 800T` | Neon-noir signature — red halation on highlights |
| `Kodachrome` | Warm shift, vintage |
| `Super 8` | Heavy grain, soft, light leaks, sprocket holes |
| `16mm` | Indie texture, gritty realism |
| `VHS` | Scan lines, color bleed, tracking errors |
| `IMAX 65mm` | Ultra-clean large-format clarity |

#### Advanced Finish Terms

- `"lifted blacks"` — shadows never go fully black; cinema-grade finish
- `"crushed blacks"` — deep, dark shadows; noir, horror
- `"bleach bypass"` — desaturated, high-contrast silver-halide look
- `"HDR dynamic range"` — extreme detail in highlights and shadows
- `"analog cross-processing"` — shifted color channel look; editorial, music video

---

## V. Audio Design — The 6-Layer Audio Matrix

Deploy these exact triggers in the **`AUDIO:` tail block** at the end of every prompt. The `AUDIO:` label is the most reliable syntax — it clearly separates audio direction from visual direction.

> **Critical default:** If you don't specify audio, Aurora adds a generic background music bed. **Always close with explicit direction**, including `"no music"` or `"no score"` when you want clean ambience only.

### The 6 Layers

| Audio Layer | What It Is | How to Use It |
|---|---|---|
| **1. Room Tone / Ambiance** | The underlying "silence" of a space | Most important layer. Layer: distant humming fan, fluorescent buzz, distant traffic. Wide shot = `"spacious reverb"`. Intimate = `"dry, close acoustic space"`. |
| **2. Foley (Physical SFX)** | Physical sounds of movement and interaction | Match the physics you prompted. `"Heavy boots crunching on wet asphalt"`, `"visceral chest thump"`, `"metallic clatter"`. **Never prompt Foley without active movement on screen.** Specificity matters: `"boots on wet asphalt"` beats `"footsteps"`. |
| **3. Active Sync (Vocal / Dialogue)** | Character performs dialogue, sings, or reacts | Include `"mouth moving"` or `"lips synced to lyrics"`. Ground with physical traits: `"head nodding, emotional expression"`. |
| **4. Passive Sync (Vibing)** | Character listens to music WITHOUT performing | `"Listens deeply to the beat, head nodding to rhythm, tapping fingers on the wheel"`. **CRITICAL:** Forbid vocal generation — `"No singing, no mouth movements to lyrics."` |
| **5. The Score (Music & Genre)** | Emotional undertone and musical identity | Be hyper-specific: `"low droning cello"`, `"sparse dark synth pad"`, `"driving orchestral percussion"`. Avoid generic `"dramatic music"`. |
| **6. Dynamic Arcs (The Build)** | How audio evolves through the scene | Tie to a visual cue: `"music starts intimate and builds powerfully as the camera pushes in, then abrupt silence on the hard cut"`. |

### Audio-Visual Keyword Matrix

| Layer | Goal | Prompt Keywords | Guardrails |
|---|---|---|---|
| Ambiance | Acoustic environment | `echoing warehouse ambiance`, `muffled rain against glass`, `dead silence`, `distant city sirens` | Match spatial reality |
| Foley | Physical sound | `heavy boots crunching gravel`, `visceral chest thump`, `metallic clatter`, `fabric tearing` | Never prompt without active movement |
| Active Sync | Dialogue / vocal | `mouth moving strictly`, `lips synced to lyrics`, `heavy exhausted breathing` | Must include "mouth moving" or "lips synced" |
| Passive Sync | Vibing to music | `head nodding to rhythm`, `tapping fingers on wheel`, `completely vibing` | Forbid singing: "No singing, no mouth movements" |
| Score | Genre music identity | `low droning cello`, `dark synth pad`, `Lo-Fi hip hop beat`, `trap hats with 808s` | Be hyper-specific |
| Dynamic Arc | Audio evolution | `music builds powerfully`, `sudden bass drop`, `rising crescendo`, `abrupt cut to silence` | Tie arc to a specific visual cue |

### Voice Specification Formula 

For multi-clip dialogue — prevents Aurora from shifting voice profiles between clips:

```
Voice: [gender], [age range], [dB volume], [words per minute pace], [Hz pitch range], [articulation quality], [acoustic resonance]. [Character] says [adverb]: "[exact line]"
```

*Example:* `"Voice: Nigerian female, late-20s, 65 dB, 140 words per minute, 220 Hz pitch range, crisp articulation, dry acoustic resonance. She says calmly: 'I knew this would happen.'"`

### Dialogue Formatting Rules

- **Format:** `[Character] [adverb]: "[quoted line]"`
- Always use straight or curly quotes
- **Adverb tags:** `says calmly`, `whispers`, `shouts`, `mumbles`, `growls`, `sings`, `stammers`
- **Practical limits:** One sentence per character per ~6 seconds; max two short exchanges in a 10-second clip
- **Lip-sync accuracy:** ~70% on first pass — the cleanest workflow is one speaker per clip, then composite via Extend from Frame
- **Singing:** Supported with lip-sync; multi-language voice works (specify language explicitly) — English is highest quality
- **Voiceover without mouth movement:** Use `"Audio narration:"` trigger instead of `"Audio:"` — this detaches the voice from the character's lips entirely: `"Subject's mouth is completely closed. Audio narration: I couldn't believe what I saw."`

### `Audio narration:` — Inner Voice / Voiceover Trigger

To generate a non-diegetic voiceover where no character's mouth moves:
> `"Her mouth is completely closed, lips pressed firmly together, zero lip movement. Audio narration: I knew I should have taken the earlier train."`

### Trans-Diegetic Sound 

Sound that transitions between diegetic and non-diegetic — a character's hummed tune that swells into full score:
> `"Character hums softly to herself, which gradually builds into a full orchestral swell"`

### Composer Proxy References

Use stylistic proxies instead of bare names — avoids moderation filters and is equally effective:

| Composer | Effective Proxy |
|---|---|
| Hans Zimmer | `"Hans Zimmer-inspired brass ostinato, BRAAM stab, Inception-style horn swell"` |
| Ennio Morricone | `"Morricone-style harmonica wail + tremolo whistle ostinato"` |
| John Williams | `"Williams-style orchestral adventure theme"` |
| Trent Reznor/Atticus Ross | `"Reznor/Ross-style dark ambient electronic score"` |
| Vangelis | `"Vangelis-style analog pad"` / `"pulsing synthwave"` |
| Daft Punk | `"Daft Punk-style electronic groove"` |
| Joe Hisaishi | `"Hisaishi-style piano motif"` |
| Cliff Martinez | `"Martinez-style minimal synth arpeggios"` |
| Junkie XL | `"Junkie XL-style percussive electronic score"` |

### Sound Design Genre Conventions

`sci-fi whoosh`, `deep BRAAM`, `horror dread tone`, `sudden silence then sting`, `comedy stinger`, `boing`, `rimshot`, `transition swell building to a hit`

### Mixing Terms

`reverb-drenched`, `dry vocal close-mic'd`, `low-pass filtered`, `telephone-EQ vocal`, `lo-fi cassette warble`, `vinyl crackle`, `AM radio quality`

> **Timing limitation:** Fine cue timing within a clip is a documented constraint — beats land where the model places them. `"beat of silence then sting"` works at the broad level, but frame-accurate cue timing is not possible.

### Genre Music Quick Reference

| Genre | Music Prompt |
|---|---|
| Action / Thriller | `driving orchestral percussion and brass building to crescendo` |
| Horror | `dissonant strings`, `low rumbling drone`, `eerie silence broken by high-pitch sting` |
| Romance | `soft piano and strings`, `gentle acoustic guitar`, `warm cello melody` |
| Sci-Fi | `ambient electronic score`, `pulsing synthesizers`, `minimalist electronic drone` |
| Western | `sparse acoustic guitar and harmonica`, `dust-swept silence` |
| Fantasy | `sweeping orchestral with choral voices`, `Joe Hisaishi-style piano motif` |
| Comedy | `upbeat playful piano`, `quirky ukulele rhythm` |
| War | `military drums and brass`, `tense sustained strings` |
| Cyberpunk / Noir | `synthwave`, `dark ambient electronica`, `low jazz bass line` |
| Documentary | `neutral ambient underscore`, `light acoustic textures` |
| Hip-Hop | `boom-bap loop`, `lo-fi bed`, `trap hats with 808s` |
| Synthwave | `pulsing synthwave bass`, `Vangelis-style analog pad` |

---

## VI. The Stability Constraint (MANDATORY CLOSER)

End every single prompt with this closing clause. It is the officially recommended xAI workaround for not having negative prompts — a dedicated closing phrase that outperforms 90% of prompts when included.

**Formula:**
> `"Keep [identity / composition / product detail] stable. Single subject only."`

**Examples:**
- `"Keep facial identity consistent throughout. Single subject only, no extra characters entering the frame."`
- `"Preserve original composition and framing. Zero additional subjects."`
- `"Maintain consistent character clothing, hair, and face across all frames."`
- `"Keep product detail and branding elements sharp and stable throughout."`

---

## VII. Production Workflow

### The Image-First Pipeline (Gold Standard)

The single most important production technique on Grok Imagine. Generating a perfect still first, then animating it, is unanimously recommended by xAI and all research guides. Animation amplifies base-image flaws rather than fixing them.

**Step 1 — Generate the Still**
Write a detailed 5-pillar prompt and generate in **Quality Mode** (not Speed Mode). Quality Mode is mandatory for any cinematography-grade still you intend to animate.

**Step 2 — Review Before Animating**
Check: composition, lighting, subject identity, any visible text, hand/finger geometry. Any messy fingers, illegible text, or weird hair must be solved at the still stage — Aurora will not fix them during animation.

**Step 3 — Write a Short Motion Prompt (≤40 words)**
Do NOT re-describe the image — Aurora already sees it. Describe only **what changes**.
- Do NOT contradict the image (if the still shows a man, don't write "a woman dances")
- Specify motion intensity explicitly: `"slowly drifting"`, `"violently shaking"`, `"racing past at high speed"` — Aurora picks subdued defaults without adverbs

**Image-to-Video Template:**
> `"Animate [specific element] with [subtle/strong motion]. Add [camera move] and [ambient change]. Keep [identity/composition/product detail] stable."`

**Step 4 — Generate Variations**
Generate up to **4 variations simultaneously** — rerolling the same prompt produces materially different results.

**Step 5 — Chain via Extend from Frame** (if needed)
For sequences longer than 15 seconds, chain via Extend from Frame, then stitch in CapCut or your NLE. Plan for **2–3 chain maximum** before quality degrades significantly.

---

### Video Extension System (Master Consistency Lock)

When extending a video to create longer scenes:

**Rules:**
1. Generate your first clip using the `@` reference system
2. Click the **Extend from Frame** button on the generated video (automatically loads the final frame as seed)
3. **Do NOT repaste your original prompt** — this causes instant style drift
4. Begin the extension prompt with the **Master Consistency Lock**, followed by the narrative continuation
5. Keep extensions to **6–10 seconds per segment** for strongest seams
6. Maximum **2–3 chains** before quality degrades

**Master Consistency Lock Template:**

```

Seamlessly continue directly from the very last frame where [describe exact ending state of previous clip].

[Describe the next action in prose here.]
```

---

### The Trailer Beat Assembly Framework

For 10–15 second clips, structure as a mini-film with narrative beats. Generate each beat as a separate clip, then assemble in NLE:

| Beat | Focus | Technical Directives |
|---|---|---|
| **Beat 1 — Establishing Shot** | Geography, scale, environmental lighting. No complex character actions. | `24mm wide angle, slow dolly-in, volumetric lighting, drone acoustics` |
| **Beat 2 — Character Intro** | Medium or close-up. Character texture, SSS skin, subtle ambient micro-motion. | `85mm lens, Rembrandt lighting, shallow DoF, subtle breathing motion` |
| **Beat 3 — Action/Conflict** | Kinetic physics and aggressive Foley. Character detail sacrificed for motion clarity. | `Fast shutter speed, whip pan, motion blur, heavy impact SFX` |
| **Beat 4 — The Reaction** | Slow movement, dramatic lighting shift, intense emotional resonance. | `Extreme close-up, negative fill, high contrast, melancholic score` |

---

## VIII. The Master Prompt Template

Use this as your complete production scaffold. Fill every section, then **convert to flowing prose** before submitting. Delete what doesn't apply. Keep total under 150 words. End with the Stability Constraint.

```
[FRONT-LOAD: Genre/style anchor + Subject + Primary action + Setting — first 20-30 words]

[CAMERA: Body, lens, aspect ratio, focal length, optical imperfections]
[Shot type + single camera move]
[Then/Camera switch/Cut to: next beat if needed]

[SUBJECT: Age, feature, clothing material, posture, emotional state]
[Action with intensity modifier + physical consequence]
[Dialogue: vocal texture + exact words in quotes]

[SETTING: Location with textural specificity]
[Depth: shallow DoF/heavy bokeh OR deep focus]
[Atmosphere: mist/rain/dust/haze/fog]
[Foreground framing if voyeuristic]

[MICRO-TEXTURES: visible pores, sub-surface scattering]
[Moisture/particles as relevant]
[Absolutely no CGI smoothing, no waxy skin]

[PHYSICS: Heavy physical weight, realistic gravity, grounded momentum]
[Strict object permanence. Zero morphing. Consistent skeletal anatomy.]
[real-time speed, no slow motion] (if full-speed action needed)

[LIGHTING: Key light direction + quality + source]
[Atmosphere: volumetric haze/god rays/neon reflections]
[Color grade: teal-and-orange/crushed blacks/warm amber/etc.]
[Film stock: one only]
[Subtle 35mm film grain]

AUDIO: [Room tone/ambient], [Foley SFX tied to actions], [Score: specific genre + instruments], [Dialogue if any: Voice spec + adverb: "exact words"]

Keep [identity/composition/detail] stable. Single subject only. 24fps cinematic.
```

---

## IX. Genre Preset Library (22 Genres — Full Blueprints)

---

### Action / Action-Thriller

**Visual:** Hard key light, anamorphic flares, practical sodium streetlamps, muzzle-flash bloom, hot rim light, high-contrast chiaroscuro
**Camera:** Whip pans, crash zooms, low-angle hero shots, tracking follows, speed-ramps, crane reveals, Dutch tilts
**Lens:** Anamorphic 1.8x at 2.39:1 / wide 21mm for chases / 35mm hero / 85mm reactions
**Color:** Teal-and-orange or bleach-bypass, crushed blacks, Kodak Vision3 500T
**DP Reference:** Michael Mann, Nolan/Hoytema, John Wick/Stahelski, Greig Fraser, Mann/Spinotti
**Audio:** Driving orchestral percussion and brass building to crescendo, impact SFX, shockwave bass
**Mood adjectives:** relentless, taut, propulsive, breakneck, visceral, paranoid, lethal, kinetic

> **Example prompt:** A black '67 Mustang weaves through Los Angeles freeway traffic at dusk, pursued by two matte-black SUVs. Low-angle tracking shot from bumper height, anamorphic 35mm, then snap-zoom to driver's eyes when she shifts gears. Sodium-orange highlights, crushed shadows, anamorphic lens flares, teal-and-orange grade, bleach-bypass film grain, Michael Mann *Heat* aesthetic. Speed-ramp from 24fps to 60fps slow-mo on the gear shift. AUDIO: roaring V8, percussive sub-bass score, screeching rubber. Keep single driver in frame. 24fps cinematic.

---

### Horror — Psychological / Supernatural / Slasher / Body Horror / Found Footage

**Visual:** Single practical bulb swinging, green-cyan moonlight, flashlight beam, key from below, flickering fluorescent, candlelight only
**Camera:** Slow dolly-in on eyes, locked-off symmetrical wide, handheld breathing camera, 360° dread orbit
**Lens:** Wide 18–24mm for distortion / 50mm for unease / macro 100mm for body horror / fisheye 8mm for found footage
**Sub-genre palettes:**
- Psychological: desaturated bruise-purple
- Supernatural: silver-blue + sickly green
- Slasher: Argento red and Bava blue (1978 anamorphic)
- Body horror: sickly yellow-green flesh (Cronenberg)
- Found footage: chroma noise, time-code burn-in
**DP Reference:** Eggers/Blaschke, Aster/Pogorzelski, Carpenter/Cundey, Argento, Cronenberg, Blair Witch
**Audio:** Low 40Hz drone, refrigerator hum, clock tick, sudden sting, heartbeat bass pulse, wet whisper

> **Psychological example:** A woman sits motionless at a kitchen table at 3 AM, a single hanging bulb swinging slowly above her. Locked-off symmetrical wide on 35mm, then 6-second slow dolly-in to extreme close-up on her unblinking left eye. Robert Eggers / Jarin Blaschke aesthetic, candlelight + bulb practical, deep ink blacks, desaturated bruise-purple grade, 1.66:1, organic film grain. The bulb sways at one cycle per four seconds. AUDIO: clock tick, low 40Hz drone, refrigerator hum, a single wet whisper: "you're already inside." Keep subject stable. 24fps cinematic.

> **Tip:** Aurora softens explicit gore. Imply via `"split skin"`, `"dark stain spreading"` rather than describe wounds graphically.

---

### Sci-Fi — Space Opera / Cyberpunk / Dystopian / Hard Sci-Fi / Retrofuturism

**Visual:** Volumetric god rays, holographic glow, HUD reflections in eyes, cold cyan key + magenta fill, CRT phosphor green
**Camera:** Slow rotating ship reveal, dolly-zoom on alien horizon, floating zero-G handheld, FPV megacity flythrough, orbital pan
**Sub-genre palettes:**
- Space opera: deep navy + warm bloom, anamorphic 2.39:1
- Cyberpunk: electric blue + magenta on wet asphalt, heavy haze
- Dystopian: desaturated concrete and sickly amber
- Hard sci-fi: clinical white + charcoal, 35mm "human"
- Retrofuturism: 70s warm orange-mustard-brown or 80s synthwave purple-teal
**DP Reference:** Villeneuve/Fraser, Kubrick, Scott/Cronenweth, Wong Kar-wai/Doyle, Syd Mead

> **Cyberpunk example:** A lone hacker in a translucent black raincoat steps out of a ramen stall in Neo-Kowloon at 2 AM, rain falling around her. Low-angle 24mm handheld push-in, then crash-zoom to her augmented eye reflecting Cantonese kanji. Blade Runner 2049 mood, Roger Deakins lighting style, electric blue + hot magenta, volumetric haze, chromatic aberration, wet asphalt reflections. Her coat ripples in updraft from a passing hovercar. AUDIO: synthwave bassline 90bpm, sizzling neon hum, distant rain, holographic ad jingle in Mandarin. Single subject only. 24fps cinematic.

---

### Drama — Literary / Family / Courtroom / Period

**Visual:** Naturalistic motivated lighting, window-as-key, practical lamps, Rembrandt triangle, Barry Lyndon candlelight for period
**Camera:** Locked-off symmetrical, slow push-in over 8–10 seconds, OTS reverse, static medium two-shot
**Lens:** 35mm "human eye" / 50mm for monologue / 75–85mm for portrait / 1.85:1 for prestige period
**Color:** Muted earth tones, low-saturation skin (Bradford Young/Lol Crawley), Kodak Portra 400
**DP Reference:** PT Anderson/Elswit, Brady Corbet/Crawley, Sidney Lumet, Joe Wright/McGarvey, Kubrick/Alcott

> **Example:** An elderly father and his adult daughter sit across a kitchen table in soft morning light; she places her hand near his without touching it. Locked-off symmetrical two-shot on 35mm, slow 10-second push-in to her hand. Lol Crawley / Brady Corbet aesthetic, north-facing window as soft key, muted earth tones, faint Kodak grain, 1.66:1. Steam rises from two cups; her thumb twitches once. AUDIO: mantel clock tick, distant traffic, no music; she finally whispers: "I read your letter." Keep both subjects stable. 24fps cinematic.

---

### Romance / Romantic Drama

**Visual:** Warm golden hour, soft diffused window, candlelight, dust-mote backlight, fairy lights, rim through hair
**Camera:** Intimate slow push-in, OTS reverse, 360° during embrace, crane up away from lovers, rack focus to eyes
**Lens:** **85mm portrait at f/1.4 is the romance lens**; 50mm intimate; vintage 35mm for nostalgia
**Color:** Pastel sunset, Kodak Portra 400, Wong Kar-wai saturated reds and emeralds
**DP Reference:** Wong Kar-wai/Doyle, Linklater, Guadagnino/Mukdeeprom, Celine Song
**Note:** Lip-sync warps facial geometry on head-on kisses — frame as profile or three-quarter, or cut just before lips meet

> **Rain-kiss example:** Two lovers caught in a sudden Tokyo rainstorm pull each other under a neon convenience-store awning. Slow 360° orbit at chest height, 35mm, slight handheld breathing. Wong Kar-wai / Christopher Doyle — saturated emerald and ruby neon, water droplets caught in rim light, anamorphic flares. Her hand slides up his soaked collar; rain in slow-motion. AUDIO: ambient rain on awning, distant scooter hiss, soft Mandopop ballad piano, soft inhale; no spoken line. Single couple only. 24fps cinematic.

---

### Thriller — Psychological / Crime / Techno

**Visual:** Single hard side-key, venetian-blind shadows, fluorescent buzz, monitor-glow blue, server-rack LED
**Camera:** Slow creeping push-in, locked-off surveillance, telephoto compressed crowd, split-diopter
**Lens:** 75–135mm telephoto for compression, 35mm + split-diopter, anamorphic 2.39:1
**Color:** Desaturated cool cyan (Fincher), Mann teal-and-amber, Pakula muted grey-green
**DP Reference:** Fincher/Cronenweth/Messerschmidt, Mann/Spinotti, Pakula/Willis, Soderbergh

> **Example:** A detective sits alone in a fluorescent-lit precinct at 2 AM, scrolling a manila file. Locked-off telephoto 100mm from across the room, slow 8-second push-in. Fincher / Erik Messerschmidt — desaturated cyan grade, lifted blacks, hard fluorescent buzz, monitor glow on face, 2.39:1. He turns one page, freezes, the lamp flickers once. AUDIO: ballast hum, page slide, distant radio dispatch chatter, low 30Hz drone. Keep subject stable. 24fps cinematic.

---

### Fantasy — Epic / Dark / Urban / Fairy Tale

**Visual:** Volumetric god rays, golden magic-hour, bioluminescent mushroom glow, torchlight flicker, enchanted runes, dragon-fire underlight
**Camera:** Sweeping aerial drone, slow crane-up to castle, 360° hero orbit, Vertigo dolly-zoom on portal
**Lens:** Wide 21–28mm for landscapes, anamorphic 2.39:1 for epic, macro for fairies
**Sub-genre palettes:**
- Epic: golden + emerald + sapphire (Jackson/Lesnie)
- Dark fantasy: desaturated grey-green and blood-rust (del Toro)
- Fairy tale: pastel storybook with illuminated-manuscript gold (Miyazaki)
**DP Reference:** Jackson/Lesnie, del Toro/Navarro, Miyazaki/Ghibli
**Note:** Multi-creature battles glitch past 2 figures — render hero vs single foe. Ghibli requires `"watercolor texture, soft brushstrokes"` or defaults to generic anime.

> **Ghibli example:** A round forest spirit with leaf-like ears sits beneath a glowing mushroom in light rain. Static medium 50mm, soft 6-second handheld breath. Studio Ghibli watercolor texture, Miyazaki palette — pastel emerald and sky-blue, soft brushstrokes, childlike wonder. Rain-drops bead on its fur, eyes blink slowly, one ear twitches. AUDIO: Joe Hisaishi-style piano motif, rain patter, forest ambience, a soft whimsical chime. Single subject. 24fps cinematic.

---

### Film Noir / Neo-Noir

**Visual:** Venetian-blind shadows on face, single hard tungsten key, cigarette smoke catching rim, rain-soaked sodium lamp, neon fill
**Camera:** Low-angle paranoid composition, locked-off Dutch tilt, slow dolly through smoke, OTS in dim booth
**Lens:** Classic noir: 32–40mm deep focus; neo-noir: anamorphic 2.39:1, 35–50mm shallow
**Color:** Classic: `true black-and-white, no color, high-contrast film` (John Alton); Neo: teal shadows + amber sodium (Deakins) or magenta-and-cyan (Refn)
**DP Reference:** Wilder/Seitz, Welles/Toland, Carol Reed/Krasker, Polanski/Alonzo, Refn/Sigel

> **Classic B&W example:** A trench-coated detective lights a cigarette under a flickering "HOTEL" sign as a 1947 Plymouth idles in rain. Low-angle 32mm, locked-off, slight Dutch tilt, deep focus. John Alton / Billy Wilder — true black-and-white, no color, high-contrast film. Venetian-blind shadows stripe his face, single hard tungsten key, sodium-lamp rim, cigarette smoke catching light. AUDIO: jazz alto saxophone, rain on awning, lighter flick, distant car horn, VO: "She walked in like a problem I couldn't afford to solve." Single subject. 24fps cinematic.

---

### Western — Classic / Revisionist / Modern

**Visual:** Hard noon sun, golden-hour low side-light, silhouette against horizon, dust catching backlight
**Camera:** Wide vista establishing, low-angle hero on horseback, slow standoff dolly, **200mm Leone telephoto for eyes**
**Lens:** Classic: anamorphic 2.39:1, 25–40mm vistas; Modern: ARRI Alexa 65 + Deakins clarity
**Color:** Saturated amber + cobalt sky Technicolor (Leone); muted sepia and dust (revisionist); golden + ash-grey (modern Deakins)
**DP Reference:** Ford/Hoch, Leone/Delli Colli, Peckinpah/Ballard, Coens/Deakins

> **Leone standoff example:** Two gunslingers face each other in a sun-bleached Mexican plaza at high noon; a tumbleweed rolls between them. Leone formula — extreme telephoto 200mm compressed shot of squinting eyes, alternating with low-angle holsters. Tonino Delli Colli — saturated amber + cobalt sky, hard noon sun, Technicolor grade, anamorphic 2.39:1. Sweat-drop on temple. AUDIO: Morricone-style harmonica wail + tremolo whistle ostinato, fly buzz, jangling spur, single church bell. Two subjects only. 24fps cinematic.

---

### Documentary — Nature / Verité / Investigative

**Visual:** Natural daylight only, golden hour, overcast soft-box sky, macro ring light
**Camera:** 400–800mm telephoto observation (nature), observational handheld (verité), Ken Burns slow pan-zoom on archive
**Lens:** 400–800mm + macro 100mm for nature; 24–35mm wide handheld for verité; 50–85mm at f/2.8 for talking heads
**Color:** National Geographic saturated greens and amber; naturalistic for verité; desaturated for investigative
**DP Reference:** BBC NHU/Doug Allan, Werner Herzog, Errol Morris, Frederick Wiseman, Ken Burns

> **Nature example:** A snow leopard crouches on a Himalayan ridge at dawn, breath visible, watching a Markhor goat 200m below. 600mm telephoto locked tripod, slow 4-second rack focus from leopard's eye to distant prey. BBC NHU / Doug Allan aesthetic, dawn alpenglow, National Geographic grade — deep blues + warm amber rock. Tail flicks once; cloud shadow drifts across ridge. AUDIO: wind, distant ungulate bleat, calm narration: "In the quiet of these heights, patience is everything." 24fps cinematic.

---

### Period Drama / Historical

**Eras and their fingerprints:**

| Era | Palette | Stock/Grade |
|---|---|---|
| Ancient (Rome/Greece) | Ochre, terracotta, bronze | Hard Mediterranean sun, 35mm sepia-bronze |
| Medieval | Mossy green, rust-iron | Barry Lyndon candlelight only |
| Victorian | Sepia-umber, gas-lamp fog | Crimson Peak ornate |
| 1920s Jazz Age | Champagne gold, peacock teal | Tungsten chandelier, smoke-haze |
| 1950s | Turquoise, salmon, cherry-red | Kodachrome saturation, Super 16mm |
| 1970s | Burnt-orange, harvest-gold, avocado | Kodak 5247 emulation, slow zooms |
| 1980s | Hot pink, electric blue, chrome | Magenta-cyan two-color, fog machine, VHS bleed |
| 1990s | Desaturated bleach-bypass | Fight Club green-cyan, dirty fluorescents |

**Visual:** Soft candlelight practical, window light, warm amber fireplace, Rembrandt setup, slow dolly, two-shot dialogue
**DP Reference:** Kubrick/Alcott (Barry Lyndon), Joe Wright/McGarvey, Vermeer painterly light

---

### Cyberpunk

**Visual:** Rain-slicked neon megacity, cyan-teal night, magenta and orange neon punch, heavy atmospheric haze always, humans dwarfed by brutalist architecture
**Camera:** FPV megacity flythrough, slow Villeneuve-scale wides, low-angle handheld push-in
**Lens:** Wide 24–28mm with chromatic aberration, anamorphic 2.39:1
**Color:** Electric blue + magenta on wet asphalt, deep blacks, volumetric haze
**The single most powerful anchor:** `"Blade Runner 2049 mood, Roger Deakins lighting, ARRI Alexa, anamorphic 2.39:1"`
**DP Reference:** Villeneuve/Fraser, Scott/Cronenweth, Wong Kar-wai/Doyle, Syd Mead

---

### War / Military

**Visual:** Bleach-bypass standard — drained color, retained silver, sickly greens, concrete greys, 45° shutter for staccato motion, blood and sand smearing the lens
**Camera:** 90% handheld, either extreme ground-level low POV or oner long-take Steadicam
**Lens:** 35mm with stripped lens coatings
**Color:** Desaturated khaki, washed-out war palette; Apocalypse Now: lurid orange napalm
**DP Reference:** Janusz Kamiński (Saving Private Ryan), Seamus McGarvey (1917), Lubezki (Children of Men)
**Mood adjectives:** harrowing, visceral, chaotic, mud-caked, shell-shocked, hallucinatory, mournful

---

### Comedy

**Sub-genres:**
- **Slapstick:** Wide locked-off symmetrical framing (Keaton, Tati), undercranked fast-motion, high-key flat lighting, 4:3 Academy ratio
- **Romantic comedy:** High-key with primary-color pops, saturated cream-butter-yellow, eye-level static medium shots, 35mm shallow DoF
- **Dark comedy:** Wes Anderson pastel symmetrical deadpan (centered composition, 40mm anamorphic), or Coen Brothers earthy bleakness, or Lanthimos clinical detachment

**Visual:** High-key bright, warm saturated, expressive facial close-ups
**Audio:** Upbeat playful piano, comedic timing SFX, exaggerated impact sounds, boing, rimshot

---

### Animation & Anime

| Studio Style | Prompt Keywords |
|---|---|
| **Studio Ghibli** | `"watercolor texture, soft brushstrokes, Miyazaki palette — pastel emerald and sky-blue, childlike wonder"` |
| **Madhouse/Satoshi Kon** | `"psychological, reality-bending edits, cinematic hard-cut style"` |
| **Ufotable (Demon Slayer)** | `"hybrid 2D/3D digital, dazzling effects animation, electric blade trails"` |
| **MAPPA (Jujutsu Kaisen)** | `"dynamic high-action, fluid combat choreography, expressive linework"` |
| **Studio Trigger** | `"explosive Gainax-DNA hyper-stylization, bold colors"` |
| **Makoto Shinkai** | `"photorealistic painted city backgrounds, lens flares, light particles, Your Name weather"` |
| **Spider-Verse** | `"mixed 3D/2D, halftone Ben-Day dots, ink lines on 3D forms, on-2s frame rate, chromatic aberration"` |
| **Pixar/Disney 3D** | `"appealing rounded design, subsurface skin scatter, soft global illumination"` |
| **Stop Motion** | `"claymation texture, visible material imperfections, stop-motion frame jitter"` |
| **80s OVA Anime** | Aurora confirmed strength — `"1980s anime OVA style, cel shading, bold line art"` |

> **Note:** Anime stylings are Aurora's strongest mode and clear the Spicy moderator more reliably than photoreal.

---

### Music Video

**Sub-genres:**

| Style | Visual Signature |
|---|---|
| **Pop MV** | Hype Williams cyclorama, single-color rim accent, beauty butterfly key, ring-light catchlight, saturated candy palette, beat-synced cuts |
| **Hip-Hop MV** | Centered torso framing on solid color, fisheye performance lens, low-angle hero, jewel-tone neon, slow-mo choreographed swagger |
| **Rock MV** | Handheld smoke-filled warehouse, hard red backlight, single bare bulb, 16mm gritty contrast, whip-pans on snare hits |
| **Indie/Dreamy MV** | Sun-bleached Super 8, Gondry-style practical effects, washed-out faded palette, lo-fi grain, slow handheld lyrical pans |
| **Synthwave MV** | Magenta-and-cyan neon grid, chrome surfaces, smoke machine, 80s VHS aesthetic |

---

### Commercial / Advertising

**Sub-verticals:**

| Category | Visual Signature |
|---|---|
| **Luxury** | Champagne gold, ivory, jet black, single hard kicker raking across brushed steel, Phantom 1000fps macro orbits |
| **Automotive** | Gunmetal/anthracite/racing-green, atmospheric haze, raindrop slow-mo, motion-control 360° orbit |
| **Tech/Apple** | Pure white seamless infinity cove, iridescent gradients, motion-controlled product reveal |
| **FMCG** | Saturated primaries, golden-hour skin, glossy wet-look splashes |
| **Food** | 45° hero angle (Chef's Table) or 90° overhead (Tasty), 100mm macro, soft window-light key, gimbal slow push-in, Phantom slow-mo pour |

**Universal commercial signatures:** `motion-control precision`, `Phantom Flex 4K splash/sizzle slow-mo`, `macro probe inside product`, `whip-pan logo reveal`, `scale-shift extreme close-up to wide reveal`

---

### Social Media / Short Form

**9:16 vertical rules:**
- Safe zones: top 250px and bottom 350px reserved for UI overlay — keep subject centered
- Hook in first 2 seconds
- On-screen text overlay baked in if needed
- Jump cuts every 1.2–1.5 seconds synced to trending audio
- `"iPhone 15 Pro front camera"` — single best UGC/TikTok aesthetic anchor: bundles handheld micro-pulses, ~26mm field, slight overexposure, and selfie framing
- Ring-light flat-key authentic phone-shot aesthetic, 30fps

---

### Superhero

**Sub-genres:**

| Style | Visual Signature |
|---|---|
| **MCU** | Saturated primary high-key with Steadicam circle-around hero pose |
| **DC Snyderverse** | Operatic slow-mo god-pose mythic, crushed blacks, teal-and-bronze, religious iconography, Larry Fong lightning practicals |
| **Indie Superhero (Logan/Unbreakable)** | Grounded handheld neo-Western with natural light |

---

### Post-Apocalyptic

**Two schools:**
- **Bleached/desaturated** — The Road, Children of Men — grey concrete, muted palette, handheld
- **Saturated/graphic-novel** — Mad Max: Fury Road — maximum contrast, silver-and-blue vs orange-and-sand, Eric Whipp day-for-night

---

## X. Anti-AI Guardrail Copypasta

### For Grok (embed in Pillar 6 as positive commands):

```
Heavy physical weight, realistic gravity, grounded momentum.
Accurate fluid dynamics. Strict object permanence. Zero morphing.
Consistent skeletal anatomy. Realistic cloth simulation.
Visible pores, translucent sub-surface scattering. Absolutely no CGI smoothing, no waxy skin.
real-time speed, no slow motion. [omit if you want slow-mo]
```

### For Other Tools with Negative Prompt Fields (Runway, Kling, Stable Video):

```
CGI, 3D render, plastic skin, waxy skin, morphing, melting limbs, extra fingers, cartoon,
illustration, anime, smooth texture, overlapping dialogue, fast motion, soap opera effect,
unnatural physics, video game graphics, floating movement, underwater motion artifact.
```

---

## XI. Platform Parameters & Technical Reference

### Grok Imagine Technical Specifications (April 2026)

| Parameter | Options | Recommendation |
|---|---|---|
| Engine | Aurora (autoregressive MoE) | Sequential token prediction — parses prose, not tags |
| Duration | 1–15 seconds (Reference-to-Video: max 10s; Video Edit: max 8.7s) | 5–8s for single-beat action; 10–15s for multi-beat narrative |
| Aspect Ratio | 16:9, 9:16, 1:1, 4:3, 3:4, 3:2, 2:3 | 16:9 cinema; 9:16 social vertical |
| Resolution | 480p (fast) / 720p (quality) | Always use 720p for final output; 480p for rapid A/B testing |
| Generation Mode | Normal / Fun / Custom / Spicy | Normal for cinematic; Fun for comedy/animation; Spicy (Premium+ / SuperGrok + 18+ required) |
| Reference Images | Up to 7 images via `@` tag system | Desktop platform only |
| Negative Prompts | Not supported | Embed anti-AI guardrails as positive commands in Pillar 6 |
| Image-to-Video | Supported — strongest mode | Generate key frame in Quality Mode first, then animate |
| Audio | Native — music, SFX, dialogue, lip-sync | Use `AUDIO:` section label for best synchronization |
| Extension | Extend from Frame button | Use Master Consistency Lock; 2–3 chain max |
| Max Prompt Length | ~10,000 characters | Full 7-pillar prompt fits comfortably; optimal 50–150 words |
| Generation Speed | Under 20 seconds | Rapid enough for iterative A/B testing |
| API Pricing | ~$4.20 per generation (official API) | |
| Upscaling | Native output stays at 720p regardless of `4K` or `8K` tokens | For genuine 4K, run through Topaz Labs Grok Imagine upscaler |
| Ranking | #1 Artificial Analysis Video Arena (Elo 1,329, April 2026) | |

### Official API Parameters

```json
{
  "model": "grok-imagine-video",
  "prompt": "your full cinematic prompt",
  "duration": 8,
  "aspect_ratio": "16:9",
  "resolution": "720p"
}
```

### When to Use Competing Tools Instead

| Tool | Best For |
|---|---|
| **Grok Imagine** | Ideation, image-to-video, audio-bundled content, anime stylings, Spicy creative work, commercial/product |
| **Veo 3.1** | Hero dialogue scenes, precise lip-sync, multi-character conversation |
| **Sora 2** | Final 1080p delivery hero shots, cinematic realism |
| **Kling 3.0** | Text-to-video, precise motion control |

### Common Mistakes & Fixes

| Mistake | Problem | Fix |
|---|---|---|
| `knight, castle, epic, 8K, cinematic` | Tag stacking — treated as disconnected keywords | Write natural directing sentences |
| `no blur`, `no extra characters` | Negative prompts ignored — worsens output | Say `sharp focus`, `single subject only` |
| Re-describing image in I2V | Contradicts source image | Focus only on motion and change |
| No camera direction | AI makes random compositional choices | Always specify shot type + one camera movement |
| Vague motion: "the thing moves" | Generic, weak result | Specific verb + intensity: "surges forward violently" |
| Timestamp brackets `[0:00-0:05]` | Aurora ignores bracket numbers | Use narrative sequence words: "first... then... suddenly..." |
| 15-second complex multi-element prompt | Temporal drift, morphing artifacts | Keep under 10s for complex scenes; use "Camera switch." for beats |
| No AUDIO block | Generic muzak defaults | Always end with explicit `AUDIO:` direction |
| No Stability Constraint | Character drift, extra subjects | Always close with "Keep [X] stable. Single subject only." |

---

## XII. Full Worked Master Examples

---

### Example 1: The Hard-Cut Dramatic Scene
*Demonstrating prose sequencing, strict lip isolation, and editorial control.*

Cinematic literary drama. A shirtless man in his 30s, muscular, in a gritty mechanic shop, crying with raw desperation. Slow camera push-in on ARRI Alexa 65, 35mm lens, aspect ratio 2.35:1. He points a trembling finger, shouting with voice breaking and deep raspy passion, visibly forming the words: "If you walk out that door right now, there is no coming back!" His mouth moves strictly; ONLY his mouth moves. Bloodshot sclera, damp eyelashes, slow subtle shedded tears catching harsh overhead fluorescent light. Heavy physical weight, realistic gravity, grounded momentum. Strict object permanence. Zero morphing. Consistent skeletal anatomy.

Camera switch. Rear-view tracking shot follows the man in a yellow tank top walking steadily toward the shop door. He delivers his line over his shoulder with deadpan monotone restraint, barely moving his lips: "I know... And right now, I'd rather be alone." ONLY his mouth moves. Deep depth of field looking down the length of the shop. Moody industrial lighting transitioning to high-contrast cinematic silhouette. Crushed blacks. Subtle 35mm film grain.

AUDIO: Echoing industrial room tone, distant fluorescent buzz, raw frustrated voice, heavy breathing, steady footfalls on concrete. No music.

Keep both subjects stable. Single frame. 24fps cinematic.

---

### Example 2: The Micro-Texture Static Profile
*Demonstrating extreme constraint, physical weight, and fluid dynamics.*

Cinematic character study. A solitary shirtless man in jeans sits on a concrete floor, back leaning heavily against a weathered mechanic shop wall. Static locked-off side profile, ARRI Alexa 65, 85mm portrait lens, aspect ratio 2.35:1. Extremely shallow cinematic depth of field; background tools softly blurred into heavy bokeh, razor-sharp outline of his muscular profile.

He takes a slow, shaky drag from a cigarette. Then a single tear traces down his face, which he slowly wipes away with a knuckle, never breaking his weary gaze. Photorealistic organic skin: visible pores, translucent sub-surface scattering. Detailed wisps of cigarette smoke rising and curling. Faint tear trail catching overhead light. Restrained micro-expressions. Heavy physical weight in his posture. Slow chest expansion. Accurate fluid dynamics — dissipating smoke plumes. Realistic skin-to-hand friction. Zero morphing. Absolutely no CGI smoothing.

Moody low-key lighting. Harsh overhead fluorescent glare as directional rim-light, catching edges of his profile and rising smoke. Deep high-contrast chiaroscuro shadows on unlit side. Desaturated cold tint. Subtle 35mm film grain.

AUDIO: Distant fluorescent buzz, slow cigarette draw, a soft exhale, faint creak of the building. No music.

Keep single subject stable. 24fps cinematic.

---

### Example 3: Sci-Fi Action — Genre Preset Applied
*Demonstrating genre preset system, anamorphic optics, and physics.*

Epic sci-fi action movie, Matrix-inspired. A male hero in a long black trench coat stands in fighting stance on a rain-soaked city street at night, rain dripping off his coat with heavy physical weight. Slow camera push-in from medium to MCU, Sony Venice 2, Panavision Anamorphic lens, aspect ratio 2.39:1, anamorphic lens flares, oval bokeh.

Camera switch. He surges forward with impossible speed, bending backward in bullet-time slow motion — rain drops freezing in mid-air. Smooth 360-degree orbit around him as he counters with fluid martial arts. Every impact landing with grounded momentum and heavy physical consequence. Shot on Phantom Flex 4K for the slow-motion. Real-time speed on approach, then 240fps slow-motion at the contact frame.

Wet asphalt reflecting neon signs. Tall buildings with lit windows. Volumetric atmospheric haze. Deep DOF on wide orbital, shallow DoF on MCU. Water droplets on trench coat fabric, individual fabric weave, rain streaks across anamorphic lens. Particle debris from impacts. Absolutely no CGI smoothing. Strict object permanence. Zero morphing. Realistic cloth simulation on trench coat.

Cold neon practicals — cyan and magenta. Volumetric lighting, visible light beams through rain. Deep blue and cyan color grade. 24fps motion blur.

AUDIO: Dark synthwave building to driving electronic climax, rain hammering wet street, visceral impact SFX on every strike, shockwave bass on camera switch, dead silence at peak orbit freeze, then music slams back in.

Keep single hero stable. 24fps cinematic.

---

*This is a living document. The 7-Pillar architecture is the permanent planning engine. All vocabulary banks, genre presets, and workflow techniques are updated as Aurora evolves.*

