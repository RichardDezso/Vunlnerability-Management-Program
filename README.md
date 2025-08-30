# Official [Cyber Range](http://joshmadakor.tech/cyber-range) Project

# Vulnerability Management Program Implementation

In this project, we simulate the implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="https://github.com/user-attachments/assets/cfc5dbcf-3fcb-4a71-9c13-2a49f8bab3e6">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

## Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  
[Draft Policy](https://docs.google.com/document/d/1UPNPnb0mpagaz8XC0avGzvYr9HSTWgi6ZxRaKBsnoIw/edit?usp=drive_link)

---

## Step 2) Mock Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.

---

### 🎯 Objective
- Finalize vulnerability remediation timelines in a way that balances **security risk reduction** with **operational feasibility**.
- Gain **stakeholder buy-in** to ensure adoption across all departments.

---

### 🗣️ Meeting Summary (Paraphrased)
**Participants:**
- **Josh** – Cybersecurity and VM Analyst
- **Jimmy** – Server Team Manager
  
**Key Discussion Points:**
1. **Timeline Concern:**  
   - Original policy required **48-hour remediation** for all critical vulnerabilities.  
   - Department noted staffing challenges make this unrealistic for initial rollout.

2. **Proposed Adjustment:**  
   - Extend critical vulnerability SLA to **1 week** by default.  
   - Reserve 48-hour remediation only for **highly exploitable zero-day vulnerabilities**.

3. **Adoption Period:**  
   - Departments granted **6-month adjustment period** to adapt to new remediation and patching processes.

4. **Outcome:**  
   - Agreement reached to amend timelines in policy.  
   - Stakeholders expressed appreciation for inclusion in decision-making, boosting buy-in.

---

### 📌 Outcome & Value
- **Operational Realism:** Adjusted policy now matches actual capacity without undermining security.  
- **Zero-Day Protection:** Maintained rapid response for truly critical threats.  
- **Stronger Buy-In:** Early involvement of department heads increased policy acceptance.

---

### 📖 Key Takeaways for Security Governance
- **Engage stakeholders early** to avoid pushback and policy non-compliance.  
- **Differentiate between all criticals vs. urgent zero-days** for more precise SLAs.  
- **Include an adoption phase** to allow gradual process maturity.

---

---

## Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  
[Finalized Policy](https://docs.google.com/document/d/1fEdVMewDT9JLc4yxisGJj2uRla3nB51qzpF47_H6tZk/edit?usp=sharing)
<div style="text-align: center;">

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/6705819a-6aba-490e-8b57-17a964bd290b" />

</div>

---

## Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  


**Description**  
Kickoff meeting to align on **weekly credentialed vulnerability scans** of the server estate. We clarified scope, risks, and guardrails for scanning approximately **2,200 assets** and agreed on a safe pilot before full rollout.

---

### 🎯 Objective
- Begin scheduled credentialed scans without impacting availability.  
- Address concerns about resource usage and credential security.  
- Agree on a Just-In-Time access model and a pilot approach.

---

### 🗣️ Meeting Summary (Paraphrased)
**Participants:**  
- **Josh** – Cybersecurity and VM Analyst
- **Jimmy** – Server Team Manager

**Key Points:**  
1. **Scan plan:** Weekly scans targeting server infrastructure. Estimated **4–6 hours** to scan the environment of ~**2,200 assets**.  
2. **Credentialed approach:** Scan engine requires **administrative credentials** to log in and validate registry keys, installed software, insecure protocols, and cipher suites.  
3. **Risk concerns:** Jimmy raised impact and safety concerns: CPU, I/O, and memory utilization, and the risk of broad admin access.  
4. **Guardrails proposed:**  
   - Start with **one pilot server**, monitor resource utilization closely.  
   - Use **Active Directory dedicated scan account**, created up front, **disabled by default**, **enabled only during the scan window**, then **disabled or deprovisioned**.  
   - Automate provisioning and toggling of the account.  
5. **Next steps:** Susan to automate account provisioning. Proceed after credentials are ready and the pilot completes successfully.

---

### 🛡️ Agreed Guardrails
- **Pilot first:** Single-server test, then staged rollout.  
- **JIT credentials:** Dedicated AD account, disabled outside the scan window.  
- **Change window:** Run scans in a defined maintenance window.  
- **Resource safety:** Use safe-check profiles, throttle where supported, and watch CPU, RAM, disk, and network.  
- **Auditability:** Log who enabled the account, when, and what was scanned.  
- **Scope control:** Target servers only, exclude fragile systems until validated.

---

### 📌 Outcome & Value
- Stakeholders agreed to a **safe, credentialed scanning model** with **JIT access**.  
- A **pilot scan** will validate performance before weekly schedules go live.  
- Automation reduces standing access and improves audit trails.

---

### 📖 Key Takeaways
- Credentialed scans give better signal quality, but you need **least privilege and JIT**.  
- A short **pilot** builds confidence and surfaces tuning needs early.  
- Clear **operational guardrails** reduce friction and speed adoption.

---

---

## Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/937cccbd-36bb-4445-97b9-e915085cda81" style="border: 2px solid black;">

[Scan 1 - Initial Scan](https://drive.google.com/file/d/1RBPVj_azKJMwmRZ8QILlb4hxIjQU3wQ7/view?usp=drive_link)




---

## Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

## Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="https://github.com/user-attachments/assets/bbf9478f-e1d1-4898-846e-b510ec8c6f72">

[Remediation Email](https://docs.google.com/document/d/1Eiuc2sxkQ7p-vThyEe3fvX0fGQmOrWBmZA9HbTcoGVQ/edit?tab=t.0)

---

## Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 

# Post-Initial Discovery Scan – Server Team Debrief

**Description**  
Follow-up with the Server Team after the first credentialed pilot scan. We confirmed **no performance impact**, reviewed **top findings** (outdated Wireshark, deprecated TLS/cipher suites, misconfigured Guest account, a few Windows Update items), and aligned on remediation via change control.

---

## 🎯 Objectives
- Validate that scanning did **not** affect availability or performance.  
- Prioritize findings and map each to a **repeatable fix**.  
- Prep remediation packages ahead of the next **Change Control Board (CCB)**.

---

## ✅ What we validated
- **Scan impact:** No outages, no abnormal CPU/RAM/disk; only expected connection spikes during the window.  
- **Patch mgmt:** Windows Update is in place; OS/application updates will flow next cycle.  

---

## 🔎 Top findings (pilot sample)
1. **Outdated Wireshark installs** across several servers.  
2. **Local Guest account** was a member of **Administrators** on at least one host (should be disabled and non-privileged).  
3. **Deprecated protocols/ciphers** enabled (TLS 1.0/1.1; medium-strength cipher suites).  
4. **Informationals:** self-signed host certs; Edge Chromium item likely resolved by patch cycle.

---

## 🛠 Remediation plan (actionable)
**A) Remove old Wireshark**  
- Use the repo script: `[Uninstall-Wireshark-Targeted.ps1](https://github.com/RichardDezso/Uninstall-Wireshark-Targeted)`  
  - Target by version/pattern or set `-MinVersion 4.2.0`.  
  - Run via Intune/SCCM or remote PS; log to `C:\ProgramData\WiresharkRemediation\remove-wireshark.log`.

**B) Fix Guest account configuration** *(baseline it)*  
- Ensure the **Guest** local account is **disabled** and **not** in Administrators.  
  ```powershell
  Get-LocalUser -Name 'Guest' -ErrorAction SilentlyContinue | Disable-LocalUser
  Remove-LocalGroupMember -Group 'Administrators' -Member 'Guest' -ErrorAction SilentlyContinue

**C) De-risk protocols and cipher suites**

-   **Disable TLS 1.0/1.1** (server & client) and prefer TLS 1.2/1.3.

-   Enforce modern cipher suites via GPO:\
    `Computer Configuration → Administrative Templates → Network → SSL Configuration Settings → SSL Cipher Suite Order`.

-   Stage/ring deployments; pilot on a non-critical OU before broad rollout.

**D) Let patch mgmt clear the update items**

-   No custom action unless detections persist after the next cycle; then investigate supersedence/detection logic.

* * * * *

📦 Deliverables (from Security to Server Team)
----------------------------------------------

-   **Wireshark removal package** (script + detection logic).

-   **Guest account hardening baseline** (disable/deny, group membership check).

-   **TLS/cipher hardening template** (GPO backup or script with rollback).

-   **Validation runbook** with pre/post checks.

* * * * *

🔁 Validation (pre/post checks)
-------------------------------

-   **Before:** snapshot of versions, Guest membership, TLS/protocol state, cipher order.

-   **After:** rescan + confirm:

    -   Wireshark removed (or ≥ allowed version).

    -   Guest disabled and not privileged.

    -   TLS 1.0/1.1 disabled; only modern suites allowed.

    -   Patch items closed by the next update window.

* * * * *

🚧 Risks & notes
----------------

-   Some legacy integrations may still negotiate TLS 1.0/1.1---use staged rollout + fallback plan.

-   Confirm **no apps rely on Wireshark/Npcap** before removing Npcap (we're removing Wireshark only by default).

-   Keep exceptions time-boxed with owner + review date.

* * * * *

📅 Next steps
-------------

-   Build remediation artifacts (Security).

-   Submit CCB change(s) for:

    1.  Wireshark removal, 2) Guest baseline, 3) TLS/cipher hardening (ringed).

-   Execute pilot OU → monitor → expand.

* * * * *


---

## Step 9) Mock CAB Meeting: Implementing Remediations

**Description**  
The Change Control Board (CAB) reviewed and **approved** the plan to harden servers by removing **legacy TLS protocols** and **weak cipher suites**, using a **tiered rollout** and a tested **rollback** path.

---

## 🎯 Objectives
- Reduce crypto risk by eliminating insecure protocol/suite negotiation.
- Roll out safely in stages with clear rollback and owner accountability.
- Prove effectiveness through monitoring and a follow-up vulnerability scan.

---

## 🔄 Scope of Change
- **Disable**: Deprecated TLS versions (e.g., 1.0/1.1) and medium/weak cipher suites.
- **Keep/Prefer**: Modern protocols and strong cipher suites already supported by the platform.
- **No app code changes** expected; the host simply refuses legacy handshakes.

---

## 💡 Why it matters
When legacy options are left enabled, clients and servers can “negotiate down” to them. That’s how otherwise secure systems end up using weak crypto. Removing the legacy options forces secure defaults and aligns with common compliance baselines.

---

## 🚀 Implementation Plan (Tiered)
1. **Pilot** — Small, low-risk cohort. Monitor closely for 48–72 hours.  
2. **Wave 1** — Non-critical tiers after pilot green-light.  
3. **Wave 2** — Remaining servers.  
4. **Exceptions** — Time-boxed, documented owner, review date.

**Change window:** off-hours. **Reboot required** for protocol changes.  
**Monitoring:** system health, app connectivity, TLS telemetry, and error rates.

---

## 👥 Roles & Responsibilities
- **Risk/SecOps**: Design remediation, define success criteria, track metrics.  
- **Infrastructure**: Deploy changes, monitor rollout, execute rollback if needed.  
- **Application Owners**: Validate critical paths, approve exceptions, sign off.  
- **CAB**: Governance, schedule, and final approval.

---

## 📦 Deliverables
- **Remediation package**: Protocol and cipher hardening with environment-ready settings.  
- **Rollback plan**: Clear steps to restore prior configuration if required.  
- **Runbook**: Pre-checks, change steps, post-checks, and communication templates.  
- **Monitoring plan**: What to watch, thresholds, and who responds.  
- **Validation plan**: How we confirm risk is closed (see below).

---

## ✅ Validation & Success Criteria
**Pre-change**  
- Baseline: current protocol/cipher exposure, key app transactions, and health metrics.

**Post-change**  
- No TLS 1.0/1.1 exposure observed in scans.  
- Key applications function normally (no handshake or integration errors).  
- No sustained uptick in error rates or support tickets.

**Success =** clean re-scan + stable app telemetry + stakeholder sign-off.

---

## ⚠️ Risk Handling
- **Compatibility**: Pilot first; maintain a temporary exception path with owner and expiry.  
- **Operational**: Schedule reboots; communicate impact windows in advance.  
- **Rollback**: Documented, tested, and ready if unexpected issues arise.

---

## 📝 CAB Decision
- **Outcome**: Approved to proceed with pilot → waves, rollback in place.  
- **Follow-ups**: Share pilot results at next CAB; submit wave schedules; confirm exception list.

---
---
## Step 10 ) Remediation Effort

#### Remediation Round 1: Outdated Wireshark Removal

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/RichardDezso/Uninstall-Wireshark-Targeted)  

<img width="634" alt="image" src="https://github.com/user-attachments/assets/7b4f9ab2-d230-4458-ac0f-c0ff070ae79a">

[Scan 2 - Third Party Software Removal](https://drive.google.com/file/d/1UiwPPTtuSZKk02hiMyXf31pXUIeC5EWt/view?usp=drive_link)


#### Remediation Round 2: Insecure Protocols & Ciphers

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/RichardDezso/Set-TlsProtocol)
[PowerShell: Insecure Ciphers Remediation](https://github.com/RichardDezso/Set-TlsCipherSuites)

<img width="630" alt="image" src="https://github.com/user-attachments/assets/0e96120d-8ec9-4f76-8e42-79c752200010">

[Scan 3 - Ciphersuites and Protocols](https://drive.google.com/file/d/1Qc6-ezQvwReCGUZNtnva0kCZo_-zW-Sm/view?usp=drive_link)


#### Remediation Round 3: Guest Account Group Membership

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/joshmadakor1/lognpacific-public/blob/main/automation/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1jVgikjfrV1YjOcL3QRT_oUB0Y82w22V7/view?usp=drive_link)


#### Remediation Round 4: Windows OS Updates

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="https://github.com/user-attachments/assets/870a3eac-3398-44fe-91c0-96f3c2578df4">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1tmDjeHl5uiGitRwWy8kFRi33q-nGi1Zt/view?usp=drive_link)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="https://github.com/user-attachments/assets/51f0aae8-7f36-4d90-b29f-5257e57155f9">

[Remediation Data](https://docs.google.com/spreadsheets/d/1FTtFfZYmFsNLU6pm8nTzsKyKE-d2ftXzX_DPwcnFNfA/edit?gid=0#gid=0)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1rvueLX_71pOR8ldN9zVW9r_zLzDQxVsnSUtNar8ftdg/edit?usp=drive_link) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.
Extension
Extension Embed



Actions

Your Business

Settings

Help
Search Amazon

United States
Search Amazon

