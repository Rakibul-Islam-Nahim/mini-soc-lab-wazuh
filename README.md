# Mini SOC Lab – Project Showcase

## 1. Project Overview

**Project Title:** Mini SOC (Security Operations Center) Lab using Wazuh  
**Objective:** Build a functional SOC lab to monitor, detect, and analyze security events using Wazuh Manager and Agents in a real-world–like environment.

This project demonstrates hands-on experience with:

- SIEM concepts
- Log collection and analysis
- Agent–manager architecture
- NAT traversal using Reverse SSH
- Incident detection and alerting

---

## 2. Architecture Diagram

![Architecture Diagram](/diagrams/Architecture-Diagram.png)

**Architecture Description:**

- **Wazuh Manager (Ubuntu VM):** Central server running Wazuh Manager, Indexer, and Dashboard.
- **Wazuh Agent (VPS / Linux Host):** Collects system logs, security logs, web server logs and Vulnearble Server logs.
- **Network Challenge:** Manager behind NAT.
- **Solution:** Reverse SSH tunnel from Agent to Manager.

---

## 3. Lab Environment

| Component      | Details           |
| -------------- | ----------------- |
| Host OS        | Windows           |
| Virtualization | Oracle VirtualBox |
| Manager OS     | Ubuntu 22.04 LTS  |
| Agent OS       | Ubuntu 22.04 LTS  |
| SIEM Tool      | Wazuh 4.14.7      |
| Network Mode   | NAT + Reverse SSH |

---

## 4. Network & Connectivity Setup

![data flow diagram](/diagrams/data%20flow.png)

### Data Flow Diagram

The Wazuh Manager includes wazuh-remoted, analysisd, the alert generator, and Filebeat. Data flows from Wazuh Agents to the Manager and then to the Wazuh Dashboard, where users can monitor and analyze logs. The Wazuh Indexer stores events efficiently and enables various search and analysis operations.

### Problem

- Manager VM is behind NAT
- Agent cannot directly reach Manager

### Solution

- Reverse SSH tunnel from Agent to Manager
- Agent connects to Manager via localhost tunnel

**Why Reverse SSH?**

- Bypasses NAT limitations
- Common real-world SOC workaround

---

## 5. Wazuh Installation Summary

### Manager Components

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### Agent

- Installed and registered to Manager
- Successfully connected and reporting

![Agents connected Successfully](/screenshots/agent-connect-suc.png)

---

## 6. Agent Registration & Verification

- Agent added using authentication key
- Agent status verified from dashboard

**Proof:**

- Active agent visible in Wazuh Dashboard
- Logs being received in real time

![Dashboard View](/screenshots/agent-working.png)

---

## 7. Security Monitoring & Alerts

### Test Scenario: Successfull root access

**Steps:**

```bash
ssh nahim@vpsIP
```

**Result:**

- Wazuh detects root access
- Alert generated with severity level

**Alert Information:**

- Timestamp
- Attacker IP
- Attack Descriptions
- Data Source User
- Data Destination User

![My login Status](/screenshots/ssh-login-attempt.png)

### Test Scenario: Failed SSH Login

**Steps:**

```bash
ssh root@vpsIP
```

**Result:**

- Wazuh detects authentication failure
- Alert generated with severity level

**Alert Information:**

- Timestamp
- Attacker IP
- Attack Descriptions
- Data Source User
- Data Destination User

![My login Status](/screenshots/ssh-login-attempt.png)

---

## 8. Logs & Analysis

- Agent logs: `/var/ossec/logs/ossec.log`
- Manager processes incoming logs
- Indexer stores searchable data

This demonstrates full **log → analysis → alert** pipeline.

---

## 9. Challenges Faced & Solutions

| Challenge            | Solution                             |
| -------------------- | ------------------------------------ |
| NAT connectivity     | Reverse SSH tunnel                   |
| Agent not connecting | Version & key mismatch fix           |
| Indexer issues       | Clean reinstall & correct cert setup |
| Network confusion    | IP tracing and routing analysis      |

---

## 10. Key Learning Outcomes

- Understanding SIEM architecture
- Agent–manager communication
- Real-world networking challenges
- Log-based threat detection
- Troubleshooting complex Linux services

---

## 11. Future Improvements

- Add multiple agents
- Enable File Integrity Monitoring (FIM)
- Add Sysmon / Windows agent
- Integrate email or Slack alerts
- Simulate brute-force or malware scenarios

---

## 12. Conclusion

This Mini SOC Lab demonstrates practical SOC skills using open-source tools. It reflects real-world scenarios such as NAT traversal, centralized monitoring, and incident detection.

This project strengthens hands-on cybersecurity and SOC analyst capabilities.

---

## 13. Author

**Name:** Rakib Ul Islam Nahim  
**Role:** Cybersecurity Student / SOC Learner  
**Focus Areas:** SOC, SIEM, Blue Teaming

---

_(End of Project Showcase)_
