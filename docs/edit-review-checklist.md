# Edit Review Checklist

Use this checklist before importing an edited Traktor mapping.

## Before Editing

- Start from a known-good export.
- Create a rollback backup.
- Identify whether the change is in-place or requires adding/removing rows.
- Confirm the command family is already proven, or create a seed export first.

## Mechanical Checks

- XML parses.
- Base64 controller blob decodes.
- Frame boundaries line up.
- `CMAS` count matches its row count.
- `DCBM` count matches its binding count.
- Section byte sizes match the actual frame contents.
- No duplicate binding IDs were introduced.

## Behavioral Checks

- The mapping uses explicit assignment instead of `Device Target`.
- Modifier layers have inverse guards where needed, such as `M1=0` and `M1=1`.
- Toggle, hold, direct, and output behavior match the requested interaction.
- Deck B/C/D rows were verified against a real non-Deck-A seed when the family is opaque.
- No unrelated FX unit, slot, or deck target was changed.

## Import Test

- Import the edited mapping in Traktor.
- Set `In-Port` and `Out-Port` manually if needed.
- Test only the edited controls first.
- Spot-check the neighboring controls that share the same command family.
- Keep the failed file if Traktor hangs or crashes, then restore the rollback.

## After A Successful Test

- Document the changed rows.
- Document any newly discovered field rule.
- Note whether the pattern is proven for one deck, all decks, one controller, or all controllers.
