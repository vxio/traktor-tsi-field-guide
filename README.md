# Traktor AI Mapping Notes

Practical notes for using AI coding agents to inspect, edit, and expand Native Instruments Traktor controller mappings.

The goal is to help Traktor users automate careful edits to exported `.tsi` files without manually clicking hundreds of rows in Controller Manager. The emphasis is safety: small edits, backups, seed exports, and repeatable verification.

This repository intentionally does not include any personal Traktor settings, mapping exports, backups, collections, logs, or device-specific private layouts.

## Who This Is For

- Traktor users with complex MIDI mappings.
- DJs building mappings across several controllers or decks.
- AI agents and coding assistants helping edit exported `.tsi` files.
- Developers trying to understand enough of the `.tsi` structure to make conservative edits.

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

- [Agent Workflow](docs/agent-workflow.md): how an AI agent should approach `.tsi` editing.
- [TSI Format Notes](docs/tsi-format-notes.md): observed structure and frame parsing rules.
- [Mapping Patterns](docs/mapping-patterns.md): reusable patterns for modifiers, deck targeting, grids, and layered controls.
- [Troubleshooting](docs/troubleshooting.md): what import hangs usually mean and how to recover.
- [Privacy And Sanitization](docs/privacy-and-sanitization.md): what not to commit.

## Relationship To Existing Tools

The most useful public reference found during this work was [Super Xtreme Mapper](https://github.com/SuperXtremeMapper/super-xtreme-mapper). Its source and documentation helped clarify frame semantics, especially frame sizes and nested mapping structures.

This repository is not a replacement for a full Traktor mapping editor. It is a field guide for careful AI-assisted mapping work.

## License

These notes are licensed under CC BY 4.0. That makes the material easy for people and AI agents to reuse with attribution.

If this repo later grows executable tooling, consider licensing code files under MIT while keeping documentation under CC BY 4.0.
