# Agent Workflow For Traktor Mapping Edits

This guide is written for AI coding agents working with exported Traktor `.tsi` files.

## Operating Rules

- Work from exported copies, not live assumptions.
- Create a backup before every write.
- Keep backups outside the live import folder when possible.
- Never edit a `.tsi` unless the change is small enough to describe exactly.
- Prefer in-place payload changes over adding or deleting mapping rows.
- After each edit, report the changed file, exact mapping change, what to test, and rollback file.
- Stop when a command family is not understood well enough.

## Safe Edit Ladder

Use the lowest-risk edit that can accomplish the task.

1. In-place MIDI rebinding with unchanged command payload.
2. In-place value change on a proven command family.
3. In-place modifier condition change using a known condition tuple.
4. Clone rows inside a family that has already been proven by a successful import.
5. Add new rows only after a user-created seed proves the command family.
6. Avoid deleting rows unless a Traktor-created export proves the delete pattern.

## Backup Rule

Before writing the active export, create a rollback copy named with the purpose and date.

Example:

```text
backups/export.pre-beatjump-reorder-YYYYMMDD-01.tsi
```

The backup should be the exact pre-edit file.

## Seed Export Rule

When a mapping family is unknown, ask the user to create one or two minimal examples in Traktor and export again.

A good seed export answers:

- Which command did Traktor create?
- Which binding ID was used?
- Which fields changed?
- Did Traktor add companion rows?
- Did Traktor use direct, toggle, hold, or output interaction mode?

Do not extrapolate from a visible row if the family may have hidden companion behavior.

## Modifier Layer Rule

When adding a modifier layer to an existing physical control, guard the original layer explicitly.

Example:

```text
Original behavior: M1=0
Shifted behavior:  M1=1
```

This prevents both layers from firing together.

## Deck Assignment Rule

Do not use `Device Target` for user-facing mappings.

Prefer explicit assignments:

```text
Deck A
Deck B
Deck C
Deck D
```

Some command families encode deck assignment in the visible target field. Others encode it in command-specific selector fields. Use a user-created seed when in doubt.

## Report Format

After each edit pass, report:

1. Which file changed.
2. What exact mapping was added or changed.
3. What the user should test in Traktor.
4. What the rollback file is called.

Keep reports factual. Do not claim success until Traktor import and behavior are confirmed.
