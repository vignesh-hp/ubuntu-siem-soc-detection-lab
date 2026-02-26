# ubuntu-siem-soc-detection-lab
Built a SOC detection engineering lab using Splunk, simulating SSH brute force, privilege escalation, MITRE mapping, and incident tracking.
The lab detects and correlates:
SSH brute force attempts
Successful login after brute force
Privilege escalation via sudo
MITRE ATT&CK T1068 mapping
Incident status tracking
Risk scoring and severity classification

🏗 Architecture

Ubuntu Linux VM (Log Source)
Splunk Enterprise (SIEM)
Custom Correlation Rules
Alert-Based Event Logging
Dashboard Visualization

🚨 Detection Rules Implemented
1️⃣ SSH Brute Force Detection
Multiple failed login attempts from same IP
2️⃣ SSH Success After Brute Force
Successful login after repeated failures
3️⃣ Privilege Escalation Correlation
SSH login followed by sudo usage within 5 minutes

Mapped to:
MITRE ATT&CK – T1068 Privilege Escalation

🔥 Alert Enrichment

Each alert contains:
ALERT_TYPE
SEVERITY
STATUS (Open)
USER
HOST
MITRE Mapping

📊 SOC Dashboard Components

Brute Force Incidents
Privilege Escalation Count
Critical Alerts
Open Incidents
Risk Score (24h)
MITRE T1068 Counter
Attack Timeline

Latest SOC Alerts Table

📈 Risk Scoring Logic

Example:
Brute Force = 5 points
Success After Brute Force = 15 points
Privilege Escalation = 25 points

Total Risk Score calculated using Splunk SPL aggregation.

🎯 Skills Demonstrated
Detection Engineering
SIEM Rule Development
Correlation Logic
MITRE ATT&CK Mapping
Incident Tracking Simulation
Risk Quantification
SOC Dashboard Design
