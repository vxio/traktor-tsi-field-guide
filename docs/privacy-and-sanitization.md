# Privacy And Sanitization

Traktor folders can contain personal data and device-specific configuration. Do not publish raw working folders.

## Do Not Commit

Avoid committing:

```text
*.tsi
*.nckf1
*.nml
*.nml.gz
Traktor logs
Crash logs
Collection backups
Cover art
Stripe/transient analysis files
Personal controller exports
Backup rollback files
Third-party mappings unless their license allows redistribution
```

## Safe To Commit

Generally safe:

```text
general workflow notes
sanitized field observations
high-level command-family lessons
generic examples using placeholder MIDI controls
scripts that operate on user-provided files but do not include those files
```

## Sanitizing Examples

Prefer placeholders:

```text
ChNN.CC.NNN
Deck A/B/C/D
Modifier M1/M2/M3
```

Avoid exposing:

- personal device names
- custom set names
- collection paths
- backup filenames with personal structure
- raw exported controller blobs

## Third-Party References

It is fine to link to public references.

Do not copy third-party mapping files or source code into this repository unless the license permits it and attribution is preserved.
