# Golden Image Workflow

Golden images are approved still references used to keep generated shots visually consistent.

## When to create golden images

- Before image-to-video generation.
- Before multi-shot sequences with recurring characters.
- Before a model transfer where identity/style drift is likely.
- Before marketing assets if the look is not fully locked.

## What to lock

- Characters: neutral face, full-body silhouette, wardrobe, hair, skin, signature prop.
- Locations: readable geography, landmarks, time-of-day baseline, palette, material texture.
- Props: scale, material, wear, markings, state variants.
- Style: palette, lighting quality, grain/finish, realism level.

## Production use

1. Generate 2-4 candidate reference stills.
2. Select one approved image per asset or state.
3. Assign asset IDs and store prompt/settings/source model.
4. Use the still as I2V start frame or reference asset where supported.
5. Generate 2-3 video variations per shot and discard outputs with identity, physics, or morphology failures.

## Quality rule

Do not use a dramatic, shadow-heavy, occluded still as the only identity reference. Create a clean reference first, then dramatic variants.
