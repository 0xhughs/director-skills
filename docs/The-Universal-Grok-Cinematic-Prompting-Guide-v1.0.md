# The Universal Grok Cinematic Prompting Guide
### A system for turning any scenario into a high-control Grok/Aurora cinematic video prompt

This guide teaches any capable LLM how to write Grok Imagine / Aurora video prompts using the systems from the Master Guide V3.2 and Grok Genre Expansion v1.0. It is written as an operational manual. Feed this file to an LLM with a user's scene idea, and the LLM should return a compact, directorial, Aurora-readable prompt.

The goal is not to write poetic descriptions. The goal is to direct the rendering engine.

---

## HOW TO USE THIS GUIDE

When a user describes a scene they want generated, follow this process in order:

1. **Understand the scene.** Identify subject, setting, action, emotional tone, genre, aspect ratio, duration, audio needs, and whether reference images are attached.
2. **Ask only if essential.** Ask for missing essentials only when they would change the prompt. Otherwise infer confidently and flag the assumption.
3. **Choose the correct workflow.** Use text-to-video for simple concepts. Use image-first for serious cinematic, identity, product, hand, or style-critical outputs.
4. **Front-load the prompt.** Put the genre/style anchor, subject, primary action, and setting in the first 20 to 30 words.
5. **Plan with the 7 pillars.** Use the 7-pillar structure internally, then convert it into flowing directorial prose.
6. **Use narrative sequence, not timestamp brackets.** Grok/Aurora responds better to "First... then... suddenly..." and to `Camera switch.` / `Cut to:` than to bracketed timecodes.
7. **Append explicit audio.** Always use an `AUDIO:` tail block, even when the desired audio is silence or natural ambience.
8. **Close with stability.** End every prompt with a stability clause such as `Keep facial identity consistent throughout. Single subject only. 24fps cinematic.`
9. **Run the checklist.** Verify prompt economy, one camera move, physical consequences, guardrails, audio, and genre-specific failure fixes.

Your job is to translate the user's vision into a precise, cinematic, AI-readable prompt. Do not impose a new story. Do not over-expand a simple idea. Do not turn a one-beat scene into a trailer unless the user asks.

---

## THE GOLDEN RULES

### Direct the engine, do not decorate the idea

Aurora understands directorial prose better than keyword piles. Write what appears, what changes, how the camera behaves, what the light does, what physics apply, and what the audio contains.

Weak:
```
knight, castle, cinematic, 8K, dramatic, epic
```

Strong:
```
Epic high fantasy. A mud-streaked knight in dented brass armor staggers through a ruined castle gate at dawn, gripping a cracked sword with both hands. Low-angle 35mm tracking shot, cold mist curling around his boots, torchlight flickering across wet stone.
```

### Front-load what matters most

The first 20 to 30 words carry the strongest semantic weight. Always start with:

```
[Genre/style anchor] + [subject] + [primary action] + [setting]
```

Correct:
```
Cinematic cyberpunk thriller. A lone hacker in a translucent black raincoat steps out of a ramen stall in Neo-Kowloon at 2 AM...
```

Incorrect:
```
Shot on ARRI Alexa with Cooke S7/i at T2.0 with anamorphic lens flares in a rainy neon city, a lone hacker...
```

### Write positive commands

Grok/Aurora does not use a traditional negative prompt field. Negative wording often reinforces the unwanted concept. Replace negatives with positive visible instructions.

| Instead of | Use |
|---|---|
| `no blur` | `sharp focus, clean facial detail` |
| `no extra characters` | `single subject only, empty background` |
| `no CGI smoothing` | `visible pores, natural skin texture, translucent sub-surface scattering` |
| `no floating movement` | `heavy physical weight, realistic gravity, grounded momentum` |

Exception: `no music` and `no score` can work because they describe audio track contents.

### Respect prompt economy

Optimal Grok cinematic prompts are usually 50 to 150 words. Above 200 words, details dilute and behavior becomes chaotic. Strip filler such as "we see," "there is," and "the camera shows."

Use:
```
Muscular man crying in heavy rain, bloodshot eyes, wet eyelashes, chest heaving.
```

Avoid:
```
We see a muscular man who is crying and there is heavy rain and the scene is very emotional.
```

---

## THE MASTER OUTPUT TEMPLATE

Use this as the final prompt shape. The final prompt should be plain text, not a markdown table. Keep it concise.

```
[FRONT-LOAD: genre/style anchor + subject + primary action + setting.]

[Camera body or format], [lens and focal length], [aspect ratio], [shot type], [one camera movement]. [Subject description with age/features/wardrobe/posture]. [Action with intensity modifier and physical consequence]. [Setting with depth, atmosphere, and texture]. [Lighting source and direction]. [Color grade or film stock]. [Micro-textures and physics guardrails.]

[If multi-beat: Then... / Suddenly... / Camera switch. / Cut to: ...]

AUDIO: [room tone], [foley tied to visible action], [score or no score], [dialogue/voice if needed].

Keep [identity/composition/product/detail] stable. Single subject only. 24fps cinematic.
```

### Image-to-video motion template

When a reference image or generated still already contains the visual design, do not re-describe the image. Describe only what changes.

```
Animate [specific element] with [subtle/strong motion]. Add [single camera move] and [ambient change]. Keep [identity/composition/product detail] stable.
```

Example:
```
Animate the woman's wet hair and jacket fabric with subtle wind. Add a slow camera push-in as neon rain reflections ripple behind her. AUDIO: muffled city rain, distant traffic, low dark synth pad. Keep facial identity and composition stable. Single subject only. 24fps cinematic.
```

---

## HARD FORMATTING RULES

| Rule | Right | Wrong |
|---|---|---|
| Prompt style | Flowing directorial prose | Keyword pile |
| Timing | `First... then... suddenly...` | `[0:00-0:03]` bracket timestamps |
| Transitions | `Camera switch.` or `Cut to:` | Vague "next shot" wording |
| Camera movement | One clear move per clip | Push-in + orbit + crane + whip pan |
| Audio | Dedicated `AUDIO:` tail block | Unspecified generic music |
| Stability | Prompt closes with stable identity/composition | Prompt ends abruptly |
| Negatives | Positive visible instructions | `no bad anatomy, no blur, no extra...` |
| Reference tags | Weave `@Image1` directly into prose | Put tags in isolated metadata with no action |

---

## DURATION AND COMPLEXITY LOGIC

Grok/Aurora handles short clips best when each clip has one strong idea. For complex scenes, generate multiple clips and edit them together.

| Clip Type | Best Duration | Best Structure |
|---|---:|---|
| Single portrait / product / mood beat | 5 to 8 seconds | One camera move, one action |
| Dialogue line | 6 to 10 seconds | One speaker per clip |
| Action moment | 5 to 8 seconds | One impact, one physical consequence |
| Mini narrative | 10 to 15 seconds | Two beats maximum, use `Camera switch.` |
| Trailer sequence | Multiple clips | Build separate establishing, character, conflict, reaction beats |

If the user asks for too many actions in one clip, compress the idea or split it. Beyond two beats per clip, coherence degrades.

---

## THE 7-PILLAR PLANNING SYSTEM

Use these pillars internally before writing the final prose. Do not output them as rigid labels unless the user asks for a planning breakdown.

1. **Camera Specs.** Camera body or format, lens, focal length, aspect ratio, frame-rate feel, optical imperfection.
2. **Camera Movement.** One movement, one shot type, optional official transition trigger.
3. **Subject & Action.** Identity, wardrobe, posture, emotional anatomy, action verb, physical consequence.
4. **Setting & Depth.** Location, depth of field, foreground/background, atmosphere.
5. **Micro-Textures.** Skin, fabric, particles, surfaces, moisture, decay, physical material detail.
6. **Physics & Motion.** Weight, gravity, object permanence, cloth, hand/finger guardrails, lip isolation.
7. **Lighting & Finish.** Directional light source, color grade, film stock, grain, halation, final look.

Then add:

```
AUDIO: [six-layer audio direction]
Keep [identity/composition/detail] stable. Single subject only. 24fps cinematic.
```

---

## CAMERA LANGUAGE

### Camera bodies and formats

Choose one camera/format token that matches the desired look.

| Look | Prompt Token | Effect |
|---|---|---|
| Premium cinema | `ARRI Alexa Mini LF` / `ARRI Alexa 65` | Natural skin, highlight roll-off, cinematic warmth |
| Gritty sharp realism | `RED V-Raptor` / `RED Monstro 8K` | Hyper-detailed, punchy, high contrast |
| Large-scale epic | `IMAX 65mm` / `IMAX 70mm Film` | Monumental scale, clean detail |
| Indie / vintage | `16mm film` / `Super 16` / `Bolex H16` | Organic grain, softer image |
| Neon / low light | `Sony Venice 2` | Clean shadow detail, vibrant color |
| Slow motion | `Phantom Flex 4K` | Slow-motion language responds better |
| Found footage | `VHS camcorder` / `handheld camcorder` | Scan lines, noise, color bleed |
| Social / UGC | `iPhone 15 Pro front camera` | Natural phone look, handheld micro-pulses |

### Lens and focal length

Always pair focal length with the word `lens`.

| Lens | Use |
|---|---|
| `14mm / 16mm / 18mm lens` | Horror distortion, chaos, cramped spaces |
| `24mm wide lens` | Action, establishing, environmental motion |
| `35mm lens` | Documentary realism, street scenes, natural perspective |
| `50mm lens` | Grounded neutral perspective |
| `85mm portrait lens` | Intimacy, romance, emotional close-ups |
| `100mm macro lens` | Texture, product, eyes, object detail |
| `200mm telephoto lens` | Surveillance, compression, isolation |
| `anamorphic lens` | Scope, horizontal flares, blockbuster feel |
| `fisheye lens` | Found footage, extreme sports, stylized distortion |

### Camera movement

Use exactly one camera movement per clip.

| Move | Prompt Phrase |
|---|---|
| Static | `static locked-off frame` |
| Push-in | `slow camera push-in` / `slow dolly in` |
| Pull-back | `camera pull-back reveal` |
| Tracking | `tracking shot` / `parallax tracking` |
| Handheld | `handheld with organic human jitters, slight instability, subtle breathing motion` |
| Whip pan | `whip pan with extreme directional motion blur` |
| Orbit | `slow 360-degree orbit` |
| Rack focus | `rack focus from [A] to [B]` |
| FPV drone | `FPV drone dive, fast aggressive agile` |
| Snorricam | `Snorricam, body-mounted, face locked at center, background moving chaotically` |

### Shot type

| Shot | Use |
|---|---|
| Extreme wide / establishing | Scale, geography, isolation |
| Wide shot | Full body plus environment |
| Medium shot | Character and action balance |
| Medium close-up | Dialogue, face and shoulders |
| Close-up | Emotion and reaction |
| Extreme close-up | Eyes, hands, suspense, but avoid moving face ECUs if waxiness appears |
| Over-the-shoulder | Conversation or reveal |
| POV | Immersion, subjectivity |
| Insert shot | Product, prop, clue, hand detail |

For full-body shots, include `boots and floor visible`. For extreme wides, include `tiny silhouette` if the model keeps zooming in.

---

## SUBJECT, ACTION, AND PERFORMANCE

### Character description formula

```
[Age range] + [distinct physical feature] + [clothing material/detail] + [emotional state] + [body posture]
```

Example:
```
Weathered male detective in his 50s, salt-and-pepper stubble, rumpled brown wool trench coat, collar turned up, shoulders hunched, scanning the alley with quiet suspicion.
```

### Use cinematic verbs

| Generic | Better |
|---|---|
| moves | surges, drifts, lunges, glides, stumbles, hurtles |
| looks | scans, peers, glares, studies, stares wide-eyed |
| walks | strides, slinks, staggers, prowls, marches |
| runs | sprints, bolts, scrambles, charges, flees |
| falls | collapses, crumbles, tumbles, plummets |
| hits | strikes, slams, smashes, impacts, shatters |
| speaks | mutters, shouts, whispers, gasps, growls |

### Action must create consequence

Never state an action without its physical result.

Weak:
```
He falls.
```

Strong:
```
He collapses onto the wet concrete with heavy physical momentum, shoulder striking first, water splashing outward, dust and grit sticking to his sleeve.
```

### Write anatomy, not abstract emotion

Aurora understands physical symptoms better than labels.

| Emotion | Use Physical Detail |
|---|---|
| Grief | bloodshot sclera, damp eyelashes, quivering chin, single glistening tear track |
| Anger | flared nostrils, clenched jaw, bulging temple veins, twitching cheek muscle |
| Shock | slack jaw, widened pupils, frozen facial muscles, sudden loss of color |
| Suppression | rapid blinking, swallowing hard, tense neck tendons, forced stillness |
| Fear | shallow breathing, shoulders raised, eyes darting, lips parted but silent |

Do not write "very emotional." Write what the body does.

---

## SETTING, TEXTURE, PHYSICS, AND LIGHT

### Setting depth

A strong setting has foreground, subject plane, background, and atmosphere.

Useful phrases:

- `foreground silhouettes partially obscuring the frame`
- `rain-soaked neon reflections on wet asphalt`
- `dust motes floating in a shaft of light`
- `fog rolling through broken windows`
- `heat haze shimmering above the road`
- `snow falling softly in the background`
- `volumetric god rays piercing storm clouds`

### Micro-texture shield

Use micro-textures to prevent plastic or video-game aesthetics.

```
Visible pores, translucent sub-surface scattering, flushed capillaries, glistening micro-sweat, individual fabric weave, scuffed concrete, suspended dust motes.
```

### Physics guardrail

Use this when realism matters:

```
Heavy physical weight, realistic gravity, grounded momentum. Accurate fluid dynamics. Strict object permanence. Zero morphing. Consistent skeletal anatomy. Realistic cloth simulation.
```

If full-speed motion is required, add:

```
real-time speed, no slow motion.
```

### Hand and finger workaround ladder

Hands are a common failure point. Prefer these in order:

1. Hide hands: `hands in pockets`, `hands behind back`
2. Cover hands: `leather gloves`, `tactical gloves`
3. Occupy hands: `gripping a steering wheel`, `holding a coffee mug`
4. Crop hands: `framed chest-up, hands out of frame`
5. Slow gestures: `one slow deliberate hand movement`
6. Lock with image-to-video: solve the hand pose in a still first

### Lighting must be directional

Do not write "dramatic lighting." Name the source, direction, and behavior.

| Weak | Strong |
|---|---|
| dramatic lighting | hard rim light from the left, deep shadow falloff |
| cinematic lighting | warm tungsten practical lamp from camera-right, soft window spill behind |
| horror lighting | harsh overhead fluorescent green ballast, deep under-eye shadows |
| beautiful light | golden hour backlight, warm halo around hair, long shadows |

### Color and finish

Choose one coherent grade or stock.

| Look | Prompt Token |
|---|---|
| Action blockbuster | `teal-and-orange color grade, crushed blacks` |
| War / gritty thriller | `bleach bypass, desaturated metallic contrast` |
| Neon noir | `magenta-cyan neon, wet asphalt reflections` |
| Romance / memory | `Kodak Portra 400, warm pastel skin tones` |
| Classic noir | `true black-and-white, no color, high-contrast film` |
| Vintage | `Super 8 film grain, light leaks, gate weave` |
| Clean commercial | `crystal-clear digital cinematography, clean product highlights` |

Use only one film stock per prompt.

---

## AUDIO DESIGN

Always end with an explicit `AUDIO:` block. If you do not specify audio, Grok may add generic background music.

### The 6 audio layers

| Layer | What to Specify |
|---|---|
| Room tone | space, silence, air, reverb, environmental bed |
| Foley | sounds caused by visible action |
| Active sync | dialogue, singing, mouth movement, lip sync |
| Passive sync | character reacts to music without singing |
| Score | genre, instrument, energy |
| Dynamic arc | how sound builds, cuts, or changes |

### Audio examples

Natural ambience:
```
AUDIO: dry close room tone, faint fluorescent buzz, fabric rustle, no music, no score.
```

Action:
```
AUDIO: heavy boots splashing through wet asphalt, metallic clatter, distant sirens, driving orchestral percussion building under the chase.
```

Horror:
```
AUDIO: low room tone, distant pipe knocks, breath close to microphone, dissonant string drone rising into sudden silence.
```

Music performance:
```
AUDIO: lips synced to lyrics, head nodding to rhythm, saturated pop vocal, tight kick and bass, crowd wash behind.
```

Passive listening:
```
AUDIO: lo-fi hip hop beat from car speakers, character tapping fingers to rhythm, no singing, no mouth movement to lyrics.
```

### Dialogue rules

Use this format:

```
[Character] [adverb]: "[exact line]"
```

Keep dialogue short. One sentence per character per 6 seconds is a safe limit. For multi-character dialogue, use one speaker per clip when possible.

For voiceover with no lip movement, use:

```
Her mouth is completely closed, lips pressed together, zero lip movement. Audio narration: "I knew I should have taken the earlier train."
```

---

## REFERENCE IMAGE AND IDENTITY RULES

When the user provides reference images, weave the tags directly into the prose.

```
A muscular man matching @Image1 sits alone in a motel bathroom, wet hair clinging to his forehead...
```

Rules:

- Use one reference tag per visual identity.
- Do not invent tags if no image exists.
- If the user changes images, update the mapping and do not reuse old wardrobe assumptions.
- For identity-critical scenes, use image-first workflow.
- End with identity stability language.

Stability examples:

```
Keep facial identity consistent throughout. Single subject only.
Maintain consistent character clothing, hair, and face across all frames.
Preserve original composition and framing. Zero additional subjects.
Keep product detail and branding elements sharp and stable throughout.
```

---

## IMAGE-FIRST PIPELINE

Use this for serious cinematic output, product shots, faces, hands, wardrobe, style matching, and anything that must remain consistent.

1. **Generate the still first.** Use Quality Mode and a full visual prompt.
2. **Review the still.** Check face, hands, text, wardrobe, composition, lighting, and artifacts.
3. **Fix the still before animation.** Animation amplifies base image flaws.
4. **Write a short motion prompt.** Keep it under 40 words when possible. Describe only what changes.
5. **Generate variations.** Rerolling can materially improve output.
6. **Extend carefully.** For longer sequences, extend from the final frame and use a continuity lock.

### Master Consistency Lock

Use this when extending a clip:

```
Seamlessly continue directly from the very last frame where [exact ending state of previous clip]. [Next action in prose]. Keep identity, wardrobe, lighting, and composition stable.
```

Do not paste the original full prompt into an extension. That causes drift.

---

## GENRE ANCHOR SYSTEM

Choose one genre anchor at the start of the prompt. Then adapt subject, action, setting, and audio around it.

| Genre | Starter Anchor |
|---|---|
| Action / Thriller | `Cinematic action thriller, anamorphic 2.39:1, teal-and-orange, low-angle handheld, Michael Mann aesthetic` |
| War | `Bleach-bypass war cinematography, shoulder-mounted handheld 24mm, Spielberg/Kaminski aesthetic` |
| Crime / Heist | `Neo-noir heist, Panavision anamorphic 35mm, Michael Mann teal-orange, motivated practicals` |
| Psychological Horror | `Psychological horror, locked-off symmetrical frame, candlelight, desaturated bruise-purple shadows` |
| Found Footage | `Found footage, VHS fisheye 8mm, chroma noise, time-code burn-in, no music` |
| Hard Sci-Fi | `Hard sci-fi, IMAX 65mm, clinical white-charcoal palette, contemplative wide frame` |
| Cyberpunk | `Cyberpunk, wet asphalt neon, magenta-cyan reflections, anamorphic 2.39:1` |
| Prestige Drama | `Prestige drama, 35mm naturalistic, muted earth tones, Kodak Portra 400` |
| Romance | `Romantic drama, 85mm portrait lens, saturated neon, slow 360-degree orbit` |
| Classic Noir | `Classic film noir, true black-and-white no color, high-contrast venetian-blind shadows` |
| Epic Fantasy | `Epic high fantasy, scope composition, volumetric god rays, golden magic-hour atmosphere` |
| Ghibli-like Animation | `Watercolor fantasy animation, soft brushstrokes, pastel emerald and sky-blue palette` |
| Coming-of-Age | `Coming-of-age indie, 35mm Zeiss lens, Kodak Portra 400, muted A24-style grade` |
| Adventure | `Adventure exploration, 24mm warm wide frame, earth-toned natural light, FPV reveal` |
| Disaster | `Disaster epic, 14mm ultra-wide, massive scale, debris and smoke with controlled particles` |
| Sports Hype | `Nike-commercial sports hype, low hero angle, Phantom Flex 4K slow-motion capability` |
| Post-Apocalyptic | `Post-apocalyptic desert action, cobalt-vs-orange contrast, rusted chrome vehicles` |
| Experimental | `Experimental art house, static observational frame, single duotone palette, surreal physics` |
| Music Video | `Music video, saturated candy palette, beat-synced snap-zooms, bold rim light` |
| Mockumentary | `Mockumentary cringe comedy, locked-off talking head, flat fluorescents, awkward silence` |
| Superhero | `Superhero spectacle, low-angle orbit, volumetric particles, teal-orange grade, glowing energy source` |
| UGC / Social | `UGC TikTok authentic, iPhone 15 Pro front camera, natural window light, 9:16 vertical` |

---

## GENRE FAILURE FIXES

| Problem | Fix |
|---|---|
| Action defaults to slow motion | Add `real-time speed, no slow motion` |
| Classic noir renders as desaturated color | Write `true black-and-white, no color` |
| Ghibli-like output becomes generic anime | Add `watercolor texture, soft brushstrokes` |
| Horror gore is softened | Imply with physical detail such as `dark stain spreading`, `split skin`, `wet torn fabric` |
| Disaster particles collapse | Use only 2 to 3 particle systems and name each separately |
| Romantic kiss warps | Use profile/three-quarter framing or cut just before lips meet |
| Multi-character dialogue moves wrong mouth | One speaker per clip, locked jaw on listener |
| Period drama faces look waxy | Pull back to MCU, avoid moving face ECU |
| Crowds collapse | Foreground hero plus silhouettes in fog or out-of-focus background |
| Hands break | Hide, cover, occupy, crop, slow, or lock in image-to-video |

---

## COMMON FAILURE MODES AND FIXES

| Problem | Diagnosis | Fix |
|---|---|---|
| Prompt feels generic | No subject-first front-load | Rewrite first sentence with genre, subject, action, setting |
| AI ignores timing | Timestamp brackets used | Use prose sequence and `Camera switch.` |
| Scene morphs | Too many actions or camera moves | Reduce to one action and one move |
| Character duplicates | Weak stability | Add `single subject only` and identity stability |
| Skin looks waxy | No micro-texture | Add pores, SSS, capillaries, sweat, grain |
| Motion feels floaty | No physics | Add weight, gravity, grounded momentum |
| Fight becomes slow | Aurora slow-motion bias | Add `real-time speed, no slow motion` |
| Hands fail | Hands exposed and moving | Hide, cover, occupy, crop, slow, or image-lock |
| Audio is generic | Missing `AUDIO:` | Add explicit room tone, foley, score, or no score |
| Dialogue lip sync fails | Too many speakers | Use one speaker per clip |
| Product changes | No product stability | Add `Keep product detail and branding elements sharp and stable` |
| Wide shot becomes close-up | Subject too important in prompt | Add `tiny silhouette`, `boots and floor visible`, or stronger wide-shot language |

---

## ITERATION LOOP

When the user gives feedback:

1. **Read the exact complaint.** Do not assume a broader problem.
2. **Make the smallest change.** Fix the broken clause, not the whole prompt.
3. **Translate casual feedback into technical edits.**
4. **Preserve what already works.**
5. **Only ask if the fix requires a creative choice.**

### Feedback translation guide

| User says | Likely Meaning | Edit |
|---|---|---|
| "Too much" | Too many actions or details | Cut actions and compress prose |
| "Make it more cinematic" | Weak camera/light/finish | Add camera body, lens, movement, directional light, grade |
| "More realistic" | Missing physics and texture | Add weight, gravity, micro-textures, grounded motion |
| "It looks AI" | Plastic/waxy/morphing | Add pores, SSS, film grain, object permanence |
| "Too slow" | Slow-motion bias | Add `real-time speed, no slow motion` |
| "The face changed" | Weak identity lock | Add reference tag and stability closer |
| "Wrong mouth moves" | Multi-character lip failure | One speaker per clip, locked jaw on listener |
| "The hands are bad" | Hand geometry failure | Hide, cover, occupy, crop, slow, or image-first |
| "The audio is weird" | Generic music/default mix | Rewrite `AUDIO:` precisely |

---

## PRE-DELIVERY CHECKLIST

- [ ] First 20 to 30 words contain genre/style, subject, action, and setting.
- [ ] Prompt is directorial prose, not a keyword pile.
- [ ] Prompt is ideally 50 to 150 words.
- [ ] No bracket timestamps.
- [ ] Uses `First... then...` or `Camera switch.` / `Cut to:` if multi-beat.
- [ ] No more than two beats in one clip.
- [ ] One camera movement per clip.
- [ ] Camera body or format chosen only if useful.
- [ ] Focal length includes the word `lens`.
- [ ] Subject has identity, wardrobe material, posture, and emotional anatomy.
- [ ] Action includes physical consequence.
- [ ] Setting has atmosphere, depth, and texture.
- [ ] Lighting names source, direction, and behavior.
- [ ] Color grade or film stock is coherent and singular.
- [ ] Micro-textures prevent plastic/waxy output.
- [ ] Physics guardrails cover weight, gravity, object permanence, and morphing.
- [ ] Hands are handled intentionally if visible.
- [ ] Crowds are simplified if more than 6 visible people.
- [ ] Dialogue is short and one speaker per clip where possible.
- [ ] `AUDIO:` block is explicit.
- [ ] Stability closer is present.
- [ ] Genre-specific failure fixes are applied.

---

## FINAL PRINCIPLES

**Front-load the core.** If the subject/action/setting appears late, Aurora under-prioritizes it.

**Prose beats tags.** Write like a director giving instructions, not like a search engine query.

**One clip, one main idea.** Split complexity across clips instead of overloading one generation.

**Physics sells realism.** Weight, gravity, contact, cloth, and object permanence matter more than empty "cinematic" words.

**Texture kills AI plastic.** Pores, sweat, dust, fabric weave, rust, grain, and atmosphere are high-yield.

**Audio must be commanded.** If you do not specify audio, Aurora may choose for you.

**Stability closes the gate.** End with identity, composition, or product stability every time.

---

*A universal system for Grok/Aurora cinematic video prompting, adapted from Master Guide V3.2 and Grok Genre Expansion v1.0.*
