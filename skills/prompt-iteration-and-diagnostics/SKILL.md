---
name: prompt-iteration-and-diagnostics
description: "Diagnose failed AI image or video outputs, identify root causes, revise prompts with single-variable iteration, and produce structured prompt revision reports."
---

# prompt-iteration-and-diagnostics

## When to use
- The user shows or describes a failed output and asks how to fix it.
- The user wants prompt diagnostics, iteration, A/B variants, failure analysis, or a revision report.
- The output has drift, bad anatomy, wrong motion, weak realism, camera chaos, text/logo errors, prompt collapse, or model transfer failure.
- The prose, dialogue, or film package has generic AI voice, weak story logic, rights/provenance gaps, or release-quality concerns.

## When not to use
- The user has no output or failure description and only needs first-draft prompting.
- The issue is a tool outage or account/billing problem.
- The user asks for unsafe bypass instructions.

## Required inputs
- Original prompt
- Observed output or failure description
- Target model/tool
- Desired result

## Optional inputs
- Reference images
- Settings/parameters
- Seed/version
- Previous attempts
- Continuity bible

## Workflow
1. Restate the intended result and the actual failure.
2. Classify failure: prompt ambiguity, contradiction, overload, model limitation, continuity drift, temporal overload, reference conflict, safety/policy rejection, or parameter mismatch.
3. Identify the smallest change likely to improve the result.
4. Apply the one-variable rule for iterative tests unless the prompt is fundamentally broken.
5. Rewrite using the relevant skill: image, video, continuity, style, or model-adaptation.
6. Produce a revision report with diagnosis, changed fields, unchanged anchors, expected improvement, and next test.
7. When the failure is a model limitation, redesign the shot or route to a better model instead of forcing the same prompt.

## Decision logic
- If output is 80 percent correct, make minimal edits.
- If identity drift appears, strengthen references and bible anchors.
- If motion fails, reduce actions and camera moves.
- If text/logos fail, choose a text-capable model or simplify typography.
- If a prompt is rejected, remove unsafe/IP-sensitive content and do not provide bypass tactics.

## Output formats
- Failure diagnosis
- Revised prompt
- A/B test variants
- Prompt revision report
- Continuity update recommendations
- Model-routing note
- Story/voice/release QC report

## Quality checks
- Diagnosis maps to a specific prompt or model cause.
- Revisions preserve what already worked.
- Only meaningful variables change per test.
- The report distinguishes fixable prompt issues from model limitations.
- Story, voice, continuity, performance, rights, and provenance checks are separated when evaluating a full AI film package.
- No unsafe bypass methods are included.

## Anti-patterns
- Rewriting the entire prompt after a small failure
- Adding long negative lists without prioritization
- Blaming the model before checking contradictions
- Ignoring uploaded reference conflicts
- Treating policy rejection as a prompt-engineering puzzle.

## Exit criteria
- The user has a revised prompt and a clear next test or model-routing decision.

## Supporting files
Read only the supporting file needed for the active task:
- `references/iteration_diagnostics.md`
- `references/failure_modes.md`
- `references/revision_loops.md`
- `references/story_voice_release_qc.md`
- `templates/prompt_revision_report.md`
- `templates/failed_output_intake.md`
