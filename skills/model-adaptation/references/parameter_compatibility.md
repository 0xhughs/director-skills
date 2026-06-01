# Parameter Compatibility

Track these fields separately from prompt text whenever possible:
- aspect_ratio
- duration
- resolution/quality tier
- seed
- reference image/video/audio IDs
- negative prompt
- style preset
- camera preset/control
- start frame/end frame
- extension mode
- lip-sync/audio source

## Compatibility policy
- Supported: include exact field and value.
- Unsupported: rewrite as prompt text if safe, or remove.
- Unknown: mark unknown; do not invent.
- Inherited: for editing/I2V, note when aspect/duration follows source media.
