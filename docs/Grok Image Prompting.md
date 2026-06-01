# Grok Imagine Prompting Guide — Image Prompting

> **Part 2 of 6** | Component deep dive, templates, style/lighting/camera keyword libraries, text rendering, and image editing prompts.

---

## 3. Image Prompting — Component Deep Dive

### Subject

**Importance:** Required — the most critical element  
**Position:** Beginning of prompt  
**Role:** Defines what the image is fundamentally about

Write with specificity: age, appearance, clothing, emotional state, and relationship to the environment.

| Weak | Strong |
|------|--------|
| "A woman" | "A 30-year-old South Asian woman in a tailored charcoal blazer" |
| "A dog" | "A golden retriever mid-leap, ears pinned back, joy in its face" |
| "A building" | "A brutalist concrete office tower looming over a narrow Tokyo alleyway" |

**Example subject descriptions:**
- `an elderly fisherman with weathered skin and deep-set eyes`
- `a teenage girl in a neon-lit cyberpunk city, her reflection in the puddles beneath her`
- `a translucent jellyfish drifting through the streets of Tokyo, bioluminescent`
- `a heavily modified orange off-road buggy racing toward the camera`

### Action / Pose

**Importance:** High — determines energy and narrative  
**Position:** Immediately after subject  
**Role:** Implies motion, emotion, and storytelling

Weak verbs produce static, generic images. Strong verbs produce energy and narrative:

| Weak verbs | Strong verbs |
|------------|-------------|
| standing | surges, lunges, shatters |
| walking | strides, drifts, stumbles |
| looking | gazes, glares, squints into |
| sitting | slumps, perches, crouches |
| holding | clutches, cradles, brandishes |
| running | sprints, bolts, tears through |

**Example action phrases:**
- `surges forward through heavy rain, coat whipping behind`
- `crouches low, peering around the corner of a concrete pillar`
- `unfurls her wings against the storm`
- `shatters the glass wall with a backhand strike`
- `cradles a glowing orb in cupped hands`

### Environment / Setting

**Importance:** High — frames the entire visual world  
**Position:** After subject and action  
**Role:** Establishes location, time period, weather, and atmosphere

Be specific: name the location type, time of day, weather conditions, and architectural/natural details.

**Example settings:**
- `in a crumbling baroque cathedral, shafts of dusty light through broken windows`
- `on a fog-covered suspension bridge at 3 AM, rain slicking the cables`
- `in a neon-drenched Tokyo alleyway, wet pavement reflecting pink and blue signage`
- `on the red dunes of Mars, ancient alien ruins in the background`
- `in a sunlit Victorian library with floor-to-ceiling bookshelves and rolling ladders`
- `in a minimalist white studio with stark overhead fill lighting`

**Time/weather cues (always include at least one):**
- `at golden hour`
- `under heavy overcast sky`
- `in heavy rain`
- `fog drifting through`
- `deep winter, blue moonlight`
- `late afternoon, long shadows`
- `at dusk, city lights flickering on`

### Lighting

**Importance:** Very high — determines mood, realism, and cinematic quality  
**Position:** After environment, before style  
**Role:** Defines how the scene is illuminated

This is where most amateur prompts fail. Generic terms like "bright" or "dark" give the model nothing to work with. Use specific lighting language:

**Natural lighting terms:**
- `golden hour sunlight` — warm, directional, long shadows
- `blue hour` — post-sunset cool blue ambient
- `overcast soft light` — diffused, flat, shadowless
- `harsh midday sunlight` — high contrast, hard shadows
- `moonlight` — cool, dim, silver-blue
- `dappled light through leaves` — moving patterns, depth
- `window light` — directional, interior soft fill

**Studio lighting terms:**
- `Rembrandt lighting` — 45° key light, triangular cheek shadow
- `softbox fill` — even, flattering, near-shadowless
- `rim light` — backlight separating subject from background
- `three-point lighting` — key + fill + rim, classic setup
- `dramatic side lighting` — hard contrast, strong shadows
- `butterfly lighting` — key light above nose, butterfly shadow

**Stylized lighting terms:**
- `neon lighting` — colored synthetic ambient
- `volumetric god rays` — light shafts through atmosphere
- `chiaroscuro` — extreme dark/light contrast, painterly
- `lens flare` — bright point light artifact
- `bioluminescent` — self-glowing organic quality
- `candlelight` — warm, flickering, low-key

**Color temperature keywords:**
- `warm color grade` — oranges, ambers, reds
- `cool tones` — blues, teals, silvers
- `desaturated` — muted, film-like
- `vibrant saturated colors` — pop art energy
- `cinematic teal and orange` — Hollywood blockbuster look
- `pastel color palette` — soft, airy, Wes Anderson

See also: [Section 6 — Lighting Keyword Library](#6-lighting-keyword-library)

### Style / Medium

**Importance:** High — determines visual language  
**Position:** Woven throughout or as closing clause  
**Role:** Sets the entire artistic register

Define style explicitly. If you don't, Aurora defaults to a photorealistic/cinematic hybrid.

**Core style categories:**
- `photorealistic` / `hyperrealistic` / `8K photography`
- `cinematic` / `film still` / `anamorphic lens`
- `anime` / `manga` / `Studio Ghibli style`
- `oil painting` / `watercolor` / `acrylic`
- `charcoal sketch` / `pencil drawing`
- `vector illustration` / `flat design`
- `3D render` / `CGI` / `Pixar-style`
- `surrealism` / `Salvador Dalí style`
- `art nouveau` / `art deco`
- `graphic novel` / `comic book`
- `concept art` / `matte painting`

See: [Section 5 — Style Keyword Library](#5-style-keyword-library)

### Camera / Composition

**Importance:** High — determines framing and emotional impact  
**Position:** Near the end of the prompt  
**Role:** Tells Aurora how to frame the shot

Camera and composition keywords are among the most reliable prompt levers for images. Aurora responds strongly to lens and shot-type language.

**Shot types:**
- `extreme close-up` — detail of eyes, hands, texture
- `close-up` — face or object fills frame
- `medium shot` — subject from waist up
- `wide shot` — full body + environment
- `extreme wide shot` / `establishing shot` — location dominant
- `aerial shot` / `bird's eye` — from above
- `worm's eye` — from below looking up

**Lens simulation:**
- `35mm lens look` — slight distortion, street photography
- `50mm` — natural human eye perspective
- `85mm lens` — portrait flattering, slight compression
- `telephoto` / `200mm` — compressed background, isolated subject
- `fisheye` — extreme distortion, wide field
- `macro` — extreme close detail

**Perspective:**
- `low angle` — subject appears powerful, dominant
- `high angle` — subject appears small, vulnerable
- `Dutch angle` — diagonal tilt, tension/unease
- `over-the-shoulder` — POV storytelling
- `eye-level` — neutral, natural

**Depth of field:**
- `shallow depth of field` — blurred background, subject in focus
- `bokeh` — soft background blur circles
- `deep focus` — everything sharp
- `tilt-shift` — miniature effect, tilted focal plane

See: [Section 7 — Camera & Composition Keyword Library](#7-camera--composition-keyword-library)

### Quality / Detail Modifiers

These keywords signal to Aurora what fidelity level to aim for:

| Modifier | Effect |
|----------|--------|
| `8K resolution` | Highest detail instruction |
| `4K photography` | High resolution photorealistic |
| `ultra-detailed` | Forces fine texture work |
| `sharp focus` | Crisp edges, no blur |
| `hyperdetailed` | Emphasizes micro-textures |
| `cinematic quality` | Film-grade color and contrast |
| `professional photography` | Implies technical competence |
| `photojournalism style` | Handheld, documentary aesthetic |
| `studio-quality render` | Clean, controlled output |
| `concept art quality` | Professional illustration grade |

### Mood / Emotion

Emotion-driven adjectives affect output strongly. Aurora's chat model reads emotional direction and reinforces it through color grading, lighting intensity, composition choices, and figure body language.

**Replace generic with specific:**

| Generic | Specific alternatives |
|---------|----------------------|
| happy | joyful, elated, carefree, radiant |
| sad | melancholic, desolate, grief-stricken |
| cool | electric, charged, razor-sharp |
| dark | ominous, brooding, oppressive |
| calm | serene, meditative, hushed |
| scary | dread-inducing, paranoid, unsettling |
| fun | playful, whimsical, lighthearted |
| romantic | tender, intimate, longing |

**High-impact mood terms:**
- `nostalgic` — warm, hazy, slightly desaturated
- `melancholic` — cool tones, isolation, quiet
- `electric` — high contrast, energy, dynamism
- `tense` — dramatic lighting, tight framing
- `dreamlike` — soft edges, surreal colors
- `oppressive` — heavy shadows, low ceilings
- `triumphant` — upward angles, warm light
- `ethereal` — glowing, light, otherworldly


---

## 4. Image Prompting — Templates

### Template 1: Emotion-Driven Portrait

```
Close-up of [subject description] in [setting], [emotion/mood] atmosphere, 
[lighting], [camera/lens type], [style keywords].
```

**Example A — Joyful Portrait:**
```
Close-up of a carefree young woman laughing under golden sunlight, wind moving 
through her hair, joyful and nostalgic mood, cinematic lens flare, warm color 
grade, shallow depth of field, 50mm lens look, photoreal natural light.
```

**Example B — Brooding Portrait:**
```
Close-up of a silver-haired man in his 60s staring into a foggy harbor at dusk, 
melancholic and resigned atmosphere, cool blue ambient with distant lamp warmth, 
85mm lens compression, shallow depth of field, cinematic film grain, desaturated 
color grade.
```

([Source: GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine))

---

### Template 2: Five-Part Formula

```
[Scene: what's happening and where] — [Style: visual aesthetic] — 
[Mood: emotional direction] — [Lighting: time/quality] — 
[Camera: shot type, lens, focus].
```

**Example A — Urban Noir:**
```
A detective in a long coat steps from a shadowed doorway into a rain-slicked alley 
at midnight — neo-noir cinematic style — tense and paranoid mood — sodium-vapor 
streetlights reflecting in puddles — low angle, wide shot, anamorphic lens.
```

**Example B — Nature Scene:**
```
A lone wolf standing on a ridge above a valley of pine trees blanketed in morning 
mist — photorealistic nature photography — serene and primordial mood — early 
morning diffused light — medium wide shot, telephoto lens compression.
```

([Source: GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine))

---

### Template 3: Photorealistic Scene

```
A hyper-realistic [subject], [physical details]. [Action/context]. 
[Lighting type], [camera specifics], [depth of field], [resolution/quality].
```

**Example A — Portrait:**
```
A hyper-realistic close-up portrait of an elderly fisherman with weathered skin, 
wearing a yellow raincoat. Raindrops dripping from the brim of his hat. Cinematic 
lighting, 85mm lens, depth of field, sharp focus on eyes, 8K resolution.
```

**Example B — Environmental:**
```
A hyper-realistic aerial view of a fishing village at high tide, white-walled 
houses pressed to a rocky cliff, turquoise Mediterranean water below. Late afternoon 
golden hour, drone camera perspective, ultra-wide lens, deep focus, photojournalism 
style, 4K.
```

([Source: XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))

---

### Template 4: Anime / Illustration

```
[Anime/illustration style descriptor] of [subject] in [setting]. 
[Action/expression]. [Color palette], [lighting approach], 
[specific style reference if needed].
```

**Example A — Action:**
```
Anime clean line art of an astronaut riding a translucent jellyfish through the 
streets of Tokyo. The jellyfish glows with bioluminescence, crowds watching in awe. 
Vibrant saturated colors, studio lighting, wide angle shot, Makoto Shinkai 
atmospheric style.
```

**Example B — Slice of Life:**
```
Soft anime illustration of a teenage girl reading at a café window on a rainy 
afternoon, steam rising from a mug beside her. Muted warm palette, diffused window 
light, medium shot, gentle nostalgic mood, Studio Ghibli-inspired background detail.
```

---

### Template 5: Product Photography

```
[Product name/description] in [setting/context]. [Shot type], camera at [angle]. 
[Lighting setup]. [Background]. [Style/mood].
```

**Example A — Clean Studio:**
```
A sleek matte black wireless headphone on a minimal concrete surface. Overhead 
three-quarter angle shot, camera at eye level. Soft studio lighting with subtle 
rim light separating the product from the background. Pure white background with 
gentle shadow. Product photography, commercial quality, sharp focus throughout.
```

**Example B — Lifestyle:**
```
A smart water bottle glowing softly on a wooden desk beside a MacBook at dusk, 
warm desk lamp light. Medium shot at a slight downward angle. Lifestyle photography 
style, warm amber tones, shallow depth of field, lived-in productive desk 
environment.
```

([Inspired by Scenario product example](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))

---

### Template 6: Architectural Visualization

```
[Architectural type] with [key design features]. [Setting/location]. 
[Time of day] with [lighting quality]. [Photography style], [camera/lens].
```

**Example A — Interior:**
```
A minimalist living room with floor-to-ceiling windows overlooking the Swiss Alps. 
Mid-century modern furniture, warm fireplace, golden hour sunlight streaming in 
casting long shadows. 4K architectural photography, wide angle, deep focus.
```

**Example B — Exterior:**
```
A brutalist concrete library emerging from a dense forest clearing, its angular 
facade softened by hanging moss. Overcast morning light, cool desaturated tones. 
Architectural photography, wide establishing shot, symmetrical framing, slight low 
angle.
```

([Source: XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))


---

## 5. Style Keyword Library

### Realism Keywords

| Keyword | Effect |
|---------|--------|
| `photorealistic` | Indistinguishable from photography |
| `hyperrealistic` | Beyond-photo detail and precision |
| `8K photography` | Extreme resolution implication |
| `4K render` | High-fidelity digital |
| `documentary photography` | Candid, unposed, natural |
| `photojournalism` | Handheld, moment-capture aesthetic |
| `editorial photography` | Styled, magazine-quality |
| `studio photography` | Controlled, professional setup |
| `RAW photograph` | Unprocessed, authentic look |
| `DSLR photo` | Consumer-camera realism |
| `film grain` | Analog texture, slight noise |
| `35mm film` | Classic analog warmth and grain |
| `Kodak Portra 400` | Warm, skin-tone-friendly film stock |
| `Fujifilm Velvia` | Saturated, high-contrast slide film |
| `Ilford HP5` | Classic black and white film |

### Anime Keywords

| Keyword | Effect |
|---------|--------|
| `anime` | General Japanese animation style |
| `manga` | Black and white comic panel style |
| `clean line art` | Crisp outlines, flat color |
| `cel shading` | Animation cell fill, bold outlines |
| `Studio Ghibli style` | Detailed backgrounds, painterly |
| `Makoto Shinkai style` | Hyperdetailed sky, light effects |
| `shonen anime` | Action-oriented, bold |
| `shojo anime` | Soft, romantic, detailed faces |
| `cyberpunk anime` | Neon, mech, dystopian |
| `isekai style` | Fantasy world, vibrant palette |
| `chibi` | Cute, exaggerated proportions |
| `mecha` | Mechanical suits, sci-fi |

### Painterly Keywords

| Keyword | Effect |
|---------|--------|
| `oil painting` | Rich texture, visible brushwork |
| `watercolor` | Transparent washes, soft edges |
| `acrylic painting` | Opaque, vibrant colors |
| `gouache` | Flat, matte, illustrative |
| `impressionism` | Loose brushwork, captured light |
| `expressionism` | Distorted, emotional |
| `Monet style` | Soft, dappled light |
| `Rembrandt style` | Dark backgrounds, dramatic lit faces |
| `digital painting` | Painterly but digitally rendered |
| `concept art` | Professional illustration for games/film |
| `matte painting` | Film background art style |
| `folk art` | Naive, pattern-based |

### Cinematic Keywords

| Keyword | Effect |
|---------|--------|
| `cinematic` | Film-grade aesthetic |
| `film still` | Single frame from a movie |
| `anamorphic lens` | Horizontal lens flare, widescreen |
| `teal and orange color grade` | Hollywood action look |
| `cinematic color grading` | Professional color treatment |
| `widescreen` | 2.39:1 aspect, cinematic framing |
| `noir` | High contrast, shadows, mystery |
| `neo-noir` | Modern noir with color |
| `Hollywood blockbuster` | High production value |
| `Wes Anderson style` | Symmetrical, pastel, quirky |
| `Kubrick style` | One-point perspective, cold |
| `Nolan style` | IMAX, practical effects look |

### Surreal Keywords

| Keyword | Effect |
|---------|--------|
| `surrealism` | Dream logic, impossible elements |
| `Salvador Dalí style` | Melting objects, dreamscapes |
| `René Magritte style` | Conceptual juxtaposition |
| `psychedelic` | Vivid, kaleidoscopic |
| `dreamlike` | Soft, hazy, logic-defying |
| `liminal space` | Uncanny empty familiar spaces |
| `glitch art` | Digital distortion |
| `vaporwave` | 80s/90s pastel nostalgia |
| `synthwave` | Neon grid, retro-futurism |
| `dark fantasy` | Gothic, ominous, mystical |
| `cosmic horror` | Lovecraftian scale and dread |

### Graphic Novel Keywords

| Keyword | Effect |
|---------|--------|
| `graphic novel` | Illustrated narrative style |
| `comic book art` | Halftone dots, bold outlines |
| `DC Comics style` | Gritty superhero aesthetic |
| `Marvel Comics style` | Dynamic, action-pose |
| `ink wash` | East Asian brush and ink |
| `woodcut print` | Textured, high-contrast |
| `linocut` | Bold, printmaking aesthetic |
| `Frank Miller style` | Black/white extremes, gritty |
| `Art Spiegelman style` | Raw, expressive illustration |

### Photography-Specific Keywords

| Keyword | Effect |
|---------|--------|
| `35mm lens` | Slight distortion, wide-normal |
| `50mm lens` | Natural perspective |
| `85mm lens` | Portrait focal length, flattering |
| `telephoto 200mm` | Subject isolation, compressed depth |
| `fisheye lens` | Extreme distortion, 180° |
| `macro lens` | Extreme close-up detail |
| `tilt-shift` | Miniature effect |
| `long exposure` | Motion blur, light trails |
| `double exposure` | Two images overlaid |
| `cross-process` | Unusual color shifts |
| `Kodak Portra` | Warm, neutral skin film |
| `Fuji Velvia` | Saturated landscape film |
| `Ektachrome` | Punchy, slightly cool |
| `Polaroid` | Instant film square format |


---

## 6. Lighting Keyword Library

### Natural Lighting

| Keyword | Description | Color Temp |
|---------|-------------|-----------|
| `golden hour` | 1 hour after sunrise / before sunset, warm directional | Warm amber |
| `blue hour` | After sunset, soft blue ambient fills scene | Cool blue |
| `overcast light` | Cloud-diffused, flat, no shadows | Neutral |
| `harsh midday sun` | High contrast, hard shadows, hot highlights | Neutral-warm |
| `dappled sunlight` | Pattern through leaves, moving | Warm patches |
| `window light` | Side-directional indoor natural | Neutral-warm |
| `moonlight` | Very low intensity, silver-blue | Cold silver-blue |
| `starlight` | Almost dark, minimal ambient | Deep cool |
| `sunrise` | Directional warm, pink/orange sky | Warm pink |
| `sunset` | Rich warm, orange-red | Warm orange |
| `fog light` | Diffuse, atmospheric, glowing edges | Neutral-cool |
| `underwater light` | Caustics, dancing patterns | Cyan/green |

### Studio Lighting

| Keyword | Description | Use Case |
|---------|-------------|----------|
| `Rembrandt lighting` | 45° key, triangular cheek shadow | Dramatic portraits |
| `softbox lighting` | Even, diffused, flattering | Portraits, products |
| `rim lighting` | Backlight creating edge glow | Separation from BG |
| `key light` | Primary directional source | All lit scenes |
| `fill light` | Secondary soft light, reduces shadows | Balanced portraits |
| `three-point lighting` | Key + fill + rim setup | Professional portrait |
| `butterfly lighting` | Key above nose, shadow below | Glamour/fashion |
| `clamshell lighting` | Two sources above/below | Beauty photography |
| `split lighting` | 50/50 left/right division | Character studies |
| `hair light` | Overhead backlight for hair | Separation effect |
| `background light` | Illuminates BG separately | Depth |
| `loop lighting` | Slight below-nose shadow loop | Commercial portraits |

### Stylized Lighting

| Keyword | Description |
|---------|-------------|
| `neon lighting` | Colored neon glow, cyberpunk |
| `volumetric lighting` / `god rays` | Light shafts through atmosphere |
| `chiaroscuro` | Extreme dark/light painterly contrast |
| `bioluminescent` | Organism self-glow, teal/blue/green |
| `lens flare` | Bright point-source light artifact |
| `candlelight` | Warm, flickering, low-key |
| `firelight` | Warm orange, dancing shadows |
| `blacklight` / `UV` | Fluorescent colors on dark |
| `fairy lights` | Small warm point sources |
| `lava glow` | Deep orange uplight |
| `neon sign light` | Local colored spill |
| `holographic` | Rainbow diffraction |
| `plasma glow` | Electrical discharge light |

### Color Temperature Keywords

| Keyword | Kelvin Range | Visual Effect |
|---------|-------------|---------------|
| `warm color grade` | 2700–4000K | Amber, honey, cozy |
| `cool tones` | 6500–10000K | Blue, crisp, clinical |
| `neutral` | 5000–5500K | Natural daylight |
| `desaturated` | — | Muted, faded, film |
| `warm film look` | — | Kodak-style organic warmth |
| `teal and orange` | — | Hollywood action grade |
| `sepia` | — | Aged, nostalgic |
| `cyan and crimson` | — | High-fashion contrast |
| `monochrome` | — | Full black and white |
| `duotone` | — | Two-color processing |


---

## 7. Camera & Composition Keyword Library

### Shot Types

| Shot Type | Description | Use Case |
|-----------|-------------|----------|
| `extreme close-up` (ECU) | Single detail: eye, finger, texture | Intimacy, tension |
| `close-up` (CU) | Face / object fills frame | Emotion, detail |
| `medium close-up` (MCU) | Head to upper chest | Interviews, portraits |
| `medium shot` (MS) | Waist up | Conversation, character |
| `medium wide shot` (MWS) | Full body with some environment | Character in context |
| `wide shot` (WS) | Full body + significant environment | Establishing character |
| `extreme wide shot` (EWS) | Location dominant | Establishing scenes |
| `aerial shot` | From directly above | Scale, pattern |
| `bird's eye view` | High angle overhead | Overview, God perspective |
| `worm's eye view` | From ground looking up | Power, dominance |
| `drone shot` | High altitude, cinematic | Landscapes, establishing |
| `over-the-shoulder` (OTS) | From behind one subject toward another | Dialogue, POV |
| `POV shot` | From character's viewpoint | Immersion |

### Lens Simulation

| Lens | Focal Length | Effect |
|------|-------------|--------|
| Fisheye | 8–15mm | Extreme distortion, 180° FOV |
| Ultra-wide | 14–24mm | Dramatic environment, distorted edges |
| Wide angle | 24–35mm | Street photography feel |
| Normal | 50mm | Human eye perspective |
| Portrait | 85mm | Face flattering, slight compression |
| Short telephoto | 105–135mm | Tighter portrait, no distortion |
| Telephoto | 200–300mm | Strong compression, subject isolation |
| Super telephoto | 400mm+ | Extreme compression, wildlife feel |
| Macro | Any | Extreme close-up capability |
| Tilt-shift | Any | Selective focus, miniature effect |
| Anamorphic | Any | Horizontal flare, cinematic widescreen |

### Perspective

| Keyword | Description | Effect |
|---------|-------------|--------|
| `low angle` | Camera below eye level | Subject dominant, powerful |
| `high angle` | Camera above eye level | Subject small, vulnerable |
| `eye level` | Camera at subject's eye height | Natural, neutral |
| `bird's eye` | Directly above | Overhead, pattern-focused |
| `worm's eye` | Looking straight up | Extreme upward perspective |
| `Dutch angle` | Camera tilted diagonally | Tension, unease, wrongness |
| `over-the-shoulder` | Behind one subject | Dialogue, relationships |
| `forced perspective` | Visual tricks with scale | Surreal, playful |
| `two-point perspective` | Urban, architectural depth | Cityscapes |
| `one-point perspective` | Road/hallway vanishing point | Kubrick look, tension |

### Framing

| Keyword | Description |
|---------|-------------|
| `rule of thirds` | Subject off-center at grid intersections |
| `centered / symmetrical` | Subject perfectly centered |
| `negative space` | Intentional empty area around subject |
| `dynamic composition` | Diagonal lines, movement implied |
| `golden ratio` | Spiral-based natural composition |
| `framed within frame` | Window/door framing the subject |
| `leading lines` | Lines guiding eye to subject |
| `headroom` | Space above subject's head |
| `tight crop` | Little space around subject |

### Depth of Field

| Keyword | Description |
|---------|-------------|
| `shallow depth of field` | Subject sharp, background blurred |
| `deep focus` | Everything front to back in focus |
| `bokeh` | Background blur quality (soft circles) |
| `tilt-shift` | Selective horizontal focus plane |
| `focus rack` | Shift of focus within a shot |
| `soft focus` | Dreamy slight blur throughout |
| `pan focus` | Everything sharp, documentary style |


---

## 8. Text Rendering in Images

### Overview

Text rendering is one of Aurora's acknowledged **standout strengths**, and one of its clearest differentiation points from DALL-E 3 and Midjourney. ([XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))

> "Whether you need a neon sign reading 'Cyberpunk 2077' or a handwritten note, the model renders characters with high accuracy. This makes it an invaluable tool for graphic designers and marketers." — [XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/)

**Reliability by use case:**

| Use Case | Reliability |
|----------|------------|
| Short phrases (2–5 words) | Excellent |
| Single word logos | Excellent |
| Signs and storefronts | Excellent |
| Longer sentences | Good |
| Cursive / handwriting | Good |
| Long paragraphs | Mixed |
| Non-Latin scripts | Mixed |

### Syntax for Text Rendering

**Method 1 — Direct quotes:**
```
A neon sign on a brick wall that says "OPEN LATE" in red block letters.
```

**Method 2 — "says" instruction:**
```
A futuristic neon sign that says 'XS ONE CONSULTANTS' in bright blue cursive font.
```

**Method 3 — Integrated description:**
```
A coffee shop chalkboard menu with "COLD BREW $5" written in casual hand lettering.
```

The model understands the `says 'text'` pattern as a separation of visual style from textual content — this is the most reliable syntax for exact text control. ([XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))

### Tips for Accurate Text

1. **Keep text short:** 1–5 words is the sweet spot. Longer text introduces character errors.
2. **Specify font style:** "bold sans-serif," "handwritten cursive," "neon tube font," "serif newspaper headline"
3. **Specify color of text:** "white text on dark background," "red glowing letters"
4. **Specify context:** "on a sign," "on a storefront," "in a speech bubble," "on a product label"
5. **Don't overload:** If your prompt has many text elements, prioritize one and omit the rest
6. **Capitalize important words:** Helps the model identify the text string vs description

**Tested example (from XsOne):**
```
A futuristic neon sign on a brick wall that says 'XS ONE CONSULTANTS' in bright 
blue cursive font. Cyberpunk aesthetic, wet pavement reflection, night time, 
volumetric fog.
```

### Limitations

- Long strings (>8 words) show increased character substitution errors
- Non-Latin scripts (Arabic, Chinese, Korean) are less reliable
- Overlapping text with busy backgrounds reduces accuracy
- The chat model revision may alter quoted text strings — check `revised_prompt` if text output is wrong
- No way to specify exact typeface by font name — use descriptive style terms only


---

## 9. Image Editing Prompts

### How Editing Works

The image editing endpoint accepts a **source image + text instruction**. Aurora modifies the image according to the instruction while maintaining the non-specified elements. ([xAI Docs](https://docs.x.ai/developers/model-capabilities/images/generation))

**Endpoint:** `POST https://api.x.ai/v1/images/edits`

**Modes:**
- **Single image editing:** One source image + prompt
- **Multiple image editing:** Up to 5 source images; aspect ratio follows first image by default (override with `aspect_ratio` parameter)

Source images can be provided as:
- Public URL
- Base64-encoded data URI (`data:image/png;base64,...` or `data:image/jpeg;base64,...`)

### How to Phrase Edits

The fundamental rule: **lock what stays, describe what changes**.

```
❌ Weak edit instruction:
"Make it more dramatic"

✅ Strong edit instruction:
"Keep the subject and pose exactly as-is. Change the background from a white 
studio to a thunderstorm over the ocean. Add dramatic lightning in the sky. 
Keep the lighting on the subject's face unchanged."
```

**Structure for edits:**
```
Keep [elements to preserve]. Change [specific modification]. 
Add [new elements if needed]. Adjust [specific tweaks].
```

### Edit Types

**Style transfer:**
```
Render this image as an oil painting in the style of impressionism.
```
```
Render this as a pencil sketch with detailed shading.
```
```
Render this as pop art with bold colors and halftone dots.
```
```
Render this as a watercolor painting with soft edges.
```

**Background change:**
```
Keep the subject and their lighting exactly the same. Replace the background 
with a dense foggy forest at dusk.
```

**Object add:**
```
Keep everything exactly the same. Add a small white cat sitting on the desk 
in the lower right corner.
```

**Object remove:**
```
Remove the car parked in the background on the left side. Fill the space 
with the same street and buildings.
```

**Enhancement:**
```
Enhance this photo to ultra-high resolution and perfect clarity. Correct 
lighting, exposure and color balance. Naturally remove blemishes while 
keeping realistic skin texture. No cartoonish or plastic look.
```

**Color adjustment:**
```
Keep the composition and all elements identical. Shift the entire color 
grade from warm amber to cool teal. Desaturate slightly for a film look.
```

### Iterative Refinement (Conversational Approach)

Grok Imagine is built into a chat interface, which enables conversational iteration. After a generation, you can follow up with simple instructions:

```
[Initial generation]
"A woman sitting in a cozy café with her laptop..."

[Follow-up 1]
"Make it darker and moodier."

[Follow-up 2]
"Change the background to rain on the window."

[Follow-up 3]
"Add a half-empty coffee cup on the table."
```

This approach is faster than writing a new prompt from scratch, and Aurora maintains context across turns. ([XsOne Consultants](https://xsoneconsultants.com/blog/grok-aurora-image-generator/))

### Multi-Image Editing (API)

You can provide up to **5 source images** for multi-image editing. Use case: combining elements from multiple reference photos.

```python
import xai_sdk
import base64

client = xai_sdk.AsyncClient()

source_images = [
    "https://example.com/face-reference.jpg",
    "https://example.com/clothing-reference.jpg",
    "https://example.com/pose-reference.jpg",
]

response = await client.image.sample(
    prompt="Combine the face from the first image with the clothing from the second, posed like the third. Photorealistic, studio lighting.",
    model="grok-imagine-image",
    image_url=source_images,
)
```


---

