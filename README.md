# Traktor Mapping Automation Notes

Practical notes for safely inspecting, editing, and expanding Native Instruments Traktor controller mappings.

The goal is to help Traktor users automate careful edits to exported `.tsi` files without manually clicking hundreds of rows in Controller Manager. The emphasis is safety: small edits, backups, seed exports, and repeatable verification.

This repository intentionally does not include any personal Traktor settings, mapping exports, backups, collections, logs, or device-specific private layouts.

## Who This Is For

- Traktor users with complex MIDI mappings.
- DJs building mappings across several controllers or decks.
- Developers and tool builders trying to understand enough of the `.tsi` structure to make conservative edits.

## Core Principle

Treat Traktor mapping exports as fragile binary data wrapped in XML.

Many `.tsi` files look like ordinary XML from the outside, but controller mappings may be stored in packed binary blobs such as `DeviceIO.Config.Controller`. Editing those blobs by guesswork can make Traktor hang or crash on import.

Use this workflow instead:

1. Export a known-good `.tsi`.
2. Back it up before every write.
3. Make the smallest possible change.
4. Prefer in-place edits over adding or deleting rows.
5. Import and test in Traktor before expanding further.
6. When a command family is unknown, create one manual seed export in Traktor and diff it.

## Repository Contents

- [Automation Workflow](docs/automation-workflow.md): a cautious workflow for automated `.tsi` editing.
- [TSI Format Notes](docs/tsi-format-notes.md): observed structure and frame parsing rules.
- [Mapping Patterns](docs/mapping-patterns.md): reusable patterns for modifiers, deck targeting, grids, and layered controls.
- [Troubleshooting](docs/troubleshooting.md): what import hangs usually mean and how to recover.
- [Privacy And Sanitization](docs/privacy-and-sanitization.md): what not to commit.

## Relationship To Existing Tools

The most useful public reference found during this work was [Super Xtreme Mapper](https://github.com/SuperXtremeMapper/super-xtreme-mapper). Its source and documentation helped clarify frame semantics, especially frame sizes and nested mapping structures.

This repository is not a replacement for a full Traktor mapping editor. It is a field guide for careful mapping automation.

## License

These notes are licensed under CC BY 4.0. That makes the material easy for people, tools, and documentation projects to reuse with attribution.

If this repo later grows executable tooling, consider licensing code files under MIT while keeping documentation under CC BY 4.0.
