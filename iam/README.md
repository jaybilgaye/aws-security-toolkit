# IAM — least privilege that survives an audit

Patterns for scoping data-platform access on AWS. The example
[`least-privilege-data-platform-role.json`](least-privilege-data-platform-role.json) is a
deployable identity policy for a typical ETL / analytics job role.

## Why it's written this way

| Statement | Pattern | Why it matters |
|---|---|---|
| `DataLakeScopedReadWrite` | Scope to the **exact bucket + prefixes**, never `s3:*` on `*` | The #1 audit finding is over-broad S3. Granting `curated/*` + `staging/*` is provable least privilege. |
| `KmsForDataLakeViaS3Only` | `kms:Decrypt`/`GenerateDataKey` gated by `kms:ViaService = s3...` | The role can decrypt data **through S3** but cannot use the CMK directly — blocks key misuse. |
| `GlueCatalogReadOnly` | Catalog reads scoped to one database | Jobs read schema, they don't mutate the catalog. |
| `DenyUnencryptedS3Writes` | Explicit **Deny** on `PutObject` without `aws:kms` SSE | An explicit deny beats any allow — even if a bucket policy lapses, this role physically cannot write plaintext. |

## The principle

Least privilege isn't a policy you write once — it's a process:

1. **Start from deny, add only what breaks.** Not the reverse.
2. **Attach to roles, not users.** Use short-lived role credentials (STS / instance profiles / IRSA), never long-lived access keys.
3. **Generate from real usage.** Use IAM Access Analyzer to build policies from CloudTrail activity instead of guessing.
4. **Re-review on a schedule.** Entitlement drift is the default state.

> Replace the account ID `111122223333`, region, bucket and KMS key ARN with your own before use.
