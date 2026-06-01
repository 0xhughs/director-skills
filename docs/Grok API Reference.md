# Grok Imagine Prompting Guide — API Reference

> **Part 4 of 6** | Complete API parameters for image and video generation, all endpoints, polling patterns, batch generation, and quick reference card.

---

## 10. API Parameters — Image

### Endpoint Summary

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `https://api.x.ai/v1/images/generations` | POST | Text-to-image generation |
| `https://api.x.ai/v1/images/edits` | POST | Image editing with source image |

### Full Parameter Table

| Parameter | Type | Default | Range/Options | Description |
|-----------|------|---------|--------------|-------------|
| `model` | string | — | `"grok-imagine-image"` | Model identifier |
| `prompt` | string | — | Up to ~1000 chars | Text prompt for generation or editing |
| `n` | integer | 1 | 1–10 | Number of images to generate |
| `aspect_ratio` | string | `"auto"` | See table below | Output aspect ratio |
| `resolution` | string | `"1k"` | `"1k"`, `"2k"` | Output resolution (2k in beta) |
| `response_format` | string | `"url"` | `"url"`, `"b64_json"` | Response format (OpenAI SDK) |
| `image_format` | string | — | `"base64"` | Base64 output (xAI SDK) |
| `image_url` | string | — | URL or base64 data URI | Source image for editing (xAI SDK) |
| `image` | object | — | `{url: "...", type: "image_url"}` | Source image for editing (curl/HTTP) |

> **Not supported:** `quality`, `size`, `style` — these parameters exist in documentation but are currently no-ops. ([Reddit r/grok](https://www.reddit.com/r/grok/comments/1qtdbqs/a_glimpse_into_groks_image_prompt_rewriting/))

### Aspect Ratio Options (Image)

| Ratio | Use Case |
|-------|----------|
| `auto` | Model selects best ratio for prompt content |
| `1:1` | Social media, thumbnails |
| `16:9` | Widescreen, YouTube, presentations |
| `9:16` | Mobile, Stories, TikTok |
| `4:3` | Presentations, traditional displays |
| `3:4` | Portraits, Pinterest |
| `3:2` | Standard photography |
| `2:3` | Portrait photography |
| `2:1` | Banners, headers |
| `1:2` | Tall banners |
| `19.5:9` | Modern smartphone displays |
| `9:19.5` | Tall smartphone displays |
| `20:9` | Ultra-wide displays |
| `9:20` | Tall ultra-wide |

([xAI Docs](https://docs.x.ai/developers/model-capabilities/images/generation))

### Batch Generation

Generate up to 10 images in one API call:

```python
import xai_sdk

client = xai_sdk.Client()

response = client.image.sample_batch(
    prompts=["A mountain at dawn"] * 5,  # Same prompt, 5 variations
    model="grok-imagine-image",
    n=5,
)

for image in response:
    print(image.url)
```

Or with the HTTP API:

```bash
curl -X POST https://api.x.ai/v1/images/generations \
  -H "Authorization: Bearer $XAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "grok-imagine-image",
    "prompt": "A mountain at dawn",
    "n": 5
  }'
```

### Concurrent Different Prompts (AsyncClient)

For parallel generation with different prompts:

```python
import asyncio
import xai_sdk

async def generate_concurrently():
    client = xai_sdk.AsyncClient()
    source_image = "https://example.com/reference.jpg"
    
    prompts = [
        "Render this image as an oil painting in the style of impressionism",
        "Render this image as a pencil sketch with detailed shading",
        "Render this image as pop art with bold colors and halftone dots",
        "Render this image as a watercolor painting with soft edges",
    ]
    
    tasks = [
        client.image.sample(
            prompt=prompt,
            model="grok-imagine-image",
            image_url=source_image,
        )
        for prompt in prompts
    ]
    
    results = await asyncio.gather(*tasks)
    
    for prompt, result in zip(prompts, results):
        print(f"{prompt}: {result.url}")

asyncio.run(generate_concurrently())
```

([xAI Docs](https://docs.x.ai/developers/model-capabilities/images/generation))

### Output Formats

**URL format (default):**
```json
{
  "data": [
    {
      "url": "https://storage.x.ai/...",
      "revised_prompt": "3D render of a gray cat..."
    }
  ]
}
```

**Base64 format:**
```json
{
  "data": [
    {
      "b64_json": "data:image/png;base64,...",
      "revised_prompt": "..."
    }
  ]
}
```

**Important:** Generated images are in **JPG format**. URLs are on xAI-managed storage and are **temporary** — download and store locally if you need persistence.

**No watermarks:** Unlike DALL-E and Midjourney, Grok Imagine does not add watermarks to generated images. ([Latenode](https://latenode.com/blog/ai-technology-language-models/xai-grok-grok-2-grok-3/content-boundaries-can-grok-2-generate-nsfw-images-and-how-its-regulated))


---

## 15. API Parameters — Video

### Endpoint Summary

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `https://api.x.ai/v1/videos/generations` | POST | Text-to-video, image-to-video, reference images |
| `https://api.x.ai/v1/videos/{request_id}` | GET | Poll generation status |
| `https://api.x.ai/v1/videos/extensions` | POST | Video extension |
| `https://api.x.ai/v1/videos/edits` | POST | Video editing |

### Full Parameter Table

| Parameter | Type | Required | Default | Options | Description |
|-----------|------|----------|---------|---------|-------------|
| `model` | string | Yes | — | `"grok-imagine-video"` | Model identifier |
| `prompt` | string | Yes | — | — | Text description of scene/motion |
| `duration` | integer | No | — | 1–15s | Video length in seconds |
| `aspect_ratio` | string | No | `"16:9"` | See table below | Output aspect ratio |
| `resolution` | string | No | `"480p"` | `"480p"`, `"720p"` | Output resolution |
| `image` | string/object | No (image-to-video) | — | URL or base64 | Source image for i2v |
| `reference_images` | array | No (reference mode) | — | Max 7 images | Style/content reference images |
| `video` | string | No (editing/extension) | — | URL or base64 | Source video for edit/extend |

### Aspect Ratio Options (Video)

| Ratio | Use Case |
|-------|----------|
| `1:1` | Social media, thumbnails |
| `16:9` | Widescreen, YouTube (default) |
| `9:16` | Mobile, TikTok, Stories |
| `4:3` | Presentations |
| `3:4` | Portrait video |
| `3:2` | Cinematic photography |
| `2:3` | Vertical photography |

**Note:** Video editing and extension inherit aspect ratio from source — not configurable.

([fal.ai API docs](https://fal.ai/models/xai/grok-imagine-video/image-to-video/api), [xAI Docs](https://docs.x.ai/developers/model-capabilities/video/generation))

### Duration Options by Mode

| Mode | Input Duration | Output Duration |
|------|---------------|----------------|
| Text-to-video | N/A | 1–15s |
| Image-to-video | N/A | 1–15s |
| Reference images | N/A | 1–10s |
| Video editing | Max 8.7s input | = Input duration |
| Video extension | 2–15s input | 2–10s (additional) |

### Polling Pattern

Video generation is asynchronous. The pattern:

1. **Submit:** `POST /v1/videos/generations` → receive `request_id`
2. **Poll:** `GET /v1/videos/{request_id}` every 5 seconds
3. **Check status:** `done` | `expired` | `failed`

```python
import os
import time
import requests

headers = {
    "Content-Type": "application/json",
    "Authorization": f"Bearer {os.environ['XAI_API_KEY']}",
}

# Submit generation
response = requests.post(
    "https://api.x.ai/v1/videos/generations",
    headers=headers,
    json={
        "model": "grok-imagine-video",
        "prompt": "A glowing crystal-powered rocket launching from red Mars dunes",
        "duration": 10,
        "aspect_ratio": "16:9",
        "resolution": "720p",
    },
)

request_id = response.json()["request_id"]

# Poll until done
while True:
    result = requests.get(
        f"https://api.x.ai/v1/videos/{request_id}",
        headers={"Authorization": headers["Authorization"]},
    )
    data = result.json()
    if data["status"] == "done":
        print(data["video"]["url"])
        break
    elif data["status"] in ("expired", "failed"):
        print(f"Generation failed: {data['status']}")
        break
    time.sleep(5)
```

**Using xAI SDK (Python):**
```python
import os
import xai_sdk

client = xai_sdk.Client(api_key=os.getenv("XAI_API_KEY"))

response = client.video.generate(
    prompt="A glowing crystal-powered rocket launching from the red dunes of Mars",
    model="grok-imagine-video",
    duration=10,
    aspect_ratio="16:9",
    resolution="720p",
)

print(response.url)
```

**Using AI SDK (JavaScript/TypeScript):**
```javascript
import { createXai } from "@ai-sdk/xai";
import { experimental_generateVideo as generateVideo } from "ai";

const xai = createXai({ apiKey: process.env.XAI_API_KEY });

const { video } = await generateVideo({
    model: xai.video("grok-imagine-video"),
    prompt: "A glowing crystal-powered rocket launching from the red dunes of Mars",
    providerOptions: {
        xai: { duration: 10, aspectRatio: "16:9", resolution: "720p" },
    },
});
```

([xAI Docs](https://docs.x.ai/developers/model-capabilities/video/generation))


---

## 20. Quick Reference Card

### Image Prompt Formula

```
[Subject + Action] + [Environment/Setting] + [Lighting] + [Style/Medium] + [Camera/Composition] + [Mood]
```

**Minimum viable:**
```
[Subject doing action], [setting], [lighting], [style], [camera].
```

**Full example:**
```
An elderly fisherman with weathered skin sits alone on a fog-covered pier at dawn, 
mending nets. Diffused cool morning light, overcast sky. Hyperrealistic photography. 
85mm lens, medium shot. Melancholic and solitary mood.
```

### Video Prompt Formula

```
[Subject + one action] + [one camera movement] + [style] + [lighting] + [audio cue]
```

**Minimum viable:**
```
[Subject doing one thing], [one camera move], [style].
```

**Full example:**
```
A woman in a beige trench coat walks slowly through a rain-slicked Paris alley at dusk, 
slow following shot from behind, cinematic realistic, warm streetlight amber glow, 
ambient sound of rain and distant traffic.
```

### Top 10 Style Keywords

| Rank | Keyword |
|------|---------|
| 1 | `cinematic` |
| 2 | `photorealistic` |
| 3 | `hyperrealistic` |
| 4 | `anime` |
| 5 | `oil painting` |
| 6 | `concept art` |
| 7 | `film still` |
| 8 | `watercolor` |
| 9 | `graphic novel` |
| 10 | `surrealism` |

### Top 10 Lighting Keywords

| Rank | Keyword |
|------|---------|
| 1 | `golden hour` |
| 2 | `Rembrandt lighting` |
| 3 | `volumetric god rays` |
| 4 | `neon lighting` |
| 5 | `blue hour` |
| 6 | `chiaroscuro` |
| 7 | `softbox fill` |
| 8 | `rim lighting` |
| 9 | `overcast diffused` |
| 10 | `candlelight` |

### Top 10 Camera Keywords

| Rank | Keyword |
|------|---------|
| 1 | `slow dolly in` |
| 2 | `85mm lens` |
| 3 | `shallow depth of field` |
| 4 | `low angle` |
| 5 | `orbit 180` |
| 6 | `handheld style` |
| 7 | `close-up` |
| 8 | `wide establishing shot` |
| 9 | `bokeh` |
| 10 | `Dutch angle` |

### All Aspect Ratios

**Image:**

| Ratio | Use Case |
|-------|----------|
| `auto` | Let model decide |
| `1:1` | Instagram, thumbnails |
| `16:9` | YouTube, presentations |
| `9:16` | TikTok, Stories |
| `4:3` | Presentations |
| `3:4` | Portraits |
| `3:2` | DSLR photography |
| `2:3` | Portrait photography |
| `2:1` | Banners |
| `1:2` | Tall banners |
| `19.5:9` | Modern phone landscape |
| `9:19.5` | Modern phone portrait |
| `20:9` | Ultra-wide |
| `9:20` | Ultra-tall |

**Video:**

| Ratio | Use Case |
|-------|----------|
| `16:9` | YouTube, default |
| `9:16` | TikTok, Reels |
| `1:1` | Social feeds |
| `4:3` | Presentations |
| `3:4` | Portrait video |
| `3:2` | Cinematic |
| `2:3` | Vertical |

### All API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `https://api.x.ai/v1/images/generations` | POST | Text-to-image |
| `https://api.x.ai/v1/images/edits` | POST | Image editing |
| `https://api.x.ai/v1/videos/generations` | POST | Text-to-video, image-to-video, reference |
| `https://api.x.ai/v1/videos/{request_id}` | GET | Poll video status |
| `https://api.x.ai/v1/videos/extensions` | POST | Video extension |
| `https://api.x.ai/v1/videos/edits` | POST | Video editing |

### Duration Limits

| Mode | Duration |
|------|---------|
| Text-to-video | 1–15 seconds |
| Image-to-video | 1–15 seconds |
| Reference images mode | 1–10 seconds |
| Video editing input | Max 8.7 seconds |
| Video editing output | = Input duration |
| Video extension input | 2–15 seconds |
| Video extension output | 2–10 seconds (additional) |

### Resolution Options

| Type | Options |
|------|---------|
| Image | `1k`, `2k` |
| Video | `480p` (default, faster), `720p` (HD) |

### Batch Limits

| Type | Limit |
|------|-------|
| Image batch per request | 10 |
| Reference images per video | 7 |
| Source images for multi-image edit | 5 |

### Prompt Revision Field

```json
{
  "data": [
    {
      "url": "https://storage.x.ai/...",
      "revised_prompt": "[what the model actually received]"
    }
  ]
}
```

Always read `revised_prompt` when debugging unexpected outputs.

### Platform Access Summary

| Platform | Image | Video | NSFW |
|----------|-------|-------|------|
| grok.com | ✓ | ✓ | With subscription |
| X/Twitter app | ✓ | Limited | More restricted |
| Grok iOS/Android | ✓ | ✓ | Spicy Mode available |
| xAI API | ✓ | ✓ | Standard filters |


---

