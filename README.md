# Cloud & DevOps Fundamentals — Practice Repo

A hands-on learning project covering AWS security fundamentals, Linux CLI, 
and Git version control — built as part of my transition toward 
GRC engineering and cloud security roles.

## What's in here

- `hello.txt` — basic file operations and Git tracking practice
- `script.sh` — executable shell script (permissions practice: chmod, ownership)
- Branch history demonstrating feature-branch workflow

## Skills demonstrated

**AWS**
- IAM user creation with least-privilege principles and MFA
- S3 bucket configuration: default encryption (SSE-S3), Block Public Access
- Wrote and applied a custom bucket policy enforcing HTTPS-only access 
  (explicit deny on `aws:SecureTransport: false`) — a preventive control 
  pattern relevant to SOX ITGC and vendor security assessment work

**Linux CLI**
- Directory navigation and file management
- File permission management (chmod numeric notation, ownership with chown)
- Understanding permission structure: owner/group/other read-write-execute

**Git / GitHub**
- Repository initialization, staging, and committing
- Remote repository setup and authentication via Personal Access Token
- Branching and workflow practice (feature branches, merge-ready structure)

## Why this matters

Coming from an IT audit and security compliance background (SOX 404 ITGC/ITAC 
testing, Continuous Controls Monitoring platform design), I'm building hands-on 
technical fluency in the tools that underpin modern GRC engineering — 
policy-as-code, cloud security controls, and version-controlled infrastructure.

## Next steps

- [ ] EC2 instance + SSH practice
- [ ] Terraform / Infrastructure as Code
- [ ] OPA/Rego policy-as-code examples
- [ ] Python scripting for AWS API integration