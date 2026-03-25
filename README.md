# Entra ID Credential Compromise Incident Response

## Overview
This project documents a simulated enterprise security incident involving a phishing (vishing) attack that resulted in credential compromise within a Microsoft Entra ID environment.

The investigation demonstrates a full incident response workflow, including identity log analysis, SIEM correlation, containment, remediation, and security control improvements aligned with Zero Trust principles.

---

## Incident Summary
- **Attack Type:** Vishing (voice phishing) + credential compromise  
- **Affected System:** Microsoft Entra ID (Azure AD)  
- **Impact:** Unauthorized access to corporate account  
- **Severity:** High  
- **Status:** Contained and remediated  

---

## Key Findings
- Successful authentication using single-factor credentials due to lack of enforced MFA registration  
- Unauthorized actions performed by attacker:
  - Password reset via self-service  
  - Creation of malicious security group (`THIS IS PHISHED`)  
  - Privilege escalation attempt through group ownership  
- Multiple login attempts originating from Microsoft Azure IP addresses  
- Over 350 security alerts analyzed during investigation  

---

## Detection and Analysis

### Identity Logs (Microsoft Entra ID)
- Identified anomalous sign-in activity
- Confirmed successful login without MFA challenge
- Detected password reset and post-compromise activity

### SIEM Analysis (Wazuh)
- Correlated 350+ endpoint and security alerts  
- Identified authentication events and privilege escalation indicators  
- Observed active connections to cloud infrastructure during attack window  

---

## MITRE ATT&CK Mapping
- **T1566.004** – Phishing (Vishing)  
- **T1078** – Valid Accounts  
- **T1098** – Account Manipulation  
- **T1069** – Permission Groups Discovery  
- **T1078.004** – Cloud Accounts  

---

## Root Cause
The primary control failure was incomplete MFA registration. Although Conditional Access policies were configured to require MFA, enforcement failed because the user had not registered an authentication method.

---

## Remediation Actions

### Immediate Containment
- Revoked all active sessions  
- Reset compromised account credentials  
- Removed malicious group and access changes  
- Blocked attacker IP addresses  

### Security Improvements
Implemented Zero Trust Conditional Access policies:
- Enforced MFA registration and authentication  
- Required compliant devices  
- Restricted access to trusted locations  
- Blocked legacy authentication protocols  
- Enabled risk-based access controls  

### Additional Hardening
- Strengthened password and lockout policies  
- Validated SIEM monitoring coverage  
- Reviewed identity and access configurations  

---

## Impact Assessment
- Prevented further unauthorized access  
- Reduced risk of lateral movement and privilege escalation  
- Strengthened identity security posture across the environment  
- Improved detection and response capabilities  

---

## Lessons Learned
- MFA policies must include enforced user registration  
- Social engineering attacks remain a high-risk entry point  
- Identity telemetry must be integrated into SIEM solutions  
- Conditional Access policies require continuous validation and tuning  

---

## Technologies Used
- Microsoft Entra ID (Azure AD)  
- Wazuh SIEM  
- Windows Endpoint Security Logs  
- Conditional Access Policies  

---

## Repository Contents
- `incident-report.pdf` — Full incident report with detailed analysis, logs, and remediation steps  

---

## Disclaimer
All data in this project is simulated for educational purposes. No real user or organizational data is exposed.
