# Contributing

Thanks for helping improve the Traktor TSI Field Guide.

This repository is documentation-first. Contributions should make `.tsi` mapping work safer, clearer, or easier to verify.

## Good Contributions

- General workflow improvements.
- Sanitized field observations.
- Reproducible import or crash lessons.
- Links to public references with attribution.
- Small scripts or examples that operate on user-provided files without including those files.

## Do Not Contribute

- Personal `.tsi` exports.
- Traktor collections or backups.
- Crash logs or analytics logs.
- Third-party mapping files unless their license clearly allows redistribution.
- Device names, collection paths, or other identifying details from a private setup.
- Raw controller blobs copied from private exports.

## Writing Style

- Prefer concrete, testable guidance.
- Mark uncertain observations as provisional.
- Separate mechanical file-format facts from behavior confirmed by Traktor import tests.
- When describing a failed edit, include what made it fail and what fixed it.

## Verification

Before opening a pull request or publishing a change:

1. Check that no raw Traktor exports or backups are included.
2. Check that examples use placeholders such as `ChNN.CC.NNN`.
3. Check that any command-family claims say whether they are proven or provisional.
4. Check that linked third-party references are public and attributed.
