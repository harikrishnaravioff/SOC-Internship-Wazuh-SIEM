# Week 4 — Dashboarding & Final Reporting

## Objective

Presenting data like a Professional SOC Analyst.

---

## Task 1: Custom Dashboard in Wazuh/Kibana

### Total Alerts per Day

Used the `wazuh-alerts-*` index and created a **bar chart** with a date histogram on the `@timestamp` field to visualize daily alert volume across the monitoring period.

### Top 5 Security Rules Triggered

Built a **pie chart** using the `rule.description` field with a Terms aggregation limited to 5 buckets. This showed the most frequently fired rules at a glance, making it easy to identify the dominant threat patterns.

### Agent Status

Used the `wazuh-monitoring-*` index and created a **metric visualization** splitting by the `status` field to display Active, Disconnected, and Pending agents in real time. This gives instant visibility into endpoint health across the environment.

---

## Task 2: Final Internship Project Report

A complete PDF report was prepared summarizing all 4 weeks of the internship. The report covers:

- **Week 1** — Environment setup and configuration of Wazuh Manager, Indexer, and Dashboard on VirtualBox
- **Week 2** — Log collection and monitoring with agent deployment and authentication event analysis
- **Week 3** — Threat detection through attack simulation including brute force, EICAR file testing, and command monitoring
- **Week 4** — Dashboard design and final reporting, bringing together all skills into a professional SOC analyst workflow

The full report is available in the `Final-Report/` folder.

---

## Screenshots

> Add your Week 4 screenshots to the `screenshots/` folder and reference them below.

```
![Total Alerts Per Day](screenshots/alerts-per-day.png)
![Top 5 Rules](screenshots/top5-rules.png)
![Agent Status Dashboard](screenshots/agent-status.png)
![Full Custom Dashboard](screenshots/full-dashboard.png)
```
