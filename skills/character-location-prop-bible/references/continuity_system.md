# Continuity System

## Asset IDs
Use stable IDs:
- CH-001 character
- LOC-001 location
- PROP-001 prop
- COST-001 costume
- STYLE-001 visual rule

## Immutable vs mutable
Immutable anchors stay stable across the project: face shape, age range, height impression, silhouette, location geography, prop design, palette rules.

Mutable state changes by scene/shot: emotion, dirt, damage, weather, lighting state, prop position, wardrobe layer, injury, time of day.

## Update protocol
1. Record source of change.
2. Update only changed fields.
3. Add scene/shot state row.
4. Note conflicts and chosen resolution.
5. Generate a concise prompt anchor block.
