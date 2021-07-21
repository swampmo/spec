---
name: Identifiers
route: /Identifiers
---

# DSNP Identifiers

## Specification Status

| Version | Status   |
| ------  | -------- |
| 1.0     | Proposed |

## DSNP User Id

- MUST be registered in the [Identity Registry](/Identity/Registry)
- MUST be hexadecimal
- MUST truncate any leading zeros
- MUST have a `0x` prefix
- MUST NOT be longer than 8 bytes

## DSNP Content Hash

- MUST be hexadecimal
- MUST be 32 bytes long
- MUST have a `0x` prefix
- MUST be a [keccak-256 hash](https://keccak.team/files/Keccak-submission-3.pdf) of the bytes of the content

### DSNP Protocol Scheme

- MUST always be the string `dsnp://`

## DSNP Announcement Id

DSNP Announcement Id consists of three parts, the scheme, the user id, and the content hash.

Any [Announcement Types](/Announcements/Overview#announcement-types) with a `fromId` and `contentHash` have a DSNP Announcement Id.

### Example
```
dsnp://0x1234567890abcdef/0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef
```

| part | value |
| ---- |------ |
| Scheme | `dsnp://` |
| User Id | `0x1234567890` |
| Content Hash | `0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef` |