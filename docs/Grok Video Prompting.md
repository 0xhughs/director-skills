# Grok Imagine Prompting Guide — Video Prompting

> **Part 3 of 6** | Video foundations, 30+ camera movements, templates, all 5 video modes (text-to-video, image-to-video, reference, editing, extension), audio and lip sync.

---

## 11. Video Prompting — Foundations

### How Video Prompts Differ from Image Prompts

Video prompting follows the same principles as image prompting but with critical constraints driven by the temporal dimension:

| Dimension | Image | Video |
|-----------|-------|-------|
| Prompt length | 50–150 words | 30–80 words |
| Scene complexity | Can be complex | One shot preferred |
| Camera moves | As many as you want | One move maximum |
| Actions | Can be multiple | One main action |
| Style | Any | Keep it simple |
| Conflicting instructions | Tolerated | Causes instability |

The shorter prompt requirement is not about the model's capacity — it's about **motion stability**. Overloaded prompts produce incoherent motion or flickering. ([GenAIntel](https://www.genaintel.com/guides/how-to-prompt-grok-imagine), [Chat4O](https://chat4o.ai/blog/detail/Grok-Imagine-AI-Video-Generation-on-Chat4O-A-Step-by-Step-Tutorial-Ready-to-Use-Prompts-25fa95f0df9d/))

### The One-Shot Rule

Each video generation is one shot. Do not try to direct a full movie in one prompt.

```
❌ Multi-scene overload:
"A woman walks through Paris, then stops at the Eiffel Tower, then sits at 
a café, then runs to catch a train, then boards it and looks out the window 
as the city fades behind her."

✅ Single shot:
"A woman in a beige trench coat walks slowly through a rain-slicked Parisian 
street at dusk, slow dolly-in following her from behind, cinematic."
```

### The Three Pillars

```
Subject + Action + Camera + Style
```

- **Subject:** Who/what is in the scene, described specifically
- **Action:** The one motion happening (verb-led)
- **Camera:** The one camera movement
- **Style:** Visual aesthetic (cinematic, anime, etc.)

Optionally add: **Lighting** + **Audio cues** + **Pacing**

### Natural Language Description

Describe motion like you're directing a scene on set:

```
"The camera slowly pushes in on the astronaut's helmet, the reflection of 
the nebula shifting as she turns her head toward the distant star."
```

Rather than:
```
"astronaut, nebula, helmet, reflection, slow push, space"
```

### Aurora's Unified Multimodal Architecture for Video

Aurora video generates synchronized audio automatically during the render pass — not in post-production. This means:

- Background music auto-generates to match scene mood
- Sound effects sync with visual events
- Dialogue auto-generates lip sync if dialogue is included in the prompt
- No separate audio editing step is required for basic content

The synchronization works because audio and visual modalities share latent representations in the training architecture. ([Vidofy AI](https://vidofy.ai/en/models/grok-imagine))

### Duration and Resolution

| Parameter | Options |
|-----------|---------|
| Duration | 1–15 seconds |
| Resolution | 480p (default, faster), 720p (HD) |

**Practical notes:**
- Short clips (6–10 seconds) tend to have more stable motion
- 15-second generations are slower and may show motion degradation
- 720p significantly increases generation time
- Free tier: 6 seconds typical
- Paid tiers: up to 15 seconds


---

## 12. Video Prompting — Component Deep Dive

### Subject Description

Same rules as image prompts — be specific. But in video, you also need to think about how the subject interacts with motion.

**Good subject descriptions for video:**
- `a woman in a flowing white dress` (clothing moves naturally)
- `a heavily modified orange off-road buggy` (vehicle + motion = natural)
- `an astronaut in a white spacesuit` (rigid = stable for orbital/floating moves)
- `a golden retriever running on a beach` (animal motion prompts work well)

**Elements that move well in video:**
- Hair, fabric, clothing
- Smoke, fog, water, fire
- Light particles, bokeh
- Facial expressions (micro-movements)
- Small hand gestures
- Vehicle motion
- Camera parallax

**Elements to keep stable:**
- Background architecture (instability = flickering buildings)
- Character identity (don't describe too loosely)
- Static props

### Action / Motion

One action per video prompt. Use specific, directed motion verbs:

**Effective action verbs for video:**

| Category | Verbs |
|----------|-------|
| Human motion | walk, turn, look up, smile, reach, crouch, leap, spin |
| Travel | sprint, stride, stagger, drift, slide |
| Object motion | open, pour, reveal, lift, shatter, fall, roll |
| Subtle human | breathe deeply, blink slowly, tilt head, nod |
| Combat | lunge, dodge, parry, sweep, strike |
| Emotional | collapse with laughter, freeze in shock, look up in awe |

**Action phrasing patterns:**

```
"...slowly turns to face the camera, expression shifting from confusion to recognition"
"...pours steaming coffee into a mug, the dark liquid swirling"
"...steps back from the window as lightning flashes outside"
"...sprints through the crowd, weaving between people"
```

### Camera Movement

Camera movement is the single most impactful variable in video prompting. Use exactly one movement per prompt.

**Full list of 30+ supported camera movements** (from [YouTube: Grok AI Camera Movement Guide](https://www.youtube.com/watch?v=6MWg-LpSRDM)):

| Movement | Prompt Keyword | Effect |
|----------|----------------|--------|
| Slow Dolly In | `slow dolly in` | Camera slowly moves toward subject; focused, emotional pull |
| Slow Dolly Out | `slow dolly out` | Camera retreats from subject; reveals context |
| Fast Dolly In | `fast dolly in` | Rapid approach; urgency, drama |
| Dolly Zoom | `dolly zoom` / `Vertigo effect` | Background scales while subject stays same size; disorienting |
| Macro Zoom | `macro zoom` | Extreme close-up pull; detail reveal |
| Hyper Zoom | `hyper zoom` | Very fast extreme zoom; shock reveal |
| Over The Shoulder | `over the shoulder shot` | POV from behind character; immersion |
| Fisheye | `fisheye lens` | Curved distortion; surreal or action |
| Reveal From Behind | `reveal from behind` | Camera moves from behind obscuring object; dramatic |
| Fly Through Shot | `fly through shot` | Camera passes through space or object; immersive |
| Reveal From Blur | `reveal from blur` / `rack focus reveal` | Focus pulls from blurred to sharp |
| Rack Focus | `rack focus` | Focus shifts from foreground to background or vice versa |
| Tilt Up | `slow tilt up` | Camera tilts upward; reveals height or sky |
| Tilt Down | `slow tilt down` | Camera tilts downward; grounds the scene |
| Truck Left | `truck left` | Camera slides left parallel to scene |
| Truck Right | `truck right` | Camera slides right parallel to scene |
| Orbit 180 | `orbit 180` | Camera orbits 180° around subject |
| Fast 360 Orbit | `fast 360 orbit` | Fast full orbit; energy, showcase |
| Slow Cinematic Arc | `slow cinematic arc` | Slow partial orbit; elegant, heroic |
| Pedestal Down | `pedestal down` | Camera descends vertically |
| Pedestal Up | `pedestal up` | Camera ascends vertically |
| Crane Up | `crane up` | Camera rises as in a crane shot |
| Crane Down | `crane down` | Camera descends from height |
| Smooth Zoom In | `smooth zoom in` | Optical zoom in, not dolly |
| Smooth Zoom Out | `smooth zoom out` | Optical zoom out |
| Snap Zoom | `snap zoom` | Instantaneous zoom; shock, comedy |
| Handheld Style | `handheld style` | Slight natural shake; documentary |
| Whip Pan | `whip pan` | Rapid lateral camera sweep; kinetic energy |
| Dutch Angle | `Dutch angle` | Tilted frame; tension, unease |
| Following Shot | `following shot` | Camera follows behind moving subject; journey feeling |
| Side Tracking | `side tracking` | Parallel tracking; shows movement profile |

**Prompt template for camera movement:**
```
[Subject doing action], [camera movement], [style], [lighting].
```

**Example:**
```
An astronaut walking across a red Martian desert toward ancient ruins, 
slow cinematic arc circling from front to behind, cinematic, harsh sunlight.
```

### Lighting

Use the same lighting vocabulary as image prompts but keep it to one or two terms for video stability:

**Good for video:**
- `harsh sunlight` — stable, defined
- `golden hour warm light` — stable, atmospheric
- `neon city night` — stable, atmospheric
- `soft overcast` — stable, diffused
- `candlelight flickering` — adds natural motion

**Avoid for video:**
- Complex multi-source studio setups (unstable across frames)
- Highly specific lighting combinations that are hard to maintain temporally

### Style

Keep style direction simple for video:

| Style Keyword | Works Well |
|---------------|-----------|
| `cinematic realistic` | Excellent |
| `anime clean line art` | Excellent |
| `documentary` | Excellent |
| `studio product commercial` | Good |
| `soft futuristic cinematic` | Good |
| `UGC-style selfie video` | Good |
| Complex multi-style combinations | Poor |

### Pacing

One word is sufficient. Controls the energy and editing rhythm of the generated content:

- `slow` — deliberate, emotional, minimal motion
- `medium` — balanced, natural
- `energetic` — high motion, dynamic

For cleaner results, `slow + subtle motion` is the most stable combination. ([Chat4O](https://chat4o.ai/blog/detail/Grok-Imagine-AI-Video-Generation-on-Chat4O-A-Step-by-Step-Tutorial-Ready-to-Use-Prompts-25fa95f0df9d/))

### Audio Cues

Since Aurora generates audio natively, you can direct it:

**Ambient sound:**
```
"ambient sound of city traffic and distant music"
"sound of ocean waves"
"quiet forest ambiance, birds"
"industrial hum and echo"
```

**Music style reference:**
```
"Music style reference: Ambient cinematic, emotional, minimal electronic, slow tempo"
"upbeat commercial background music"
"dramatic orchestral swell"
"lo-fi hip hop beats"
```

**Dialogue/speech (see Lip Sync below):**
```
Speech: "Hello, I'm here to show you something amazing."
```

**Sound effects:**
```
"sound of footsteps on wet pavement"
"metallic clang, echo"
"soft notification chime"
```

### Lip Sync

Grok Imagine Video natively generates lip-synced dialogue. To trigger it:

1. Include spoken dialogue in the prompt
2. Prefix with `Speech:` for clarity
3. Specify the character's emotion and delivery

```
A woman in a red blazer looking directly into the camera, medium shot, 
studio lighting, professional YouTube style. 
Speech: "This is the product that changed everything for me."
Tone: enthusiastic, warm, direct.
```

The model generates both the video and the synchronized lip movement for the dialogue. No external lip-sync tool required. ([YouTube — Create Long Video with Grok AI](https://www.youtube.com/watch?v=4SetPdFsWvE), [Scenario](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))


---

## 13. Video Prompting — Templates

### Template 1: Text-to-Video (Standard)

```
[Subject description and setting]. 
[One action verb phrase].
Camera: [one camera movement].
Style: [visual style].
Lighting: [one lighting description].
Audio: [ambient/music/sfx].
Constraints: one continuous shot, [duration] seconds.
```

**Example A — Cinematic Nature:**
```
A lone wolf standing on a snow-covered ridge at dawn, pine forest below 
blanketed in mist. The wolf raises its head and howls into the pale sky.
Camera: slow tilt up from wolf to sky.
Style: cinematic realistic wildlife documentary.
Lighting: cold blue dawn light.
Audio: ambient wind, distant echo of howl.
Constraints: one continuous shot, 8 seconds.
```

**Example B — Urban Action:**
```
Realistic cinematic wide shot in a desert canyon. A heavily modified 
orange off-road buggy races toward the camera at high speed, kicking up 
a huge dust trail. Harsh sunlight, heat haze, rocky cliffs in the distance.
Camera: low to the ground, fast tracking shot.
Style: cinematic action.
Audio: roaring engine, wind, dust.
Constraints: one shot, 6 seconds, energetic pacing.
```

([Scenario](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))

---

### Template 2: Image-to-Video

```
[What moves in the image]. 
[What the camera does].
Style: [visual style].
Lighting: [lighting instruction].
Background: [what stays stable].
Constraints: [what should NOT move].
```

**Example A — Portrait Animation:**
```
Animate subtle wind moving through her hair and a slight smile forming 
on her face. Her eyes blink naturally once.
Camera: slow dolly in, very subtle.
Style: cinematic portrait, photoreal.
Lighting: maintain the existing golden hour warmth from source image.
Background: keep the bokeh background stable, no movement.
Constraints: do not change her clothing, expression baseline, or camera angle.
```

**Example B — Product Animation:**
```
Animate the steam rising from the coffee mug and a gentle parallax 
push-in toward the product.
Camera: slow dolly in.
Style: lifestyle product commercial, clean.
Background: keep the wooden desk stable.
Constraints: no movement from the product itself, stable identity.
```

([Chat4O](https://chat4o.ai/blog/detail/Grok-Imagine-AI-Video-Generation-on-Chat4O-A-Step-by-Step-Tutorial-Ready-to-Use-Prompts-25fa95f0df9d/))

---

### Template 3: Multi-Shot Sequence

For longer narratives, describe each shot as a separate paragraph. Aurora sequences them:

```
Shot 1: [Scene description, camera, action]

Shot 2: [Next scene, camera, action — connected to Shot 1]

Shot 3: [Next scene, camera, action]

Style: [consistent visual style across all shots]
Audio: [consistent or transitioning audio]
```

**Example — Product Commercial:**
```
Shot 1: Extreme close-up of hands pouring water into the MoodBottle Smart, 
the bottle lighting up blue as it fills. Slow macro zoom in on the glowing 
display. Studio product lighting.

Shot 2: Medium shot of a woman at a desk, reaching for the bottle and 
taking a drink. She smiles at the camera. Warm office lifestyle lighting.

Shot 3: Close-up of the bottle screen showing "Hydration Goal Met!" with 
a soft chime and glow pulse. Pull back slowly to reveal the full bottle.

Style: Commercial product video, clean, bright, upbeat.
Audio: soft UI chimes, upbeat background music.
```

([Scenario](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))

---

### Template 4: Product Commercial

```
Create a video of this scene:
Product: [Product name and key description]
Audience: [Target audience description]
Shot: [Camera angle, character position, framing]
Action: [What the character/product does]
Background: [Environment]
Tone: [Emotional register]
Speech: "[Dialogue if needed]"
Style: [Visual style]
Audio: [Music/sfx]
```

**Example — Tech Product:**
```
Create a video of this scene:
Product: MoodBottle Smart — a smart water bottle that glows to remind you 
to hydrate, connects to your phone, stylish and practical.
Audience: Health-conscious young professionals and students.
Shot: Medium frontal shot, camera at eye level. YouTuber seated at desk, 
centered in frame, holding the product upright near chest, looking directly 
into camera.
Action: Animated expression, open mouth mid-speech, active hand gesture 
with free hand.
Background: Clean home office, softly blurred.
Tone: Upbeat, friendly, relatable, enthusiastic.
Speech: "This little bottle has genuinely changed how I drink water."
Style: UGC YouTube review, natural lighting.
Audio: Subtle background room tone, no music.
```

([Scenario](https://www.scenario.com/blog/grok-imagine-video-examples-90430d1))

---

### Template 5: Cinematic Scene

```
[Atmospheric establishing line]. [Subject]. [Single dramatic action]. 
Camera: [specific cinematic move].
Style: [cinematic style reference].
Lighting: [lighting setup].
Mood: [one word pacing/emotion].
```

**Example A — Sci-Fi:**
```
A glowing crystal-powered rocket stands on the red dunes of Mars, ancient 
alien ruins lighting up in the background. The rocket ignites and launches 
vertically, a column of blue flame pushing it skyward into a sky full of 
unfamiliar constellations.
Camera: slow crane up following the rocket's ascent.
Style: cinematic science fiction, epic.
Lighting: deep space ambient, warm alien sunset backlight.
Mood: triumphant.
```

([xAI Docs](https://docs.x.ai/developers/model-capabilities/video/generation))

**Example B — Drama:**
```
Rain falls heavily on a narrow cobblestone street in a medieval city at 
night. A cloaked figure steps out of a dark archway, looking left and right 
before hurrying forward.
Camera: slow tracking shot following from the side.
Style: cinematic fantasy drama, film grain.
Lighting: torch-lit walls, wet stone reflections.
Mood: tense.
```

---

### Template 6: UGC-Style

```
[Device type / phone / selfie context]. [Person description]. 
[What they're doing]. [Casual setting].
Style: authentic UGC, handheld, slight natural shake.
Lighting: natural indoor/outdoor.
Audio: ambient room sound, no background music.
[Optional: Speech line]
```

**Example:**
```
Phone selfie style video. A 25-year-old woman in casual clothes filming 
herself unboxing a product on her living room couch. She pulls the product 
from a box and holds it up to the camera, grinning.
Style: authentic UGC TikTok style, handheld, slight natural shake.
Lighting: natural window light from the left.
Audio: ambient room sound, paper rustling.
Speech: "Okay, it finally came — look at this thing."
```


---

## 14. Video Modes

### Text-to-Video

**Input:** Prompt text only  
**Output:** Generated video clip  
**Endpoint:** `POST /v1/videos/generations`

The model generates video from a text description alone. No reference image. Camera, style, lighting, and audio all inferred from prompt.

**Required fields:** `prompt`, `model`

### Image-to-Video

**Input:** Prompt text + source image  
**Output:** Animated video starting from the source image  
**Endpoint:** `POST /v1/videos/generations` with `image` field

The source image becomes the **first frame** of the video. The model animates it forward according to the prompt. This is the most reliable mode for character consistency.

**Key behavior:**
- Aspect ratio defaults to input image ratio
- Override with `aspect_ratio` parameter (will stretch image if dimensions differ)
- Good for animating portraits, products, landscapes

**Required fields:** `prompt`, `model`, `image` (URL or base64)

### Reference Images Mode

**Input:** Prompt text + up to 7 reference images  
**Output:** Generated video influenced by the references  
**Endpoint:** `POST /v1/videos/generations` with `reference_images` field

**Critical distinction from image-to-video:** Reference images do NOT become the first frame. They influence the style, character, and content of the generation without locking the temporal starting point.

**How to reference images in your prompt:**

Use `<IMAGE_1>`, `<IMAGE_2>` etc. placeholders in the prompt text to specify which reference to draw from:

```
Generate a video of <IMAGE_1> walking through a cyberpunk city at night. 
Camera: slow dolly following from behind.
Style: match the visual style from <IMAGE_2>.
```

**Use cases:**
- Consistent character across scenes
- Style reference from existing artwork
- Environment reference + character reference simultaneously

**Required fields:** `prompt`, `model`, `reference_images` (array of image objects)  
**Max duration:** 10 seconds when using reference images

([xAI Docs](https://docs.x.ai/developers/model-capabilities/video/generation))

### Video Editing

**Input:** Prompt text + source video  
**Output:** Edited version of the source video  
**Endpoint:** `POST /v1/videos/edits`

Modify existing footage with natural language instructions:

```
"Make her dress yellow."
"Make him blonde and wearing a red dress."
"Make his armor red and silver."
"Add rain to the outdoor scene."
"Shift the color grade to teal and orange."
```

**Constraints:**
- Input video: max **8.7 seconds**
- Output: same duration as input
- Aspect ratio: matches input (not configurable)
- Resolution: matches input, capped at 720p

### Video Extension

**Input:** Prompt text + source video  
**Output:** Extended version of the source video  
**Endpoint:** `POST /v1/videos/extensions`

Continue a clip beyond its original end point:

```
"She then walks toward the shops and goes into one of them, saying 'It's time to shop.'"
```

**Constraints:**
- Input video: 2–15 seconds
- Extension output: 2–10 seconds (default: 6 seconds)
- Aspect ratio: matches input (not configurable)
- Resolution: matches input, capped at 720p
- Can chain multiple extensions for longer content

**Chaining strategy for longer videos:**
```
Generate (6–10s) → Extend (6–10s) → Extend again → ...
```

Each extension should have a logical narrative continuation from the previous clip. ([YouTube — Grok AI Full Tutorial 2026](https://www.youtube.com/watch?v=pxchioM5cNQ))


---

