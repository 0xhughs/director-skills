# Kling AI: Practical Prompt Engineering Reference Card

> **File:** `kling-ai-guide.md` · Daily use reference for filmmakers, ad creatives, producers  
> **Verified:** May 25, 2026 · Based on Kling 3.0 / O3 current state

---

## 1. QUICK START CHECKLIST — 15 Things for Every Kling Prompt

- [ ] **1. Choose the right model first** — Don't default to the newest/most expensive. Match model to task (see §2).
- [ ] **2. Set aspect ratio before writing prompt** — 16:9 landscape, 9:16 portrait, 1:1 square. I2V input image must match.
- [ ] **3. Lead with camera + subject** — First sentence describes camera position and primary subject action. Front of prompt dominates weighting.
- [ ] **4. Write in prose, not tag lists** — Natural language paragraphs outperform comma-separated keywords. Kling understands cinematic direction.
- [ ] **5. Specify the camera move explicitly** — "slow dolly in," "tracking shot at waist height," "static locked-off." Kling responds to these directly.
- [ ] **6. Name your lighting setup** — "golden hour," "chiaroscuro," "three-point," "sodium vapor night." Don't just say "cinematic lighting."
- [ ] **7. Include one style reference** — Named cinematographer, film title, or camera body ("Roger Deakins Blade Runner 2049," "ARRI Alexa," "16mm grain").
- [ ] **8. For audio (3.0/O3 only): use character brackets** — `[CharacterName, tone]: "dialogue"`. Define who speaks and when.
- [ ] **9. Write a negative prompt** — Minimum: `blurry, distorted hands, extra fingers, extra limbs, watermark, morphing face`.
- [ ] **10. For I2V: focus the prompt on MOTION, not appearance** — The image handles the look; you handle what moves and how.
- [ ] **11. For Elements consistency: use @ElementName in every shot** — Even if the element is obvious; repetition reinforces the binding.
- [ ] **12. For multi-shot (3.0): label shots explicitly** — "Shot 1:", "Shot 2:", or use Custom Multi-Shot fields. Don't blend shots in single paragraph.
- [ ] **13. Test in Standard tier first** — Concept test at 20 credits/5s. Only upgrade to Pro/Master for selected final versions.
- [ ] **14. Keep actions physically plausible** — One physics action per shot. Complex hand interactions → frame wider, describe simpler.
- [ ] **15. If it refuses: check for trigger words** — Common false positives: chest, pig, exorcism, certain medical terms. Rephrase with synonyms or try Chinese-language prompt.

---

## 2. MODEL & FEATURE DECISION TREE

```
WHAT DO YOU NEED?

├── Single short clip (up to 10s), simple scene
│   ├── Just testing / cheap iteration → Kling 2.5 Turbo Standard
│   ├── Social media content (high volume) → Kling 2.5 Turbo Standard
│   └── Final quality output → Kling 3.0 Pro
│
├── Multi-shot sequence (up to 6 shots, up to 15s)
│   ├── Prompt-driven narrative → Kling 3.0 Pro (Custom Multi-Shot)
│   └── Character-consistent narrative → Kling O3 Pro (Multi-shot + Elements)
│
├── Character consistency across clips
│   ├── Character face + appearance only → Kling 3.0 Pro (Elements, 3–4 ref images)
│   └── Character face + VOICE → Kling O3 (voice cloning + Elements)
│
├── Start from an image
│   ├── Simple animation → I2V Standard (any model)
│   ├── High-quality animation → I2V 3.0 Pro
│   ├── Keyframe-to-keyframe transition → Start+End Frame (O1 or 3.0 Pro)
│   └── Animate with specific motion path → Motion Brush (I2V 1.5+, GUI only)
│
├── Continue an existing clip → Extend (any model, 5s segments)
│
├── Restyle existing footage → O3 Reference Video mode
│
├── Lip sync speech to existing clip → Lip Sync feature (post-generation)
│
├── Native audio in the video → 3.0 or O3 (enable audio at generation)
│
├── Virtual garment fitting → Try-On (Kolors model)
│
└── Talking head / avatar → Avatar 2.0 interface or I2V + Lip Sync
```

---

## 3. THE UNIVERSAL KLING PROMPT TEMPLATE

### T2V (Text-to-Video)
```
[CAMERA POSITION & MOVEMENT] shot of [SUBJECT DESCRIPTION] [ACTION/BEHAVIOR] 
in [ENVIRONMENT]. [LIGHTING SETUP: source, quality, direction]. 
[ATMOSPHERE/WEATHER if relevant]. 
[COLOR GRADE / STYLE REFERENCE]. 
[AUDIO INTENT if 3.0/O3: ambient, music, or dialogue bracket].
Duration: [Xs]. 
Negative prompt: [WHAT TO EXCLUDE].
```

**Example:**
```
A slow dolly push-in from medium shot to close-up of a weathered detective sitting 
at a rain-fogged bar, hands wrapped around a whisky glass, staring at nothing. 
Tungsten bar lighting from above-right, deep chiaroscuro shadow on the left side 
of his face. Rain audible against glass windows. 
Neon exterior signage casts a faint red glow on the bar counter. 
Color: desaturated warm — Darius Khondji Seven palette.
Audio: bar ambient, low jazz piano, rain on glass.
Duration: 10s.
Negative: blurry, extra limbs, morphing face, TV-movie lighting.
```

### I2V (Image-to-Video) — Motion Focus
```
[SUBJECT from image] [MOTION: what they do / how they move]. 
[CAMERA MOVEMENT]. [BACKGROUND MOVEMENT if any].
[ONE atmospheric change if needed].
Duration: [Xs].
Negative prompt: [appearance changes you want to prevent].
```

**Example:**
```
The woman lifts her gaze slowly from the book, turns to face left, 
a slight smile crossing her face. 
Camera holds steady — medium shot.
A breeze stirs her hair gently. Café sounds rise slightly.
Duration: 7s.
Negative: changing hairstyle, outfit change, background morphing.
```

### Multi-Shot (3.0/O3 Custom)
```
Shot 1 ([Xs]): [CAMERA]. @[Element]. [ACTION]. [ENVIRONMENT]. [LIGHTING]. [AUDIO].
Shot 2 ([Xs]): [CAMERA]. @[Element]. [ACTION]. [ENVIRONMENT]. [LIGHTING]. [AUDIO].
Shot 3 ([Xs]): [CAMERA]. @[Element]. [ACTION]. [ENVIRONMENT]. [LIGHTING]. [AUDIO].
[Up to 6 shots; min 3s each; max 500 characters per shot; total ≤15s]
```

---

## 4. TOP 30 POWER PHRASES THAT ELEVATE KLING OUTPUT

*All community-verified as producing consistent improvement:*

**Camera & Motion:**
1. `slow dolly push-in` — reliable camera approach motion
2. `rotating lens around the subject` — orbit/arc movement
3. `camera holds on [subject/detail]` — deliberate linger/hold
4. `handheld, documentary presence` — organic handheld feel
5. `static locked-off, tripod` — reliable stillness
6. `crane shot rising to reveal` — elevation + reveal
7. `tracking shot at waist height` — kinetic follow
8. `camera slowly pulls back to reveal` — widening reveal

**Lighting:**
9. `golden hour, warm directional light, long shadows` — cinematic sunset
10. `chiaroscuro — extreme contrast, deep shadow` — noir/drama
11. `volumetric light shafts through [source]` — atmospheric godrays
12. `neon signs casting colored light on wet pavement` — cyberpunk night
13. `single practicalwindow light, naturalistic` — indie/drama naturalism
14. `backlit silhouette against bright background` — dramatic outline

**Style & Grade:**
15. `Roger Deakins / Blade Runner 2049 palette` — amber+cobalt cinematic
16. `35mm film grain, natural halation in highlights` — organic film quality
17. `teal-and-orange cinematic grade` — Hollywood blockbuster look
18. `Cinestill 800T — halation around lights` — night photography aesthetic
19. `desaturated, muted, Nordic palette` — cold emotional restraint
20. `Makoto Shinkai / Studio Ghibli anime style` — Japanese animation

**Atmosphere & Texture:**
21. `wet pavement, neon reflections, rain` — urban night atmosphere
22. `morning mist, soft diffuse light, silence` — peaceful establishing
23. `visible breath in cold air` — winter/tension atmosphere
24. `slow motion — [X]fps equivalent — time expands` — hero physics moment
25. `subsurface scattering on skin, photorealistic texture` — close-up realism

**Emotional Intent:**
26. `a flicker of doubt crosses the face` — micro-expression
27. `eyes alive and searching` — engaged character performance
28. `breathing slows to near stillness` — tension/contemplation
29. `a beat of silence before responding` — dialogue pacing
30. `the camera holds long enough to feel uncomfortable` — slow-burn tension

---

## 5. CHEAT SHEET TABLES

### Camera Movement vs. Kling Preset Availability

| Move | Prompt Phrase | Preset? |
|---|---|---|
| Push-in/Dolly | `slow dolly push-in toward` | ✅ Zoom (forward) |
| Pull-back | `camera pulls back, dollying away` | ✅ Zoom (out) |
| Truck lateral | `camera trucks left/right` | ✅ Horizontal |
| Pedestal | `camera rises/descends on pedestal` | ✅ Vertical |
| Pan | `camera pans left/right` | ✅ Pan |
| Tilt | `camera tilts up/down` | ✅ Tilt |
| Roll/Dutch | `camera rolls [X] degrees, Dutch angle` | ✅ Roll |
| Orbit/Arc | `rotating lens around the subject` | ❌ Prompt-only |
| Steadicam | `Steadicam float, organic sway` | ❌ Prompt-only |
| Handheld | `handheld, documentary shake` | ❌ Prompt-only |
| Drone orbit | `aerial drone circles counterclockwise` | ❌ Prompt-only |
| Crane | `camera cranes up to reveal` | Master Shot 3 |
| Dolly zoom | `dolly zoom, Vertigo effect` | ❌ Prompt-only |
| Whip pan | `rapid whip pan right, blur transition` | ❌ Prompt-only |

### Lens → Kling Effect

| Focal Length | Result |
|---|---|
| 14–18mm | Wide, distortion, environmental dominance |
| 24–28mm | Walk-about, slight perspective |
| 35mm | Natural, warm, grounded |
| 50mm | Neutral, true-eye perspective |
| 85mm | Subject isolation, portrait flattery |
| 135mm+ | Compression, subject against blur |
| Macro | Extreme detail, miniature world |
| Anamorphic | Horizontal flare, oval bokeh, scope feel |
| Tilt-shift | Selective plane, miniature effect |

### Lighting Mood Quick-Reference

| Mood | Lighting Formula |
|---|---|
| Noir/thriller | Chiaroscuro + sodium vapor/neon practicals |
| Romance/intimacy | Tungsten warmth + soft fill + practicals |
| Corporate/clean | Three-point, high-key, neutral |
| Horror | Fluorescent (flicker) + deep black + single source |
| Epic/heroic | Golden hour backlight + fill from front |
| Sci-fi | Cold LED/HMI + colored practicals |
| Documentary | Naturalistic window light + minimal fill |
| Luxury/aspirational | Soft box key + dark background + product specular |

### Color Grade Reference

| Look | Formula | Kling Phrase |
|---|---|---|
| Blockbuster | Teal shadows + orange highlights | `teal-and-orange Hollywood grade` |
| Blade Runner | Deep cobalt + amber dust | `Blade Runner 2049 color palette` |
| Nordic | Desaturated, cool grey-blue | `muted Nordic palette, desaturated` |
| Noir | Near-monochrome + warm lamp | `black and white noir, single warm source` |
| Warm indie | Lifted shadows, natural grain | `warm indie film, Kodak Vision3 grain` |
| Night photo | Halation + tungsten warmth | `Cinestill 800T halation effect` |

### Audio Pipeline (for non-3.0 models or post-production)

| Need | Tool | Notes |
|---|---|---|
| Voice synthesis | ElevenLabs v3 | 32 emotion styles, 29 languages |
| Music | Suno v4, Udio | Generate from mood/genre description |
| SFX / foley | MMAudio, Freesound | MMAudio is context-aware from video |
| Voice cloning | ElevenLabs Voice Clone | 30s clean sample minimum |
| Final mix | DaVinci Resolve Fairlight | Free professional audio DAW |

---

## 6. THE 23 GENRES AT A GLANCE

One-line formula + recommended model+feature for each:

| # | Genre | One-Line Formula | Model + Feature |
|---|---|---|---|
| 1 | Narrative Drama | Character + subtext action + intimate lighting | 3.0 O3 Pro, Multi-shot + Elements |
| 2 | Action/Thriller | Subject in motion + tracking camera + physical jeopardy | 3.0 Pro, T2V or 2-shot |
| 3a | Horror (slow-burn) | Empty environment + one wrong detail + slow push | 3.0 Pro, I2V, 10s |
| 3b | Horror (jump-scare) | Buildup shot → scare cut (multi-shot) + audio sting | 3.0 Pro, Multi-shot + Native Audio |
| 4a | Hard Sci-Fi | Utilitarian design + documentary restraint + silence | 3.0 Pro, T2V |
| 4b | Space Opera | Scale contrast (fleet → bridge → face) + audio epic | 3.0 Pro, Multi-shot + Native Audio |
| 5 | Fantasy/Epic | Hero at scale + Elements + crane shot + sweep | O3 Pro, Multi-shot + Elements |
| 6 | Romance | Stolen moment + gentle push + warm palette | 3.0 Std/Pro, I2V |
| 7a | Comedy (Broad) | Readable wide framing + sight gag + reaction shot | 3.0 Std, Multi-shot |
| 7b | Comedy (Deadpan) | Static locked-off + nothing happens + absurd scenario | 3.0 Std, Static I2V |
| 8a | Doc (Observational) | Handheld presence + naturalistic light + no performance | 2.6 Pro or 3.0 Std |
| 8b | Doc (Interview) | MCU portrait + off-camera eyeline + Lip Sync | 3.0 Pro, I2V + Lip Sync |
| 9a | Music Video (Performance) | Scale contrast + artist Elements + music sync | 3.0 Pro, Multi-shot + Elements |
| 9b | Music Video (Narrative) | Story without explanation + character Elements + beats | O3 Pro, Multi-shot + Elements |
| 10 | Commercial/TVC | Product in context + beauty lighting + luxury palette | 3.0 Pro, I2V or T2V |
| 11 | UGC/Social | 9:16 portrait + natural light + loop-friendly + simple | 2.5 Std, T2V or I2V |
| 12 | Product Video | Start/End frame rotation + studio light + clean bg | 3.0 Pro, Start+End Frame |
| 13 | Explainer/Corp | Abstract visualization + neutral palette + ambient | 3.0 Std, T2V |
| 14 | Animation | Style reference (Ghibli, Pixar, Aardman) + character action | 3.0 Pro, T2V |
| 15 | Anime | Makoto Shinkai / Ghibli reference + emotional scene | 3.0 Pro, T2V |
| 16 | Experimental | One physics transformation + stillness + duration | 3.0 Pro, T2V |
| 17 | Sports | Slow-motion hero action + arena light + kinetic camera | 3.0 Pro, T2V |
| 18 | Found Footage | VHS aesthetic + imperfect handheld + uncanny moment | 2.5 Std (720p + grain) |
| 19 | Trailer/Teaser | Rhythmic 6-shot escalation + SFX audio + silence-to-hit | 3.0 Pro, Multi-shot |
| 20 | Lip-Synced Dialogue | Character bracket syntax + voice cloning + MCU | O3 Pro, Native Audio |
| 21 | Cinemagraph | Motion Brush on one element only + everything else static | 1.6 Std, Motion Brush |
| 22 | Slow-Motion Hero | One physical action + 240fps equivalent + backlight | 3.0 Pro, T2V, 10–15s |
| 23 | Talking Head/Avatar | Portrait I2V + subtle speech motion + Lip Sync | 3.0 Pro, I2V + Lip Sync |

---

## 7. COMMON MISTAKES & FIXES

| Mistake | What Happens | Fix |
|---|---|---|
| Tag soup: `cinematic, 4K, stunning, beautiful, HDR` | Generic, flat output | Replace with specific: `slow dolly on a detective's face, tungsten bar light, Darius Khondji Seven palette` |
| Describing the image in I2V | Prompt fights the image; morphing artifacts | Only describe MOTION in I2V prompts |
| Asking for complex hand interaction at ECU | Distorted fingers, anatomy failure | Frame wider; simplify the action; avoid "piano playing," "writing," "typing" |
| `Static camera` + `sweeping pan` in same prompt | Contradictory instructions cause random output | Choose one camera behavior per shot |
| Forgetting to label shots in multi-shot | Model blends shots instead of cutting | Use "Shot 1:", "Shot 2:" labels or Custom Multi-Shot fields |
| Generating too long for complex action | Physics failure at 10s+; drift | Break complex sequences into 5s segments; extend or stitch |
| No negative prompt | Default artifacts: extra limbs, blur, watermark | Always include baseline negative prompt |
| Not using Elements for character consistency | Face changes between shots/extensions | Create Elements from 3–4 angle photos; use `@CharName` in every prompt |
| Trying to generate readable arbitrary text | Unreliable sign/logo text | For specific brand text: use post-production overlay; avoid in-frame text prompts for custom copy |
| Overly long single prompt | Prompt collapse — model ignores parts | Segment into multi-shot; trim to essential elements; front-load priorities |

### Side-by-Side Rewrites

**Before:** `A man walking in rain, cinematic, dramatic, 4K, film grain, noir style`

**After:** `A man in a soaked grey overcoat strides down a deserted 1950s New York alley. Low-angle tracking shot at knee height, camera moving with him. A single sodium vapor streetlamp overhead casts orange pools on the wet cobblestones. Deep chiaroscuro shadow fills 60% of the frame. Carol Reed The Third Man visual grammar. Film grain.`

---

**Before:** `Create a video of my character speaking a monologue`

**After (O3 multi-shot with audio):**
```
Shot 1 (7s): @HeroChar — CU, MCU, window light from right, deep shadow left. 
He looks off camera. Slight pause. Then speaks.
[HeroChar, measured, exhausted voice]: "You know the worst thing about surviving? 
You wake up the next day and have to do it again."
Shot 2 (5s): @HeroChar — he finally turns to face camera directly. Close-up. Eyes still.
[HeroChar, quieter]: "Every single day."
```

---

## 8. 25 READY-TO-USE PROMPT RECIPES

```
RECIPE 1 — NEON NIGHT WALK (T2V, 3.0 Pro, 10s, 16:9)
A lone woman walks slowly through a rain-soaked Tokyo alleyway at 2am. 
Handheld camera follows from behind at medium shot, slightly low. 
Neon signs in Japanese reflect in pooled water on the ground. 
Steam rises from a grate on her left. She doesn't look back. 
Color: teal and magenta neon cast against deep black. Cinestill 800T halation.
Audio: rain, distant train, her footsteps.
Negative: extra people, motion blur, logo visibility.
```

```
RECIPE 2 — GOLDEN HOUR PORTRAIT (I2V, 3.0 Pro, 7s)
[Input: outdoor portrait, good natural light]
Camera holds steady in medium close-up.
A warm breeze moves her hair slightly. She closes her eyes and turns her face 
up toward the last sun of the day. A slow, involuntary smile.
Duration: 7s. No dialogue.
Negative: hair color change, outfit change, background morphing.
```

```
RECIPE 3 — PRODUCT HERO SHOT (I2V, Start+End Frame, 3.0 Pro, 5s)
[Start: product facing 0°] [End: product at 90°]
Premium product rotates in clean studio. Soft box from upper left, 
reflective surface below. Material texture catches specular highlight as it rotates.
Duration: 5s, smooth rotation.
Negative: background texture change, extra products, motion artifacts.
```

```
RECIPE 4 — HORROR CORRIDOR (T2V, 3.0 Pro, 10s)
Empty hospital corridor stretching into darkness. Overhead fluorescents flicker.
Camera: extremely slow push-in at floor level, barely perceptible motion.
At the far end, a door stands slightly open. As the camera advances, 
the door swings shut. No sound. No explanation.
Lighting: flickering green-white fluorescent, deep black between pools.
Audio: HVAC hum growing slowly louder.
Negative: characters, gore, explicit.
```

```
RECIPE 5 — SLOW-MOTION WATER (T2V, 3.0 Pro, 10s)
Ultra slow-motion — 240fps equivalent. A glass of water tips off the edge of 
a marble table in bright studio light. The moment of separation: the water 
becomes a perfect arcing body, suspended, backlit, crystalline.
Camera: macro, static, tracking the fall.
Backlight from right, soft fill from front. No other elements in frame.
Audio: the slowed, pitched-down sound of the glass and liquid.
```

```
RECIPE 6 — SPACE OPERA FLEET (T2V, 3.0 Pro, 15s, Multi-shot)
Shot 1 (6s): EWS — a vast fleet in orbit above a nebula. Slow crane down 
to the command ship level. Epic orchestral swell.
Shot 2 (5s): Bridge interior. Admiral at viewport. Camera push-in from wide to MCU.
[Admiral, commanding]: "All ships — advance."
Shot 3 (4s): ECU — ignition of a thousand engines. Blue-white exhaust blooms.
The fleet moves forward. Camera static, watching them go.
```

```
RECIPE 7 — INDIE DRAMA KITCHEN (T2V, 3.0 O3, Multi-shot + Elements + Audio)
Late night kitchen. Only refrigerator hum.
Shot 1 (5s): @Sarah — MCU — staring at a cold cup of coffee. Static camera.
[Sarah, barely audible]: "I should have said something."
Shot 2 (5s): The empty chair across the table. Static. No one there.
[Sarah, off-frame]: "I know that now."
Shot 3 (5s): @Sarah's hands wrap tighter around the cup. ECU on hands. Silence.
```

```
RECIPE 8 — LUXURY WHISKY (I2V, 3.0 Pro, 5s)
[Input: clean whisky glass on wood surface, backlit]
The glass is slowly lifted by a weathered, elegant hand.
Light ripples through the amber liquid as it rises.
Hold on the glass mid-air. A beat before the sip.
Bokeh: deep f/1.4 equivalent. No other motion.
Audio: the soft scrape of glass on wood, room tone.
Negative: cheap-looking hands, background movement, product distortion.
```

```
RECIPE 9 — SOCIAL VERTICAL (T2V, 2.5 Std, 9:16, 5s)
Portrait format. A barista in a sunlit café pours latte art.
Overhead angle, slightly angled. Natural window light from left.
Focus: the pour and the swirl. Clean wooden counter.
Loop-friendly. Duration: 5s.
Negative: blurry, extra hands, busy background.
```

```
RECIPE 10 — ANIME DEPARTURE (T2V, 3.0 Pro, 10s)
Makoto Shinkai anime style — hand-painted backgrounds, soft cel animation.
A girl stands on a train platform at dusk as the last train departs.
Wind from the passing train moves her hair and skirt.
She watches it leave. She doesn't move.
Camera: medium wide, static. Sky: deep indigo and dusty rose.
Audio: piano motif, unresolved final chord.
```

```
RECIPE 11 — CORPORATE EXPLAINER (T2V, 3.0 Std, 16:9, 10s)
Abstract network visualization: nodes of light connected by thin pulse lines.
The network breathes — slowly expanding and contracting.
Camera: gentle orbit around the central cluster. Blue and white on dark bg.
No characters. No text. Pure abstract motion.
Duration: 10s, loop-friendly.
Audio: gentle ambient chime sequence.
```

```
RECIPE 12 — ROMANTIC PARIS (T2V, 3.0 Pro, 10s)
A sun-drenched Parisian café terrace, late afternoon. @Sylvie reads at a table.
Camera: slow push-in from wide to MCU, over 10 seconds.
Golden hour from right catches her hair. A breeze stirs the pages of her book.
She glances up once, amused by something off-frame, then returns to reading.
Wong Kar-wai visual grammar. Amber + soft green palette.
Audio: distant café, bicycle bell, birdsong.
```

```
RECIPE 13 — FIGHT ANTICIPATION (T2V, 3.0 Pro, 7s)
Two fighters stand 3 meters apart in a rain-soaked parking structure.
Neither moves. Rain falls in visible curtains behind them. 
Camera: static wide, both figures visible, equal frame weight.
Split lighting from opposite sources — each fighter lit from their side.
Duration: 7s. The clip ends before anything happens.
Audio: only rain and distant traffic.
```

```
RECIPE 14 — DOCUMENTARY CRAFTSMAN (T2V, 2.6 Pro, 10s)
A master ceramicist at a pottery wheel, morning light through a workshop window.
His hands work the clay — decades of practiced confidence.
He doesn't look at the camera. The camera doesn't announce itself.
Handheld, 35mm equivalent, documentary presence.
Lighting: naturalistic window light only. Warm, slightly desaturated.
Audio: the wheel, hands on wet clay, birds outside.
```

```
RECIPE 15 — GHIBLI FIELD RUN (T2V, 3.0 Pro, 8s)
Studio Ghibli anime style. A young girl runs through a sunflower field in summer.
Her hair trails, her feet barely touch the ground. Saturated warm palette.
Camera: medium wide tracking shot, camera pans to follow her.
Background: painted hand-crafted Ghibli quality, distant mountains.
Audio: cheerful orchestral theme, light strings.
```

```
RECIPE 16 — TIME OF DAY SHIFT (T2V, 3.0 Pro, 10s)
The same empty park bench. The camera is completely static. Wide shot.
Over the 10 seconds, the light transitions from golden afternoon to blue evening.
Long shadows shorten and disappear; the sky deepens from amber to indigo.
The bench is always empty. No people. Only time passing.
Audio: ambient transitions from birdsong to evening crickets.
```

```
RECIPE 17 — VHS HORROR BIRTHDAY (T2V, 2.5 Std, 10s)
Home video quality — VHS transfer with tracking artifacts. Year 1994 in corner.
A suburban backyard birthday party. Kids, balloons, a sprinkler.
The camera pans right and catches, at the far edge of the yard, 
a child standing completely still, staring directly at the camera.
Everyone else is in motion. She is not.
VHS grain, warm color shift, slight tracking wobble.
```

```
RECIPE 18 — PRODUCT 360° CLEAN (I2V, Start+End Frame, 3.0 Pro, 7s)
[Start: pair of sneakers, 0° facing]
[End: same sneakers, 120° rotation]
Premium sneaker rotates smoothly on a white surface.
Soft box lighting from above, slight fill from below.
The knit texture and sole detail catch the light as it turns.
Duration: 7s, smooth mechanical rotation.
Negative: color shift, background texture change, wobble.
```

```
RECIPE 19 — INTERROGATION SCENE (O3 Multi-shot + Elements + Audio)
Shot 1 (7s): @Detective leans forward, forearms on table. Cold LED light above.
He opens a folder slowly and doesn't look at the suspect.
[Detective, flat controlled voice]: "I know what you did."
Shot 2 (8s): @Suspect across the table — tight MCU, slight sheen of sweat.
A long silence. He blinks. Swallows.
[Suspect, voice cracking]: "I want a lawyer."
```

```
RECIPE 20 — FABRIC HERO (I2V, 3.0 Pro, 8s)
[Input: model in silk dress, minimal motion]
Ultra slow-motion — wind catches the dress and it billows dramatically.
The fabric folds and moves in complex waves, backlit by harsh window light.
The silk is translucent where the light hits hardest.
Camera: static MCU on the fabric movement. No face. Pure texture.
Duration: 8s slow-motion.
```

```
RECIPE 21 — TRAILER TEASER (3.0 Pro, Multi-shot, 15s)
Shot 1 (2s): EWS — burning skyline at night. Silence.
Shot 2 (2s): CU — a hand picking up a weapon from the ground.
Shot 3 (2s): ECU — an eye opening suddenly. Gasp.
Shot 4 (3s): Running through a crowd. Handheld urgency.
Shot 5 (3s): @Hero alone on a rooftop. Back to camera. Wind.
Shot 6 (3s): @Hero's face — jaw set. Silence.
Audio: silence for first 3 shots → rising drone → thunderous hit on shot 4.
```

```
RECIPE 22 — TALKING HEAD AVATAR (I2V + Lip Sync, 3.0 Pro, 10s)
[Input: clean professional portrait, front-facing, studio background]
Motion prompt: subject speaks naturally, slight head movement, 
occasional blink, slight hand gesture enters lower frame occasionally.
Camera: MCU, static. Then apply Lip Sync with ElevenLabs voice audio.
Style: PBS / LinkedIn professional — clean, credible, engaging.
Negative: dramatic gestures, looking off-camera, outfit change.
```

```
RECIPE 23 — CINEMAGRAPH RAIN (I2V, 1.6 Std, Motion Brush, 5s loop)
[Input: woman at rainy window, artful composition]
Motion Brush: mask only the rain on the window glass.
Motion direction: downward streaks on glass surface.
Everything else: completely static.
Duration: 5s, designed to loop seamlessly.
Negative: face movement, hair movement, body movement, background movement.
```

```
RECIPE 24 — SPORTS SLOW-MO (T2V, 3.0 Pro, 10s)
Ultra slow-motion — 240fps equivalent — a basketball player rises for a dunk.
From court level, looking up: the player rises, the ball extended above.
The crowd behind is a slow blur of motion and light.
The player hangs at the apex of the jump — held for 2 seconds.
The basket net begins to snap back. Slow. Perfect.
Arena multi-source lighting. Hard follow-spot from above.
Audio: crowd in slow-motion roar, building.
```

```
RECIPE 25 — EXPERIMENTAL APPLE (T2V, 3.0 Pro, 10s)
A red apple sits centered on a white table. 
The camera is perfectly static. Kubrick symmetry.
Over 10 seconds, dark bruising slowly spreads across the skin of the apple.
Like ink through water. Almost imperceptible at first.
The light source slowly shifts position as if hours are condensed.
No sound except a deepening refrigerator hum that becomes almost musical.
Style: Chantal Akerman — duration as subject, stillness as statement.
```

---

## 9. IMAGE-TO-VIDEO INPUT IMAGE CHECKLIST

- [ ] **Resolution:** Minimum 720p; use 1080p or higher for Pro/3.0 generations
- [ ] **File format:** JPG or PNG; under 10MB
- [ ] **Aspect ratio:** Matches target output (16:9 for landscape, 9:16 for portrait, 1:1 for square)
- [ ] **Subject placement:** Primary subject clearly visible; centered or rule-of-thirds framed
- [ ] **Lighting:** Avoid extreme backlighting or silhouettes unless that's the intended look
- [ ] **Background complexity:** Simpler backgrounds = less drift. Complex busy backgrounds increase spatial inconsistency.
- [ ] **Face visibility (for lip sync/emotion):** Front-facing or slight 3/4 angle; lips clearly visible
- [ ] **Product shots:** Clean neutral background; product against white/dark solid for product reveal
- [ ] **Motion space:** Ensure there is visual "room" in the direction the subject will move
- [ ] **No pre-existing text/logos in frame** unless specifically intended (text in I2V can become unstable mid-clip)

---

## 10. ELEMENTS (MULTI-REFERENCE) WORKFLOW RECIPE

```
STEP 1: PREPARE SOURCE IMAGES
Gather 4 photos of your character/subject:
- Front facing (clean, even lighting)
- 3/4 left angle
- 3/4 right angle  
- Full profile (side)
All with consistent costume/appearance.

STEP 2: CREATE ELEMENT
In Kling Element Library → New Element → Upload 4 images → Name it.
(For O3 voice cloning: also upload 5–30s clean audio of the voice)

STEP 3: REFERENCE IN PROMPTS
In every shot prompt that includes this character:
"@[ElementName] [action] in [environment]..."

STEP 4: TEST CONSISTENCY
Generate a 5s Standard clip. Check consistency.
If face drifts on a specific angle: add a 5th reference image from that angle.

STEP 5: SCALE TO MULTI-SHOT
Use @[ElementName] in every shot of a Custom Multi-Shot sequence.
The element binding maintains identity across all 6 shots.

NEGATIVE PROMPT FOR ELEMENT STABILITY:
"changing hairstyle, different clothing, morphing features, de-aging, aging"
```

---

## 11. START FRAME + END FRAME WORKFLOW RECIPE

```
STEP 1: DEFINE YOUR START AND END STATES
Start Frame: the visual state that begins the clip
End Frame: the visual state that ends the clip
Rule: they must be logically interpolatable (same location/scale/light)

STEP 2: GENERATE OR SELECT FRAMES
Option A: Generate both frames in Midjourney/Flux with consistent prompting
Option B: Screenshot from existing footage at key moments
Option C: Use Kling's own I2V still frames from prior generations

STEP 3: CHECK COMPATIBILITY
- Same aspect ratio for both frames
- Compatible color temperature / lighting direction
- Subject in a physically bridgeable pose difference
- If very different: accept morphing/transformation as the intended effect

STEP 4: WRITE THE INTERPOLATION PROMPT
"[Subject] transitions from [starting state] to [ending state].
[Camera movement during transition].
[Lighting holds consistent / shifts toward X].
[Any specific intermediate action]."

STEP 5: SET DURATION
5s: for clean transitions, sharp cuts, product rotation
10s: for transformation presets, complex metamorphosis

STEP 6: GENERATE AND REVIEW
- Does the midpoint look physically plausible?
- Is there unwanted morphing? → Frames are too dissimilar. Choose closer frames.
- Does identity drift? → Add Element binding; use negative prompts.
```

---

## 12. LIP SYNC WORKFLOW RECIPE

```
PRE-REQUISITE: A base video clip with:
- Humanoid face clearly visible
- Lips not obscured
- Primarily front-facing head position
- Under 10 seconds; under 100MB; MP4 or MOV

OPTION A — KLING TTS (Simplest):
1. Go to Lip Sync tool in Kling interface
2. Upload your base video
3. Select text-to-speech
4. Type your script
5. Choose voice style / emotion preset
6. Click Generate
Result: auto-synced lip movement + Kling-generated voice

OPTION B — CUSTOM AUDIO (Best quality):
1. Record or generate audio with ElevenLabs, Murf, or similar
   - Clean audio, no background music or noise
   - Match audio duration to video duration (or shorter)
2. Upload base video to Lip Sync tool
3. Click "Match Mouth Type" — wait for face detection
4. Upload custom audio file (MP3/WAV/M4A; under 30s; under 20MB)
5. If audio longer than video: crop option appears — use it
6. Generate and review

MULTI-CHARACTER (Pro mode required for 3+):
- Pro mode: up to 4 character tracks with separate audio
- Each track is independent; timing is controllable
- Characters cannot be individually targeted in Standard mode

BEST PRACTICES:
- Generate the base clip with: "character is speaking, front-facing, lips visible, subtle head movement"
- Use negative prompt in base clip: "extreme head movement, looking away from camera"
- For anime/stylized: expect lower quality sync; use realistic renders for best results
```

---

## 13. EXTEND CHAIN WORKFLOW

```
STEP 1: GENERATE A CLEAN BASE CLIP
Requirements for a good extend base:
✓ Stable motion (not mid-action at a volatile moment)
✓ Consistent lighting (no extreme dynamic range)
✓ Clear environmental context
✓ The last frame looks like it "could continue"

STEP 2: FIRST EXTENSION
Go to Extend tool → Select your clip → Write continuation prompt:
"[Subject] continues [action]. [Camera behavior]. 
[Maintain environment descriptors from original clip]."
Generate. Review last frame of extension.

STEP 3: CHAIN DECISION
If extension looks clean: extend again (up to 3-4 total)
If visual drift detected: STOP extending. Use the last-frame restart.

LAST-FRAME RESTART METHOD (prevents drift accumulation):
→ Screenshot the last frame of your current best clip
→ Use that frame as a Start Frame for a new I2V generation
→ Generates fresh from that frame without accumulated drift
→ Stitch in editing software

EDITING ASSEMBLY:
- Import all clips into Premiere / DaVinci Resolve
- Trim to clean matching hold points
- Cut on action or on matched holds
- Apply consistent color grade across all clips
- Add audio layer in post

CREDIT ECONOMICS:
Each 5s Extend = ~35 credits
vs. new 5s Standard generation = 20 credits
For very short continuations, sometimes cheaper to regenerate fresh
```

---

## 14. AUDIO PIPELINE CHEAT SHEET

```
GENERATION PHASE:
┌─────────────────────────────────────────────────────┐
│ Using Kling 3.0 / O3?                               │
│                                                     │
│  YES: Enable Native Audio in generation settings    │
│  ├── Add audio descriptor to prompt                 │
│  ├── For dialogue: use [CharName, tone]: "line"     │
│  └── Specify: ambient, music mood, SFX              │
│                                                     │
│  NO (older models): Generate silent video           │
│  └── Add all audio in post-production               │
└─────────────────────────────────────────────────────┘

POST-PRODUCTION AUDIO STACK:
┌──────────────────────────────────────────────────────┐
│ Layer 1 — VOICE / DIALOGUE                          │
│   → ElevenLabs v3 (best) or Murf                   │
│   → Apply to video via Kling Lip Sync OR            │
│   → Lay directly in timeline (talking-head style)  │
│                                                     │
│ Layer 2 — MUSIC                                     │
│   → Suno v4 or Udio (generate from mood/BPM)       │
│   → Mix under dialogue at -20 to -15 dB            │
│                                                     │
│ Layer 3 — SOUND EFFECTS / FOLEY                     │
│   → MMAudio (context-aware from your video)        │
│   → Freesound.org (free CC licensed SFX)           │
│   → Record/buy professional foley packs            │
│                                                     │
│ Layer 4 — AMBIENT / ROOM TONE                       │
│   → Generate in Suno or find on Freesound          │
│   → Must match the visual acoustic environment     │
│                                                     │
│ FINAL MIX                                          │
│   → DaVinci Resolve Fairlight (free)               │
│   → Adobe Premiere Pro (paid)                      │
│   → Ensure: dialogue > SFX > music in priority     │
└──────────────────────────────────────────────────────┘
```

---

## 15. ITERATION PLAYBOOK

```
ROUND 1: Concept test
→ Use Standard tier; generate 2-3 variations
→ Judge: Is the basic scene composition right? Camera working?
→ If NO: fix prompt before spending Pro credits

ROUND 2: Direction selection
→ Identify which variation has the best bones
→ Note specifically what needs fixing: lighting? motion? character?

ROUND 3: Targeted refinement
→ Change ONE variable at a time
→ If lighting is wrong: fix that first, leave everything else constant
→ If character drifts: add Elements, don't change the whole prompt

ROUND 4: Pro/Master final
→ Only upgrade tier once you have a confirmed prompt that works
→ Generate 2 Pro versions; take the best

ROUND 5: Post-production
→ Color grade for consistency if multiple clips
→ Audio design
→ Final assembly and export

RULE: Never spend Pro credits on unproven prompt directions.
RULE: Fix one thing at a time. Changing everything at once means you don't know what worked.
RULE: Standard tier ≠ lower quality concept. It's fine for testing, not for delivery.
```

---

## 16. ANTI-PATTERNS (WHAT NEVER TO DO)

❌ **Never write tag-soup prompts** — "cinematic, 4K, stunning, dramatic, realistic" adds nothing. Describe the actual scene.

❌ **Never fight the input image in I2V** — if the image shows daylight, don't prompt for moonlight. Describe the change from the image's state.

❌ **Never chain extend indefinitely** — quality degrades after 3–4 extensions. Use the last-frame restart method.

❌ **Never rely on Kling for critical in-frame text** — logos, signs with specific copy, readable text in arbitrary fonts — will fail. Use post-production text overlays.

❌ **Never prompt for piano playing, keyboard typing, or fine writing at close range** — hand-finger anatomy still unreliable for fine motor interactions.

❌ **Never generate dialogue scenes without character brackets in 3.0/O3** — the model won't know who's speaking. Use `[CharName, tone]: "line"`.

❌ **Never use Motion Brush simultaneously with Camera Control presets or End Frame** — they are mutually exclusive features.

❌ **Never describe multiple complex actions in a single 5s clip** — one physical action per clip. "The glass falls AND the liquid splashes AND the person reacts" in 5 seconds = chaos.

❌ **Never skip the negative prompt** — it's not optional. The minimum negative prompt prevents the most common failure modes.

❌ **Never describe what's already in the image (I2V)** — you're describing the animation, not re-describing the picture.

---

## 17. COST-SAVING TACTICS

| Tactic | Savings |
|---|---|
| Concept test in Standard, finalize in Pro | ~3–5× credit savings per iteration round |
| Use 2.5 Turbo Std for high-volume social content | Cheapest reliable 1080p; 30fps |
| Generate 5s clips, extend only if needed | Cheaper than generating 10s; extend is ~35cr |
| Use I2V instead of T2V when possible | I2V gives more control → fewer wasted iterations |
| Build Elements once, reuse across a project | Elements creation is a fixed cost; reuse is free |
| Enable Smart Storyboard only after perfecting single shots | Multi-shot costs more; don't waste on unproven scenes |
| Use fal.ai API for programmatic batch workflows | Pay-per-use; no unused subscription credits |
| Generate without audio first; add audio only to selected clips | Audio doubles credit cost in 3.0; verify visuals first |
| Use Extend instead of regenerating for continuations | Extend is ~35cr vs 100cr+ for fresh Pro generation |
| Annual subscription saves ~15–20% vs monthly | Ultra annual: $119.17/mo vs $127.99/mo |

---

*End of kling-ai-guide.md*  
*Kling AI Verified State: May 25, 2026*  
*Kuaishou Technology / klingai.com*

