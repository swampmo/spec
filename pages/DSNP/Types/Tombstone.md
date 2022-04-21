# Tombstone Announcement

A Tombstone Announcement is a way to note that a previous announcement signature is invalid and the related Announcement should be considered reverted.
It is NOT possible to revert a tombstone.

## Fields

| Field | Description | Data Type | Serialization | Parquet Type | Bloom Filter |
| ----- | ----------- | --------- | ------------- | ------------ | ------------ |
| announcementType | Announcement Type Enum (`0`) | enum | [decimal](../Serializations.md#decimal) | `INT32` | no |
| createdAt | milliseconds since Unix epoch | 64 bit unsigned integer | [decimal](../Serializations.md#decimal) | `UINT_64` | no
| fromId | id of the user creating the announcement and tombstoned announcement | 64 bit unsigned integer | [decimal](../Serializations.md#decimal) | `UINT_64` | YES
| targetAnnouncementType | target tombstoned announcement type | enum | [decimal](../Serializations.md#decimal) | `INT32` | no |
| targetSignature | target announcement signature to tombstone | 65 bytes | [hexadecimal](../Serializations.md#hexadecimal) | `BYTE_ARRAY` | YES
| signature | creator signature | 65 bytes | [hexadecimal](../Serializations.md#hexadecimal) | `BYTE_ARRAY` | no

## Field Requirements

### announcementType

- MUST be fixed to `0`

### createdAt

- MUST be set to the milliseconds since Unix epoch at time of signing

### fromId

- MUST be a [DSNP User Id](../Identifiers.md#dsnp-user-id)
- MUST be the [signer](../Signatures.md) of the target announcement

### targetAnnouncementType

- MUST be the [Announcement Type](../Announcements.md#announcement-types) of the target announcement
- MUST ONLY be a Tombstone Allowed Announcement Type

#### Tombstone Allowed Announcement Types

| Value | Name |
|------ | ---- |
| 2 | [Broadcast](../Types/Broadcast.md) |
| 3 | [Reply](../Types/Reply.md) |
| 4 | [Reaction](../Types/Reaction.md) |

### targetSignature

- MUST be an [Announcement Signature](../Signatures.md) that the `fromId` has announced

### signature

- MUST be an [Announcement Signature](../Signatures.md) over the all fields except this signature field
- MUST be the signature of the `fromId` user