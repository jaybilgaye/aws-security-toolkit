# aws-security-toolkit

> A practical **AWS security toolkit**: battle-tested **IAM policy examples**, **EMR / Hadoop / Kafka security templates**, and reference snippets distilled from **15+ years of securing data platforms at enterprise (MNC) scale** — now focused on AWS.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Keywords:** AWS IAM policy examples · AWS security templates · EMR Hadoop security AWS · least privilege IAM · enterprise data platform security AWS

---

## Why this exists

Securing AWS well is mostly a pattern problem — the same IAM, encryption, and data-platform controls recur across every regulated environment, yet teams rebuild them from scratch each time. This is the umbrella repo for those reusable patterns: the things I reach for repeatedly, hardened by real enterprise-scale operation rather than copied from a docs page.

It's also the **bridge** between the data-platform past and the AWS Security present — proof that the "old" Hadoop/Kafka/EMR background is a *senior* signal: I've secured data at a scale APRA actually cares about.

---

## What's in here

| Path | Purpose |
|---|---|
| `iam/` | Least-privilege IAM policy examples + the policy-evaluation-logic explainer |
| `emr-hadoop/` | EMR / Hadoop / Kafka security templates (encryption, auth, network isolation) |
| `encryption/` | KMS patterns, S3 + EBS encryption baselines |
| `detective/` | GuardDuty, Security Hub, Config quick-start snippets |
| `docs/` | Notes + diagrams |

---

## Highlights

- **IAM policy evaluation logic** — the diagram AWS should have shipped (IAM was the #1 in-demand Melbourne JD skill).
- **EMR/Hadoop hardening** — encryption-in-transit/at-rest, Kerberos, fine-grained access — from running this in production at scale.
- **Least privilege that survives an audit** — policies written to pass a CPS 234 review, not just to work.

---

## Status

🟢 **Rolling repo** — populated continuously as posts and patterns ship. Scaffold + README first (Day 0).

---

## Related

- 📖 Blog: IAM Policy Evaluation Logic — the diagram AWS should have made *(post coming soon)*
- 📖 Blog: Securing Hadoop/EMR on AWS — lessons from MNC-scale *(post coming soon)*
- 🌐 More at **[aiopsone.com](https://aiopsone.com)** — AI-powered AWS Security & Cloud Operations for APRA-regulated Australia.
