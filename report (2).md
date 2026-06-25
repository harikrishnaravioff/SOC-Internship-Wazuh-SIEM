# Week 3 — Attack Simulation & Detection

## Executive Summary

Week 3 involved switching roles and acting as the attacker rather than just monitoring the dashboard. Three simulations were run on the Kali agent: repeated wrong password attempts to trigger brute force detection, dropping an EICAR test file to see if Wazuh would detect it, and running basic commands to verify whether that activity shows up in the logs. The goal was to confirm that the Wazuh manager actually reacts to real activity rather than just displaying a green status screen.

---

## Methodology

**Brute Force Simulation** — Multiple incorrect passwords were intentionally entered over SSH, then the Threat Hunting module was filtered on agent11 to review what was detected.

**EICAR Test File** — The standard EICAR test file was downloaded onto the Kali agent and syscheck-related events were monitored to see if File Integrity Monitoring flagged the file activity on disk.

**Command Monitoring** — Basic commands were run locally including sudo activity and checking running processes. Raw event logs for agent11 were then pulled and searched through ossec log output to verify if that activity was captured.

---

## Technical Findings

### Brute Force Detection

The brute force attempts generated **26 total events** tied to authentication failure:

| Alert Level | Description |
|------------|-------------|
| Level 10 | Syslog alert — user missing password more than once |
| Level 5 | sshd authentication failed entries |
| Level 5 | unix_chkpwd password check failed |
| Level 5 | PAM user login failed entries |

The brute force attempt was clearly detected but did not cross into the Level 12 critical range on its own.

### EICAR File Detection

Wazuh did not flag the EICAR file through a dedicated malware or antivirus module since that was not configured, but **File Integrity Monitoring** picked up the surrounding activity:

- File added to the system
- Integrity checksum change
- File deleted event

These were tagged under MITRE ATT&CK as **Data Destruction** and **File Deletion**. Detection came through FIM noticing the file appear and disappear rather than any signature-based scan recognizing the EICAR string itself.

### Command Monitoring

Command activity showed up clearly in the raw logs:

- sudo to root executed successfully
- PAM login sessions opening and closing
- `ps` command run to list processes for all users

All events were logged with timestamps and rule IDs, confirming that general command execution and session activity is being captured through PAM and process-related rules.

---

## Screenshots

> Add your Week 3 screenshots to the `screenshots/` folder and reference them below.

```
![Brute Force Events](screenshots/brute-force-events.png)
![EICAR FIM Detection](screenshots/eicar-fim-detection.png)
![Command Monitoring Logs](screenshots/command-monitoring.png)
```

---

## Recommendations

- Lower the alert threshold for repeated authentication failures or add a custom rule that escalates severity after a defined number of failed attempts in a short window
- Enable VirusTotal integration or a dedicated antivirus agent for proper malware detection instead of relying on FIM to indirectly detect file changes
- Set up a more specific rule or log source for shell command history to make it easier to search for exact commands run rather than inferring activity from PAM and process events
