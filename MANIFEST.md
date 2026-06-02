# Manifest

## File tree

```text
CHANGELOG.md
LICENSE
MANIFEST.md
RESEARCH_PROVENANCE.md
README.md
SKILL.md
skills/
skills/character-location-prop-bible/
skills/character-location-prop-bible/SKILL.md
skills/character-location-prop-bible/checklists/
skills/character-location-prop-bible/checklists/continuity_checklist.md
skills/character-location-prop-bible/examples/
skills/character-location-prop-bible/examples/character_continuity_update.md
skills/character-location-prop-bible/examples/location_continuity_update.md
skills/character-location-prop-bible/references/
skills/character-location-prop-bible/references/continuity_system.md
skills/character-location-prop-bible/references/golden_image_workflow.md
skills/character-location-prop-bible/references/identity_anchors.md
skills/character-location-prop-bible/references/visual_bible_system.md
skills/character-location-prop-bible/templates/
skills/character-location-prop-bible/templates/character_profile.md
skills/character-location-prop-bible/templates/continuity_checklist.md
skills/character-location-prop-bible/templates/costume_profile.md
skills/character-location-prop-bible/templates/location_profile.md
skills/character-location-prop-bible/templates/prop_profile.md
skills/character-location-prop-bible/templates/visual_style_bible.md
skills/character-location-prop-bible/tests/
skills/character-location-prop-bible/tests/continuity_tests.md
skills/cinematic-image-prompting/
skills/cinematic-image-prompting/SKILL.md
skills/cinematic-image-prompting/checklists/
skills/cinematic-image-prompting/checklists/image_prompt_quality_checklist.md
skills/cinematic-image-prompting/examples/
skills/cinematic-image-prompting/examples/shot_list_to_image_prompts.md
skills/cinematic-image-prompting/references/
skills/cinematic-image-prompting/references/image_prompt_components.md
skills/cinematic-image-prompting/references/lighting_and_photorealism.md
skills/cinematic-image-prompting/references/negative_prompt_patterns.md
skills/cinematic-image-prompting/references/prompt_anatomy.md
skills/cinematic-image-prompting/templates/
skills/cinematic-image-prompting/templates/character_reference_sheet_prompt.md
skills/cinematic-image-prompting/templates/cinematic_still_prompt.md
skills/cinematic-image-prompting/templates/keyframe_prompt.md
skills/cinematic-image-prompting/templates/location_reference_prompt.md
skills/cinematic-image-prompting/templates/prop_prompt.md
skills/cinematic-image-prompting/tests/
skills/cinematic-image-prompting/tests/image_prompt_completeness_tests.md
skills/cinematic-video-prompting/
skills/cinematic-video-prompting/SKILL.md
skills/cinematic-video-prompting/checklists/
skills/cinematic-video-prompting/checklists/video_prompt_quality_checklist.md
skills/cinematic-video-prompting/examples/
skills/cinematic-video-prompting/examples/image_prompt_to_video_prompt.md
skills/cinematic-video-prompting/references/
skills/cinematic-video-prompting/references/ai_film_production_pipeline.md
skills/cinematic-video-prompting/references/audio_motion_timing.md
skills/cinematic-video-prompting/references/camera_lens_movement.md
skills/cinematic-video-prompting/references/negative_prompt_patterns.md
skills/cinematic-video-prompting/references/prompt_anatomy.md
skills/cinematic-video-prompting/references/video_prompt_components.md
skills/cinematic-video-prompting/templates/
skills/cinematic-video-prompting/templates/image_to_video_prompt.md
skills/cinematic-video-prompting/templates/text_to_video_prompt.md
skills/cinematic-video-prompting/templates/video_beat_prompt.md
skills/cinematic-video-prompting/tests/
skills/cinematic-video-prompting/tests/video_prompt_completeness_tests.md
skills/model-adaptation/
skills/model-adaptation/SKILL.md
skills/model-adaptation/checklists/
skills/model-adaptation/checklists/model_export_checklist.md
skills/model-adaptation/examples/
skills/model-adaptation/examples/failed_model_transfer_diagnosis.md
skills/model-adaptation/examples/image_prompt_translation.md
skills/model-adaptation/examples/same_scene_across_models.md
skills/model-adaptation/examples/universal_prompt_to_model_specific_exports.md
skills/model-adaptation/examples/video_prompt_translation.md
skills/model-adaptation/references/
skills/model-adaptation/references/failure_modes_by_model.md
skills/model-adaptation/references/image_model_profiles.md
skills/model-adaptation/references/model_capability_matrix.md
skills/model-adaptation/references/model_update_protocol.md
skills/model-adaptation/references/parameter_compatibility.md
skills/model-adaptation/references/prompt_translation_rules.md
skills/model-adaptation/references/video_model_profiles.md
skills/model-adaptation/templates/
skills/model-adaptation/templates/model_comparison_table.md
skills/model-adaptation/templates/model_specific_prompt_export.md
skills/model-adaptation/templates/multi_model_export_package.md
skills/model-adaptation/templates/prompt_translation_report.md
skills/model-adaptation/templates/universal_prompt_brief.md
skills/model-adaptation/tests/
skills/model-adaptation/tests/model_routing_tests.md
skills/model-adaptation/tests/prompt_translation_tests.md
skills/model-adaptation/tests/research_provenance_tests.md
skills/model-adaptation/tests/unknown_capability_tests.md
skills/prompt-iteration-and-diagnostics/
skills/prompt-iteration-and-diagnostics/SKILL.md
skills/prompt-iteration-and-diagnostics/checklists/
skills/prompt-iteration-and-diagnostics/checklists/diagnostic_checklist.md
skills/prompt-iteration-and-diagnostics/checklists/release_quality_checklist.md
skills/prompt-iteration-and-diagnostics/examples/
skills/prompt-iteration-and-diagnostics/examples/failed_output_to_revised_prompt.md
skills/prompt-iteration-and-diagnostics/examples/final_prompt_package_export.md
skills/prompt-iteration-and-diagnostics/references/
skills/prompt-iteration-and-diagnostics/references/failure_modes.md
skills/prompt-iteration-and-diagnostics/references/iteration_diagnostics.md
skills/prompt-iteration-and-diagnostics/references/revision_loops.md
skills/prompt-iteration-and-diagnostics/references/story_voice_release_qc.md
skills/prompt-iteration-and-diagnostics/templates/
skills/prompt-iteration-and-diagnostics/templates/failed_output_intake.md
skills/prompt-iteration-and-diagnostics/templates/final_production_package.md
skills/prompt-iteration-and-diagnostics/templates/prompt_revision_report.md
skills/prompt-iteration-and-diagnostics/tests/
skills/prompt-iteration-and-diagnostics/tests/prompt_quality_checklist_tests.md
skills/screenplay-and-scene-writing/
skills/screenplay-and-scene-writing/SKILL.md
skills/screenplay-and-scene-writing/checklists/
skills/screenplay-and-scene-writing/checklists/scene_quality_checklist.md
skills/screenplay-and-scene-writing/examples/
skills/screenplay-and-scene-writing/examples/scene_to_screenplay_excerpt.md
skills/screenplay-and-scene-writing/references/
skills/screenplay-and-scene-writing/references/dialogue_and_subtext.md
skills/screenplay-and-scene-writing/references/fountain_workflow.md
skills/screenplay-and-scene-writing/references/scene_construction.md
skills/screenplay-and-scene-writing/references/screenplay_format.md
skills/screenplay-and-scene-writing/templates/
skills/screenplay-and-scene-writing/templates/beat_sheet.md
skills/screenplay-and-scene-writing/templates/dialogue_pass.md
skills/screenplay-and-scene-writing/templates/fountain_scene.md
skills/screenplay-and-scene-writing/templates/screenplay_scene.md
skills/screenplay-and-scene-writing/tests/
skills/screenplay-and-scene-writing/tests/screenplay_scene_tests.md
skills/short-film-development/
skills/short-film-development/SKILL.md
skills/short-film-development/checklists/
skills/short-film-development/checklists/concept_quality_checklist.md
skills/short-film-development/examples/
skills/short-film-development/examples/idea_to_logline.md
skills/short-film-development/examples/logline_to_outline.md
skills/short-film-development/references/
skills/short-film-development/references/ai_storytelling_workflow.md
skills/short-film-development/references/continuity_handoff.md
skills/short-film-development/references/screenplay_structure.md
skills/short-film-development/references/story_development_workflow.md
skills/short-film-development/templates/
skills/short-film-development/templates/beat_sheet.md
skills/short-film-development/templates/idea_intake.md
skills/short-film-development/templates/logline.md
skills/short-film-development/templates/short_film_treatment.md
skills/short-film-development/templates/short_story_plan.md
skills/short-film-development/templates/story_premise.md
skills/short-film-development/templates/story_revision_audit.md
skills/short-film-development/tests/
skills/short-film-development/tests/output_format_tests.md
skills/short-film-development/tests/routing_tests.md
skills/shotlist-and-visual-breakdown/
skills/shotlist-and-visual-breakdown/SKILL.md
skills/shotlist-and-visual-breakdown/checklists/
skills/shotlist-and-visual-breakdown/checklists/shotlist_quality_checklist.md
skills/shotlist-and-visual-breakdown/examples/
skills/shotlist-and-visual-breakdown/examples/screenplay_scene_to_shot_list.md
skills/shotlist-and-visual-breakdown/references/
skills/shotlist-and-visual-breakdown/references/camera_plan.md
skills/shotlist-and-visual-breakdown/references/production_breakdown.md
skills/shotlist-and-visual-breakdown/references/shotlist_schema.md
skills/shotlist-and-visual-breakdown/templates/
skills/shotlist-and-visual-breakdown/templates/asset_list.md
skills/shotlist-and-visual-breakdown/templates/camera_plan.md
skills/shotlist-and-visual-breakdown/templates/scene_breakdown.md
skills/shotlist-and-visual-breakdown/templates/shot_list.md
skills/shotlist-and-visual-breakdown/tests/
skills/shotlist-and-visual-breakdown/tests/screenplay_to_shotlist_tests.md
skills/style-cinematography-director/
skills/style-cinematography-director/SKILL.md
skills/style-cinematography-director/checklists/
skills/style-cinematography-director/checklists/style_quality_checklist.md
skills/style-cinematography-director/examples/
skills/style-cinematography-director/examples/genre_to_visual_direction.md
skills/style-cinematography-director/references/
skills/style-cinematography-director/references/camera_lens_movement.md
skills/style-cinematography-director/references/cinematic_language.md
skills/style-cinematography-director/references/genre_style_tone.md
skills/style-cinematography-director/references/lighting_and_photorealism.md
skills/style-cinematography-director/templates/
skills/style-cinematography-director/templates/visual_style_bible.md
skills/style-cinematography-director/tests/
skills/style-cinematography-director/tests/style_translation_tests.md
tests/
tests/master_router_tests.md
```

## Skill list

- `director-skills` master router
- `character-location-prop-bible`
- `cinematic-image-prompting`
- `cinematic-video-prompting`
- `model-adaptation`
- `prompt-iteration-and-diagnostics`
- `screenplay-and-scene-writing`
- `short-film-development`
- `shotlist-and-visual-breakdown`
- `style-cinematography-director`

## Capabilities

- Hybrid usage: one master skill for ZIP/chat uploads, or nine modular native skills for agent environments with skill routing.
- Master routing from user intent into the correct story, screenplay, visual, prompt, continuity, diagnostic, or model-adaptation workflow.
- Short-story planning, AI-assisted prose development, revision audits, and voice QC.
- Story ideation, loglines, treatments, scene lists, and revision plans.
- Screenplay scene writing, Fountain output, dialogue passes, beats, and visual action rewriting.
- Shot lists, camera plans, scene breakdowns, asset lists, and continuity notes.
- Cinematic image prompts for characters, locations, props, costumes, keyframes, posters, concept art, and stills.
- Cinematic video prompts for T2V, I2V, time-blocked shots, audio cues, edit notes, and continuity guardrails.
- Character/location/prop/costume/style bible creation, golden-image planning, and continuity updates.
- Prompt failure diagnosis, story/voice/release QC, and structured iteration.
- Cinematography/style translation from genre and tone to camera, lens, light, color, texture, and design.
- Model-specific prompt translation, comparison, export packages, and unknown-capability handling.

## Known limitations

- The suite distills local guides and does not guarantee live model specs.
- Markdown tests are human/agent validation scenarios, not automated test runners.
- Several comparison-only models have low or unknown source confidence.
- Unsafe bypass tactics and explicit-content operational instructions were intentionally excluded.
- Rights, provenance, and copyright notes are risk guidance, not legal advice.

## Model profiles created

- Grok Imagine / Aurora
- Gemini image / Nano Banana
- GPT-image-2
- Le Chat / FLUX Ultra
- Gemini Veo 3.1
- Gemini Omni video
- Kling AI
- Seedance 2.0
- Midjourney
- Stable Diffusion
- Ideogram
- Runway
- Pika
- Luma
- Sora
- Hailuo
- DALL-E
- FLUX direct

## Reference files created

- `skills/character-location-prop-bible/references/continuity_system.md`
- `skills/character-location-prop-bible/references/golden_image_workflow.md`
- `skills/character-location-prop-bible/references/identity_anchors.md`
- `skills/character-location-prop-bible/references/visual_bible_system.md`
- `skills/cinematic-image-prompting/references/image_prompt_components.md`
- `skills/cinematic-image-prompting/references/lighting_and_photorealism.md`
- `skills/cinematic-image-prompting/references/negative_prompt_patterns.md`
- `skills/cinematic-image-prompting/references/prompt_anatomy.md`
- `skills/cinematic-video-prompting/references/ai_film_production_pipeline.md`
- `skills/cinematic-video-prompting/references/audio_motion_timing.md`
- `skills/cinematic-video-prompting/references/camera_lens_movement.md`
- `skills/cinematic-video-prompting/references/negative_prompt_patterns.md`
- `skills/cinematic-video-prompting/references/prompt_anatomy.md`
- `skills/cinematic-video-prompting/references/video_prompt_components.md`
- `skills/model-adaptation/references/failure_modes_by_model.md`
- `skills/model-adaptation/references/image_model_profiles.md`
- `skills/model-adaptation/references/model_capability_matrix.md`
- `skills/model-adaptation/references/model_update_protocol.md`
- `skills/model-adaptation/references/parameter_compatibility.md`
- `skills/model-adaptation/references/prompt_translation_rules.md`
- `skills/model-adaptation/references/video_model_profiles.md`
- `skills/prompt-iteration-and-diagnostics/references/failure_modes.md`
- `skills/prompt-iteration-and-diagnostics/references/iteration_diagnostics.md`
- `skills/prompt-iteration-and-diagnostics/references/revision_loops.md`
- `skills/prompt-iteration-and-diagnostics/references/story_voice_release_qc.md`
- `skills/screenplay-and-scene-writing/references/dialogue_and_subtext.md`
- `skills/screenplay-and-scene-writing/references/fountain_workflow.md`
- `skills/screenplay-and-scene-writing/references/scene_construction.md`
- `skills/screenplay-and-scene-writing/references/screenplay_format.md`
- `skills/short-film-development/references/ai_storytelling_workflow.md`
- `skills/short-film-development/references/continuity_handoff.md`
- `skills/short-film-development/references/screenplay_structure.md`
- `skills/short-film-development/references/story_development_workflow.md`
- `skills/shotlist-and-visual-breakdown/references/camera_plan.md`
- `skills/shotlist-and-visual-breakdown/references/production_breakdown.md`
- `skills/shotlist-and-visual-breakdown/references/shotlist_schema.md`
- `skills/style-cinematography-director/references/camera_lens_movement.md`
- `skills/style-cinematography-director/references/cinematic_language.md`
- `skills/style-cinematography-director/references/genre_style_tone.md`
- `skills/style-cinematography-director/references/lighting_and_photorealism.md`

## Templates created

- `skills/character-location-prop-bible/templates/character_profile.md`
- `skills/character-location-prop-bible/templates/continuity_checklist.md`
- `skills/character-location-prop-bible/templates/costume_profile.md`
- `skills/character-location-prop-bible/templates/location_profile.md`
- `skills/character-location-prop-bible/templates/prop_profile.md`
- `skills/character-location-prop-bible/templates/visual_style_bible.md`
- `skills/cinematic-image-prompting/templates/character_reference_sheet_prompt.md`
- `skills/cinematic-image-prompting/templates/cinematic_still_prompt.md`
- `skills/cinematic-image-prompting/templates/keyframe_prompt.md`
- `skills/cinematic-image-prompting/templates/location_reference_prompt.md`
- `skills/cinematic-image-prompting/templates/prop_prompt.md`
- `skills/cinematic-video-prompting/templates/image_to_video_prompt.md`
- `skills/cinematic-video-prompting/templates/text_to_video_prompt.md`
- `skills/cinematic-video-prompting/templates/video_beat_prompt.md`
- `skills/model-adaptation/templates/model_comparison_table.md`
- `skills/model-adaptation/templates/model_specific_prompt_export.md`
- `skills/model-adaptation/templates/multi_model_export_package.md`
- `skills/model-adaptation/templates/prompt_translation_report.md`
- `skills/model-adaptation/templates/universal_prompt_brief.md`
- `skills/prompt-iteration-and-diagnostics/templates/failed_output_intake.md`
- `skills/prompt-iteration-and-diagnostics/templates/final_production_package.md`
- `skills/prompt-iteration-and-diagnostics/templates/prompt_revision_report.md`
- `skills/screenplay-and-scene-writing/templates/beat_sheet.md`
- `skills/screenplay-and-scene-writing/templates/dialogue_pass.md`
- `skills/screenplay-and-scene-writing/templates/fountain_scene.md`
- `skills/screenplay-and-scene-writing/templates/screenplay_scene.md`
- `skills/short-film-development/templates/beat_sheet.md`
- `skills/short-film-development/templates/idea_intake.md`
- `skills/short-film-development/templates/logline.md`
- `skills/short-film-development/templates/short_film_treatment.md`
- `skills/short-film-development/templates/short_story_plan.md`
- `skills/short-film-development/templates/story_premise.md`
- `skills/short-film-development/templates/story_revision_audit.md`
- `skills/shotlist-and-visual-breakdown/templates/asset_list.md`
- `skills/shotlist-and-visual-breakdown/templates/camera_plan.md`
- `skills/shotlist-and-visual-breakdown/templates/scene_breakdown.md`
- `skills/shotlist-and-visual-breakdown/templates/shot_list.md`
- `skills/style-cinematography-director/templates/visual_style_bible.md`

## Checklists created

- `skills/character-location-prop-bible/checklists/continuity_checklist.md`
- `skills/cinematic-image-prompting/checklists/image_prompt_quality_checklist.md`
- `skills/cinematic-video-prompting/checklists/video_prompt_quality_checklist.md`
- `skills/model-adaptation/checklists/model_export_checklist.md`
- `skills/prompt-iteration-and-diagnostics/checklists/diagnostic_checklist.md`
- `skills/prompt-iteration-and-diagnostics/checklists/release_quality_checklist.md`
- `skills/screenplay-and-scene-writing/checklists/scene_quality_checklist.md`
- `skills/short-film-development/checklists/concept_quality_checklist.md`
- `skills/shotlist-and-visual-breakdown/checklists/shotlist_quality_checklist.md`
- `skills/style-cinematography-director/checklists/style_quality_checklist.md`

## Tests created

- `tests/master_router_tests.md`
- `skills/character-location-prop-bible/tests/continuity_tests.md`
- `skills/cinematic-image-prompting/tests/image_prompt_completeness_tests.md`
- `skills/cinematic-video-prompting/tests/video_prompt_completeness_tests.md`
- `skills/model-adaptation/tests/model_routing_tests.md`
- `skills/model-adaptation/tests/prompt_translation_tests.md`
- `skills/model-adaptation/tests/research_provenance_tests.md`
- `skills/model-adaptation/tests/unknown_capability_tests.md`
- `skills/prompt-iteration-and-diagnostics/tests/prompt_quality_checklist_tests.md`
- `skills/screenplay-and-scene-writing/tests/screenplay_scene_tests.md`
- `skills/short-film-development/tests/output_format_tests.md`
- `skills/short-film-development/tests/routing_tests.md`
- `skills/shotlist-and-visual-breakdown/tests/screenplay_to_shotlist_tests.md`
- `skills/style-cinematography-director/tests/style_translation_tests.md`
