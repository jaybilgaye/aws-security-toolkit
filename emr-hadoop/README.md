# EMR / Hadoop security on AWS

Hardening patterns for running EMR (and the Hadoop/Spark stack) securely — from years of
running these clusters in production, translated to AWS-native controls.

[`emr-security-configuration.json`](emr-security-configuration.json) is a deployable EMR
**security configuration**: apply it at cluster creation
(`aws emr create-security-configuration --name secure-cluster --security-configuration file://...`).

## What it does

| Layer | On-prem Hadoop | EMR equivalent (this config) |
|---|---|---|
| Encryption in transit | TLS + SASL on RPC/HTTP | `EnableInTransitEncryption` + PEM certs in S3 |
| Encryption at rest (storage) | HDFS TDE / LUKS | `LocalDiskEncryptionConfiguration` (EBS + local disk via KMS) |
| Encryption at rest (data) | — | `S3EncryptionConfiguration` SSE-KMS for EMRFS |
| Authentication | Kerberos + AD trust | `KerberosConfiguration` (dedicated KDC + cross-realm AD trust) |

## What changes vs on-prem — and what doesn't

**Doesn't change:** you still need encryption in transit, encryption at rest, strong
authentication, and an audit trail. The questions an auditor asks are identical.

**Does change:**
- **Kerberos still exists** on EMR (dedicated KDC + AD cross-realm), but **authorization**
  increasingly moves to **IAM + Lake Formation** for data access — coarse cluster auth via
  Kerberos, fine-grained data auth via IAM.
- **Ranger → IAM / Lake Formation.** Where you used Ranger policies, EMR uses IAM roles for
  EMRFS and Lake Formation grants. Map your Ranger policy intents to these.
- **Audit → CloudTrail + S3 access logs**, not a self-managed audit pipeline.

## The trap

Teams lift-and-shift the cluster into a VPC and call it secure because it's "internal."
**Internal is not a security control.** Lock down security groups to least-path, keep the
cluster in private subnets, front it with a bastion / SSM Session Manager, and encrypt
everything — the blast radius of a compromised node is the whole data lake otherwise.

> Replace the account ID, region, KMS key ARN, S3 paths and AD realm before use.
