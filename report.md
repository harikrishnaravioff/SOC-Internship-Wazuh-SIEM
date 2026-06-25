# Week 1 — Wazuh SIEM Lab Deployment

## Executive Summary

The objective of this lab was to gain practical experience with Security Information and Event Management (SIEM) technology by deploying a Wazuh monitoring environment. The deployment consisted of a Wazuh Manager running as a virtual appliance on Oracle VirtualBox and a Wazuh Agent installed on a Kali Linux virtual machine. The main goal was to establish successful communication between the manager and the agent and verify that security events were being collected and processed correctly.

This setup represents a simplified version of a real-world security monitoring environment where endpoint agents continuously send system and security data to a centralized platform for analysis. Successful deployment was confirmed when the Wazuh Dashboard displayed "1 Agent Active," indicating that the agent had been successfully enrolled and was communicating with the manager.

---

## Methodology

The deployment process began with the installation of Oracle VirtualBox and the creation of the virtual machines required for the lab environment. The Wazuh Manager virtual machine was allocated approximately four CPU cores, eight gigabytes of RAM, and fifty gigabytes of storage. The network adapter was configured in Bridged Mode to allow direct communication between the virtual machines.

The official Wazuh OVA appliance was downloaded and imported into VirtualBox. After the initial boot, a static IP address was configured to maintain consistent network connectivity. The default administrative credentials were changed, and the Wazuh Dashboard was accessed through a web browser to verify that all services were operating correctly.

The Kali Linux virtual machine was then prepared for agent installation. The Wazuh repository and GPG key were added to the system, and the Wazuh Agent package was installed using the APT package manager. The IP address of the Wazuh Manager was specified during installation so the agent could communicate with the manager once the service started.

---

## Technical Findings

The deployment was completed successfully. The Wazuh OVA appliance booted correctly and all core services were available after startup. Network communication between the Wazuh Manager and the Kali Linux agent functioned as expected, allowing the enrollment process to complete successfully.

After enrollment, the agent appeared in the dashboard with its assigned agent ID, hostname, operating system information, and IP address. The dashboard reported one active agent with no disconnected or pending agents. The enrolled system was identified as **agent11** running **Kali GNU/Linux 2026.2** with **Wazuh version 4.14.5**.

Security events and inventory information began appearing in the dashboard shortly after enrollment. The File Integrity Monitoring, Log Analysis, and Vulnerability Detection modules automatically initiated baseline monitoring on the Kali Linux system. Active alert generation was confirmed, including low and medium severity alerts collected during the monitoring period.

---

## Screenshots

> Add your Week 1 screenshots to the `screenshots/` folder and reference them below.

```
![Dashboard Active Agent](screenshots/dashboard-active-agent.png)
![Agent Enrolled](screenshots/agent-enrolled.png)
![Services Running](screenshots/services-running.png)
```

---

## Recommendations

- Replace default credentials with strong passwords managed according to a defined password policy
- Secure agent-to-manager communication using properly configured TLS certificates
- Review and tune default Wazuh rules to reduce unnecessary alerts
- Deploy additional agents to simulate a larger enterprise environment
- Maintain regular snapshots of the manager VM to ensure recovery capability
