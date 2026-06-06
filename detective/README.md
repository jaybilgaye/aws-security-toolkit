# Detective controls — quick start

The three AWS-native detective services that evidence CPS 234 ¶21/¶23. Enable them in every
in-use region (ideally centralised via a delegated administrator account in an Organization).

## GuardDuty — threat detection
```bash
aws guardduty create-detector --enable --region ap-southeast-2
# Org-wide: delegate an admin account, then auto-enable members
aws guardduty enable-organization-admin-account --admin-account-id 111122223333
```

## Security Hub — posture management + findings aggregation
```bash
aws securityhub enable-security-hub --enable-default-standards --region ap-southeast-2
# Subscribe to standards (CIS, AWS FSBP) for continuous checks
```

## AWS Config — configuration recording (the audit backbone)
```bash
# Config underpins conformance packs (see the cps234-aws-config-pack repo).
# Enable the recorder + delivery channel in every region before deploying rules.
aws configservice describe-configuration-recorders --region ap-southeast-2
```

## Turn detection into response
Detection without alerting is just storage. Wire high-risk events to alarms:
- CloudWatch metric filters on the CloudTrail log group (root usage, unauthorized API calls,
  console sign-in without MFA, IAM/policy changes).
- GuardDuty + Security Hub findings → EventBridge → SNS / ticketing / auto-remediation.

> These are the same controls the [Prowler APRA framework](https://github.com/jaybilgaye/steampipe-mod-aws-compliance-apra)
> and [Config pack](https://github.com/jaybilgaye/cps234-aws-config-pack) verify continuously.
