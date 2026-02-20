
---

markdown
# AWS IAM Interview Q&A – Scenario-Based Technical Questions

---

## IAM Core Concepts
**Q1:** Difference between IAM User and Role?  
**A:** User = permanent; Role = temporary, assumed via STS; Roles preferred for production and cross-account access.

**Q2:** IAM Policy Evaluation Logic?  
**A:** Explicit Deny → Explicit Allow → Implicit Deny

---

## IAM Policy Simulator
**Q3:** How to troubleshoot access denied in production?  
**A:** Use IAM Policy Simulator → Select role/user → Add action/resource → Run simulation → Check SCPs and permission boundaries.

**Q4:** How does SCP affect IAM Policy?  
**A:** SCP only restricts max permissions; does not grant access.

---

## Terraform IAM
**Q5:** How to safely manage IAM in Terraform?  
**A:** `aws_iam_policy_document`, modularized policies, permission boundaries, environment isolation, prevent_destroy, OIDC federation, no hardcoded JSON.

---

## IAM Attacks / Privilege Escalation
**Q6:** What is iam:PassRole abuse?  
**A:** User passes role to services (EC2, Lambda), gaining higher privileges. Mitigate via specific ARN restrictions, monitor unusual activity.

**Q7:** CloudFormation stack escalation scenario?  
**A:** If attacker has cloudformation:CreateStack → create role with admin → full compromise. Mitigate with restrictions & CloudTrail monitoring.

**Q8:** Trust Policy misconfiguration?  
**A:** `"Principal": "*"` allows any AWS account to assume role. Restrict to specific accounts/services.

---

## Kubernetes (IRSA)
**Q9:** How to securely give pods AWS access?  
**A:** IRSA → OIDC → IAM role per service account → Trust policy scoped to namespace → Annotate service account → Least privilege policies.

**Q10:** IRSA misconfigurations?  
**A:** Broad trust policy, wildcard IAM permissions, unrestricted namespaces.

---

## AWS Organizations Guardrails
**Q11:** What is a guardrail?  
**A:** SCP + OU-level restrictions enforcing compliance and preventing dangerous actions.

**Q12:** Common SCP mistakes?  
**A:** Overly restrictive (`sts:AssumeRole`), using SCP to grant access, no break-glass process.

---

## Zero Trust
**Q13:** Explain Zero Trust in AWS.  
**A:** Identity-first, temporary credentials, least privilege, multi-account isolation, continuous logging and verification, no implicit trust.

**Q14:** Zero Trust vs Privilege Escalation.  
**A:** Privilege escalation = attacker exploits misconfig. Zero Trust = architecture preventing escalation.

---

## Additional Scenario-Based Q&A
- Securing Production Account → Separate account + SCP + RBAC + MFA + monitoring  
- Mitigating STS token theft → Short sessions + CloudTrail alerts  
- CI/CD IAM best practices → OIDC federation, no static keys, assume-role  
- Multi-account design → OU + SCP layers + centralized logging + break-glass process

---

# ✅ Interview Preparation Notes
- Emphasize least privilege, temporary credentials, role assumption  
- Reference IAM Policy Simulator for debugging  
- Use Terraform examples to show production-grade management  
- Understand real-world attacks and mitigations  
- Explain Zero Trust as the defense strategy