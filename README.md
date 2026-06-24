# aws-security-toolkit

> A practical **AWS security toolkit**: battle-tested **IAM policy examples**, **EMR / Hadoop / Kafka security templates**, and reference snippets distilled from **15+ years of securing data platforms at enterprise (MNC) scale for AWS and Big Data** .

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Keywords:** AWS IAM policy examples · AWS security templates · EMR Hadoop security AWS · least privilege IAM · enterprise data platform security AWS

---

## Why this exists

Securing AWS well is mostly a pattern problem — the same IAM, encryption, and data-platform controls recur across every regulated environment, yet teams rebuild them from scratch each time. This is the umbrella repo for those reusable patterns: the things I reach for repeatedly, hardened by real enterprise-scale operation rather than copied from a docs page.



---

## What's in here

| Path | Purpose |
|---|---|
| `iam/` | Least-privilege IAM policy examples + the policy-evaluation-logic explainer |
| `emr-hadoop/` | EMR / Hadoop / Kafka security templates (encryption, auth, network isolation) |
| `encryption/` | KMS patterns, S3 + EBS encryption baselines |
| `detective/` | GuardDuty, Security Hub, Config quick-start snippets |

---

## Highlights

- **IAM policy evaluation logic** — the diagram AWS should have shipped (IAM was the #1 in-demand Melbourne JD skill).
- **EMR/Hadoop hardening** — encryption-in-transit/at-rest, Kerberos, fine-grained access — from running this in production at scale.
- **Least privilege that survives an audit** — policies written to pass a CPS 234 review, not just to work.

---

## Status

🟢 **Rolling repo — v1 content shipped.** Live: least-privilege data-platform IAM policy
(`iam/`), EMR security configuration + hardening guide (`emr-hadoop/`), CMK key policy +
key-management checklist (`encryption/`), detective-controls quick start (`detective/`).
More patterns added continuously. All examples use placeholder account IDs — replace before use.

---

## Related

- 📖 Blog: [IAM Policy Evaluation Logic — the diagram AWS should have made](https://aiopsone.com/blog/iam-policy-evaluation-logic)
- 📖 Blog: [Securing Hadoop/EMR on AWS — lessons from MNC scale](https://aiopsone.com/blog/securing-emr-hadoop-aws)
- 🌐 More at **[aiopsone.com](https://aiopsone.com)** — AI-powered AWS Security & Cloud Operations for APRA-regulated Australia.
