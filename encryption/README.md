# Encryption & key management

[`kms-key-policy-example.json`](kms-key-policy-example.json) is a least-privilege CMK key
policy for a data lake, separating three roles:

- **Root / IAM** — break-glass administration (keep IAM policies as the real control).
- **Key administrators** — manage the key lifecycle, but **cannot use it** to decrypt data
  (no `Decrypt`/`GenerateDataKey`). Separation of duties.
- **Key users** — the data-platform job role, allowed to use the key **only via S3**
  (`kms:ViaService`), never directly.

## Key-management checklist (CPS 234 ¶21)

- **Rotation on.** Enable automatic annual rotation on every customer CMK
  (`aws kms enable-key-rotation --key-id <id>`).
- **Separation of duties.** Admins manage; only workloads use. Never the same principal.
- **Scope usage.** Gate `Decrypt`/`GenerateDataKey` with `kms:ViaService` so a key bound to
  S3 can't be used elsewhere.
- **Deletion safeguards.** Treat `ScheduleKeyDeletion` as high-risk; alarm on it. A deleted
  key makes its data permanently unrecoverable.
- **Encrypt by default.** Turn on account-level EBS default encryption and S3 default
  encryption so new resources are encrypted without relying on per-resource config.

> Replace account ID, region and role names before use.
