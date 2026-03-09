# Prompt Repair Patterns

Use these patterns to revise an existing generation brief instead of rewriting everything from scratch.

## 1. Add Missing Anchors

Use when a subject is drifting.

Pattern:

- restate character id and outfit id
- restate one or two signature face or hair traits
- restate required prop or location anchor

## 2. Remove Noisy Descriptions

Use when the model is overreacting to decorative language.

Remove:

- duplicate adjectives
- conflicting style tags
- unnecessary background details
- mood terms that fight the target emotion

## 3. Promote Required Elements

If a key element is missing, move it from general description into a required element list or earlier prompt position.

Examples:

- “holding cracked phone in right hand”
- “medium close-up”
- “same black trench coat as previous shot”

## 4. Tighten Reference Strategy

Use when continuity is failing:

- add `reference_shot`
- reuse a successful prior frame
- keep sequence members in one seed group
- lock character and outfit anchors

## 5. Change Generation Mode

Switch mode when the current mode is structurally weak:

- `text2img -> img2img` if identity drift is high
- `text2video -> img2video` if motion starts well from a strong frame

## 6. Parameter Repair

Common adjustments:

- lower style weight if stylization is overpowering identity
- increase reference strength if subject drift is severe
- change seed handling if variation is too large

## 7. Batch Repair Rules

- same failure pattern across a scene -> one regeneration batch
- one-off technical glitch -> isolate to one shot
- do not mix unrelated failure types in one batch unless they share the same anchor strategy
