# AWS Config + SNS: Real-Time S3 Public Access Monitoring
> **Tools & Services:** AWS Config | Amazon SNS | Amazon S3 | IAM  
> **Domain:** Cloud Security | Compliance Monitoring | Alerting  
> **📄 [View Full Technical Documentation](./AWS_Config_SNS_Installation_Guide.pdf)**

---

## Situation

Public S3 buckets are one of the most common causes of cloud data breaches. In an AWS environment without automated compliance monitoring, a misconfigured S3 bucket, made publicly accessible either accidentally or maliciously — can go undetected for hours or days. Manual auditing is not scalable and leaves a dangerous detection gap.

---

## Task

Configure an automated, real-time monitoring and alerting system on AWS that would detect the moment any S3 bucket became publicly accessible and immediately notify a designated security contact via email — without requiring manual checks or dashboard monitoring.

---

## Action

- **Configured AWS Config** with continuous recording across all resource types, applying the managed rule `s3-bucket-public-read-prohibited` to evaluate S3 bucket compliance on an ongoing basis
- **Created an SNS topic** (`SecurityAlertsTopic`) with an email subscription, confirming the endpoint to activate notification delivery
- **Linked AWS Config to the SNS topic** by editing the delivery channel settings, enabling Config to stream compliance change notifications directly to SNS
- **Simulated a breach** by creating a test S3 bucket and applying a public-read bucket policy to intentionally trigger a NON_COMPLIANT evaluation
- **Verified end-to-end detection** by confirming the Config dashboard turned non-compliant, the SNS email alert was received with full JSON event details, and the resource timeline in Config showed the exact timestamp and configuration change
- **Remediated the misconfiguration** by removing the public bucket policy and confirmed the dashboard returned to a COMPLIANT state

---

## Result

- **Real-time detection achieved:** AWS Config flagged the non-compliant S3 bucket within minutes of the public access policy being applied
- **Automated alerting confirmed:** SNS delivered an email notification containing the full compliance change record, including the affected resource ID, region, compliance type, and timestamps
- **Full audit trail established:** The AWS Config resource timeline captured every configuration change event, providing forensic-level visibility into when the bucket became public and when it was remediated
- **Zero manual intervention required:** The entire detect-and-alert pipeline operated automatically from misconfiguration to notification

---

## Key Concepts Demonstrated

- Continuous compliance monitoring using AWS Config managed rules
- Event-driven alerting architecture with SNS
- S3 bucket policy misconfiguration and remediation
- Cloud security audit trail and forensic investigation using resource timelines
