# Mapping Patterns

These patterns are generalized from successful Traktor mapping edits. They are meant to guide cautious work, not replace import testing.

## Modifiers

A small modifier scheme is easier to reason about.

Recommended roles:

```text
M1 = primary shift
M2 = local or secondary shift
M3 = deck focus or performance deck target
```

Avoid inventing extra modifiers until there is a real space or state problem.

## Modifier Conditions

When the same physical button has two layers, both layers need explicit conditions.

Example:

```text
Base layer:    M1=0
Shifted layer: M1=1
```

If the base layer has no inverse condition, it may fire at the same time as the shifted layer.

## Deck Focus

For shared performance controls, `M3` can represent deck focus:

```text
M3=0 -> Deck A
M3=1 -> Deck B
M3=2 -> Deck C
M3=3 -> Deck D
```

Important: the `M3` condition alone does not necessarily change Traktor's command assignment. Many command families also require an internal deck selector or explicit assignment field.

## Explicit Assignment

Avoid `Device Target`.

Use explicit deck assignment whenever possible:

```text
Deck A
Deck B
Deck C
Deck D
```

If a command family stores assignment in an opaque selector field, create a seed export for one non-Deck-A example and copy the proven pattern.

## Grid Expansion

A grid can usually be expanded safely after one full row or one full deck bank is proven.

Good expansion pattern:

1. Confirm the source rows import and work.
2. Identify the exact field that changes between cells.
3. Change only that field for the target cells.
4. Keep MIDI binding, interaction mode, assignment, and modifier conditions unchanged unless they are part of the proven pattern.

## Beatjump Bank Pattern

For a 2x4 beatjump grid, a playable layout is:

```text
top row:    -4,  +4,  -8,  +8
bottom row: -16, +16, -32, +32
```

The important lesson is not the exact command ID or field index, which may vary by version. The lesson is that once the amount field is proven, reordering can often be done as an in-place value swap.

## Solo Behavior Pattern

Solo behavior usually needs multiple rows on the same control.

For example:

```text
selected target -> force ON
other targets   -> force OFF
```

Do not assume toggle rows can act as force-on or force-off rows. Use a Traktor-created direct/force-state seed.

## Output And LEDs

For LEDs, use output mappings rather than input mappings.

Examples:

```text
Add Out > Deck Common > Sync On
Add Out > Deck Common > Master
```

Generic MIDI devices may still require manual `In-Port` and `Out-Port` selection after import.
