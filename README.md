📌 AWS Multi-Account Compliance Architecture

🔸 Project Overview
This project demonstrates an enterprise-style compliance architecture in AWS. It centralizes compliance evidence across multiple accounts by forwarding AWS Config logs and AWS Security Hub findings into a single management account.

The workflow simulates how cleared GovCloud and enterprise environments aggregate compliance data for audit readiness, continuous monitoring, and RMF documentation.

🔸 Tools & Services

AWS Config – resource state tracking, compliance snapshots

AWS Security Hub – compliance/security findings (CIS, AWS Best Practices, NIST 800-53)

S3 (central evidence bucket) – encrypted, versioned evidence storage

Cross-Account S3 Bucket Policy – secure log delivery from member accounts

EventBridge (optional) – export Security Hub findings into S3 for long-term storage

🔸 Two Approaches: Lessons Learned

1. The “Unethical” / Quick & Dirty Way (What I Tried First)

Enabled Config + Security Hub manually in each account.

Each account had its own S3 bucket, creating silos.

Findings stayed isolated in each account.

Result = duplication, audit blind spots, and no central visibility.

This violated best practices — an auditor would have to log into multiple accounts to piece compliance together.

2. The Best Practice / Enterprise Way (Final Implementation)

Built a single evidence bucket in the management account.

Applied a cross-account bucket policy so the dev account could write logs into mgmt’s bucket.

Designated the management account as Security Hub aggregator to collect findings org-wide.

Verified centralized evidence: both Config logs + Security Hub findings now land in mgmt.

Result = scalable, audit-ready architecture that mirrors how GovCloud / DoD teams operate.

📌 Key Lesson
The wrong approach works short-term but creates chaos.
The right approach builds centralized, automated, and scalable compliance visibility across the organization.

🔸 Workflow

Central Evidence Bucket – created in mgmt with versioning + SSE-KMS.

AWS Config – mgmt + dev accounts deliver logs into the central bucket (AWSLogs/<AccountID>/Config/...).

Security Hub – mgmt account acts as the aggregator, collecting findings from dev + mgmt.

Cross-Account Policies – ensure secure log delivery without exposing public access.

Evidence Validation – confirmed logs + findings centralized in mgmt account.

🔸 Evidence (Screenshots / Reports)

S3 bucket showing both mgmt + dev Config logs

Security Hub console displaying findings from multiple accounts

Bucket policy JSON (cross-account delivery)

Sample Security Hub finding JSON stored in S3

🔸 Key Takeaways

✅ Centralized compliance evidence → single source of truth

✅ Cross-account bucket policies designed securely

✅ Aggregated Security Hub findings → one pane of glass

✅ Mirrors enterprise / GovCloud compliance workflows

✅ Prepares foundation for Step 4: ATO documentation (POA&M, control mapping)
