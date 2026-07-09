# Compliance Controls Mapping — AWS Security Configuration

This document maps hands-on AWS technical configurations (built in this repo) 
to recognized compliance control frameworks — NIST 800-53 and SOC 2 Trust 
Services Criteria — reflecting how audit-tested control objectives translate 
into real cloud infrastructure settings.

---

## Control 1: Encryption of Data at Rest

| Field | Detail |
|---|---|
| **Control Objective** | Sensitive data must be encrypted while stored, to protect confidentiality if underlying storage media is compromised |
| **Framework Reference** | NIST 800-53: SC-28 (Protection of Information at Rest) / SOC 2: CC6.1 |
| **Technical Implementation** | S3 bucket configured with default encryption (SSE-S3) — AWS automatically encrypts every object using AES-256 at write time |
| **Evidence / How to Verify** | Console: S3 → Bucket → Properties → Default encryption shows "Enabled, SSE-S3"; CLI: `aws s3api get-bucket-encryption --bucket <bucket-name>` |
| **Control Type** | Preventive, automated |
| **Testing Approach** | Pull the bucket encryption configuration via API/CLI as evidence; confirm it is enabled and has not been disabled since the last review period |

## Control 2: Encryption of Data in Transit

| Field | Detail |
|---|---|
| **Control Objective** | Data must be protected from interception while moving between systems or users |
| **Framework Reference** | NIST 800-53: SC-8 (Transmission Confidentiality and Integrity) / SOC 2: CC6.7 |
| **Technical Implementation** | Bucket policy with explicit Deny statement blocking any request where `aws:SecureTransport` is `false` |
| **Evidence / How to Verify** | CLI: `aws s3api get-bucket-policy --bucket <bucket-name>`; confirm the Deny/SecureTransport statement is present |
| **Control Type** | Preventive, automated |
| **Testing Approach** | Attempt an HTTP (non-HTTPS) request against the bucket using a presigned URL and confirm it is rejected |

## Control 3: Least Privilege / Access Control

| Field | Detail |
|---|---|
| **Control Objective** | Users should only have the access necessary to perform their function; no shared or root-level credentials for daily use |
| **Framework Reference** | NIST 800-53: AC-6 (Least Privilege) / SOC 2: CC6.1, CC6.2, CC6.3 |
| **Technical Implementation** | Named IAM user created separate from root, with MFA enforced, rather than performing daily operations via the root account |
| **Evidence / How to Verify** | IAM Console → Users → confirm MFA device attached; IAM Credential Report: `aws iam generate-credential-report` shows root account not used for routine activity |
| **Control Type** | Preventive |
| **Testing Approach** | Review IAM credential report for root account last-used timestamp; confirm it is not being used operationally |

## Control 4: Public Access Restriction

| Field | Detail |
|---|---|
| **Control Objective** | Prevent unauthorized or anonymous access to sensitive stored data |
| **Framework Reference** | NIST 800-53: AC-3 (Access Enforcement) / SOC 2: CC6.1 |
| **Technical Implementation** | S3 Block Public Access enabled at the bucket level (all four sub-settings on) |
| **Evidence / How to Verify** | CLI: `aws s3api get-public-access-block --bucket <bucket-name>`; confirm all four settings show `true` |
| **Control Type** | Preventive |
| **Testing Approach** | Attempt anonymous access to a bucket object via a plain browser URL and confirm rejection with `AccessDenied` |

---

## Why this matters

Each control above follows the same lifecycle an auditor would test in a real 
environment: a stated **objective**, a **technical implementation**, a way to 
pull **evidence**, and a repeatable **test**. This mirrors the SOX 404 ITGC 
testing methodology (design effectiveness + operating effectiveness) applied 
to cloud-native infrastructure rather than legacy on-prem systems — the core 
skill set behind GRC engineering and policy-as-code practices.
