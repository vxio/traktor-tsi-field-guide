# Troubleshooting

This document lists common failure modes seen while editing exported Traktor mappings.

## Traktor Hangs Or Crashes On Import

Treat this as a bad mapping file.

Immediate recovery:

1. Force quit Traktor if needed.
2. Restore the last known-good backup.
3. Confirm the backup imports.
4. Preserve the failed file for diffing.
5. Do not repeat the same edit strategy.

Likely causes:

- stale `CMAS` or `DCBM` size fields
- stale row counts
- malformed nested frame boundaries
- command-family semantics Traktor rejects
- row deletion in a fragile family
- rows added from an incomplete seed

## XML Parses But Traktor Still Fails

XML validity only proves the outer wrapper is readable.

A `.tsi` can still fail because the controller blob is semantically invalid.

Also, local frame boundary checks only prove mechanical structure. They do not prove Traktor accepts the mapping behavior.

## A Shifted Layer Fires Both Actions

Patch the original layer with the inverse modifier condition.

Example:

```text
Original row: M1=0
Shifted row:  M1=1
```

This rule applies whenever a modifier layer is added to the same physical control.

## Deck B/C/D Still Hits Deck A

Do not assume the visible `M3` condition changes assignment.

Check whether the command family also has:

- a target assignment field
- a deck selector field
- a combined deck-and-slot selector
- a bank offset such as `0-3`, `4-7`, `8-11`, `12-15`

Best fix:

1. Make one correct non-Deck-A seed manually in Traktor.
2. Export.
3. Diff that exact family.
4. Copy the complete assignment tuple to sibling rows.

## Toggle Versus Hold Versus Direct

Do not infer behavior from the command name alone.

Interaction mode matters:

```text
Toggle
Hold
Direct
Output
```

If the user asks for "always on" or "always off", verify that the source seed uses a force-state style row, not a toggle row.

## What To Do After A Crash

Use the corrected export as source of truth.

Ask:

- What rows did Traktor accept?
- Did Traktor modify existing rows instead of adding new rows?
- Did Traktor add hidden companion rows?
- Did Traktor change assignment fields outside the obvious row?

Then document the family-specific rule before making more edits.
