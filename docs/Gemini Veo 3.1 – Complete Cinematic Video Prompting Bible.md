# Gemini Veo 3.1 – Complete Cinematic Video Prompting Bible
### Research Findings, Industry Techniques & Full Prompting Guide

***

## Executive Overview

Google DeepMind's **Veo 3.1** represents a fundamental shift in AI video generation — from passive description to active cinematic direction. Built on Veo 3, it delivers stronger prompt adherence, native multi-layer audio, improved audiovisual quality in image-to-video workflows, and advanced creative controls including frame interpolation and reference-image conditioning. Released broadly across the Gemini API and Vertex AI through late 2025 and early 2026, the Veo 3.1 family now forms the backbone of professional AI video production workflows.[^1][^2][^3][^4]

This document is the comprehensive industry reference for Veo 3.1 video prompting. It covers every creative and technical lever available to filmmakers, from shot composition and camera grammar through audio design, rendering, texture, genre-specific techniques, and advanced multi-shot workflows.

***

## Part 1: Model Variants & Technical Specifications

### 1.1 The Veo 3.1 Model Family

There are three production variants, each optimized for a different balance of cost, speed, and quality:[^5][^3]

| Model | Best For | Resolution | Key Traits |
|---|---|---|---|
| **Veo 3.1 (Standard)** | Final production cuts, cinematic output | Up to 4K (3840×2160)[^6] | Maximum visual fidelity; supports all advanced features including Ingredients to Video[^7] |
| **Veo 3.1 Fast** | Standard production workflows | 1080p Enhanced | High quality with faster generation; ideal for rapid iteration on professional projects[^3] |
| **Veo 3.1 Lite** | High-volume, cost-effective generation | 720p / 1080p | Most cost-effective; same speed as Fast at less than half the cost; full audio support[^2][^8] |

### 1.2 Core Technical Capabilities

All Veo 3.1 variants share these foundational specifications:[^2][^6][^1]

- **Video duration:** 4, 6, or 8 seconds per clip (extendable via Scene Extension)
- **Aspect ratios:** 16:9 (landscape) and 9:16 (portrait/vertical — native, not cropped)[^9]
- **Resolution tiers:** 720p (preview/Lite), 1080p Enhanced (Fast/Standard), 4K (Standard via AI upscaling)[^6]
- **Audio:** Native dialogue, SFX, ambient, and music cues — all generated with the video[^1]
- **Watermarking:** SynthID digital watermark embedded in all outputs[^1]
- **API model string:** `veo-3.1-generate-preview` (Gemini API)[^10]

### 1.3 The 4K Upscaling Engine

Veo 3.1 Standard's 4K capability is genuine AI upscaling, not pixel stretching. The engine analyzes scene content and intelligently reconstructs fine texture details — fabric weave patterns, skin pore detail, foliage complexity, and architectural surface variation — making it suitable for theatrical projection and broadcast workflows.[^11]

***

## Part 2: The Core Prompting Framework

### 2.1 The Five-Part Cinematic Formula

Every effective Veo 3.1 prompt is built around a structured five-part framework. This is the official Google-recommended formula and the starting point for all professional work:[^12][^1]

```
[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance]
```

| Component | What to Define | Examples |
|---|---|---|
| **Cinematography** | Shot type, camera movement, lens, composition | Medium shot, crane shot, shallow DOF, tracking |
| **Subject** | Character or focal object with specific detail | "A woman in her 30s with sharp eyes and silver hair" |
| **Action** | What the subject is doing — precise verbs | "Slowly raises a lantern, scanning the shadows" |
| **Context** | Location, time of day, environment, background | "Crumbling castle courtyard, pre-dawn fog" |
| **Style & Ambiance** | Aesthetic, mood, lighting, color grade | "Gothic horror, cold blue-green tones, heavy grain" |

**Canonical Example Prompt (Google Official):**
> *Medium shot, a tired corporate worker, rubbing his temples in exhaustion, in front of a bulky 1980s computer in a cluttered office late at night. The scene is lit by the harsh fluorescent overhead lights and the green glow of the monochrome monitor. Retro aesthetic, shot as if on 1980s color film, slightly grainy.*[^1]

### 2.2 The Extended Six-Part Formula (Advanced)

For complete cinematic and audio control, expand to six parts:[^13]

```
[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance] + [Audio Cues]
```

Adding `[Audio Cues]` explicitly tells the model what to generate on the soundstage — dialogue, SFX, and ambience — preventing the model from filling silence arbitrarily.[^14]

### 2.3 Optimal Prompt Length

Research and testing consistently shows 100–200 words as the optimal range for Veo 3.1 prompts. Shorter prompts leave too much to chance; longer prompts risk contradictions and semantic noise. For multi-shot timestamp prompts, each timed segment can be 30–60 words.[^15]

***

## Part 3: Camera & Cinematography Language

This is the most critical section for cinematic output. Veo 3.1 responds to professional film vocabulary with high precision. Using exact cinematography terms is the primary lever for controlling tone, emotion, and visual style.[^16]

### 3.1 Camera Movements

| Movement | Description | Best Used For |
|---|---|---|
| **Dolly-in / Dolly-out** | Camera physically moves toward or away from subject | Building intimacy (in) or revealing context (out) |
| **Tracking Shot** | Camera follows subject horizontally | Action, walking scenes, chase sequences |
| **Crane Shot** | Camera elevates from low to high | Epic reveals, scale, power moments[^1] |
| **Aerial / Drone View** | Overhead perspective | Establishing shots, landscapes, geography |
| **Slow Pan** | Horizontal pivot, measured pace | Scene reveals, environmental storytelling |
| **Whip-Pan** | Fast lateral swing creating motion blur | Dynamic transitions, urgency[^17] |
| **POV Shot** | Camera acts as character's eyes | Immersion, horror, first-person action[^18] |
| **Handheld Shot** | Subtle shake simulating human-held camera | Documentary, realism, urgency, found-footage[^19] |
| **Static / Locked-Off** | Camera does not move | Performance focus, tension, dialogue[^20] |
| **Steadicam / Smooth Tracking** | Stabilized follow | Continuous action, hallway scenes, suspense |
| **Rack Focus / Pull Focus** | Focus shifts between foreground and background | Revealing hidden elements, emotional shift |
| **Arc Shot / 180° Orbit** | Camera circles around subject | Dramatic reveals, character-centric drama[^1] |
| **Tilt Shot** | Camera pivots vertically | Power dynamics (tilt-up = authority; tilt-down = vulnerability) |
| **Dutch Angle / Canted Frame** | Camera tilted on axis | Psychological unease, disorientation, horror |
| **Boom / Jib** | Arm-mounted sweep | Smooth vertical/arc motion in confined spaces |

### 3.2 Shot Composition & Framing

| Shot Type | Abbreviation | Frame Coverage | Emotional Use |
|---|---|---|---|
| **Extreme Wide Shot** | EWS | Full landscape/environment | Scale, isolation, world-building |
| **Wide / Establishing Shot** | WS | Full subject + environment | Scene setting, geography |
| **Full Shot** | FS | Full body | Character introduction, body language |
| **Medium Wide Shot** | MWS | Waist to head | Conversation, movement |
| **Medium Shot** | MS | Chest to head | Standard dialogue, interaction |
| **Medium Close-Up** | MCU | Shoulders to head | Emotional dialogue |
| **Close-Up** | CU | Face only | Emotion, reaction, detail |
| **Extreme Close-Up** | ECU | Eyes, lips, hands | Extreme tension, sensory detail |
| **Over-the-Shoulder** | OTS | Subject seen from behind another | Conversational exchange |
| **Two-Shot** | — | Two subjects in frame | Relationship, dialogue balance |
| **Insert Shot** | — | Object or detail | Narrative clue, texture emphasis |
| **Cutaway** | — | Away from main action | Context, reaction, parallel action |

Prompt Example:
> *Extreme close-up of trembling hands clutching a crumpled letter, soft candlelight, shallow depth of field, warm amber tones, Victorian period drama style.*[^21]

### 3.3 Lens & Depth-of-Field Techniques

| Technique | Effect on Image | Prompt Language |
|---|---|---|
| **Shallow Depth of Field** | Subject sharp, background blurred (bokeh) | "shallow depth of field," "f/1.8 aesthetic" |
| **Deep Focus** | Everything in sharp focus | "deep focus," "all elements in sharp detail" |
| **Wide-Angle Lens** | Wider perspective, slight distortion | "wide-angle lens," "16mm look" |
| **Telephoto Compression** | Subjects appear stacked, background brought close | "telephoto compression," "200mm lens" |
| **Macro Focus** | Extreme close-up of very small objects | "macro lens," "extreme close-up of surface texture" |
| **Soft Focus** | Dreamy, romantic blur | "soft focus," "diffused light, dreamlike" |
| **Anamorphic Lens Flare** | Horizontal lens flare streaks | "anamorphic lens flare," "cinematic lens flare" |
| **Fisheye** | 180° ultra-wide distortion | "fisheye lens," "extreme barrel distortion" |

***

## Part 4: Lighting & Color

### 4.1 Lighting Setups

| Lighting Style | Prompt Terms | Genre/Mood |
|---|---|---|
| **Three-Point Lighting** | "professional studio lighting," "clean even illumination" | Corporate, interview, product |
| **Chiaroscuro / High Contrast** | "dramatic chiaroscuro," "deep shadows, bright key light" | Film noir, horror, thriller[^22] |
| **Golden Hour / Magic Hour** | "golden hour sunlight," "warm amber backlight" | Romance, drama, epic adventure |
| **Blue Hour / Dusk** | "blue hour, soft twilight," "cool desaturated dusk" | Melancholy, mystery, urban noir[^23] |
| **Motivated Lighting** | "lit by a single candle," "neon sign as key light" | Realism, atmospheric immersion |
| **Rembrandt Lighting** | "Rembrandt lighting, triangle of light on cheek" | Portrait drama, character intensity |
| **Silhouette** | "strong backlit silhouette against a bright horizon" | Mystery, epic scale, poetry |
| **Underlighting** | "light source below subject," "low-angle upward light" | Horror, supernatural, villainy |
| **Practical Lights** | "lit by fire glow / streetlamps / TV flicker" | Naturalism, intimacy, noir |
| **High-Key Lighting** | "bright, even, high-key lighting, minimal shadows" | Comedy, commercial, lifestyle |
| **Low-Key Lighting** | "low-key lighting, dominant shadows, minimal fill" | Horror, thriller, noir, drama |
| **Hard Light** | "harsh directional light, sharp shadow edges" | Intensity, conflict, realism |
| **Soft Light** | "soft diffused light, no harsh shadows" | Romance, calm, product beauty |

### 4.2 Color Grading & Palettes

Describing a color grade or palette in prompts instructs Veo 3.1 to produce the equivalent of a post-production LUT:[^24][^23]

| Grade / Look | Prompt Language | Typical Genre |
|---|---|---|
| **Teal & Orange** | "teal-orange grade, warm skin tones against cool backgrounds" | Action blockbuster, thriller |
| **Desaturated / Bleach Bypass** | "desaturated colors, bleached highlights, gritty feel" | War, psychological thriller |
| **Warm Amber / Sepia** | "warm amber tones, golden sepia grading" | Period drama, Western, nostalgia |
| **Cool Blue-Green** | "cool blue-green palette, melancholic tones" | Sci-fi, noir, drama[^21] |
| **Neon / Cyberpunk** | "neon-saturated, teal-magenta bias, deep blacks" | Cyberpunk, urban night, action[^23] |
| **High Contrast Black & White** | "high contrast B&W, deep blacks, blown highlights" | Film noir, documentary, art film[^25] |
| **Kodachrome / Analog Film** | "1970s Kodachrome aesthetic, warm grain, soft highlights" | Period pieces, nostalgia, indie[^24] |
| **Flat / Log Look** | "flat color profile, low contrast, cinema log aesthetic" | Realism, documentary style |
| **Vibrant / Saturated** | "vivid saturated colors, high contrast, punchy palette" | Comedy, animation, viral social |

***

## Part 5: Texture, Rendering & Film Stock

This is one of the most underused areas of Veo 3.1 prompting. Specifying texture and rendering style controls the entire tactile feel of the video.[^7][^26]

### 5.1 Film Stock & Analog Textures

| Look | Prompt Language |
|---|---|
| **35mm Film Grain** | "35mm film grain," "slight grain texture, analog feel"[^7] |
| **Super 8 / 8mm** | "Super 8 aesthetic, light leaks, heavy grain, warm tones" |
| **VHS Tape** | "VHS tape look, scan lines, color bleeding, slight static"[^27] |
| **16mm Documentary** | "16mm documentary aesthetic, handheld, gritty grain" |
| **Kodak Vision3** | "Kodak Vision3 film stock, warm rich highlights, dense blacks" |
| **Fuji Velvia** | "Fuji Velvia color, hyper-saturated greens and reds, deep contrast" |
| **Polaroid / Instant Film** | "Polaroid aesthetic, slightly faded, warm vignette, soft detail" |
| **Black & White Film** | "classical black and white film, silver halide grain, high contrast" |
| **Anamorphic Scope** | "anamorphic widescreen, horizontal lens flares, squeezed bokeh" |

### 5.2 Digital & CGI Rendering Styles

| Style | Prompt Language | Use Case |
|---|---|---|
| **Photorealistic CGI** | "photorealistic rendering, ray-traced lighting, 4K detail" | VFX shots, product visualization |
| **Unreal Engine Look** | "Unreal Engine 5 aesthetic, real-time rendering, cinematic lighting" | Game trailers, sci-fi |
| **Physically Based Rendering** | "physically based materials, metallic reflections, subsurface scattering skin" | Product demos, architecture |
| **Matte Painting Style** | "matte painting aesthetic, sweeping hand-painted environments" | Epic fantasy, sci-fi |
| **Claymation** | "claymation style, handmade textures, stop-motion feel"[^28] | Comedy, children's, quirky art |
| **Pixar/3D Animation** | "Pixar-style 3D animation, smooth surfaces, warm expressive lighting"[^17] | Family, animated storytelling |
| **Anime** | "anime style, cel-shaded, high contrast line art, vivid colors" | Anime, manga-inspired shorts |
| **2D Animation** | "flat 2D animation, bold outlines, graphic design aesthetic" | Explainer, stylized storytelling |
| **Stop Motion** | "stop motion animation, physical texture, deliberate frame rate"[^28] | Quirky, artisanal, advertising |
| **Watercolor / Impressionist** | "watercolor animation, flowing paint, soft edges" | Art, literary adaptation |

### 5.3 Environmental Textures & Surfaces

Describing the physical texture of environments directly guides Veo's rendering of material surfaces:[^26]

- **Stone & architecture:** "worn cobblestones," "crumbling mortar between ancient bricks," "marble with natural veining"
- **Organic / nature:** "moss-covered bark," "rain-soaked leaf litter," "iridescent water surface"
- **Metallic / industrial:** "brushed stainless steel," "rusted corrugated iron," "reflective chrome"
- **Fabric / clothing:** "heavy wool coat texture," "worn denim fade," "silk catching light"
- **Glass & reflections:** "rain droplets on glass," "partial window reflection doubling the scene"
- **Skin:** "visible pore detail," "freckled complexion," "sun-weathered skin creases"

***

## Part 6: The Complete Audio Prompting System

Veo 3.1 generates a complete, synchronized audiovisual experience from text alone. The audio system has four layers, all controlled via prompt language.[^29][^14][^1]

### 6.1 The Four Audio Layers

| Layer | What It Is | Prompt Syntax |
|---|---|---|
| **Dialogue** | Spoken character lines with lip sync | `A man says, "We have to leave now."` |
| **Sound Effects (SFX)** | Action-triggered or scene sounds | `SFX: thunder cracks in the distance` |
| **Ambient / Room Tone** | Background environmental soundscape | `Ambient noise: quiet hum of a starship bridge` |
| **Music Cues** | Mood-based underscoring | `Music: soft orchestral swell, building tension` |

### 6.2 Dialogue Prompting

Use the following formula for maximum lip-sync accuracy and voice clarity:[^14]

```
Speaker: [identity]. Line: "[exact words]." Delivery: [tone, pace, emotion]. Timing: [when line starts].
```

**Examples:**
- `A tired detective looks up and says, "Of all the offices in this town, you had to walk into mine." Gravelly, weary delivery, line begins after a 1-second pause.`[^1]
- `A young woman whispers excitedly, "What did you find?" Her face is in close-up, natural lip sync to the line.`[^10]
- `Warm female voiceover says, "Everything begins with a single frame." Tutorial tone, medium pace, no visible speaker.`[^14]

**Dialogue best practices:**
- Keep lines to one sentence for clips under 8 seconds[^14]
- Place quotation marks around exact spoken text[^1]
- Describe the voice character (gravelly, bright, trembling, confident)
- Specify lip sync explicitly: "natural lip sync to the quoted line"
- Avoid multiple speakers in the same short clip unless using multi-shot workflows

### 6.3 Sound Effects (SFX) Prompting

SFX must be linked to visible actions for greatest realism. Use this formula:[^14]

```
Add [sound] exactly when [visible action] happens. Keep it [volume/style].
```

**SFX by genre:**

| Genre | Typical SFX Prompts |
|---|---|
| **Action** | `SFX: tires screech, rapid gunfire, shattered glass` |
| **Horror** | `SFX: distant door creak, whispering voices, heartbeat thud` |
| **Sci-Fi** | `SFX: electronic hum, spaceship engine ignition, interface beeps` |
| **Romance** | `SFX: soft piano key, rustling leaves, distant church bells` |
| **Documentary** | `SFX: natural wind, gravel footsteps, ambient bird calls` |
| **Western** | `SFX: distant wind, horse hooves on dry earth, spur jingle` |
| **Thriller** | `SFX: clock ticking, sharp violin sting, stealthy footsteps` |

### 6.4 Ambient Sound & Room Tone

Ambience grounds the clip in a physical space. Never leave it unspecified for realism:[^29][^14]

```
Ambient noise: [environmental description], [volume instruction relative to any dialogue].
```

**Examples by setting:**
- Indoor quiet: `"quiet studio room tone, soft air conditioning hum, no music"`
- Urban: `"outdoor street ambience, distant traffic, occasional pedestrian footsteps"`
- Nature: `"outdoor morning ambience, birds, light wind through grass, no music"`
- Sci-fi: `"minimal futuristic interface hum, very low volume, sterile silence"`
- Period drama: `"candlelit room, crackling fire, distant rain on window panes"`
- Horror: `"eerie silence, distant dripping water, low subliminal drone"`

### 6.5 Music Prompting

For in-clip music cues, describe mood rather than specific copyrighted titles:[^14]

- `"soft orchestral swell beginning at the scene's emotional peak"`
- `"sparse piano motif, low volume, melancholic"`
- `"dark electronic pulse building in intensity, no melodic lyrics"`
- `"upbeat acoustic guitar underlay, warm and hopeful"`
- `"no music, only natural sound and room tone"`
- `"short optimistic sting at the end of the clip"`

### 6.6 Audio Negative Prompts

Use these when specific audio elements would break the scene:[^30]

- `no background music` / `no singing` / `no random crowd noise`
- `no dramatic horror score` (for tension-only silence)
- `no spoken dialogue` (for pure visual/SFX clips)
- `no robotic narration` / `no cartoon sound effects`
- `subtle ambient sound only, leave room for voiceover in editing`

***

## Part 7: Genre-Specific Prompting Blueprints

### 7.1 Action & Thriller

**Key visual elements:** High camera dynamism, motion blur, tight editing rhythm, kinetic energy[^20]

**Prompt template:**
> `[Fast tracking / handheld] [protagonist] [physical action — chase, fight, explosion] [urban/industrial environment], [time: night or dusk], [teal-orange grade, high contrast], [motion blur on fast moves], [SFX: impact, engine roar, radio chatter], [score: dark electronic pulse].`

**Example:**
> *Fast handheld tracking shot following a masked courier sprinting through a rain-soaked Tokyo alleyway at night. She vaults over a market stall, scattering produce. Neon signs reflect in puddles. Teal-orange grade, anamorphic lens flares, motion blur on fast movement. SFX: rapid footsteps, vendors shouting, distant siren. Music: heavy electronic beat driving forward.*

### 7.2 Horror & Psychological Thriller

**Key visual elements:** Slow reveals, darkness, negative space, unsettling symmetry, handheld unease[^18]

**Lighting:** Low-key, underlighting, motivated candle/flashlight, desaturated color

**Prompt template:**
> `[Slow push-in / POV / static locked-off] [empty or threatening environment], [atmospheric fog, flickering light source], [minimal subject, or partial reveal of threat], [desaturated cold palette, heavy shadows], [SFX: distant creak / whispering / heartbeat], [no music — only ambient dread].`

**Example:**
> *Slow push-in through candle-lit mansion hallway. Fog crawls along the stone floor. A single flickering candle illuminates ornate picture frames. At the far end of the corridor, a ghostly silhouette stands motionless. Cold desaturated palette, heavy shadows, high contrast. SFX: distant thunder, faint whisper, floorboard creak. No music. VHS grain texture.*[^18]

**Horror vocabulary words to include:** *moonlit, cursed, flickering, whispers, abandoned, ritual, fog, VHS grain, unnatural stillness, eerie silence*[^18]

### 7.3 Film Noir

**Key visual elements:** Chiaroscuro, rain-soaked streets, venetian blind shadows, cigarette smoke, black & white or muted[^25][^22]

**Example:**
> *Film noir tracking shot down a rain-soaked city street at night. A mysterious figure in a long trenchcoat walks through pools of streetlight, hat pulled low. Dramatic shadows cut across wet cobblestones. Venetian blind shadow pattern on a brick wall. High contrast black and white with selective color — the red of a lit cigarette. SFX: distant jazz, rain on asphalt, slow footsteps. Ambient: foghorn in the distance.*[^25]

### 7.4 Science Fiction

**Key visual elements:** Scale, futuristic tech, neon, starfields, chrome, practical light sources[^21]

**Visual styles:** Cyberpunk (neon/rain), hard sci-fi (clinical/clean), space opera (vast scale), dystopia (worn/broken)

**Prompt template:**
> `[Wide establishing / aerial / extreme close-up on tech] [futuristic subject], [technological action], [environment: orbital station / megacity / alien terrain], [neon-saturated or clinical white palette], [anamorphic flares], [SFX: interface hum, thruster ignition, electronic voice], [score: dark synth or orchestral].`

**Example:**
> *Wide shot of a lone astronaut in a worn EVA suit floating against a gas giant in deep space. Stars slowly rotate as the planet's storm systems churn below. Photorealistic rendering, lens flare from distant sun, sharp focus on suit texture — scratches, dust, patch insignia. Cold, clinical palette. SFX: breathing inside helmet, distant ship radio crackle, suit pressurization hiss. Ambient: vast cosmic silence.*

### 7.5 Western

**Key visual elements:** Dusty landscapes, golden hour, rugged textures, wide establishing shots, slow builds[^31]

**Example:**
> *Low-angle wide shot of a lone gunfighter silhouetted against a burning sunset over a dusty canyon. Camera slowly tilts up. Cracked dry earth in foreground. Wind moves their long duster coat. Warm sepia-amber color grade, slight 35mm grain. SFX: distant wind, spur jingle, hawk cry. Ambient: desolate silence except wind. Music: sparse acoustic guitar motif.*

### 7.6 Romance & Drama

**Key visual elements:** Soft light, shallow DOF, intimate framing, warm tones, human detail[^20]

**Example:**
> *Medium close-up of two people facing each other on a rain-covered café terrace at dusk. Warm window light from inside spills onto their faces. One reaches slowly for the other's hand. Shallow depth of field, soft focus on background rain. Warm amber and soft green palette. Airy, gentle composition. SFX: soft rain on umbrella, distant piano from inside, traffic hum. No music — only ambient warmth.*

### 7.7 Fantasy & Epic Adventure

**Key visual elements:** Vast landscapes, magical lighting, creature and world detail, crane shots for scale[^1]

**Example:**
> *Crane shot starting low on a lone hiker and ascending high above, revealing they are standing on the edge of a colossal mist-filled canyon at sunrise. Crystalline waterfalls pour from cliff faces. Epic fantasy style, awe-inspiring, soft morning golden light. SFX: swelling orchestral score beginning as the canyon is revealed, distant eagle cry, wind. Deep focus across entire landscape.*[^1]

### 7.8 Documentary & Realism

**Key visual elements:** Handheld camera, natural light, observational framing, authentic texture[^20]

**Example:**
> *Handheld medium shot following a fish market vendor at dawn, moving through crowded aisles. Natural overhead fluorescent and open-sky light mixing. Slight camera shake from movement. Documentary aesthetic, 16mm grain feel, desaturated realistic palette. SFX: shouted prices, ice scooping, fish hitting stainless steel. Ambient: crowded market drone. No color grade — raw look.*

### 7.9 Animation Styles

| Style | Core Prompt Language |
|---|---|
| **Anime** | "anime style, cel-shaded, dynamic action lines, vivid color contrast, Ghibli-influenced lighting"[^32] |
| **Pixar 3D** | "Pixar-style 3D animation, soft warm volumetric lighting, expressive character design"[^17] |
| **Stop Motion** | "stop motion animation, visible material texture, deliberate frame rate, miniature set"[^28] |
| **Claymation** | "claymation style, handmade fingerprint texture, matte clay surfaces, warm character colors"[^28] |
| **2D / Flat** | "flat 2D animation, bold black outlines, graphic novel aesthetic, high contrast palette" |
| **Watercolor** | "watercolor animation, flowing washes, soft bleed edges, hand-painted texture" |

### 7.10 Music Video & Commercial

**Key visual elements:** High-energy editing rhythm, vibrant color, stylized lighting, product/performer focus[^20]

**Example (Music Video):**
> *Wide shot inside an empty industrial warehouse transformed into a concert space. LED strips pulse in time with the beat. A solo performer dances with total abandon, camera tracking around them in a smooth arc. Vibrant saturated palette, lens flares from stage lights, slight motion blur on fast moves. SFX: pounding bass, crowd energy without crowd, speaker crackle. Music: pounding electronic beat, no lyrics.*

**Example (Product Commercial):**
> *Close-up product video of a premium glass perfume bottle on a white marble surface, soft morning light from the left. Camera performs a slow 360° orbit. Shallow depth of field, bokeh background. No voiceover. SFX: subtle glass clink at the start, quiet studio room tone. No music. Clean, luxury aesthetic.*[^14]

***

## Part 8: Advanced Creative Workflows

### 8.1 Workflow: First & Last Frame (Frame Interpolation)

Veo 3.1's most powerful advanced feature — define exactly where the shot starts and exactly where it ends, and the model generates the cinematic motion in between.[^33][^4]

**Step 1 – Create the Starting Frame**
Generate a still image using Gemini 2.5 Flash Image (Nano Banana) or upload any photo. Define composition, lighting, and subject position precisely.

**Step 2 – Create the Ending Frame**
Generate a second image showing where the camera or scene should arrive. This can be a different angle, zoom level, emotional moment, or even a different location (for surreal transitions).

**Step 3 – Animate with Veo 3.1**
Upload both images via the First and Last Frame feature. Write a prompt focused entirely on the **motion and audio** that connects them:[^34]

```
Do NOT redescribe the visuals — they are already defined by the frames.
Direct: what camera movement happens, what audio plays, what action occurs mid-transition.
```

**Example prompt for interpolation:**
> *The camera performs a smooth 180-degree arc shot, starting on the singer's front-facing close-up and circling around to arrive at a wide POV from behind her on stage. Audio: crowd erupts in sustained applause, live concert ambience, acoustic reverb of the venue.*[^1]

**Use cases:**
- Scene transitions between two visual ideas
- Before/after transformations
- Character entering a new environment
- Revealing scale (from intimate close-up to wide shot)
- Dream sequences and surreal morphs

### 8.2 Workflow: Ingredients to Video (Reference Image System)

Provide up to 4 reference images as "ingredients" — characters, environments, objects, or style references — and Veo 3.1 uses them as visual anchors for identity and aesthetic consistency across the generated clip.[^35][^9]

**The four ingredient types:**[^26]

| Ingredient Type | What to Provide | What It Controls |
|---|---|---|
| **Subject/Character** | Reference photo or generated portrait | Face identity, costume, hairstyle — prevents character drift |
| **Environment/Setting** | Reference image of the location | Scene architecture, lighting setup, background composition |
| **Object** | Reference image of a specific prop | Object shape, color, material accuracy |
| **Style/Texture** | Reference image of a visual aesthetic | Color grade, film grain, artistic style consistency |

**Prompt strategy with Ingredients:**
When using reference images, your text prompt should focus only on:
- What the subject **does** (action)
- How the **camera** moves
- What **audio** plays
- Any **differences** from the ingredient image

Do not redescribe what is already visible in the ingredient images.[^34]

**Example multi-ingredient prompt:**
> *Using the provided images for the detective character, the woman in the dark dress, and the noir office setting: Create a medium shot of the detective behind his desk. He looks up at the woman and says in a weary voice, "Of all the offices in this town, you had to walk into mine." Dramatic low-key lighting from the desk lamp. SFX: rain on windows, distant jazz.*[^1]

### 8.3 Workflow: Timestamp Prompting (Multi-Shot Sequence)

Direct a complete multi-shot sequence with precise cinematic pacing within a single generation by assigning timed segments. Note: this is treated as a prompting convention — verify support in your specific endpoint's documentation.[^36][^12][^1]

**Format:**

```
[00:00-00:02] Shot type, subject/action description. SFX/Audio cue.
[00:02-00:04] Shot type, subject/action description. SFX/Audio cue.
[00:04-00:06] Shot type, subject/action description. SFX/Audio cue.
[00:06-00:08] Shot type, subject/action description. SFX/Audio cue.
```

**Full example (exploration scene):**

```
[00:00-00:02] Medium shot from behind a young female explorer in a leather satchel and ponytail, pushing aside jungle vines to reveal a hidden path.
[00:02-00:04] Reverse shot of her freckled face filled with awe, ancient moss-covered ruins visible in the background. SFX: rustle of dense leaves, distant exotic bird calls.
[00:04-00:06] Tracking shot following her as she runs her hand over intricate carvings on a crumbling stone wall. Emotion: wonder and reverence.
[00:06-00:08] Wide high-angle crane shot revealing the lone explorer standing small at the center of a vast forgotten temple complex, half-swallowed by the jungle. SFX: a swelling, gentle orchestral score begins.
```


### 8.4 Workflow: Scene Extension

Veo 3.1's Scene Extension technology maintains visual coherence across multiple connected segments, enabling continuous narratives exceeding 60 seconds while preserving character consistency and environmental continuity. Generate clip A, then use its final frame as the first frame of clip B, chaining shots together with shared visual anchors.[^11]

***

## Part 9: Negative Prompting & Constraint Language

Veo 3.1 responds better to **positive constraints** than simple "no X" instructions. Rather than listing banned words, describe the desired scene in a way that implicitly excludes unwanted elements.[^30][^1]

### 9.1 The Constraint Formula

```
Main creative prompt + targeted constraint + revision note
```

| Problem | Weak Negative Prompt | Strong Constraint Language |
|---|---|---|
| Random text on signs/clothing | "no text" | "keep all signage and clothing surfaces clean without readable words" |
| Character face drift | "no face change" | "maintain the same face shape, hairstyle, and outfit color throughout the entire shot" |
| Physics errors (floating, teleporting) | "no weird physics" | "keep all motion physically plausible; objects move only with realistic force and momentum" |
| Background clutter | "simple background" | "keep the background uncluttered with a single clear subject, minimal props" |
| Wrong audio mood | "no music" | "no background music; only natural room tone; leave audio space for voiceover in editing" |
| Too much camera shake | "stable camera" | "smooth, professionally controlled camera movement; avoid unintentional shake" |

### 9.2 Limit Negative Constraints

Never use more than 3 negative constraints in a single prompt. Pick the three failure modes that would make the clip unusable, and ignore the rest. Over-constraining creates noisy, conflicting instructions.[^30]

***

## Part 10: Prompt Engineering Best Practices

### 10.1 Writing Principles

1. **Write like a director, not a search engine.** Use present tense, active verbs, vivid nouns. Think of it as a storyboard note or shot list entry.[^19][^31]
2. **One clear action per clip.** Veo 3.1 excels at single-shot sequences. Avoid asking for complex narrative arcs in a single 8-second clip.[^31]
3. **Specify what you want, not what you don't want.** Positive descriptions produce more stable output than long exclusion lists.[^16][^30]
4. **Plan audio from the beginning** — not as an afterthought. Treat the audio layer as a parallel screenplay.[^14]
5. **Use specific rather than generic language.** "A vintage red convertible muscle car driving fast along a winding coastal highway at sunset, ocean waves crashing below" vs. "a car driving".[^16]
6. **100–200 words is optimal** for a single-clip prompt.[^15]
7. **Test, iterate, refine.** Start with a base prompt, identify the specific element that's failing, and adjust that element in isolation.[^30]

### 10.2 The JASON Method (Advanced Framework)

For maximum prompt adherence in complex productions, use a structured JSON-style decomposition:[^7]

```json
{
  "shot": "medium close-up",
  "camera_movement": "slow dolly-in",
  "subject": "worn leather jacket, 30s man, stubble, piercing grey eyes",
  "action": "glances left, then directly into camera",
  "environment": "rain-soaked bus shelter, night, neon sign glow",
  "lighting": "motivated neon red-blue split light, deep shadows",
  "lens": "shallow depth of field, 85mm portrait look",
  "color_grade": "desaturated, blue-cyan cool palette",
  "texture": "35mm grain, slight diffusion",
  "audio_dialogue": "He says quietly: 'They were right about everything.'",
  "audio_sfx": "rain on roof, bus driving past, distant music",
  "audio_ambient": "wet street ambience, low volume",
  "negative": "no camera shake, keep face consistent, no random text"
}
```

Then convert this JSON to flowing prompt language before submitting.

### 10.3 Prompt Enhancement with Gemini

If a prompt feels underdeveloped, ask Gemini to analyze and enrich it with more cinematic and descriptive language before sending to Veo. This two-step approach leverages Gemini's language capabilities as a creative director's assistant.[^1]

***

## Part 11: Complete Prompt Reference Library

### 11.1 Action

> *Fast handheld tracking shot following a motorcycle through downtown Hong Kong at night, weaving through neon-lit traffic. Rain on the lens, motion blur, tires spraying water. Low-angle perspective. Teal-orange grade, anamorphic flares. SFX: screaming engine, honking horns, tire spray. Score: driving electronic pulse.*

### 11.2 Horror

> *POV walking slowly through an abandoned carnival at night. Creaking ferris wheel above. Faint children's laughter in the distance that stops suddenly. Fog thickens. A shadow crosses in front of the camera. VHS grain texture, washed-out desaturated palette, heavy shadow. SFX: creak, wind, sudden silence. No music.*[^18]

### 11.3 Film Noir

> *Film noir tracking shot down a rain-soaked city street at night. Mysterious figure in a long coat and hat walks through pools of streetlight. Dramatic shadows, venetian blind light pattern on a brick wall. High contrast black and white with selective color on a lit cigarette tip. SFX: distant jazz piano, rain on asphalt, measured footsteps. Ambient: foghorn.*[^25]

### 11.4 Sci-Fi (Space Opera)

> *Wide establishing shot of a massive battle cruiser emerging from hyperspace above a ringed gas giant. Star fields rotate slowly. Explosions of blue-white light along the ship's hull. Epic orchestral score builds. SFX: deep resonant hyperspace exit, ion thrusters, hull stress. Photorealistic CGI, anamorphic widescreen, 4K detail. Cold blue-steel color palette.*

### 11.5 Fantasy

> *Crane shot beginning low on a cloaked sorceress standing in a moonlit forest clearing, rising high to reveal an enormous ruined temple behind her covered in glowing ancient runes. Mist swirls between the trees. Epic fantasy, warm magical golden light contrasting cool moonlight, shallow depth of field on the sorceress, deep focus on the ruins. SFX: gentle chanting, crackling magical energy, distant owl. Score: sweeping strings.*

### 11.6 Western

> *Low-angle extreme wide shot of a lone rider on horseback cresting a ridge at golden hour, silhouetted against a burning sun setting over mesa country. Wind moves the rider's coat. Warm amber-sepia grade, slight 35mm grain. SFX: distant wind, horse breath, spur jingle. Music: sparse, melancholic acoustic guitar. Silence carries weight.*

### 11.7 Romance

> *Soft medium shot of two people sharing an umbrella at a night market, surrounded by warm lantern light. They lean close, studying each other's faces. Shallow depth of field on their expressions, bokeh of distant lights. Warm amber-gold palette, gentle glow. SFX: raindrops on umbrella, distant market sounds, soft music box melody. Intimate, quiet.*

### 11.8 Documentary

> *Handheld medium shot following a solo climber ascending a rocky face at dawn. Natural golden-hour light from the east. Documentary 16mm grain, no color grade — raw, honest. The camera breathes with slight movement. SFX: wind, gloves scraping rock, labored breath. Ambient: high-altitude silence. No music.*

### 11.9 Psychological Thriller

> *Locked-off medium shot of a person sitting motionless at a dining table in an empty house at 3AM. All lights are off except a single kitchen bulb. They stare at the phone on the table. Camera does not move. Dutch angle, barely perceptible. Desaturated cold palette. SFX: refrigerator hum, distant ticking clock, their breathing. Music: barely audible low drone that slowly rises.*

### 11.10 Period Drama

> *Medium shot of a Victorian woman reading a letter by candlelight in a cluttered drawing room. The candle flame flickers. Her expression shifts from hope to grief. Warm candlelight key, deep shadows, cool background. Shallow depth of field. Shot as if on 35mm film, warm grain. SFX: crackling fire, rain on window, paper rustling. No score — only ambient.*

***

## Part 12: Model Feature Quick Reference

| Feature | How to Use It | Prompt Focus |
|---|---|---|
| **Text-to-Video** | Text prompt only | Full 5-part formula |
| **Image-to-Video** | Upload reference image + text | Focus only on motion and audio[^34] |
| **First & Last Frame** | Two images + Veo API config | Describe the connecting motion and audio[^10] |
| **Ingredients to Video** | Up to 4 reference images | Action, camera, audio; skip redescribing images[^35] |
| **Scene Extension** | Generate then chain clips | Match lighting, palette, camera vocabulary between shots[^36] |
| **Add/Remove Object** | Existing video + instruction | Describe object and placement; note: uses Veo 2, no audio[^1] |
| **Timestamp Prompting** | Single prompt with [MM:SS] blocks | Each block = shot type + action + audio[^1] |

***

## Part 13: Common Mistakes & How to Fix Them

| Mistake | Why It Happens | Fix |
|---|---|---|
| Random text on backgrounds | Model fills negative space | "keep all signage clean and unreadable" |
| Character changes appearance mid-clip | Insufficient identity anchors | Use Ingredients to Video + describe identity in detail per shot |
| Unintended background music | Default audio behavior | "no background music; natural room tone only"[^37] |
| Camera movement ignores instructions | Too many competing instructions | Reduce to one camera instruction; make it the first element |
| Poor lip sync | Line too long for clip duration | Use max one sentence; specify "natural lip sync to the exact quoted line" |
| Physics errors (floating objects) | Complex motion description | Simplify; "keep motion physically plausible and grounded" |
| Over-generic output | Vague prompt language | Replace generic nouns with specific, visual ones |
| Conflicting style instructions | Mixed aesthetic signals | Choose one film reference or aesthetic; commit fully |

***

*Sources: Google Cloud Blog Veo 3.1 Ultimate Prompting Guide, Google Gemini API Video Documentation, Google DeepMind Veo Prompt Guide, Google Blog Veo 3.1 Ingredients to Video Update, Google Blog Veo 3.1 Lite Developer Release, Veo 3.1 Lite on Vertex AI, Native Audio Prompt Guide 2026, FAL.ai Veo 3.1 Release, Veo 3.1 4K Update Analysis, AI Films Google Veo 3.1 Guide, Atlabs Veo 3.1 Prompting Guide, LTX Studio Veo 3.1 Prompt Guide, Veo 3 Negative Prompt Guide, Skywork.ai Cinematic Presets, Veo 3.1 First Last Frame Fast Model, Veo 3.1 Ingredients Feature Overview.*[^3][^28][^38][^4][^2][^12][^33][^6][^35][^9][^34][^10][^11][^30][^14][^1]

---

## References

1. [Ultimate prompting guide for Veo 3.1 | Google Cloud Blog](https://cloud.google.com/blog/products/ai-machine-learning/ultimate-prompting-guide-for-veo-3-1) - This guide is a framework for directing Veo 3.1, our latest model. Veo 3.1 is state-of-the-art and b...

2. [How developers can use Veo 3.1 Lite for AI video generation](https://blog.google/innovation-and-ai/technology/ai/veo-3-1-lite/) - # Build with Veo 3.1 Lite, our most cost-effective video generation model

Mar 31, 2026

Our most co...

3. [Veo 3.1 Lite and a new Veo upscaling capability on Vertex AI](https://cloud.google.com/blog/products/ai-machine-learning/veo-3-1-lite-and-a-new-veo-upscaling-capability-on-vertex-ai) - Veo 3.1 Fast: This option delivers faster video generation while maintaining high quality, making it...

4. [VEO 3.1 is now available on fal](https://blog.fal.ai/veo-3-1-is-now-available-on-fal/) - Veo 3.1 introduces frame interpolation, allowing users to define and transition smoothly between the...

5. [Veo 3.1 Lite - Google's Fastest AI Video Model](https://www.imagine.art/apps/veo-3.1-lite) - Create realistic AI videos with Veo 3.1 Lite. Turn prompts into high-quality cinematic video outputs...

6. [Google Veo 3.1 4K Update Brings Professional-Grade ...](https://wavespeed.ai/blog/posts/google-veo-3-1-4k-update-brings-professional-grade-ai-video-generation/) - The headline feature of Veo 3.1 is 4K resolution output at 3840x2160 pixels. This makes Veo 3.1 the ...

7. [Veo 3.1 Prompting Guide Development | PDF | Camera Lens](https://www.scribd.com/document/950228154/Veo-3-1-Prompting-Guide-Development) - film grain Adds a textural, analog feel. to the video, mimicking the look of traditional film stock....

8. [Veo 3.1 Lite — Google's Most Affordable AI Video Generator](https://www.vo3ai.com/veo3-1-lite) - Unlike the flagship Veo 3.1 which targets 4K cinema-grade output, Veo 3.1 Lite focuses on HD (720p) ...

9. [Veo 3.1 Ingredients to Video: More consistency, creativity ...](https://blog.google/innovation-and-ai/technology/ai/veo-3-1-ingredients-to-video/) - Turn images into expressive videos with richer dialogue and consistent characters ... our capability...

10. [Generate videos with Veo 3.1 in Gemini API](https://ai.google.dev/gemini-api/docs/video) - Veo 3.1 lets you create videos using interpolation, or specifying the first and last frames of the v...

11. [Google Veo 3.1 4K Guide: Master the "Ingredients to Video...](https://studio.aifilms.ai/blog/google-veo-31-official-release-january-2026) - First, state-of-the-art AI upscaling to 4K resolution that reconstructs fine textures rather than si...

12. [The ultimate prompting guide for Veo 3.1](https://www.atlabs.ai/blog/the-ultimate-prompting-guide-for-veo-3-1) - Direct cinematic shots and audio with professional film techniques ... Cinematography: Specify the f...

13. [Mastering Veo 3.1: 7 Secrets to Writing Better AI Prompts](https://www.glbgpt.com/hub/mastering-veo-3-1-7-secrets-to-writing-better-ai-prompts/) - To write better AI prompts for Veo 3.1, you must use a structured, directorial formula: [Cinematogra...

14. [Veo 3 Native Audio Prompt Guide 2026: Dialogue, SFX, and Lip Sync](https://www.veo3ai.io/blog/veo-3-native-audio-prompt-guide-2026) - A practical Veo 3 native audio prompt workflow for dialogue, SFX, ambience, and lip sync in short AI...

15. [Veo 3 Prompts - Video Generation Guide](https://www.veed.io/learn/veo-3-prompts) - Effective Veo 3 prompts follow a 5-component structure: subject & action, setting & environment, cam...

16. [Google launched Veo 3. Here's how to best prompt it: 1. Be ...](https://www.linkedin.com/posts/how-to-prompt_breaking-google-launched-veo-3-heres-activity-7331680349959131138-jBd9) - Be Clear, Concise, and Descriptive: Specificity is Paramount: Avoid vague language. Clearly describe...

17. [The Ultimate Veo 3.1 Prompt Guide](https://www.dreamhost.com/blog/veo-3-1-prompt-guide/) - Master Veo 3.1 prompting with this complete guide. Learn the exact prompt formulas, techniques, and ...

18. [Lights, Camera… SCREAM! Veo 3.1 Halloween Prompt ...](https://videoweb.ai/blog/detail/Lights-Camera-SCREAM-Veo-3-1-Halloween-Prompt-Spellbook-53eebd7eca1b/) - Create cinematic Halloween AI videos with Veo 3.1 using these ready-to-use spooky prompts, scene tem...

19. [Veo 3 Prompt Guide – Tips & Examples](https://leonardo.ai/news/mastering-prompts-for-veo-3/) - Veo tends to respond well to prompts that read like visual direction—simple, image-focused, and writ...

20. [Veo 3 Video Prompt Examples and Best Practices](https://www.powtoon.com/blog/veo-3-video-prompt-examples/) - Explore Veo 3 video prompt examples that actually work. Structure prompts, control style, and get be...

21. [Veo 3.1 Prompt Guide](https://www.imagine.art/blogs/veo-3-1-prompt-guide) - Explore 25 ready-to-use Veo 3.1 prompts to create high-quality AI videos. Copy proven prompt structu...

22. [snubroot/Veo-3-Prompting-Guide](https://github.com/snubroot/Veo-3-Prompting-Guide) - Example: POV vlog-style footage in 4K, realistic cinematic look. A large, furry Yeti holds a camera ...

23. [Moody Film Color Grading LUT Filter Pack for Cinematic Visuals](https://filmora.wondershare.com/video-creative-tips/moody-film-color-grading-lut-filter-pack.html) - This moody film color grading LUT-inspired filter collection is designed for content creators who wa...

24. [Free VEO 3.1 Prompt Consistency Tool: AI Video Stability](https://hrlimon.com/tools/veo-prompt-consistency) - Master Free VEO 3.1 Prompt Consistency for cinematic AI videos. Use our tool to maintain character a...

25. [Best Google Veo 3 Prompt Examples and Templates](https://ulazai.com/veo3-prompt-examples/) - Copy tested Google Veo 3 prompt examples, templates, and best practices for cinematic trailers, prod...

26. [How to Use Veo 3.1 Ingredients to Video](https://www.atlascloud.ai/blog/guides/how-to-use-veo-3-1-ingredients-to-video-transforming-static-photos-into-cinematic-ai-clips) - Style/Texture Image: This set the visual look, from 35mm film grain to specific color sets. It makes...

27. [I have a few hours to kill. Send me your Veo 3 prompts and ...](https://www.reddit.com/r/singularity/comments/1kwwh5f/i_have_a_few_hours_to_kill_send_me_your_veo_3/) - Two masked figures, dressed in fedoras and trench coats, are holding a bewildered bank manager at gu...

28. [How to create effective prompts with Veo 3](https://deepmind.google/models/veo/prompt-guide/) - Start your prompt by defining the sort of video you want to create. Is it realistic, animated, stop-...

29. [Can Veo 3.1 do audio? and how should you use it professionally?](https://www.cometapi.com/can-veo-3-1-do-audio-and-how-should-you-use-it-professionally/) - Example prompts (copy-paste ready). 1 — Natural-sounding ambient + effect + short dialogue. Prompt: ...

30. [Veo 3 Negative Prompt Guide: Fix Common AI Video ...](https://www.veo3ai.io/blog/veo-3-negative-prompt-guide-2026) - Learn how to write Veo 3 negative prompts and constraint language to fix random text, camera chaos, ...

31. [Veo 3 Prompting Best Practices Guide | PDF | Camera](https://www.scribd.com/document/873395256/veo-3-best-practices) - Use this doc as the backbone for your custom GPT's system prompt. Focus on clarity, single-shot prom...

32. [How I Made an Anime Movie with AI (Sora 2 & Veo 3.1 Full Workflow)](https://www.youtube.com/watch?v=dRTz0O1LClc) - ... animation, test both video models side-by-side, and look at how each one handles action, dialogu...

33. [veo3.1-first-last-frame-to-video-fast](https://www.eachlabs.ai/google/veo3-1/veo3-1-first-last-frame-to-video-fast) - It is designed for workflows requiring rapid turnaround on frame interpolation while maintaining acc...

34. [Veo 3.1 Prompt Guide](https://ltx.studio/blog/veo-prompt-guide) - This guide shows you how to structure Veo 3.1 prompts that deliver precise, production-ready video c...

35. [Veo 3.1 Ingredients to Video | Consistent Character AI Video](https://www.vo3ai.com/veo3-ingredients) - Veo 3.1 Ingredients to Video lets you generate video using "ingredient images" as visual references....

36. [Veo 3.1 Multi-Prompt Storytelling Best Practices (2025)](https://skywork.ai/blog/multi-prompt-multi-shot-consistency-veo-3-1-best-practices/) - Provide sparse ambience and motif guidance: “Soft rain and distant traffic; subtle synth motif at lo...

37. [Nearly all my recent Veo 3.1 videos have ridiculous background music](https://www.reddit.com/r/Bard/comments/1odpnvy/nearly_all_my_recent_veo_31_videos_have/) - And if they have dialog, it turns dialog into a song. I have tried negative prompting "Audio: NO bac...

38. [Veo 3.1 Cinematic Presets: Best Practices for Fast Visual ...](https://skywork.ai/blog/veo-3-1-cinematic-presets-best-practices-storytelling/) - Composition: “close-up, eye-level, subject framed with shallow depth of field” · Camera: “gentle dol...

