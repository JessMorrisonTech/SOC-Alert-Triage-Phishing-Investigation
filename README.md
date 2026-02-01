# 🛡️ SOC Alert Triage – Phishing Investigation (SOC Simulator)

## 📌 Overview

This project documents a simulated **SOC alert triage and phishing investigation** completed in a SOC Simulator environment using Splunk-style logs, email telemetry, firewall events, and threat intelligence lookups.

The scenario mirrors a realistic SOC shift involving:
- Multiple inbound alerts
- Alert prioritization decisions
- False positives vs true positives
- Event correlation across data sources
- Escalation based on impact and containment status

---

## 🔍 Environment & Tooling

- **SIEM:** Splunk-style log interface  
- **Log Sources:**
  - Email gateway logs
  - Firewall / web-browsing logs
- **Threat Intelligence:** Internal reputation tool (VirusTotal-like)
- **Scenario Type:** Phishing detection & response

---

## 🧠 Investigation Summary

During the simulation, I investigated five alerts that arrived over a short time window. These included:

- Legitimate emails incorrectly flagged as malicious (False Positives)
- Phishing attempts flagged as supsicious by existing security controls
- An end user click on malicious link in phishing email resulting in allowed outbound traffic to malicious URL
- An incident requiring immediate escalation due to potential host compromise

Several alerts were related and required correlation across email and firewall data to understand the full scope of activity.

---

## 📂 Case Breakdown (High-Level)

### 🟢 False Positives

- Legitimate sender
- Clean URLs confirmed via threat intelligence
- No suspicious behavior or follow-up activity

**Action Taken:**  
Alert closed with documentation

**Outcome:**  
No escalation required

---

### 🟡 True Positives – Contained

**Indicators Observed:**
- Phishing email using Amazon look-alike (doppelgänger) domains
- Urgent language designed to prompt action
- Shortened URLs used to obscure the final destination
- User clicked the link
- Firewall successfully blocked outbound traffic

**Action Taken:**
- Validated malicious intent using threat intelligence
- Correlated email and firewall logs
- Confirmed no user or system impact
- Recommended phishing awareness training and sender blocking on mail Tenant

**Outcome:**  
Threat contained by existing security controls; no escalation required

---

### 🔴 True Positive – Escalated Incident

**Key Indicators:**
- Phishing email impersonating Microsoft using a typosquatted domain
- Urgent messaging designed to induce fear and immediate action
- User clicked the phishing link
- Firewall allowed outbound HTTPS traffic
- Destination URL confirmed malicious via threat intelligence

**Why This Required Escalation:**
- Successful access to a malicious site
- Potential for credential harvesting or malware delivery
- Risk extended beyond email-level containment

**Action Taken:**
- Correlated email and firewall logs
- Identified affected user, host, internal IP, and destination IP
- Verified no additional users were targeted
- Escalated for host isolation and incident response

**Outcome:**  
Incident escalated for further investigation and containment

---

## 🧩 Correlation & Analysis Highlights

- Pivoted from email alerts to firewall web-browsing logs
- Mapped user → host → IP → outbound destination
- Distinguished between:
  - Attempted compromise
  - Successful access with potential impact
- Used alert severity as guidance, not a decision-maker

---

## 📉 Lessons Learned

### 1. MTTR vs Thoroughness
I rushed the ending of an investigation due to time concerns from pivoting from email alert and logs to firewall logs and missed additional host-level indicators.

**Takeaway:**  
Speed matters, but thorough investigation prevents missed compromises.

---

### 2. Escalation Is Impact-Based
Not all phishing alerts warrant escalation.

- Blocked link → only documentation required
- Allowed access → escalation required

**Takeaway:**  
Escalate based on exposure and impact, not alert type alone.

---

### 3. Correlation Is Critical
The most valuable findings came from connecting multiple alerts across data sources rather than investigating alerts in isolation. Linking the Email alert and logs to firewall logs to understand the exact events that occurred proved vital. Additional missed alerts also would have come from identifying Host-level/end point detection logs. 

---

## 🧪 Skills Demonstrated

- SOC alert triage and prioritization
- Phishing analysis and detection
- SIEM log analysis (email and firewall)
- Event correlation across multiple log sources
- Threat intelligence validation
- Incident escalation decision-making
- Clear and structured incident documentation
- Post-incident self-review and improvement

---

## 🔄 Investigation Challenges & Analyst Approach

The SIEM environment simulated continuous, real-time log ingestion, requiring investigation while new events were actively appearing.

Key challenges included:
- Sifting through large volumes of normal background traffic to identify relevant activity
- Determining whether alerts were isolated or part of a broader sequence
- Pivoting quickly between log sources while maintaining investigative context

To address this, I:
- Extracted key parameters (user, IP address, sender, recipient, URL) from alerts
- Performed targeted searches to isolate related activity across email and firewall logs
- Narrowed time windows to reduce noise and improve clarity of events

---

## 📈 Why This Project Matters

This simulation reflects real SOC analyst responsibilities, including:
- Incomplete or ambiguous data
- Time pressure
- Multiple concurrent alerts
- Judgment-based escalation decisions

It emphasizes analytical thinking and investigative discipline over tool-specific mechanics.

