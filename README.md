# 📌 AWS Multi-Account Compliance Architecture  

🔸 **Project Overview**  
This project demonstrates how to centralize compliance evidence across multiple AWS accounts using AWS Config and AWS Security Hub. It simulates an enterprise/GovCloud-style compliance setup, where findings and logs from member accounts are aggregated into a single management account for audit readiness and continuous monitoring.  

---  

🔸 **Tools & Services**  
- **AWS Config** – resource state tracking, configuration history  
- **AWS Security Hub** – compliance/security findings (CIS, AWS Best Practices, NIST 800-53)  
- **Amazon S3 (Central Evidence Bucket)** – encrypted, versioned compliance log storage  
- **Cross-Account S3 Bucket Policy** – secure delivery of logs from member accounts  
- **EventBridge (optional)** – export Security Hub findings into S3  

---  

🔸 **Workflow**  
1. **Initial Attempt (Unethical / Quick & Dirty)** – Enabled Config + Security Hub separately in each account (mgmt + dev). Each account had its own S3 bucket, creating silos. Findings were isolated, with no single source of truth. This approach was inefficient, audit-unfriendly, and not scalable.  
2. **Best Practice Implementation (Enterprise Way)** – Created a single evidence bucket in the management account. Applied a cross-account S3 bucket policy to allow member accounts to deliver Config logs securely. Designated the management account as the Security Hub aggregator. Verified findings from both mgmt + dev appear in the mgmt console and Config logs flow into the central bucket.  

---  

🔸 **Evidence (Screenshots / Reports)**  
- S3 bucket with both mgmt + dev Config logs (`AWSLogs/<AccountID>/Config/...`)  
- Security Hub console showing findings from management + dev accounts  
- Cross-account bucket policy JSON  
- Example Security Hub finding JSON exported to S3  

---  

🔸 **Key Takeaways**  
- Learned the difference between siloed setups vs centralized compliance.  
- Built a scalable enterprise-style architecture for compliance evidence.  
- Gained hands-on with cross-account permissions and aggregator setup.  
- Demonstrated continuous monitoring practices aligned with GovCloud/FedRAMP standards.  

---  

## 📚 References & Documentation  
- [AWS Config Documentation](https://docs.aws.amazon.com/config/)  
- [AWS Security Hub Documentation](https://docs.aws.amazon.com/securityhub/)  
- [DISA STIGs & NIST 800-53](https://public.cyber.mil/stigs/)  
- [Google Doc – Full Project Documentation](#)  
