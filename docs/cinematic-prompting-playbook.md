# The Cinematic Prompting Playbook

A unified reference for writing photorealistic and cinematic AI image prompts. Merged from three research documents, deduplicated, with every unique detail preserved.

**Core principle:** Most AI prompts fail because they describe a *thing* rather than a *shot*. The strongest prompts read like a director's shot card — prompt as if a real photo is being captured in the moment, using photography and cinematography language. Modern photoreal models (Midjourney v6+, Flux, Z-Image, SDXL, Imagen, Nano Banana Pro, Seedream 4.5, gpt-image-1.5, Sora, Seedance) have been trained on millions of captioned film stills and photographs, so industry terms act as compressed style tokens.

**The formula:** Stack one element from each pillar — `[Subject + Action] + [Shot + Lens] + [Location + Atmosphere] + [Lighting + Color] + [Film Stock + Grain] + [Texture detail]`.

---

## Table of Contents

1. [The Camera: Shot & Composition](#i-the-camera-shot--composition)
2. [The Heart: Subject, Action & Expression](#ii-the-heart-subject-action--expression)
3. [The World: Location & Atmosphere](#iii-the-world-location--atmosphere)
4. [The Vibe: Lighting & Color](#iv-the-vibe-lighting--color)
5. [The Film: Film Stock & Grain](#v-the-film-film-stock--grain)
6. [The Detail: Textures & Surfaces](#vi-the-detail-textures--surfaces)
7. [Prompt Architecture & Templates](#vii-prompt-architecture--templates)
8. [Advanced Techniques & Flagged Extras](#viii-advanced-techniques--flagged-extras)
9. [Model-Specific Notes](#ix-model-specific-notes)
10. [Pre-Generate Checklist](#x-pre-generate-checklist)

---

## I. The Camera: Shot & Composition

The camera pillar tells the model where it is, what lens it has, and how it frames the subject. This is the single highest-leverage section because it controls scale, psychology, and depth. Shot size dictates how much of the subject and environment is visible, and combined with camera angle, it forms the visual language of a film. Most filmmakers categorize 9–12 core shot sizes, but over 30 named variations exist.

### Shot Sizes (Framing)

| Shot | Abbrev. | What it shows | Narrative use |
|------|---------|---------------|---------------|
| Extreme Wide / Extreme Long Shot | EWS / ELS | Subject tiny in vast environment | Isolation, scale, establishing |
| Wide / Long Shot | WS / LS | Full subject + surroundings | Establishing locations |
| Full Shot | FS | Subject head-to-toe, fills frame | Action, full-body presence |
| Medium Long Shot / Cowboy | MLS / CS | Knees up (cowboy = mid-thigh) | Westerns, group blocking, fashion |
| Medium Shot | MS | Waist up | Dialogue, neutral framing |
| Medium Close-Up | MCU | Chest up | Interviews, emotional dialogue |
| Close-Up | CU | Head & shoulders | Emotion, intimacy |
| Big Close-Up | BCU | Whole face fills frame | Intense emotion |
| Extreme Close-Up | ECU / XCU | Eyes, lips, single detail | Tension, reveal, macro |
| Two-Shot | 2S | Two subjects in frame | Relationships |
| Over-the-Shoulder | OTS | Behind one subject toward another | Conversations, placing viewer in scene |
| Point-of-View | POV | Through character's eyes | Immersion |
| Insert / Cutaway | — | Object detail (watch, photo) | Plot reveals |

### Camera Angles

- **Eye-level** – neutral, documentary, natural perspective
- **Low-angle (LAS)** – heroic, dominance, power, imposing
- **High-angle (HAS)** – diminishes subject, vulnerability, smallness
- **Dutch / canted angle** – disorientation, unease, dynamic action
- **Bird's-eye / overhead / God's-eye / top-down** – omniscient, abstract, contextual
- **Worm's-eye** – extreme upward
- **Hip-level, knee-level, ground-level** – varied perspective shifts
- **Aerial / drone shot** – sweeping landscape
- **Reverse shot, reaction shot** – sequential narrative framing

### Camera Movement (critical for video models & implied motion)

Static, pan (L/R), tilt (up/down), push-in / dolly-in, pull-back / dolly-out, truck, pedestal, arc, crane/jib, Steadicam, handheld, whip pan, snap zoom / crash zoom, dolly zoom (Vertigo effect), rack focus, drone aerial, Snorricam, follow shot, orbit, parallax, tracking.

### Lens & Focal Length

Focal length is one of the most under-used but powerful tokens. It controls compression, distortion, and depth of field.

- **14–24mm ultra-wide** – dramatic distortion, environmental immersion, vast landscapes, claustrophobic interior distortion
- **35mm** – classic documentary/street/journalistic look
- **50mm "nifty fifty"** – natural human-eye perspective
- **85mm portrait** – flattering compression, creamy bokeh, portrait classic
- **100mm macro** – extreme detail, textures, insects, jewelry
- **135–200mm telephoto** – strong background compression, subject isolation
- **Tilt-shift** – miniature effect / architectural correction
- **Anamorphic** – widescreen, oval bokeh, horizontal flares, 2.39:1 cinematic feel
- **Fisheye** – extreme curvature

Add: `f/1.4 shallow depth of field`, `bokeh`, `rack focus`, `deep focus`.

### Composition Rules

- **Rule of Thirds** – place subject at intersections of a 3×3 grid for balance
- **Leading lines** – roads, fences, rivers, curved/straight lines guiding the eye to the focal point
- **Symmetry & central framing** – authoritative, Wes Anderson aesthetic
- **Golden ratio / Fibonacci spiral**
- **Frame within a frame** – doorways, windows, foliage as natural frames
- **Negative space** – isolation, minimalism
- **Depth layering** – foreground / midground / background
- **Triangular / diagonal composition** – dynamism, dynamic tension
- **Filling the frame** – intimacy
- **Headroom / lead room / nose room** – spatial breathing room
- **180-degree rule** – sequential shot consistency
- **L-cut staging / depth staging**
- **Depth of field** – shallow (f/1.4) for bokeh isolation; deep (f/16) for landscapes

### Aspect Ratio

`1:1` (editorial), `4:3` (vintage), `3:2` (35mm), `4:5` (Instagram), `16:9` (cinema), `2.39:1` (anamorphic widescreen / cinemascope), `9:16` (vertical/social/mobile), `6:17` (panorama).

---

## II. The Heart: Subject, Action & Expression

This pillar gives the image its soul. The AI will default to beautiful but vacant mannequins — without specificity here, prompts produce generic stock-photo people. The base prompt anatomy is **Subject + Action + Physical traits + Wardrobe + Setting + Details**. Specificity beats generality: "businesswoman in a blue suit looking at a graph" outperforms "person in office."

### Subject Description Layers

- **Identity** – age, gender, ethnicity, body type, archetype
- **Physical traits** – build, height, hair (color, length, texture), eye color, skin
- **Wardrobe** – fabric, material, fit, era, accessories (e.g., "weathered wool peacoat, frayed cuffs")
- **Hair & grooming** – texture, styling, length
- **Distinguishing marks** – scars, freckles, tattoos, jewelry
- **Posture & body language** – the silhouette before the face; confident stance, slouched, contrapposto

### Action Verbs (avoid static "standing")

Running, leaping, crouching, leaning, reaching, embracing, recoiling, pouring, gripping, gazing, mid-stride, caught mid-laugh, exhaling smoke, turning sharply, whispering, glancing over shoulder, lighting a cigarette, adjusting glasses, pouring coffee. Mid-action verbs ("frozen mid-step," "caught in motion") create cinematic tension.

### Facial Expressions — Ekman's 7 Universal Emotions

Paul Ekman's research established 7 universally recognized facial expressions, each with specific muscle cues:

| Emotion | Visual Cues to Prompt |
|---------|----------------------|
| Happiness | Crow's feet, raised cheeks, Duchenne smile (eyes engaged), eye-muscle contraction |
| Sadness | Drooped upper eyelids, downturned lip corners, raised inner brow |
| Anger | Lowered/drawn-together brows, vertical forehead lines, hard stare, pressed/tightened lips, flared nostrils |
| Fear | Raised + drawn-together brows, raised upper eyelids, horizontally stretched lips |
| Surprise | Raised arched brows, wide eyes with white above iris, dropped jaw |
| Disgust | Wrinkled nose, raised/curled upper lip, narrowed/lowered brows |
| Contempt | Asymmetrical one-sided lip raise (the "smirk") |

### Extended Emotional Palette (nuanced states)

Excited, disappointed, regretful, confused, frustrated, curious, proud, melancholic, contemplative, defiant, serene, wistful, smug, vulnerable, sultry, longing, awestruck, determined, pensive, smoldering, exhausted, euphoric, conflicted, dissociated, suspicious, stoic, thousand-yard stare, knowing smirk, radiant, piercing stare.

### Microexpressions

Fleeting (½–5 sec) involuntary tells. Prompting "subtle microexpression of doubt" produces less theatrical, more believable realism than overt "smiling." Microexpressions are more believable than macroexpressions.

### Eye Direction & Gaze

"Direct gaze into lens," "looking off-camera left," "eyes downcast," "vacant stare," "catchlight in pupil." Gaze direction is one of the strongest emotional levers in portraiture.

### Body Language & Posing

- **Open** (confidence, approachability) – straight back, relaxed shoulders, open arms
- **Closed** (defensiveness, mystery) – crossed arms, hunched shoulders, rounded back
- **Power poses** – feet shoulder-width, hands on hips, lifted chin
- **Vulnerable** – hunched, shoulders forward
- **Hand placement** – hands act as arrows directing the viewer's eye
- **Gaze direction** – direct (connection), averted (introspection), off-frame (anticipation)
- **Contrapposto** – classical weight-shifted stance for natural elegance

---

## III. The World: Location & Atmosphere

The environment sets the narrative. Rather than asking for a "city," describe the exact biome and the particles in the air. "Forest" is weak; "moss-draped redwood understory at dawn" is strong.

### Location Layers

- **Macro setting** – country/biome (Saharan dune sea, Icelandic basalt coast, Tokyo backstreet)
- **Architectural style** – Brutalist, Art Deco, Bauhaus, Gothic, Mid-century modern, Cyberpunk megastructure
- **Era** – 1920s, Victorian, near-future, post-apocalyptic
- **Time of day** – blue hour, civil dawn, golden hour, magic hour, high noon, dusk, astronomical twilight, deep night, pre-dawn, midnight

### Location Categories

- **Urban** – Tokyo back-alley, NYC subway platform, Parisian boulevard, brutalist plaza
- **Domestic interior** – mid-century kitchen, dorm bedroom, Victorian parlor
- **Industrial** – abandoned factory, server room, oil refinery at dusk
- **Natural** – alpine meadow, mangrove swamp, basalt sea cliff, salt flat
- **Liminal/transitional** – parking garage, hotel corridor, gas station 3 a.m.
- **Speculative** – cyberpunk megacity, solarpunk vertical farm, dieselpunk airfield

### Atmosphere as a Spatial Tool

Fog, haze, and rain aren't mood filters — they are **spatial tools** that reveal light and create depth. Visible particulate gives light something to bounce off of.

- **Fog / mist / haze** – depth, mystery, separation of planes
- **Volumetric god rays / light shafts / crepuscular rays** – beams cutting through dust, trees, or smoke
- **Rain** – sheets, drizzle, downpour; reflective wet surfaces, rain-dampened surfaces
- **Snow** – powder, blizzard, sleet, frost, fresh snow flurries
- **Smoke / steam / vapor** – atmosphere, drama
- **Dust / sand / pollen / embers / ash** – airborne particles, dust motes catching the light
- **Heat haze / shimmer**
- **Overcast / stormy skies** – melancholy, drama
- **Humidity sheen, condensation, morning dew droplets**
- **Sea spray, falling petals, floating embers, lens-catching snowflakes**
- **Heavy smog, dense volumetric fog**
- **Lens artifacts that imply atmosphere** – flares, diffusion, bloom

### Mood Vocabulary

Serene, ominous, ethereal, oppressive, nostalgic, dystopian, idyllic, claustrophobic, vast, intimate, sacred, liminal, melancholic, foreboding, expansive, hyperreal, dreamlike, surreal, uncanny, dramatic, utopian, chaotic.

### Set Dressing & Props

The world becomes believable through specifics: "half-empty espresso cup," "crumpled newspaper, 1974 Le Monde," "vintage Polaroid SX-70 on table." Period-specific props anchor era better than "vintage." Environmental storytelling — "half-finished cup of coffee, scattered receipts, wedding ring on the desk."

---

## IV. The Vibe: Lighting & Color

Lighting is not a "vibe"; it is a set of controllable knobs. Lighting is arguably the most decisive factor in photorealism. Structuring your prompt like a grip rigging a film set yields the best cinematic results.

### Lighting Direction & Quality

- **Hard light** – sharp shadows, drama, texture
- **Soft / diffused light** – wraps subject, gentle shadows (overcast, softbox)
- **Side / lateral light** – sculpts form, emphasizes texture
- **Front / flat light** – reduces shadow, flattens features
- **Back light / rim light** – silhouettes, halos, separation from background
- **Top light** – dramatic eye sockets
- **Underlight** – horror, unnatural
- **Bounce / fill** – lifts shadows
- **Ambient / available light**
- **Negative fill** – absorbing light to deepen shadows

### Natural Lighting

Golden hour, blue hour / twilight, harsh midday, overcast/diffused, dappled shade, moonlight, starlight, firelight, candlelight.

### Classic Portrait Lighting Patterns

- **Rembrandt** – triangle of light on shadow-side cheek
- **Loop** – small nose shadow looping toward mouth corner
- **Butterfly / Paramount** – symmetric shadow under nose (glamour, beauty)
- **Split** – half face lit, half in shadow (drama, mystery)
- **Clamshell** – key + fill from below (beauty/cosmetics/fashion)
- **Short / Broad** – shadow side or lit side facing camera
- **Rim / Hair light** – separation from background
- **Three-point lighting** – key + fill + back

### Cinematic & Practical Lighting

- Chiaroscuro (Caravaggio), low-key (deep shadows, noir), high-key (bright, minimal shadow, commercial)
- Motivated lighting, practical lights (in-frame lamps, neon signs)
- Hard sun + deep shade (Deakins), neon-soaked (Refn/Bladerunner), candlelight (Barry Lyndon), single-source god rays (Caravaggio)
- Hard flash (Terry Richardson / Juergen Teller look), bounce flash, ring light, softbox, snoot
- Gobo / cookie shadows (shadows cast through blinds/leaves)
- Window light, north light

### Specialized & Mood Lighting

- **Neon-noir** – magenta + cyan, cyberpunk
- **Bisexual lighting** – pink + blue + purple
- **Volumetric / god rays / atmospheric haze beams**
- **Bioluminescence**
- **Caustics** – underwater/pool light patterns
- **Lens flare, anamorphic flare, halation, bloom**

### Color Temperature (Kelvin)

| Kelvin | Source |
|--------|--------|
| 1,700K | Matchstick |
| 1,900K | Candlelight |
| 3,000K | Golden hour, sunset |
| 3,200K | Tungsten/household (warm) |
| 5,600K | Daylight noon |
| 6,500K+ | Overcast / blue cool |
| 10,000K+ | Deep shade, "moonlight" |

Mixing temperatures (warm key + cool fill) is a hallmark of modern cinematography.

### Color Theory & Psychology

- **Red** – passion, energy, danger
- **Blue** – calm, melancholy, trust
- **Yellow** – optimism, joy
- **Green** – nature, growth, unease (sickness)
- **Orange/Teal** – the Hollywood blockbuster grade
- **Magenta/Cyan** – cyberpunk, synthwave

### Color Harmonies & Grading

- **Harmonies:** complementary, analogous, triadic, split-complementary, monochromatic
- **Specific palette tokens:** "muted earth tones," "desaturated cool teal & sodium-vapor amber," "pastel pink & sage," "high-saturation Kodachrome reds," "warm golds, deep S-curve contrast"
- **Grading terms:** desaturated, muted, pastel, vibrant, crushed blacks, lifted blacks/shadows, milky highlights, bleach bypass, cross-processed, ENR bleach bypass, day-for-night, sepia, Technicolor three-strip, teal-and-orange blockbuster grade, faded vintage, milky shadows, neutral-to-cool cinematic grade
- **Selective color:** monochrome with a red splash (Sin City style)
- **Reference cinematographers/colorists:** "graded like Roger Deakins," "Bradford Young low-key palette," "Christopher Doyle saturation"

---

## V. The Film: Film Stock & Grain

Naming a real film stock instantly anchors color science, contrast, grain, and dynamic range. Film stock tokens act as compressed mood presets — one stock = a mood-board. Stock has color balance: 500T = ISO 500 tungsten-balanced; 250D = ISO 250 daylight.

### Color Negative (forgiving, skin-friendly)

- **Kodak Portra 160 / 400 / 800** – pastel tones, soft skin, fine grain, low contrast, creamy, ~10-stop DR, the editorial standard
- **Kodak Ektar 100** – ultra-saturated, magenta hue, very fine grain, ~10-stop DR, landscapes
- **Kodak Gold 200** – warm, nostalgic, yellow-leaning, family-album look
- **Kodak UltraMax 400** – consumer warmth, slight punch
- **CineStill 800T** – tungsten-balanced, signature red halation (glowing rings) around highlights, neon nightlife
- **CineStill 400D / 50D** – daylight, soft palette, halation in highlights
- **Fujifilm Pro 400H** – cool greens, pastel, airy, wedding-photographer favorite (discontinued, still prompted)
- **Fujicolor C200 / Superia 400** – cooler greens, consumer 90s look, "Asian street photo" look
- **Fujifilm Superia X-TRA 400** – muted greens and magentas, 90s nostalgia
- **Lomography 800 / 400** – playful/punchy/chaotic saturation
- **Agfa Vista** – warm reds

### Color Slide / Reversal (high contrast, vivid)

- **Fuji Velvia 50 / 100** – legendary/punchy saturation, reds & greens, landscapes
- **Fuji Provia 100F** – neutral, accurate
- **Kodak Ektachrome E100** – clean cyan/blue, slight cool, fine grain
- **Kodachrome 64** – extinct but trained: iconic National Geographic reds, vintage rich contrast-heavy colors (60s/70s aesthetic)

### Black & White

- **Kodak Tri-X 400** – classic photojournalism, gritty/pronounced grain
- **Ilford HP5 Plus 400** – versatile, timeless B&W, grainy
- **Ilford Delta 3200** – dreamy, very heavy grain, low light
- **Ilford Pan F 50** – ultra-fine grain, smooth tonality
- **Ilford FP4 125** – tonal richness
- **Kodak T-MAX 100 / 400** – ultra-fine grain (100), modern T-grain
- **Fuji Acros 100** – smooth, deep blacks

### Motion Picture Stocks (cinematic grade)

- **Kodak Vision3 250D / 500T** – modern Hollywood look
- **Kodak 5219 / 5207** – Hollywood standards, low-light cinema
- **Fuji Eterna** – softer, muted (Kodak alternative)
- **16mm / Super 8** – heavy grain, vintage home-movie feel
- **70mm IMAX** – pristine, epic resolution

### Instant & Specialty

- **Polaroid SX-70 / 600** – soft, vignetted, square, faded
- **Fuji Instax** – pastel, creamy
- **Disposable camera / single-use** – flash, vignette, washed
- **Expired film** – color shifts, light leaks
- **Cross-processed (xpro)** – green/cyan shadows

### Grain Behavior (advanced)

Grain follows the speed-detail trade-off: high ISO = larger crystals = grainier and softer; low ISO = finer grain, sharper detail. True film grain is luminance-dependent: coarser in shadows, fine in midtones, near-invisible in highlights, with halation in highlights.

Useful prompt terms:
- "fine grain", "moderate grain", "heavy grain", "coarse silver halide grain"
- "luminance-dependent grain," "coarse shadow grain, fine highlight grain"
- "natural film grain, no digital noise"
- "halation around highlights / bright lights" (CineStill signature)
- "soft halation bloom"
- "scanned 35mm negative", "scanned 35mm negative texture"
- "subtle gate weave"
- "push-processed +2 stops"
- "expired film cast"
- "light leaks", "dust and scratches"
- "Lomo vignette"

### Camera Body & Lens Tokens

Body + lens combos are powerful style anchors:
- "Shot on Hasselblad 500CM," "Leica M6 with 35mm Summicron," "Contax T2," "Contax 645 with 80mm Zeiss Planar"
- "Mamiya 7II 6×7 medium format," "Pentax 67"
- "ARRI Alexa 35," "RED Komodo," "Sony Venice"
- "Hasselblad medium format," "Phase One IQ4," "Leica M11 rendering"
- "iPhone 15 Pro candid," "iPhone 4 photo," "CCTV still"

### Digital Look (when you don't want film)

"Shot on ARRI Alexa," "RED Komodo," "Sony Venice," "Hasselblad medium format," "Phase One IQ4," "Leica M11 rendering," "iPhone 15 Pro candid."

---

## VI. The Detail: Textures & Surfaces

Texture is the perceived appearance of a surface — it transforms flat 2D images into tactile experiences. Most users never describe textures, resulting in generic outputs. Force the AI to render imperfections. The critical rule: texture is revealed by directional light skimming across a surface, not by flat frontal light. Soft, diffused light minimizes texture; hard side/raking light maximizes it.

### Skin

Pores visible, peach-fuzz vellus hair, freckles, sun-spots, sweat sheen, oil shine on T-zone, dewy, oily sheen, sun-damaged, weathered, baby-soft, scarred, wrinkled, pore-level detail, dry chapped lips, goosebumps, scar tissue, stubble, 5 o'clock shadow, makeup texture (matte foundation / dewy highlight), tear streaks, mascara smudge.

### Hair

Flyaways, individual strands catching rim light, oily roots, dry ends, braided texture, wet & slicked, frizz halo, gray streaks.

### Fabric & Clothing

Worn denim with faded knees, raw selvedge, boiled wool, cashmere pilling, silk sheen, crushed velvet, linen wrinkles, leather patina, waxed canvas, ribbed knit, sequins catching light, lace shadow, frayed cuffs, sweat-darkened cotton, raw linen, crumpled silk, nubby wool, distressed denim, velvet pile, sheer chiffon, embroidered brocade, knitted cable, coarse burlap, soft linen.

### Leather

Cracked, supple, patinated, embossed, suede nap, aged dark brown leather with natural scratches and patina.

### Wood

Knotted oak, weathered driftwood, lacquered walnut, raw plywood, cracked timber, charred shou-sugi-ban (charred cedar), weathered reclaimed oak with deep grain lines, polished walnut veneer, saw marks from original milling, mid-century walnut, bamboo grain.

### Stone & Concrete

Rough granite, smooth marble, mossy fieldstone, porous limestone, slick obsidian, chiseled, honed travertine, white marble with subtle gray veining, rough board-formed concrete, weathered brick with crumbling mortar and moss, cracked plaster, terrazzo, exposed brick with mortar.

### Metal

Polished chrome, brushed steel, oxidized copper (verdigris), patinated bronze, hammered, anodized, rusted, galvanized, gilded, rusty corten (weathering steel), brushed matte black metal with specular highlights, brushed aluminum, hammered brass, rusted rebar.

### Glass

Frosted, etched, fingerprinted, dewy condensation, crystal-clear, tinted, dirty plexiglass, frosted glass.

### Liquid

Glossy water beads, viscous honey, rippled surface, foamy, splash crown.

### Organic & Natural Surfaces

Petal velvet, bark fissures, moss carpet, fur, feathers, scales, chitin, tree bark detail, lichen, wet leaves with droplets, cracked desert mud, rippled sand dunes, ice crystallization, frost on grass, dew on cobwebs, foam on waves, river-smoothed pebbles.

### Synthetic

Matte plastic, glossy lacquer, rubberized, carbon-fiber weave, latex sheen.

### Atmospheric Texture

Dust motes in beams of light, smoke layers, fog density, water condensation, lens dirt, anamorphic streak, halation bloom, chromatic aberration on edges, vignette, rolling shutter (digital), scanline (CCTV/VHS).

### Texture Modifiers

Rough, smooth, glossy, matte, satin, velvety, abrasive, silken, prickly, downy, gritty, ridged, pitted, fibrous, crystalline, iridescent, holographic, translucent, opaque, subsurface scattering.

### Photographic Imperfections (the "realism cheat code")

Slight motion blur, hand-held micro-shake, focus breathing, missed-focus front-back, dust on negative, scratch marks, tape edge, hair on scanner, light leak in corner, finger over flash, visible film grain, chromatic aberration (color fringing at edges), light bloom, subtle vignette, faded tones, medium-format film look. These imperfections trick the eye out of "AI uncanny valley."

### Detail / Render Quality Tags

- "8K, ultra-detailed, photorealistic, hyper-detailed pores, individual hair strands"
- "macro detail, raking sidelight, tactile surface fidelity"
- "subsurface scattering on skin"
- "sharp focus on eyes, falloff to soft bokeh"
- "shallow depth of field (f/1.8), creamy bokeh balls"
- "crisp micro-contrast," "specular highlights," "preserved shadow detail" — forces the diffusion model to heighten realism of how light wraps around textures

---

## VII. Prompt Architecture & Templates

### Template A: Shot Card (pipe-delimited)

A battle-tested order blending Subject+Style+Context with photographic-language principles:

```
[Medium/Style] | [Shot size + angle + lens] | [Subject + physical traits + wardrobe] |
[Action + expression + body language] | [Location + time + atmosphere] |
[Lighting direction + quality + color temp] | [Color palette/grade] |
[Film stock + grain] | [Texture/detail emphasis] | [Aspect ratio + parameters]
```

### Template B: Natural Prose (6-block)

Most photoreal models (especially Flux, Z-Image, Imagen) prefer natural prose in 3–4 sentences over keyword soup: subject sentence → lighting/time sentence → camera/composition sentence → film/grade sentence.

```
[A/An] [age + ethnicity + subject], [wardrobe with material detail],
[specific action verb mid-motion], [Ekman-grade expression with micro-detail].

[Shot size] on a [focal length] lens at [aperture], [angle],
[composition rule], [aspect ratio].

[Location with cultural/geographic specificity] at [time of day],
[weather/atmosphere with volumetric element], [mood descriptor].

[Lighting setup] with [color palette/grade],
[practical light sources], [specific lens artifact].

Shot on [camera body] with [lens], [film stock],
[grain behavior], [scan/print workflow].

[Skin texture detail], [fabric texture detail], [environmental texture],
[photographic imperfection].
```

### Template C: Priority Stack

Always stack from most important (Subject) to most subtle (Render parameters):

```
[Subject/Action] + [Location/Atmosphere] + [Camera/Lens/Composition] +
[Lighting Rig] + [Color/Film Stock/Texture] + [Negative Prompts/Parameters]
```

### Worked Example A (photoreal, shot-card style)

> "35mm film photograph, medium close-up at eye level, 85mm lens at f/1.8 — a weathered Bedouin elder, deep crow's-feet, salt-and-pepper beard, indigo turban, crimson wool cloak, mid-laugh with crinkled eyes and Duchenne smile, leaning on a carved staff — at dawn in a Saharan dune sea, golden-hour sidelight, drifting sand particles in a soft volumetric beam, warm 3000K key with cool 8000K shadow fill, muted ochre-and-teal palette — Kodak Portra 400, fine grain, subtle halation — raking light revealing every pore and fabric weave, shallow DoF, sharp focus on eyes — --ar 3:2 --style raw"

### Worked Example B (photoreal, prose style)

> "A 34-year-old Senegalese woman in a paint-flecked denim jumpsuit and frayed grey tee, leaning into a workbench mid-sand, a knowing half-smile with tired eyes. Medium close-up on an 85mm lens at f/1.8, slight low angle, rule-of-thirds with leading line of clamped wood, 3:2. Brooklyn woodshop loft at 4 p.m. golden hour, sawdust drifting in shafts of light, warm and contemplative. Single window key light from camera-right with soft bounce fill, motivated tungsten practicals in background, deep amber + teal shadow palette, subtle anamorphic flare. Shot on a Contax 645 with 80mm Zeiss Planar, Kodak Portra 400, luminance-dependent grain, Frontier scan. Visible skin pores and peach fuzz, denim fade at the knees, dust motes in light beams, faint motion blur on her right hand."

---

## VIII. Advanced Techniques & Flagged Extras

### Lens Artifacts as Style Language

Chromatic aberration, lens flare, anamorphic streaks, vignetting, barrel distortion, bokeh shape (circular vs. cat's-eye vs. anamorphic oval), diffusion filters (Tiffen Black Pro-Mist), lens breathing, swirly Petzval bokeh, Helios-44 swirl, soap-bubble bokeh, anamorphic squeeze.

### Render Engine References (for stylized/3D looks)

"Octane render, Unreal Engine 5, Cycles, V-Ray, Arnold, Redshift" — useful when leaving photoreal.

### Artist / DP References

Roger Deakins, Emmanuel Lubezki, Gregory Crewdson, Annie Leibovitz, Wes Anderson, Tarkovsky, Caravaggio, Vermeer, Hopper, Wong Kar-wai, Bradford Young, Christopher Doyle. *Caveat: many platforms throttle living-artist names.*

### Era / Decade Tags

"1970s Kodachrome editorial," "1990s grunge magazine spread," "2000s flash photography candid," "1976 photograph," "early 2000s digicam," "2010 Tumblr aesthetic." Eras carry implicit film, fashion, and grading.

### Cultural / Genre Anchors

Film noir, Spaghetti Western, A24 horror, Studio Ghibli, ukiyo-e, brutalist editorial, Y2K, Vogue editorial. Reference tokens are often more powerful than 20 adjectives: "still from Chernobyl (2019)," "screencap from a Wong Kar-wai film."

### Image Medium / Output Type

Editorial photograph, paparazzi shot, surveillance still, CCTV frame, dashcam, polaroid, daguerreotype, tintype, screencap, behind-the-scenes still, contact sheet, VHS still, found footage, newspaper halftone, magazine glossy spread, wet plate collodion.

### Shot Purpose / Narrative Beat

Establishing, reveal, climax, denouement — often shifts framing automatically. Adding a one-line implied narrative ("the moment before she answers the phone," "the moment after a shout," "stillness of held breath") often produces more emotionally compelling compositions than pure description.

### Sound / Sensory Cross-Modal Tokens

"You can almost hear the rain," "humid," "smells of petrichor." Sensory language sometimes nudges atmospheric realism even though models can't render sound.

### Weight & Scale Words

"Monumental," "diminutive," "cathedral-like," "intimate" — affect composition more than literal size words.

### Cultural & Geographic Specificity

"Lagos market at dawn" gives more than "African market." Specificity beats generality every time.

### Print / Scan Workflow Tokens

"Scanned on Noritsu HS-1800," "Frontier scan," "drum scan," "darkroom print on fiber paper" — these affect color and texture distinctly.

### Reference-Image Conditioning

Midjourney `--sref`, Nano Banana Pro reference inputs, gpt-image-1.5 input fidelity. Often more powerful than verbal description.

### Anatomical & Physical Plausibility Cues

"Anatomically correct hands, five fingers, natural finger length" — still helpful on weaker models.

### Iteration Discipline

Change one variable at a time (lens OR lighting OR stock). If the result is 80% right, don't rewrite — adjust one knob. Generate → identify the failure → add it to negative prompt → re-roll. Don't try to perfect a prompt in one shot.

### The "Micro-Contrast" Hack

If an image looks flat, adding "crisp micro-contrast," "specular highlights," and "preserved shadow detail" forces the diffusion model to heighten the realism of how light wraps around textures.

### Aspect Ratio Matched to Subject

9:16 for portraits/mobile, 2.39:1 cinemascope for vistas, 1:1 for editorial, 4:5 for Instagram, 6:17 for panoramas.

### Weighting Syntax

- **Midjourney:** `::`
- **Stable Diffusion:** `(token:1.3)` boost, `[background:0.6]` reduce
- **Flux:** uses natural language emphasis

---

## IX. Model-Specific Notes

### Midjourney v6/v7

Prefers comma-separated tokens + parameters at the very end.

| Parameter | Function |
|-----------|----------|
| `--ar` | Aspect ratio |
| `--stylize 0–1000` | Artistic interpretation |
| `--chaos 0–100` | Variation; pulls AI away from perfectly centered subjects |
| `--weird 0–3000` | Unusual aesthetics |
| `--quality 1–4` | Quality level |
| `--sref` | Style reference image |
| `--cref / --oref` | Character/omni reference |
| `--seed` | Reproducibility |
| `--no` | Negative prompt |
| `--style raw` | Strips default AI "beautification"; forces engine to obey precise photography/lighting commands |

### Nano Banana Pro / Gemini

Responds well to natural-language paragraphs and explicit photographic terminology.

### Flux / SD3.5 / SDXL

Strong with long descriptive prose; less reliant on heavy negative prompts. Supports `(token:1.3)` weighting.

### Seedream 4.5

Benefits from cinematic and atmospheric language; preserve unmodified character descriptions for consistency.

### gpt-image-1.5

Explicitly prompt "as if a real photo captured in the moment" and avoid "cinematic movie-poster" wording when realism is the goal.

### Negative Prompt Baseline (SD/Flux/SDXL)

```
deformed, disfigured, extra fingers, mutated hands, bad anatomy, blurry, low-res,
watermark, text, jpeg artifacts, plastic skin, oversaturated, cartoonish,
AI face, smooth, airbrushed, 3d render, illustration, melted geometry, overbloom
```

---

## X. Pre-Generate Checklist

- [ ] Shot size + angle + lens chosen?
- [ ] Subject specific (traits, wardrobe, posture)?
- [ ] Action verb + named expression (Ekman or nuanced)?
- [ ] Location + era + time of day?
- [ ] Atmosphere (fog/haze/particulate) defined?
- [ ] Light direction + quality + Kelvin?
- [ ] Color palette/grade specified?
- [ ] Film stock or camera body named?
- [ ] Grain level + halation if applicable?
- [ ] Texture-revealing light + material vocabulary?
- [ ] Aspect ratio + model-specific parameters?
- [ ] Negative prompt baseline applied?

> **Treat the prompt as a shot card for an imaginary cinematographer — every line should be something a DP could actually execute on set. That mental frame is what separates a wishlist from a directable prompt.**
