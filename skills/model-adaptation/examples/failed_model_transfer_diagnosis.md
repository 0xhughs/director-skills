# Example: Failed Model Transfer Diagnosis

A prompt written for Kling used a separate negative prompt and start/end frame workflow. Transferred directly to Le Chat image generation, the negatives appeared to confuse the prompt and the video controls were ignored.

Fix: convert to a still-image prompt, remove video-only settings, rewrite negatives as positives, and mark start/end frame unsupported for that target.
