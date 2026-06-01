# Grok Imagine — Professional Daily Reference Card
> Companion to `grok-imagine-research.md` · May 2026  
> **This card is for daily use** — cut out sections, paste into your workflow

---

## 1. Quick Start Checklist — 12 Things Every Prompt Needs

Before you generate, confirm:

- [ ] **1. Subject first** — First sentence names exactly what the image is of
- [ ] **2. Scene, not just subject** — Environment, time of day, or context described
- [ ] **3. Light source named** — Not "good lighting" — a specific source, direction, and quality
- [ ] **4. Camera reference** — At least one camera body, lens, or focal length
- [ ] **5. Color direction** — A film stock, grade name, or palette description
- [ ] **6. Mood stated** — How the viewer should feel, not just what they see
- [ ] **7. Natural language sentences** — Not a tag list
- [ ] **8. 40–80 words total** — Count before generating
- [ ] **9. Subject is front-weighted** — Subject in sentence 1, style at the end
- [ ] **10. No negative prompts** — Rewrite exclusions as positive ("calm sea" not "no waves")
- [ ] **11. No quality filler** — Delete "stunning", "8K", "masterpiece", "ultra-detailed"
- [ ] **12. Aspect ratio correct** — Match to your delivery platform before generating

---

## 2. The Universal Grok Imagine Prompt Template

```
[SUBJECT + PHYSICAL DESCRIPTION + ACTION/POSE].
[ENVIRONMENT/SETTING — location, time of day, season].
[LIGHTING — source, direction, quality, modifiers].
[MOOD — how it should feel to the viewer].
[CAMERA — body/format, lens, aperture, depth of field].
[COLOR — film stock, grade, or palette].
[STYLE REFERENCE — genre, photographer, publication, art movement — 1 only].
```

### Filled Example:

```
A master glassblower, Italian male, 60s, gathering molten glass from a furnace in a Venice workshop, leather apron showing burn marks.
Interior workshop at dusk, furnace glow providing the only light source, orange and amber tones.
Available light only — warm backlight from furnace rimming his silhouette, no studio setup.
Documentary intimacy — the weight of a lifetime of craft visible in his hands and posture.
Sony A7R V with 35mm f/2, slightly underexposed, handheld.
Kodak Portra 800, warm and filmic, grain visible.
Documentary photography tradition, Magnum Photos quality.
```

---

## 3. Top 30 Power Phrases That Consistently Elevate Output

### Camera & Lens
1. `shot on Hasselblad H6D with 80mm f/2.8` — medium format clarity signal
2. `85mm f/1.4, shallow depth of field, background bokeh` — portrait lens standard
3. `400mm telephoto compression, background brought close` — wildlife/sports
4. `24mm tilt-shift, verticals perfectly corrected` — architecture
5. `35mm f/2 Leica rendering, documentary quality` — street, candid

### Lighting
6. `Rembrandt lighting, triangular shadow on cheek` — dramatic portrait
7. `single large softbox from camera-left, soft wrapped light` — clean studio
8. `golden hour, warm low sun, long diagonal shadows` — outdoor warmth
9. `Vermeer northern window light, soft directional daylight` — naturalistic interior
10. `Cinestill 800T halation around practical lights` — moody night city

### Color & Film
11. `Kodak Portra 400, warm skin tones, lifted blacks` — wedding/lifestyle warmth
12. `Fujifilm Velvia 50, hyperaturated greens and reds` — landscape punch
13. `Ilford HP5 pushed to 1600, coarse grain, deep blacks` — street B&W
14. `teal and orange color grade, complementary split` — cinematic commercial
15. `bleach bypass, desaturated, high contrast, silver retention` — film noir

### Mood & Atmosphere
16. `morning mist, soft depth layers, reduced contrast` — atmospheric landscape
17. `volumetric god rays through smoke, light beams visible` — dramatic atmosphere
18. `chiaroscuro shadows, low-key, small light source` — dramatic fine art
19. `rain-soaked streets, reflections of neon in puddles` — night city atmosphere
20. `overcast flat light, even fill, no shadows, maximum texture` — documentary

### Style Anchors
21. `editorial fashion, Vogue Italia aesthetic, intentional and conceptual`
22. `photojournalism style, AP wire quality, authentic moment`
23. `Dutch Golden Age still life, chiaroscuro, dark oak table` — still life
24. `Wes Anderson symmetrical framing, pastel palette, centered` — quirky narrative
25. `Studio Ghibli 1990s production painting, handpainted, warm` — animation

### Technical Quality Signals
26. `visible pores, peach fuzz catching sidelight, SSS in skin` — skin realism
27. `individual strand detail, fine flyaways catching rim light` — hair realism
28. `fabric weave visible at surface, natural drape and weight` — textile realism
29. `condensation on glass, water surface tension, refraction` — liquid/glass realism
30. `environmental portrait, candid not posed, authentic working moment` — documentary

---

## 4. Decision Tree: Desired Result → Recommended Approach

```
What do you primarily need?

├── PHOTOREALISTIC IMAGE
│   ├── Portrait → Add: camera + lens + specific lighting setup + skin description
│   ├── Product → Add: surface + single light source + angle + no props
│   ├── Landscape → Add: specific location + time of day + f/16 hyperfocal
│   └── Food → Add: vessel + surface + light direction + color grade

├── STYLIZED / ILLUSTRATED IMAGE
│   ├── Anime → Add: studio era + handpainted vs digital + color palette
│   ├── Oil painting → Add: art historical period + specific painter or movement
│   ├── Comic/graphic novel → Add: specific inker style + panel framing
│   └── Concept art → Add: production context + style artist references

├── CINEMATIC IMAGE
│   ├── Film still → Add: decade + genre + 2-3 film references + anamorphic if applicable
│   ├── Music video → Add: era + light quality + energy level
│   └── Commercial → Add: product context + brand tone word

├── TYPOGRAPHY IN IMAGE
│   ├── Simple sign/label → Enclose text in quotes, specify font mood
│   ├── Complex multi-line body copy → DON'T — add text in post
│   └── Logo exploration → Keep it abstract — exact logos are restricted

├── CHARACTER ACROSS MULTIPLE IMAGES
│   └── Use reference image workflow + multi-image editing API endpoint

└── VIDEO
    └── Add: subject + specific motion verb + camera movement + audio description
        Keep under 60 words for better motion stability
```

---

## 5. Cheat Sheet Tables

### Camera Format Signals

| Signal | What Aurora understands |
|---|---|
| Hasselblad H6D / Phase One IQ4 / GFX | Medium format: extreme detail, luxurious tonality |
| Leica M11 | Classic full-frame: Leica character rendering |
| Sony A1 / Canon R5 | Modern full-frame: clean professional |
| Fujifilm X-T5 | Film simulation aesthetic, APS-C field |
| Polaroid / Holga / disposable | Intentional lo-fi, imperfection, nostalgia |

### Focal Length Signals

| Focal length | Aurora's output tendency |
|---|---|
| 14–24mm | Environmental context, slight distortion |
| 35mm | Street, documentary, natural perspective |
| 50mm | Versatile, no distortion, commercial |
| 85mm | Classic portrait, flattering, compression |
| 135–200mm | Telephoto compression, subject isolation |
| 400mm+ | Wildlife, sports, extreme background compression |
| Macro | Extreme close-up, surface detail, abstraction |
| Tilt-shift | Architecture, corrected verticals |
| Anamorphic | Cinematic oval bokeh, horizontal flare |

### Lighting Quick Reference

| Setup | Best for | Key phrase |
|---|---|---|
| Rembrandt | Dramatic portrait, fine art | `Rembrandt lighting, triangular shadow` |
| Butterfly/Paramount | Glamour, beauty | `butterfly lighting, beauty dish` |
| Clamshell | Cosmetics, beauty | `clamshell, fill from below` |
| Split | Fashion, edgy editorial | `split lighting, half face in shadow` |
| Window (Vermeer) | Natural, painterly interior | `northern window light, soft directional` |
| Golden hour | Warm outdoor portrait | `golden hour, low sun, long shadows` |
| Blue hour | Architecture, mood | `blue hour, deep indigo sky, interior glow` |
| Film noir | Cinematic, detective, dramatic | `venetian blind shadows, single hard source` |

### Film Stock Quick Reference

| Stock | Tone | Best use |
|---|---|---|
| Kodak Portra 400 | Warm, pastel highlights | Portrait, wedding, lifestyle |
| Kodak Portra 800 | Warmer, slight grain | Low-light portrait |
| Fujifilm Pro 400H | Very pastel, cool highlights | Wedding, soft lifestyle |
| Fujifilm Velvia 50 | Hyper-saturated | Landscape, nature |
| Cinestill 800T | Warm, halation, night | Urban night, cinema feel |
| Kodak Tri-X 400 | Aggressive grain, deep blacks | Street, documentary B&W |
| Ilford HP5 | Versatile grain | Street, pushed B&W |
| Kodak Ektar 100 | Punchy primaries, crisp | Landscape, travel |

### Style / Genre Quick Reference

| I want | Prompt anchor phrase |
|---|---|
| Fashion editorial | `high fashion editorial, Vogue aesthetic, intentional` |
| Commercial clean | `commercial photography, clean studio, product context` |
| Street vérité | `street photography, Cartier-Bresson, decisive moment` |
| Documentary | `documentary photography, candid, Magnum quality` |
| Fine art | `fine art photography, gallery-ready, conceptual` |
| Cinematic | `cinematic film still, [decade] aesthetic` |
| Luxury advertising | `luxury advertising, communicates [heritage/sensuality/precision]` |
| Social-native | `[platform] aesthetic, not professionally lit, authentic` |

---

## 6. The 30 Use Cases At a Glance — One-Line Formula

| # | Use case | One-line formula |
|---|---|---|
| 1 | Editorial fashion portrait | Subject + garment specifics + location + editorial lighting + magazine reference |
| 2 | Beauty close-up | ECU + skin description + makeup + clamshell/beauty dish + Phase One/Hasselblad |
| 3 | Corporate headshot | MS + clean three-point + grey seamless + 85mm + "trustworthy, approachable" |
| 4 | Environmental portrait | Subject + occupation + location + available light only + documentary film stock |
| 5 | Street photography | Candid + specific city + available mixed light + 35mm + B&W film stock |
| 6 | Photojournalism | Wide shot + event context + f/8 deep focus + "AP wire quality, not art-directed" |
| 7 | Wedding & lifestyle | Couple + golden hour + garden/venue + 85mm f/1.8 + Pro 400H |
| 8 | Product hero shot | Product on white + single octabox + precise angle + "no props, no people" |
| 9 | Product lifestyle | Subject using product + real environment + 35mm f/2 + candid not posed |
| 10 | Food editorial | Dish with specific states + single window light + dark moody background + 85mm |
| 11 | Food social-native | Overhead flat-lay + specific props + bright airy light + 1:1 aspect ratio |
| 12 | Interior residential | No people + morning window light + tilt-shift corrected + specific aesthetic |
| 13 | Architecture exterior | Building at blue/golden hour + reflection pool + tilt-shift + no people |
| 14 | Landscape epic | Named location + dawn/dusk light split + hyperfocal f/16 + "monumental scale" |
| 15 | Landscape intimate | Specific detail + overcast light + single warm accent + quiet mood |
| 16 | Wildlife | Species + behavioral moment + telephoto 400mm+ + "genuine not staged" |
| 17 | Sports action | Athlete + peak moment + telephoto compression + "decisive frame" |
| 18 | Macro/detail | Subject + dawn sidelight + razor-thin DoF + grass-level angle |
| 19 | Astrophotography | Named location + Milky Way + dark skies + 14mm f/2.8 + ISO 6400 feel |
| 20 | Conceptual fine art | Subject + symbolic environment described spatially + "museum-wall worthy" |
| 21 | Still life | Objects with states + Dutch Golden Age lighting + dark background + 85mm macro |
| 22 | Fashion lookbook | Full-length + garment description + location with architecture + walking motion |
| 23 | Luxury advertising (watch) | Named product + wrist angle + 10:10 hands + snoot light on bezel + "quiet wealth" |
| 24 | UGC / social-native | 9:16 + candid self-shot feel + "not professionally lit" + VSCO-adjacent warm |
| 25 | Cinematic film still | Era + genre + dual practical light sources + film references + anamorphic |
| 26 | Anime illustration | Studio + era + handpainted quality + specific scene + emotion word |
| 27 | Western editorial illustration | Publication reference + visual metaphor described spatially + graphic composition |
| 28 | Concept art (character) | Character brief + occupation + armor/costume wear condition + game references |
| 29 | Concept art (environment) | Scale description + atmosphere + color palette + Syd Mead / concept art reference |
| 30 | Surreal / dreamscape | Realistic scene + single surreal juxtaposition + "unreality from juxtaposition only" |

---

## 7. Common Mistakes & Fixes

| Mistake | Result | Fix |
|---|---|---|
| Tag list instead of sentences | Generic, averaged output | Write natural language sentences |
| Subject buried at end of prompt | Wrong subject focus | Put subject in sentence 1 |
| "Stunning, breathtaking, 8K, masterpiece" | Wastes tokens, no improvement | Delete all quality adjectives; add actual visual description |
| No light source specified | Flat, uninspiring illumination | Name a light source, direction, and quality |
| Negative prompt used | Ignored in Grok Imagine | Rephrase as positive: "calm sea" not "no waves" |
| Multiple major style references | Style bleed, muddy output | Choose ONE style anchor |
| Prompt over 150 words | Key elements dropped | Cut to under 100 words; prioritize most important elements |
| Generic film/camera adjectives | No aesthetic impact | Use specific camera body and focal length names |
| No color direction | AI default oversaturated palette | Add film stock name or explicit palette |
| Requesting complex text in image | Garbled or misspelled | Enclose text in quotes; keep under 6 words; for critical text, add in post |
| Asking for hands doing complex gestures | Anatomy errors | Give hands a simple physical task or keep hands out of frame |
| Not checking `revised_prompt` | Wasting iteration cycles | Review API response field to see what Aurora actually used |

---

## 8. 20 Ready-to-Use Prompt Recipes

Copy, modify the [BRACKETED ELEMENTS], generate.

**R-01: Natural light portrait — outdoor golden hour**
```
[SUBJECT DESCRIPTION], standing in [ENVIRONMENT], golden hour, warm afternoon sun from camera-right casting long soft shadows. Shot on Sony A7R V with 85mm f/1.4, shallow depth of field. Skin: natural, healthy, warmly lit. Expression: [EMOTIONAL QUALITY]. Fujifilm Pro 400H color profile, pastel highlights.
```

**R-02: Studio fashion — high contrast**
```
High fashion editorial portrait. [SUBJECT IN DETAILED GARMENT], against black seamless. Split lighting: key light hard from camera-left, deep shadow right half of face. Rim light from behind separating figure from background. Shot Hasselblad H6D 80mm. B&W, Tri-X grain. Vogue Paris editorial aesthetic.
```

**R-03: Cinematic portrait — film still**
```
Cinematic film still, 1970s neo-noir aesthetic. [SUBJECT] in [LOCATION WITH PRACTICAL LIGHTS: diner/bar/phone booth]. Neon from [DIRECTION] painting face in [COLOR]. Single overhead fluorescent [OPPOSITE DIRECTION] in cold white. Anamorphic lens, oval bokeh from out-of-focus neon signs. Color: Kodak 5247 emulation. Mood: melancholy, solitary.
```

**R-04: Clean product hero — e-commerce**
```
Product photograph. [PRODUCT DESCRIPTION] on pure white background. Single large octabox from upper-left, soft shadow to lower-right grounding the product. [PRODUCT ANGLE — 35 degrees from horizontal, front face toward camera]. No props, no context, no hands. Shot with telephoto macro equivalent. Ultra-sharp throughout.
```

**R-05: Food — editorial moody**
```
Editorial food photograph. [DISH DESCRIPTION — include specific states like "jammy yolk", "matte glaze"]. Single directional window light from left, soft and golden. Plated on [VESSEL] on [DARK SURFACE]. Background dark, almost black. Shot 85mm macro, f/5.6. Color grade: deep, desaturated, intimate.
```

**R-06: Landscape — golden hour epic**
```
Epic landscape photograph, [NAMED LOCATION], dawn/dusk. [FOREGROUND ELEMENT] in the immediate foreground, [MIDGROUND WATER/FIELD], [MOUNTAIN/STRUCTURE] in background. Light catching [UPPER ELEMENTS] in warm rose-gold, shadows still blue-grey below. Shot 24mm f/16, hyperfocal, everything pin-sharp. Fujifilm Velvia 50 saturation.
```

**R-07: Street — candid night**
```
Street photograph, [CITY], 11pm. A [SUBJECT DESCRIPTION] moves through frame, slightly motion-blurred, surrounded by indistinct crowd. Mixed practical light: sodium streetlights above, neon shop signs from right. Shot on 28mm f/2, handheld, slight tilt acceptable. Cinestill 800T, halation around lit signs. Documentary vérité, Magnum quality.
```

**R-08: Interior lifestyle**
```
Architectural interior photograph. [ROOM TYPE AND STYLE: Japanese minimalist living space / Parisian apartment / Brooklyn loft]. Early morning light from [DIRECTION] window. [2-3 KEY OBJECTS AND SURFACES]. No people. Shot 24mm tilt-shift, perfectly corrected verticals, f/8, all sharp. Color: [WARM/COOL] natural light, no grade.
```

**R-09: Wildlife moment**
```
Wildlife photograph. [SPECIES] in the moment of [SPECIFIC BEHAVIOR]. Natural habitat: [ENVIRONMENT — specific season and time of day]. Shot on 400mm f/2.8, subject isolated against [BOKEH ENVIRONMENT]. Natural available light: [DIRECTION AND QUALITY]. Not staged — genuine behavioral moment. Color: [GRADE].
```

**R-10: Beauty close-up — natural**
```
Beauty close-up, MCU. [SUBJECT DEMOGRAPHICS AND SKIN DESCRIPTION]. Natural makeup — [SPECIFIC ELEMENTS: bold lip / barely-there / no makeup]. Soft butterfly lighting, large beauty dish above, white reflector below. Clean white background. Shot Phase One 100mm macro. Skin: natural texture preserved, pores visible, dewiness. Editorial level, not glossy.
```

**R-11: Concept art — hero character**
```
Character concept art, [FRANCHISE TYPE: fantasy RPG / sci-fi film / dark fantasy game]. [CHARACTER — gender, heritage, age]. [ARMOR/COSTUME DESCRIPTION — materials, wear condition, design]. [WEAPON/TOOL]. Three-quarter view, A-pose. Neutral grey concept art background. Warm directional light from upper-left. Expression: focused, calm. Reference: [2 GAME/FILM TITLES].
```

**R-12: Surrealist composition**
```
Surrealist photograph. A [PERSON DESCRIPTION] is [MUNDANE ACTION] in a [REALISTIC INTERIOR SETTING]. But [DESCRIBE THE SINGLE SURREAL ELEMENT — e.g., "the ceiling is the surface of an ocean, fish swimming above"]. The subject shows no reaction — treats it as ordinary. Photographic realism throughout. Cinestill 800T, 35mm perspective. Crewdson / Magritte tradition.
```

**R-13: Astrophotography**
```
Astrophotography landscape. Milky Way core arching over [SILHOUETTED FOREGROUND: standing stone / lighthouse / lone tree / mountain ridgeline], [NAMED LOCATION], [MONTH]. No light pollution. Horizon has faint blue-grey gradient from [MOON/SETTING SUN] below frame. 14mm f/2.8, ISO 6400 feel, slight grain organic. Star points sharp. Mood: solitary, vast.
```

**R-14: Documentary environmental portrait**
```
Documentary portrait of [SUBJECT + OCCUPATION], in [SPECIFIC WORKSPACE: forge / kitchen / library / studio / workshop]. They are mid-[TASK — specific action], not posed, not aware of camera. Available light from [NATURAL SOURCE: window/furnace/skylight]. Shot 35mm f/2, full-frame, handheld. [FILM STOCK]. The face should show [CHARACTER QUALITY: concentration / weathering / joy / authority].
```

**R-15: Fashion lookbook — full body**
```
Fashion lookbook photograph, full-length. [SUBJECT DEMOGRAPHICS] wearing [COMPLETE OUTFIT — every garment piece with fabric and color]. Location: [SPECIFIC ENVIRONMENT: arcade / bridge / industrial courtyard / cobblestone street]. Lighting: [OVERCAST DIFFUSE / GOLDEN HOUR SIDE / OPEN SHADE]. Walk in motion, one foot forward, slight energy. Shot 35mm f/2.8. Editorial tone.
```

**R-16: Anime / animated illustration**
```
Anime illustration, [STUDIO AND ERA: 1990s Studio Ghibli / 2000s Kyoto Animation / OVA series]. [CHARACTER: gender, age, appearance, clothing] in [SCENE WITH ATMOSPHERE: cliff overlooking sea of clouds / quiet forest shrine / rain-soaked rooftop]. Art style: [HANDPAINTED ANALOG / CLEAN DIGITAL / ROUGH SKETCH QUALITY]. Color palette: [PALETTE DESCRIPTION]. Mood: [WONDER/LONGING/DETERMINATION].
```

**R-17: Still life — Dutch master**
```
Still life, Dutch Golden Age tradition. On a dark oak table draped in [COLOR] velvet: [LIST 5-7 SPECIFIC OBJECTS WITH STATES — e.g., "half-peeled lemon, spiral of zest intact; a silver goblet with wine at half-fill; two cherries with stems touching"]. Single source light from upper-left, deep chiaroscuro shadows right. Shot 85mm macro, f/5.6. Color: dark, rich, shadows nearly black.
```

**R-18: Macro detail**
```
Extreme macro photograph. [SUBJECT: dewdrop / bee on flower / mineral crystal / water droplet on feather] at high magnification. Dawn sidelight from [LEFT/RIGHT], low angle, warm golden. DoF: razor-thin — only [SPECIFIC FOCAL POINT] in sharp focus; background [BOKEH COLOR: green / blue / golden] soft. Completely static. Shot from [GROUND/SURFACE] level looking across.
```

**R-19: Night urban atmosphere**
```
Night street photograph. [CITY AND NEIGHBORHOOD], midnight. [EMPTY OR SINGLE SUBJECT]. Rain-wet pavement reflecting [NEON COLORS: pink / amber / blue / mixed]. Practical lights from [STOREFRONTS / STREETLAMPS / SIGNS]. Shot 35mm f/1.8, moderate grain, ISO 3200 feel. Cinestill 800T, halation around sources. Mood: [MELANCHOLY / ELECTRIC / LONELY / INTIMATE].
```

**R-20: Luxury product — table-top advertising**
```
Luxury advertising photograph. [PRODUCT: watch / fragrance bottle / jewelry piece], on [SURFACE: polished marble / aged leather / mirror]. [SINGLE OR MINIMAL PROP: one rose petal / ink pen / relevant object]. Narrow snoot or gridded light from [DIRECTION] creating specular highlights along [PRODUCT EDGE/SURFACE], controlled. Background: deep black gradient. Shot with macro capability, product face sharp throughout. Communicates: [BRAND VALUE WORD].
```

---

## 9. Spicy Mode Quick Notes (Professional Context Only)

**What it is:** xAI's R-rated content tier. Elon Musk's stated standard: "If it's allowed in an R-rated movie, it's allowed in Grok Imagine." (March 12, 2026)

**Access requirements:**
- SuperGrok ($30/mo) or X Premium+ ($40/mo)
- iOS or Android app only (web = no Spicy Mode in most regions)
- 18+ age verification in profile
- Two toggles: Settings → Content Preferences → "Display sensitive media" AND Imagine Settings → "Allow sensitive media generation"

**Legitimate professional applications:**
- Lingerie/swimwear advertising foundation images
- Mature fashion editorial with intentional sensuality
- Fine art figure studies (within R-rated parameters)
- Cinematic atmosphere exceeding standard moderation limits

**Hard stops — nothing will get these through:**
- Explicit sexual acts
- Sexualized depictions of real/named people
- Anyone appearing under 18
- Non-consensual scenarios

**2026 policy reality:** Post-generation server-side scanning is active. Borderline outputs auto-blur. The policy has tightened significantly since August 2025. Do not build professional pipelines that depend on Spicy Mode for client-deliverable work without evaluating current policy.

---

## 10. Iteration Playbook

### The One-Variable Rule
Change exactly one thing per iteration. Never rewrite the whole prompt to fix one problem.

### Iteration Sequence
```
Generation 1: Base prompt (50–70 words)
Evaluate: Is the COMPOSITION right?
  Yes → Continue to Generation 2
  No → Fix composition only, regenerate

Generation 2: Same prompt + composition fix
Evaluate: Is the LIGHTING right?
  Yes → Continue to Generation 3  
  No → Fix lighting only, regenerate

Generation 3: Same prompt + composition + lighting
Evaluate: Is the COLOR TREATMENT right?
  Yes → Continue to fine detail
  No → Fix color/film stock only, regenerate

Generation 4+: Fine detail corrections (skin, hands, specific props)
```

### What to Check in `revised_prompt` (API)
- Is your key subject still named?
- Is your lighting setup still present?
- What did the rewriter ADD that you didn't want?
- What did the rewriter REMOVE?

Use this information to front-load important elements in your source prompt and pre-empt rewriter changes.

### When to Start Over
- Composition fundamentally wrong (wrong aspect ratio implied, wrong scene type)
- Wrong subject was generated (a city when you wanted a person)
- Style is completely wrong despite correct style instructions
- More than 3 unsuccessful iterations on the same element

---

## 11. Anti-Patterns — What Never to Do

### Prompt Anti-Patterns

❌ **The tag stack**
```
portrait woman, beautiful, cinematic, Rembrandt, bokeh, 8K, masterpiece, 
detailed, studio, professional, sharp, aesthetic, vibrant
```
Why it fails: Tag stacks produce averaged, generic, uninspired output.

---

❌ **The buried subject**
```
Cinematic, editorial, high fashion, Vogue quality, dramatic lighting, 
stunning and beautiful image of a woman.
```
Why it fails: Style words before subject. The subject gets minimal model attention.

---

❌ **Quality adjective spam**
```
Create an ultra-detailed, breathtakingly stunning, incredibly realistic, 
hyper-sharp, masterpiece-quality, 8K resolution, professional photograph of a cat.
```
Why it fails: These words consume tokens without providing visual information. Delete all of them.

---

❌ **The negative prompt (Grok Imagine doesn't support them)**
```
A portrait of a woman, no blemishes, no extra fingers, no blur, 
no bad lighting, no watermarks, not dark.
```
Why it fails: Aurora's consumer UI ignores negative instructions. Rewrite as positives.

---

❌ **The style collision**
```
A woman in a Baroque oil painting in cyberpunk style with Wes Anderson 
color in an anime illustration style.
```
Why it fails: Style bleed — all four styles average into visual confusion. Choose one.

---

❌ **The ultra-long prompt (over 150 words)**
```
[A 200-word prompt covering every conceivable detail of a portrait]
```
Why it fails: Aurora front-weights prompts. Elements in the second half receive low weight. The rewriter may drop them entirely. Shorter and targeted is better.

---

❌ **Asking for complex hands or text in the same shot**
```
A woman holding a detailed hand-written letter, legible cursive text 
visible, fingers clearly articulated, all rings individually detailed.
```
Why it fails: Two of Aurora's most persistent failure modes combined. Hands with specific fine motor positions + legible handwritten text = high probability of generation failure.

---

❌ **Relying on generic location names**
```
A beautiful city at night, nice lights, good atmosphere.
```
Why it fails: "Beautiful city" gives Aurora no specific visual reference. Name a city, a neighborhood, or a specific architectural type.

---

❌ **The "make it better" iteration**
```
First generation: [detailed prompt]
Iteration: Make it look better and more professional.
```
Why it fails: Aurora has no understanding of what "better" means without a specific direction. State what is wrong and how to fix it.

---

❌ **Ignoring the `revised_prompt` field**

If you're using the API and never checking the `revised_prompt` field, you're flying blind. Every time Aurora's rewriter significantly changes your prompt, you learn nothing from the iteration. The `revised_prompt` field is one of the most valuable diagnostic tools available.

---

*End of Grok Imagine Professional Daily Reference Card*
*Companion document: `grok-imagine-research.md` for full technical depth*
*Document currency: May 2026 — verify Spicy Mode and content policies against current xAI AUP before building workflows*
