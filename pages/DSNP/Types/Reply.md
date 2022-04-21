# Reply Announcement

A Reply Announcement is the same as a [Broadcast Announcement](../Types/Broadcast.md),
but includes an `inReplyTo` field for noting it as a reply to a given [DSNP Content URI](../Identifiers.md#dsnp-content-uri).

## Fields

| Field | Description | Data Type | Serialization | Parquet Type | Bloom Filter |
| ----- | ----------- | --------- | ------------- | ------------ | ------------ |
| announcementType | Announcement Type Enum (`3`) | enum | [decimal](../Serializations.md#decimal) | `INT32` | no |
| contentHash | keccak-256 hash of content stored at URL | 32 bytes | [hexadecimal](../Serializations.md#hexadecimal) | `BYTE_ARRAY` | YES
| createdAt | milliseconds since Unix epoch | 64 bit unsigned integer | [decimal](../Serializations.md#decimal) | `UINT_64` | no
| fromId | id of the user creating the announcement | 64 bit unsigned integer | [decimal](../Serializations.md#decimal) | `UINT_64` | YES
| inReplyTo | Target [DSNP Content URI](../Identifiers.md#dsnp-content-uri) | UTF-8 | [UTF-8](https://datatracker.ietf.org/doc/html/rfc3629) | `UTF8` | YES
| url | content URL | UTF-8 | [UTF-8](https://datatracker.ietf.org/doc/html/rfc3629) | `UTF8` | no
| signature | creator signature | 65 bytes | [hexadecimal](../Serializations.md#hexadecimal) | `BYTE_ARRAY` | no

## Field Requirements

### announcementType

- MUST be fixed to `3`

### contentHash

- MUST be the [keccak-256 hash](https://keccak.team/files/Keccak-submission-3.pdf) of the bytes of the reference at the url

### createdAt

- MUST be set to the milliseconds since Unix epoch at time of signing

### fromId

- MUST be a [DSNP User Id](../Identifiers.md#dsnp-user-id)
- MUST be the [signer](../Signatures.md) of the announcement

### inReplyTo

- MUST be a [DSNP Content URI](../Identifiers.md#dsnp-content-uri)

### url

- MUST NOT refer to localhost or any reserved IP addresses as defined in [RFC6890](https://datatracker.ietf.org/doc/html/rfc6890)
- Resource MUST be one of the supported [Activity Content](../../ActivityContent/Overview.md) Types
- MUST use one of the supported URL Schemes

#### Supported URL Schemes

| Scheme | Description | Reference | DSNP Version Added |
| ------ |------------ | --------- | ------------------ |
| HTTPS | Hypertext Transfer Protocol Secure | [RFC2818](https://datatracker.ietf.org/doc/html/rfc2818) | 1.0 |

### signature

- MUST be an [Announcement Signature](../Signatures.md) over the all fields except the signature field