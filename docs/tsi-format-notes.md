# TSI Format Notes

These notes describe observations from Traktor Pro controller mapping exports. The format is not officially documented by Native Instruments, so treat every field as provisional until verified by import tests.

## Outer File

Many `.tsi` files are XML at the top level.

Controller mappings may be stored in entries such as:

```text
Entry Name="DeviceIO.Config.Controller"
```

The value can be a base64-encoded binary blob.

## Frame Structure

Observed binary sections use four-character frame tags and big-endian values.

Important frame tags:

```text
CMAS  mapping list
CMAI  mapping row
CMAD  mapping row payload/settings
DCBM  MIDI binding list and nested MIDI binding rows
DVST  next section after DCBM in many exports
```

Frame size semantics matter:

```text
frame start + 8 + frame size = next frame
```

The size field excludes the 8-byte frame header.

Getting this wrong can create files that look locally consistent but hang or crash Traktor during import.

## DCBM

`DCBM` links binding IDs to MIDI strings such as:

```text
Ch03.CC.004
Ch01.Note.C1
```

There is often an outer `DCBM` list frame and many nested `DCBM` binding frames.

Avoid naive tag searches such as `find("DCBM")` unless you are only doing initial exploration. Tags repeat inside the structure.

## CMAS / CMAI / CMAD

`CMAS` contains mapping rows.

Each `CMAI` row typically references:

- a MIDI binding ID from `DCBM`
- input/output direction
- a Traktor command/control ID
- a `CMAD` payload

`CMAD` contains interaction mode, assignment, set value, comments, modifiers, LED ranges, and command-family-specific fields.

## Counts And Sizes

When adding or deleting rows, both counts and byte sizes must be updated.

Observed examples:

```text
CMAS size
CMAS count
DCBM size
DCBM count
```

Earlier failed imports happened when row counts changed but section byte-lengths stayed stale.

## In-Place Edits

The safest successful edits were in-place edits that did not change row count or section size.

Examples:

- rebinding an existing row to a different MIDI control
- changing a proven command-family value
- changing a modifier condition tuple
- changing a proven deck selector field

In-place edits still need import testing.

## Fragile Operations

These operations caused problems during real mapping work:

- adding rows from an incomplete seed
- deleting rows in a command family without a Traktor-created delete reference
- assuming one visible Deck A row represents the full family
- changing generic-looking fields across unrelated command families
- using local structural checks as proof of Traktor acceptance

Structural checks are necessary but not enough.

## Useful Reference

[Super Xtreme Mapper](https://github.com/SuperXtremeMapper/super-xtreme-mapper) is a helpful public reference for frame parsing and high-level `.tsi` interpretation.

Use it as a guide for frame semantics, not as proof that every opaque Traktor command-family field is understood.
