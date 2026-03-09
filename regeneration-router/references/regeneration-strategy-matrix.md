# Regeneration Strategy Matrix

Use this matrix to decide the cheapest reliable repair path after QC.

## Route Types

- `keep`: accept current result
- `patch`: preserve current result and fix in post or with minimal prompt delta
- `partial_redo`: regenerate a single shot or a tight batch
- `full_redo`: rebuild the shot with stronger constraints

## By Failure Type

### Identity Drift

- minor: `patch` or `partial_redo`
- major: `partial_redo` with reference shot + stronger character lock
- critical: `full_redo`

### Composition Mismatch

- framing slightly off: `patch` if crop can solve it
- wrong shot size or missing subject: `partial_redo`
- totally wrong staging: `full_redo`

### Emotion Mismatch

- weak expression but usable frame: `patch` if edit can shorten exposure
- wrong facial emotion or lighting mood: `partial_redo`
- tone opposite to scene intent: `full_redo`

### Technical Defect

- minor artifact: `patch`
- visible artifact in key focal area: `partial_redo`
- broken anatomy / face / hands: `full_redo`

### Motion Failure

- motion too weak: `partial_redo` with stronger action verbs
- motion chaotic or off-model: `full_redo`

### Continuity Break

- isolated: `partial_redo`
- affects multiple linked shots: `full_redo` for the full sequence group

## Cost Rule

Prefer the cheapest route that reliably preserves:

1. story readability
2. identity continuity
3. visual quality

Do not choose `patch` if the audience will still notice the break.
