# 🛡 Ubuntu SIEM – SOC Detection Engineering Lab

## 📌 Project Overview

This project simulates a real-world Security Operations Center (SOC) detection environment using **Splunk Enterprise** and **Ubuntu Linux system logs**.

The lab demonstrates multi-stage attack detection, correlation logic, MITRE ATT&CK mapping, risk scoring, and incident tracking within a controlled SIEM environment.

The system detects and correlates:

- SSH brute force attacks  
- Successful login after brute force  
- Privilege escalation via `sudo`  
- Multi-stage attack behavior  
- Incident status lifecycle tracking  
- Risk score aggregation  

---

## 🏗 Architecture

Ubuntu VM (linux_secure logs)  
↓  
Splunk Index (main)  
↓  
Correlation Rules (SPL)  
↓  
Structured SOC Alerts (sourcetype=soc_alert)  
↓  
SOC Dashboard Visualization  

### Components Used

- Ubuntu Linux VM (log source)
- Splunk Enterprise (SIEM platform)
- Custom SPL detection queries
- Alert enrichment logic
- MITRE ATT&CK framework alignment

---

## 🚨 Detection Engineering Rules

### 1️⃣ SSH Brute Force Detection
Detects repeated failed login attempts from the same source IP.

**Logic:**
- Multiple `Failed password` events
- Aggregated by source IP

---

### 2️⃣ SSH Success After Brute Force
Detects successful login following repeated failures.

**Logic:**
- Prior failed attempts
- Followed by `Accepted password`

---

### 3️⃣ Privilege Escalation Correlation (MITRE T1068)

Detects SSH login followed by `sudo` usage within 5 minutes.

Example correlation logic:

```spl
transaction host actor maxspan=5m
```

Mapped to:

**MITRE ATT&CK – T1068: Privilege Escalation**

---

## 🔎 Alert Enrichment Model

Each generated SOC alert includes structured fields:

- `ALERT_TYPE`
- `SEVERITY`
- `STATUS` (Open)
- `USER`
- `HOST`
- `MITRE_TECHNIQUE`

Example alert event:

```
ALERT_TYPE=SSH_PRIVILEGE_ESCALATION
SEVERITY=Critical
STATUS=Open
USER=socadmin
HOST=ubuntu-siem
```

---

## 📊 SOC Dashboard Features

### 🔥 Executive KPI Overview
- Brute Force Incidents
- Critical Alerts Count
- Privilege Escalation Count
- Open Incidents

### 📈 Risk Scoring (24h)
Aggregated risk model based on alert severity weighting.

### 🧠 MITRE ATT&CK Mapping
Live counter for:
- T1068 – Privilege Escalation

### 📉 Attack Timeline
Time-based visualization of attack patterns.

### 🛑 Incident Queue
Active open incidents for analyst review.

---

## 📈 Risk Scoring Logic

Example scoring model:

| Detection Type | Risk Points |
|---------------|------------|
| SSH Brute Force | 5 |
| Success After Brute Force | 15 |
| Privilege Escalation | 25 |

Risk score calculated using:

```spl
stats sum(risk_points) as Total_Risk_Score
```

---

## 🧪 Attack Simulation Steps

To reproduce detection:

1. Generate multiple failed SSH login attempts.
2. Perform successful login.
3. Execute a `sudo` command.
4. Observe correlated SOC alert in Splunk.
5. Verify MITRE mapping and risk score update.

---

## 📂 Project Structure

```
ubuntu-siem-soc-detection-lab/
│
├── README.md
├── detections.md
├── LICENSE
└── screenshots/
```

---

## 🛡 Skills Demonstrated

- Detection Engineering (SPL Development)
- Multi-Event Correlation Logic
- MITRE ATT&CK Mapping
- Incident Lifecycle Simulation
- Risk Quantification Modeling
- SOC Dashboard Design
- Alert Enrichment and Structured Logging

---

## 🎯 Key Learning Outcomes

- Designing SOC detection workflows  
- Building correlated multi-stage attack detection  
- Mapping detections to MITRE ATT&CK framework  
- Implementing severity classification and incident tracking  
- Translating raw logs into actionable security intelligence  

---

## 🚀 Future Enhancements

- Threat intelligence enrichment
- Automated escalation simulation
- Incident closure workflow logic
- Geo-IP attacker enrichment
- Cloud log integration
