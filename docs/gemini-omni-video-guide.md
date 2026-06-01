# Gemini Omni Video — Daily Reference Guide
## For Filmmakers, Ad Creatives & Video Producers

---

> **Model Status (May 22, 2026):** The model is **Gemini Omni Flash** (launched Google I/O, May 19, 2026). It replaces Veo in the Gemini app and Google Flow. **Veo 3.1 remains the developer/API standard** on Vertex AI and Gemini API. Omni's public API is "coming weeks." This guide covers both. All advice applies to both unless noted.

---

## 1. Quick Start Checklist — 12 Things for Every Prompt

Before generating, verify:

- [ ] **Lead with cinematography** — shot type + camera movement come first
- [ ] **One action per prompt** — never request two simultaneous actions
- [ ] **Name the subject specifically** — not "a person," but "a woman in her 40s with short silver hair"
- [ ] **Specify the environment** — not "outside," but "a rain-soaked Hong Kong back alley at 2am"
- [ ] **Direct the lighting** — at minimum: time of day or dominant light source
- [ ] **Set the color/grade** — film stock, LUT reference, or descriptive palette
- [ ] **Include audio explicitly** — specify dialogue, SFX, ambient, and score (or "no score")
- [ ] **Add `(no subtitles)`** if any dialogue is present
- [ ] **State aspect ratio** — especially for vertical (9:16) content
- [ ] **Name the film stock or camera** — triggers cinematic quality heuristics
- [ ] **Set frame rate** — "24fps" for cinema; "30fps" for broadcast
- [ ] **Keep it under 400 words** — diminishing returns beyond this threshold

---

## 2. The Universal Cinematic Prompt Template

```
[SHOT SCALE], [CAMERA MOVEMENT]. [SUBJECT: physical description, age, wardrobe]. 
[ACTION: specific behavioral verbs, not emotional labels]. 
[ENVIRONMENT: location, time of day, atmospheric elements]. 
[LIGHTING: scheme, source, direction, color temperature]. 
[AUDIO: dialogue (with colon syntax), SFX, ambient, score]. 
(No subtitles.) [STYLE: film stock/camera, color grade, lens]. 
[TECHNICAL: aspect ratio, fps, duration]. 
```

**Filled example:**
```
Medium close-up, slow dolly in. A woman in her mid-40s, close-cropped silver hair, 
dark wool coat, no jewelry, stands at a rain-soaked window overlooking a grey 
industrial cityscape at dusk. She traces her finger along the glass. 
Warm amber lamp behind her, rest of apartment in shadow. Rembrandt lighting. 
She says: "It was never about the money." (No subtitles.) 
Ambient: rain on glass, distant traffic. Score: solo cello, restraint. 
Shot on ARRI Alexa, desaturated blue-grey grade. 16:9. 24fps.
```

---

## 3. Top 30 Power Phrases

These phrases consistently elevate output quality. Drop them into prompts as needed.

| # | Phrase | Effect |
|---|---|---|
| 1 | `"one continuous shot"` or `"oner"` | Prevents unwanted cuts; signals long-take aesthetic |
| 2 | `"shot on ARRI Alexa"` | Activates high-end cinematic color science |
| 3 | `"35mm Kodak Vision3 film grain"` | Warm, organic texture; period feel |
| 4 | `"shallow depth of field, razor-thin"` | Subject isolation, bokeh emphasis |
| 5 | `"(no subtitles)"` | Critical — prevents burned-in captions |
| 6 | `"Rembrandt lighting"` | Instantly adds depth to faces without over-specification |
| 7 | `"golden hour warm low-angle light"` | Transforms any exterior into cinematic beauty |
| 8 | `"anamorphic 2.39:1 widescreen"` | Signals epic/cinematic framing intent |
| 9 | `"slow dolly in"` | The most reliable dramatic movement phrase |
| 10 | `"vérité handheld, subtle documentary shake"` | Authentic realism trigger |
| 11 | `"physics accurate, gravity correct"` | Invokes Omni's world-knowledge physics reasoning |
| 12 | `"deep focus, everything sharp front to back"` | Forces Orson Welles / Citizen Kane aesthetic |
| 13 | `"SMASH CUT:"` | Reliable trigger for shocking editorial cut |
| 14 | `"no score — sound design only"` | Produces more restrained, cinematic result |
| 15 | `"ambient: [specific sounds]"` | Prevents incorrect default ambience |
| 16 | `"static locked-off, tripod"` | Essential for horror, deadpan, observational doc |
| 17 | `"teal-and-orange Hollywood grade"` | Action/commercial color grade trigger |
| 18 | `"phantom camera slow motion"` | Ultra-slow motion quality trigger |
| 19 | `"silence is the dominant audio element"` | Explicitly invokes silence as a tool |
| 20 | `"SFX: [specific sound] at [timestamp]"` | Precise sound placement |
| 21 | `"He/she says: [text]"` (colon not quotes) | Correct dialogue format for subtitle avoidance |
| 22 | `"Roger Deakins palette"` | Naturalistic warm cinematic grade trigger |
| 23 | `"inspired by Ghibli environmental detail"` | Anime world-building shorthand |
| 24 | `"no patterns, no accessories, solid [color]"` | Character consistency essential rule |
| 25 | `"VHS camcorder 1980s, tracking lines, color bleed"` | Found footage aesthetic trigger |
| 26 | `"natural smartphone zoom"` or `"selfie video of"` | Authentic UGC trigger |
| 27 | `"claymation stop-motion, visible fingerprints"` | Tactile stop-motion aesthetic |
| 28 | `"chiaroscuro lighting, extreme contrast"` | Dramatic/noir lighting shorthand |
| 29 | `"dolly zoom Vertigo effect"` | Hitchcock zoom trigger |
| 30 | `"direct address to camera, sustained eye contact"` | News, tutorial, documentary talking head |

---

## 4. Decision Tree: Desired Result → Recommended Approach

```
WHAT DO YOU WANT?
│
├── Generate from scratch (text only)
│   ├── Single shot, precise control → Veo 3.1 with 5-part formula
│   ├── Single shot, creative/world-grounded → Gemini Omni Flash
│   └── Multi-shot narrative → Veo 3.1 with timestamp format
│
├── Animate an image
│   ├── Character consistency critical → Ingredients to Video (Veo 3.1)
│   ├── Scene continuation → First frame only (Veo 3.1)
│   └── Style transformation → Gemini Omni Flash (conversational)
│
├── Edit existing video
│   ├── Change background/style/elements → Gemini Omni Flash (conversational)
│   ├── Add/remove objects → Veo 3.1 Add/Remove Object tool
│   └── Extend clip duration → Veo 3.1 Extension
│
├── Character-consistent series
│   ├── Using your own face → Omni Avatar system
│   ├── Using reference images → Ingredients to Video (3–4 refs)
│   └── Text-only consistency → Detailed verbatim character description template
│
└── Programmatic / API generation
    ├── GA today → Veo 3.1 on Vertex AI
    ├── Coming soon → Omni Flash API
    └── Budget-critical → Veo 3.1 Fast at $0.10–0.15/sec
```

---

## 5. Cheat Sheet Tables

### Camera Movement

| Intent | Phrase |
|---|---|
| Dramatic approach | `slow dolly in` |
| Mystery/reveal | `dolly out revealing wider environment` |
| Following subject | `tracking shot alongside` |
| Surveillance | `static locked-off` |
| Epic scale | `crane shot ascending from low to aerial` |
| Documentary | `vérité handheld, subtle shake` |
| Floating dream | `Steadicam glide through space` |
| Aerial reveal | `drone orbit, slow clockwise rotation` |
| Psychological unease | `Dutch angle, 15-degree canted tilt` |
| Shock/scale warp | `dolly zoom Vertigo effect` |
| First-person immersion | `POV first-person point of view` |
| Sweeping geography | `slow pan left to right, wide revealing shot` |

### Shot Scale

| Scale | Phrase |
|---|---|
| Intimate detail | `extreme close-up ECU` |
| Face/expression | `close-up CU` |
| Chest up | `medium close-up MCU` |
| Waist up | `medium shot MS` |
| Full body + context | `wide shot WS` |
| Landscape | `extreme wide establishing shot` |
| Conversation | `two-shot, both characters in frame` |
| Speaker + listener | `over-the-shoulder OTS` |

### Lighting Quick Reference

| Mood | Phrase |
|---|---|
| Drama | `Rembrandt lighting, triangular highlight, deep shadow` |
| Romance | `candlelight only, warm amber, catchlights in eyes` |
| Thriller | `split lighting, half face bright, half in darkness` |
| Horror | `single bare bulb, deep shadow, no fill` |
| Corporate | `three-point studio, clean catchlights, no harsh shadows` |
| Action | `high-contrast daylight, strong directional sun` |
| Sci-fi | `cold fluorescent, blue LED accent, monitor glow` |
| Naturalistic | `motivated practical lighting only` |
| Golden hour | `warm low-angle sunlight, long shadows, amber-gold` |
| Night | `sodium vapor orange, neon color spill, wet reflections` |

### Color & Grade

| Genre | Grade Reference |
|---|---|
| Action/blockbuster | `teal-and-orange Hollywood grade` |
| Prestige drama | `desaturated, muted, lifted shadows, Roger Deakins` |
| Horror | `cool desaturated, bleach bypass feel, crushed blacks` |
| Sci-fi | `cool blue grade, neon accent colors` |
| Romance | `warm amber, Kodak Vision3, golden skin tones` |
| Documentary | `naturalistic, accurate color, no stylistic grade` |
| Period drama | `warm sepia hints, film stock emulation, gentle grain` |
| Music video | `saturated, bold palette, high contrast` |
| Social/lifestyle | `faded shadows, lifted blacks, matte Instagram look` |

### Audio Quick Reference

| Need | Phrase |
|---|---|
| Dialogue (explicit) | `She says: [text]. (No subtitles.)` |
| Tension/dread | `Score: none. Ambient: near-silence, distant [source].` |
| Epic emotion | `Score: full orchestral swell, building to climax.` |
| Horror | `Silence as dominant audio element.` |
| Documentary | `Ambient: [environment]. No score.` |
| Action | `SFX: impacts, crowd, debris. Score: driving percussion.` |
| Romance | `Ambient: [intimate setting]. Score: solo acoustic guitar.` |
| Luxury product | `Close-mic SFX: [material sound]. Score: single piano chord.` |
| Studio audience prevention | Specify: `Ambient: [actual environment sounds]` explicitly |
| Subtitle prevention | Use `(no subtitles)` and colon format, not quotes |

### Film Stock / Camera References

| Look | Reference |
|---|---|
| Warm cinematic drama | `35mm Kodak Vision3 5219` |
| Cool prestige drama | `ARRI Alexa, natural color science` |
| High-energy commercial | `RED Komodo, high dynamic range` |
| Fashion/luxury | `Sony Venice, pastel skin tones` |
| Retro/nostalgic | `Kodak Ektachrome, vivid slide film` |
| Vintage indie | `16mm film, heavy grain, high contrast` |
| Found footage | `VHS camcorder, tracking lines, color bleed` |
| Authentic social/UGC | `natural smartphone zoom` |
| Horror atmosphere | `vintage anamorphic, vignette, grain` |

---

## 6. The 20 Genres at a Glance

| Genre | One-Line Formula |
|---|---|
| Narrative Drama | `MCU slow dolly + Rembrandt lighting + single practical + solo instrument score + no score resolution` |
| Action/Thriller | `Tracking shot + eye level + vérité jostle + teal-orange grade + SFX-only audio` |
| Horror (slow-burn) | `Static locked-off + deep perspective + silence + single motivating movement + vintage grain` |
| Horror (jump-scare) | `CU buildup + silence + SMASH CUT + bass impact + black` |
| Hard Sci-Fi | `Slow drift wide + real physics + fluorescent/monitor light + ambient hum only + deep focus` |
| Space Opera | `Crane extreme wide + scale description + orbital camera + full brass score + anamorphic` |
| Fantasy/Epic | `Crane reveal + real architectural ref + dawn light gradient + wordless vocal + IMAX feel` |
| Romance | `Handheld medium + candlelight + golden Kodak grade + fingerpicked guitar + implied silence before words` |
| Broad Comedy | `Static eye level + absurd visual juxtaposition + no score + kitchen ambience` |
| Deadpan Comedy | `Static MCU + 2-second pause + one blink + AC hum + mockumentary` |
| Observational Doc | `Handheld vérité + subject ignores camera + natural light + no score + no narration` |
| Interview Doc | `MCU + off-camera eyeline + three-point warm lighting + room tone + no score` |
| Performance Music Video | `Slow dolly MCU→ECU + single spotlight + monochrome + pop ballad score` |
| Narrative Music Video | `Match cut across time + matching score thread + warm grade + anamorphic` |
| Luxury TVC | `Macro ultra-slo-mo + black infinity + rim lights + close-mic SFX + single piano chord` |
| Automotive TVC | `Wheel-arch tracking + golden hour + engine note as score + no driver` |
| Social/UGC | `"Selfie video of" + 9:16 vertical + arm visible + natural light + phone grain` |
| Product Video | `JSON format + orbiting camera + infinity cove + material ASMR` |
| Corporate Explainer | `Direct address MCU + three-point studio + clean catchlights + soft sting post-dialogue` |
| Trailer/Teaser | `Wide silence → SMASH CUT CU → rapid cuts → score drop → black` |

---

## 7. Common Mistakes & Fixes

| Mistake | Why It Fails | Fix |
|---|---|---|
| `"A sad woman walks slowly"` | "Sad" doesn't generate specific behavior | `"A woman walks with hunched shoulders, steps dragging, looking at the ground"` |
| `"No buildings or roads visible"` | Negative instruction less reliable | `"A desolate open plain, no structures, horizon to horizon"` |
| `"She runs while the camera zooms and also pans"` | Compound movements produce confused output | `"Tracking shot alongside her as she runs"` — one movement only |
| `"She says: 'I can't do this anymore.'"` | Quotation marks trigger subtitle burn-in | `"She says: I can't do this anymore. (No subtitles.)"` |
| Vague lighting: `"good lighting"` | Model defaults to generic | `"Soft window light from camera right, warm fill from camera left"` |
| No audio spec | Model invents inappropriate audio | Always specify ambient + score/no score explicitly |
| Pattern in wardrobe | Inconsistent across shots | Use solid colors, specify hex code, no patterns |
| Prompt over 600 words | Model ignores later elements | Cut to 150–350 words; use timestamp format for multi-shot |
| "She performs a complex dance sequence involving 12 specific moves" | Too many concurrent actions | One action per prompt: "She executes a slow pirouette, arms extended" |
| No "no subtitles" | Burned-in captions | Add `(no subtitles)` to any prompt with dialogue |
| "Photorealistic perfect" | Generic quality directive | Specify film stock/camera reference instead |

---

## 8. 20 Ready-to-Use Prompt Recipes

```
1. DRAMA — THE DECISION MOMENT
Medium close-up, slow dolly in. A man, late 50s, grey stubble, weathered jacket, 
no tie — sits alone at a bar, closing time, empty glasses around him. He stares at 
a phone on the table, screen facing down. He doesn't pick it up. Score: distant 
piano, single phrase, trailing off. Ambient: low bar hum, clink of a glass 
being collected off-screen. Shot on ARRI Alexa. Desaturated warm grade. 
24fps. 16:9. (No dialogue.)

2. ACTION — THE CHASE
Tracking shot alongside a motorcyclist threading through downtown traffic at night.
Camera at wheel level, 35mm, tracking from the side. Rain-slicked streets, 
neon reflections. The rider leans into turns. No music — engine note, tires, rain, 
distant siren. Teal-orange grade, high contrast. Shot on RED Komodo. 24fps. 16:9.

3. HORROR — THE HALLWAY
Static locked-off. A long hotel corridor, symmetrical, red carpet, numbered doors. 
Dead silent. A door at the far end opens — just a crack. Nothing comes out. 
Score: none. Ambient: near-silence, air conditioning, faint electrical hum. 
Shot on 16mm film aesthetic, slight grain, vignette. 24fps. 16:9.

4. SCI-FI — FIRST CONTACT
Slow camera drift in from extreme wide. Two figures — scientists in utilitarian 
jumpsuits — stand at the base of an object that has no right angles, no 
recognizable geometry, hovering 3 meters off the surface of a grey-dust world. 
Jupiter is visible above the horizon. Score: sparse electronic, a single 
repeating tone. Ambient: suit life support, wind over vacuum. No dialogue. 
Deep focus. Cool blue grade. ARRI Alexa. 24fps. 2.39:1.

5. ROMANCE — ALMOST
Handheld medium shot. Two people in their 30s, a café table between them, 
late night, chairs stacked behind them. Their hands almost touch. 
Neither speaks. Score: solo acoustic guitar, quiet. Ambient: rain outside, 
espresso machine cooling. Candlelight only — warm catchlights in both eyes. 
Kodak Vision3 grade, skin tones golden. 24fps. 16:9. (No dialogue.)

6. COMEDY — THE EXPERT
Static medium shot, eye level. A man in a full hazmat suit attempts to fold 
a paper crane at a kitchen table. He fails. He tries again. He fails differently. 
He looks up at the camera once, briefly, then returns to the paper crane. 
Score: none. Ambient: kitchen quiet, birds outside. 24fps. 16:9. 
(No subtitles.)

7. DOCUMENTARY — THE CRAFT
Handheld medium. A bookbinder, 70s, in a small workshop, hands working precisely — 
stitching signatures into a spine. She doesn't look at the camera. Ambient: the 
specific sounds of her tools: needle through paper, thread tension, bone folder. 
No score. Natural overcast light from window. 24fps. 16:9.

8. MUSIC VIDEO — THE PERFORMANCE
Medium shot to extreme close-up, slow dolly in over 8 seconds. A singer, 
spotlight from directly above, black background, silver dress. She sings — 
performance expressive, not scripted. Lens flares from overhead spot. 
Score: powerful pop ballad, her own voice, emotional climax. 
Monochrome, slight silver retention. Anamorphic 2.39:1. 24fps.

9. LUXURY TVC — THE POUR
Ultra slow motion macro. A champagne flute receiving a pour — crystalline 
cascade, bubbles forming. Static, black infinity background. Two soft rim 
lights from behind, tiny front fill. SFX: close-mic pour, intimate. 
Score: single sustained piano chord. Color: champagne gold and white. 
No text, no narration. ARRI Alexa, T1.4. 16:9. 24fps.

10. AUTOMOTIVE TVC — THE CURVE
Low angle tracking shot, mounted at wheel arch height, alongside a dark grey 
sports car navigating a mountain hairpin at golden hour. Car sharp, road blurs. 
Specular highlight travels the door panel. SFX: precise mechanical engine note. 
No music — engine note is the music. Warm sky, cool road. ARRI Alexa. 24fps. 
16:9. (No driver visible.)

11. SOCIAL — THE DISCOVERY
Vertical 9:16. Selfie video, a creator in their late 20s in a crowded 
Marrakech souk at dusk. Natural smartphone zoom. Arm visible. She turns to 
show the spice stalls, then back to camera. She says: Okay I have been here 
ten minutes and I need to live here. (No subtitles.) Natural golden light, 
market ambient. No score. Phone grain. 24fps.

12. PRODUCT — THE REVEAL
Orbiting medium close-up, slow 360-degree camera orbit around a perfume bottle
on a black reflective surface. Rear rim lights, fog machine low haze catching 
light. At 4 seconds: stopper lifts in slow motion, fragrance mist emerges. 
SFX: close-mic material sound, soft ambient electronic score. 
Color: deep navy and gold. No text. 16:9. 24fps.

13. CORPORATE — THE STATEMENT
Medium shot, clean studio, neutral grey background. A woman, 50s, 
professional grey suit, speaks directly to camera. She says: The decisions 
we make this decade will define the next fifty years. (No subtitles.) 
Three-point warm studio lighting, clean catchlights. Ambient: room tone. 
Score: none during speech — soft two-bar piano sting after. 16:9. 24fps.

14. HORROR — THE REFLECTION
Extreme close-up: an eye. Static. 8 seconds. The eye looks left. Then right. 
Then — very slowly — it looks directly at camera for the first time. 
Score: none. SFX: none. Pure 440Hz sine tone begins at 00:04, 
imperceptibly building. Color: desaturated, crushed shadows. 
16mm grain. 24fps. 16:9.

15. ANIMATION — THE JOURNEY
2D gouache hand-painted animation. A small girl in a red coat traverses 
an enormous mushroom forest — mushrooms twice her height, glowing from 
within amber light. Parallax layers active. Score: xylophone-led whimsical 
orchestra, childlike wonder. Ambient: gentle forest wind. 12fps on twos, 
24fps container. 16:9.

16. ANIME — THE FAREWELL
Japanese anime aesthetic, Ghibli-inspired. A teenage girl, sailor uniform, 
dark braids, stands on a train platform in summer dusk. The last train 
departs — wind lifts her braids and hem. Tears forming, not falling. 
Score: piano and acoustic guitar, emotional restraint. 
Ambient: train fading, crickets beginning. Static wide, subject right third. 
Hand-painted backgrounds. 16:9. 24fps.

17. FOUND FOOTAGE — THE DOOR
VHS camcorder aesthetic, 4:3 aspect. Heavy grain, tracking artifacts. 
Three people with flashlights approach an abandoned building at night. 
Camera operator visible in window reflection. One says: 
I really don't think this is a good idea. (No subtitles.) 
Score: none. Ambient: wind, their own footsteps, distant animal. 
Green-cast VHS color shift. 24fps.

18. TRAILER STINGER — THE BEGINNING
Wide shot, total silence, 2 seconds: a lone figure stands at the center 
of a devastated city, back to camera, red sky.
SMASH CUT: ECU of the figure's eyes — haunted, resolved. 
Massive brass impact hits on the cut. 3 rapid cuts: falling debris, 
a child running, a door sealing. Score intensifies.
Wide shot: figure turns to camera. Score drops. 1 second silence. 
Voice: Something is coming. Black. 2.39:1. ARRI Alexa. 24fps.

19. EXPERIMENTAL — THE MATERIAL
Extreme close-up macro of slowly pouring honey over rough wooden surface. 
Static camera. No movement except the honey. Score: none. SFX: none. 
A tone — 220Hz — begins at 00:04, rises 1 octave by 00:08. 
Color: warm amber monochrome. Heavy grain. No narrative. 
No resolution. 8 seconds total. 16:9.

20. NEWS — THE REPORT
Medium shot, news studio. An anchor, professional, 50s, at a desk with 
a neutral map backdrop behind. She faces camera directly, controlled tone. 
She says: Officials have not yet commented on the timeline. 
An investigation is ongoing. (No subtitles.) Three-point broadcast studio 
lighting, clean, no shadows on backdrop. Ambient: studio air-conditioning. 
No score. 16:9. 30fps broadcast.
```

---

## 9. Iteration Playbook

### When Your First Generation Is Wrong

| Problem | First Change | If Persists |
|---|---|---|
| Wrong shot size | Specify more explicitly: "MCU, waist to top of head" | Add "(that's the framing)" as an anchor |
| Wrong lighting | Name the source: "lit only by [source]" | Remove all other style elements and test lighting in isolation |
| Character looks wrong | Add more physical detail; add hex codes for colors | Use Ingredients to Video with reference image |
| Audio is wrong | Add explicit ambient spec; add "no score" if unwanted | Specify every audio layer individually |
| Too much camera movement | Add "static, locked-off" or "minimal camera movement" | Test with no movement phrase first, then add |
| Physics wrong | Add "physics accurate" / "gravity correct" | Reframe as stylized animation where physics errors are acceptable |
| Subtitles appearing | Add `(no subtitles)` explicitly, use colon dialogue format | Repeat "No subtitles. No subtitles!" multiple times |
| Wrong style overall | Remove style phrases and rebuild one at a time | Add film stock reference as first style signal |

### The Single-Variable Rule

When iterating: change **one thing at a time**. Changing multiple elements simultaneously makes it impossible to know what fixed the problem. Treat each generation as an experiment.

### Multi-Attempt Strategy

- **Attempt 1:** Full prompt, 4 variants (sampleCount: 4)
- **Attempt 2:** Same prompt, different seed — if result was 80% correct
- **Attempt 3:** Targeted refinement of single failing element
- **Attempt 4+:** If fundamentally wrong after 3 attempts, rebuild from scratch

### When to Use Conversational Editing (Omni)

Once you have a clip that's "80% right" in Gemini Omni — switch to conversational editing mode:
```
"Change only the background to a night cityscape"
"Make the lighting warmer"
"Have her look directly at camera at the end"
"Remove the tree on the left"
```
Each instruction builds on the last. Character, physics, and scene memory are preserved.

---

## 10. Parameter Quick Reference

| Parameter | Values | Pro Tip |
|---|---|---|
| `aspectRatio` | `"16:9"` (default), `"9:16"` | Set in API; can't be overridden by prompt text alone |
| `durationSeconds` | 4, 6, 8 (Veo); 10 (Omni) | Use 4–6 for tight character shots; 8 for environment-heavy |
| `resolution` | `"720p"`, `"1080p"`, `"4k"` | 4K unavailable in Lite; extension caps at 720p |
| `sampleCount` | 1–4 | Always use 4 on first prompt test |
| `seed` | Integer | Same seed + same prompt = consistent variants for refinement |

**Pricing Quick Reference (Veo 3.1, May 2026):**

| Tier | $/sec | Use For |
|---|---|---|
| Veo 3.1 Fast (no audio) | ~$0.10 | Drafts, iteration, social clips |
| Veo 3.1 Fast (with audio) | ~$0.15 | Audio draft testing |
| Veo 3.1 Standard 1080p | ~$0.40–$0.50 | Final production deliverables |
| Veo 3.1 Standard 4K | ~$0.60–$0.75 | Broadcast, premium delivery |
| Consumer (Google AI Plus) | $19.99/mo | ~90 Veo 3.1 Fast videos/month |
| Consumer (Google AI Ultra) | $249.99/mo | ~1,250 videos/month via Flow |

---

## 11. Anti-Patterns — What Never to Do

These consistently produce poor results. Avoid them entirely.

1. **"Make a beautiful cinematic video of..."** — "Beautiful" and "cinematic" are too vague; specify HOW
2. **"A person walking"** — No specifics; the model defaults to the most generic possible output
3. **`"no man-made structures"`** instead of **"an open plain with only grass and sky"** — descriptive avoidance works better than explicit negation
4. **Multiple actions in one prompt:** "she runs while he talks while the camera zooms and pans" → always fails
5. **Pattern clothing for consistency shots:** "wearing a floral dress" → will look different in every generation
6. **Dialogue in quotation marks without `(no subtitles)`** → burned-in captions are nearly guaranteed
7. **Prompts over 600 words** → late elements are ignored; model defaults on specifics
8. **Requesting real celebrities by name** → always refused; describe physically instead
9. **Asking for complex hand actions in full-body shots** → high failure rate for hand anatomy
10. **"High quality 8K photorealistic masterpiece ultra HD"** → quality buzzwords do nothing; film stock references do everything
11. **No audio specification** → model invents inappropriate audio (studio audiences, wrong music)
12. **Asking for three different camera angles in one prompt** → the model picks one; specify one dominant movement per clip
13. **Complex hair styles (curls, waves) in character consistency workflows** → guarantees variation between shots; use simple styles
14. **Jewelry and accessories in character consistency workflows** → inconsistencies compound; simpler is always more consistent
15. **"Shot on iPhone, perfect cinematic quality, ARRI Alexa look"** → contradictory signals; pick one aesthetic register

---

*Last updated: May 22, 2026. Model: Gemini Omni Flash (Google I/O 2026) + Veo 3.1 (October 2025). Verify capability changes at deepmind.google/models/gemini-omni/ and ai.google.dev/gemini-api/docs/video.*

