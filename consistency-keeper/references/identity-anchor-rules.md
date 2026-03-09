# Identity Anchor Rules

Use these rules to decide which visual attributes must remain locked and which can vary shot to shot.

## Hard Anchors

Treat these as locked unless the story explicitly changes them:

- character face shape
- hair style and hair color
- skin tone
- signature wardrobe silhouette
- signature accessories
- prop identity for plot-critical objects

If a hard anchor drifts, default to `Redo`.

## Soft Anchors

These may vary slightly without breaking continuity:

- cloth folds
- camera-dependent lighting shifts
- wrinkle intensity
- makeup detail
- background crowd extras

If only soft anchors drift, default to `Watch` or `Patch`.

## State Anchors

Lock these within the current state window:

- current outfit
- injury level
- weather exposure
- dirt or blood level
- held object state

Use `shot-plan` and `asset-bible` state changes to define when a new state window starts.

## Sequence Grouping Rules

Build review groups using:

- same scene id
- same character + same outfit
- same location + same time of day
- same action beat across consecutive shots

Prefer group-level consistency judgments before individual shot judgments.

## Repair Guidance

- Face drift: strengthen reference image, character lock, and hard-anchor wording
- Costume drift: restate outfit id and visible clothing layers
- Prop drift: promote prop from background mention to required key element
- Environment drift: reinforce location anchor and time-of-day terms
- Style drift: restate format/style terms from `project-spec`
