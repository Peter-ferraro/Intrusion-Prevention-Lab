# Advanced Network Defense - IPS Integration & Automated Incident Response

## Overview

In this lab, I transitioned my security stack from a passive "Detection" model to an active "Prevention" model. I configured Suricata IDS/IPS on OPNsense to actively drop malicious traffic and engineered custom Wazuh rules to automate the incident response lifecycle by generating high-priority tickets in osTicket.

### Skills Learned

- Intrusion Prevention (IPS) Management: Configuring network interfaces for inline packet dropping and managing "Drop" vs. "Alert" rule actions.

- Detection Engineering: Authoring custom XML-based SIEM rules in Wazuh using regex and parent/child rule logic (if_sid).

- SIEM Tuning: Reducing "alert fatigue" by escalating high-fidelity logs (Blocked Malware) to critical severity levels.

- SOAR & Workflow Automation: Integrating security tools via Webhooks and APIs to automate the bridge between detection and ticketing.

- Log Analysis: Parsing complex JSON structures from Suricata eve.json to extract actionable security metadata (Source IP, Signature ID, Action).

### Tools Used

- Firewall/IPS: OPNsense, Suricata (Emerging Threats Ruleset)

- SIEM: Wazuh (Manager & Indexer)

- Ticketing/IR: osTicket

- Attacker/Victim: Kali Linux (Metasploit Framework), Windows 11

## Steps
