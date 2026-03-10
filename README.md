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

### IPS Configuration & Custom Signatures

I enabled IPS Mode on the OPNsense WAN interface and configured the system to utilize the Emerging Threats (ET) telemetry. While standard signatures were enabled, I also authored a custom Suricata rule to specifically monitor for unauthorized traffic on Port 4444 (the default Metasploit port).

<img width="3840" height="2064" alt="Screenshot 2026-03-09 140100" src="https://github.com/user-attachments/assets/ca154636-fafe-4aab-b3c4-e745f1406f62" /><br>
<br>

### Attack Execution and Prevention Validation

I generated a malicious payload using msfvenom and established a listener on the Kali machine. Upon execution on the Windows 11 target:

- Suricata successfully identified the Meterpreter construct (SID: 2025644).

<img width="3840" height="2064" alt="Screenshot 2026-03-09 141653" src="https://github.com/user-attachments/assets/b5101887-b261-4196-a57d-7d6f64a413b9" />

- The IPS Engine immediately dropped the packets, preventing the reverse shell from being established.

<img width="3840" height="2064" alt="Screenshot 2026-03-09 141557" src="https://github.com/user-attachments/assets/e4fc15f1-5fb3-4e3e-8148-cbd10e954d28" />

- Verification: I confirmed the "Action: Blocked" status in both the OPNsense eve.json logs and the Wazuh dashboard.

<img width="3840" height="2064" alt="Screenshot 2026-03-09 143614" src="https://github.com/user-attachments/assets/913311b4-34f5-4f60-8835-2f61c9752114" />
<img width="3840" height="2064" alt="Screenshot 2026-03-09 143628" src="https://github.com/user-attachments/assets/e42461ea-4a9b-42bb-ac98-cc4c105a13ea" />
<details>
  <summary>Click to expand JSON Log</summary>

  ```json
  {
    "id": "12345",
    "status": "success",
    "message": "This is a very long log entry that normally takes up space."
  }

