# Negative Prompt Patterns

Do not assume negative prompts work in every model.

## If the model supports a negative field
Use only the few failures that would ruin the output. Prefer concrete artifacts: extra fingers, warped hands, text artifacts, logo distortion, identity drift, blurry face, morphing background.

## If the model does not support negatives
Restate the desired positive condition:
- Instead of "no blur": sharp focus on the subject's eyes.
- Instead of "no extra people": single person alone in the frame.
- Instead of "no morphing": stable face shape and unchanged wardrobe throughout.

## Video constraint cap
For video, limit constraints to the top 2 to 4 risks. Over-constraining can create prompt noise.

## Safety/IP hygiene
Do not provide bypass tactics. Replace named protected characters/logos with visual descriptions unless the user has a legitimate, allowed use case and the model supports it.
