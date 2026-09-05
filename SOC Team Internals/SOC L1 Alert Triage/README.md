# SOC L1 Alert Triage

## Overview

This TryHackMe room introduced me to the fundamentals of **SOC alert triage** from an L1 analyst's perspective. I learned how security events become alerts, how to understand the information inside an alert, how to prioritize alerts, and how to investigate and resolve them using a structured workflow.

The practical work was done using a **SOC dashboard in the TryHackMe SIEM**.

## What I Learned

### From Events to Alerts

Security alerts begin with an event, such as a user login, process launch, or file download. The system records the activity in logs, which are then sent to a security solution such as a **SIEM or EDR**.

Since a SOC can receive millions of logs per day, alerts help analysts focus on activity that requires attention instead of manually reviewing every raw log.

The basic flow is:

`Event → Log → SIEM/EDR → Detection → Alert → Investigation`

### Alert Properties

I learned the main properties that help an analyst understand an alert:

- **Alert Time:** When the alert was created.
- **Event Time:** When the actual activity occurred.
- **Alert Name:** A summary of the activity that triggered the detection.
- **Severity:** Indicates the urgency, from Low/Informational through Critical/Urgent.
- **Status:** Shows whether an alert is new, being investigated, or closed.
- **Verdict:** Determines whether the alert is a True Positive or False Positive.
- **Assignee:** Shows which analyst is responsible for the alert.
- **Description:** Provides the detection logic, context, and sometimes triage guidance.
- **Alert Fields:** Contains details related to the activity, such as an affected hostname or entered command line.

### Alert Prioritisation

When there are many alerts in the queue, an L1 analyst needs to decide which ones to investigate first.

The basic prioritisation process I learned was:

1. **Filter the alerts** and focus on new, unseen, and unresolved alerts.
2. **Sort by severity**, starting with Critical, then High, Medium, and Low.
3. **Sort by time**, starting with the oldest alerts when comparing alerts of similar priority.

This helps ensure potentially serious or older threats are investigated in a timely manner.

### Alert Triage

The actual alert review can also be called alert handling, processing, investigation, or analysis. In this room, it is referred to as **Alert Triage**.

The general workflow is:

`Assign → In Progress → Investigate → Determine Verdict → Comment → Close`

During the investigation, I learned to:

- Identify who or what is affected, such as a user, hostname, cloud environment, network, or website.
- Understand the activity that triggered the alert.
- Review events before and after the alert for additional suspicious activity.
- Use threat intelligence or other available resources to verify the activity.

Some SOC teams use **Workbooks, playbooks, or runbooks** to guide analysts through investigations for specific alert categories.

## Practical Work / Lab

I worked with the **TryHackMe SOC dashboard** and applied the alert triage workflow to the alerts provided in the environment.

The dashboard allowed me to review alert properties, assign alerts, change their status and verdict, and add investigation comments.

One of the alerts I worked with was **Potential Data Exfiltration**, which contained information such as the source IP, destination, and amount of data sent and received. This allowed me to apply the concepts of alert investigation and classification to a practical SOC scenario.

The room also provided a **Restart** option in the dashboard to reset the practical environment if the expected result was not received after triage.

## Key Takeaways

- Alerts help SOC analysts focus on suspicious activity instead of manually reviewing millions of raw logs.
- Understanding alert properties is essential before beginning an investigation.
- Alert prioritisation helps L1 analysts manage a large alert queue effectively.
- L1 analysts are responsible for the initial investigation and escalation of potential threats.
- Alert triage involves reviewing the activity, investigating surrounding events, determining a verdict, documenting the reasoning, and closing the alert.
- A structured triage process helps reduce the chance of genuine attacks being overlooked.

## Conclusion

This room helped me understand the **day-to-day alert triage workflow of an L1 SOC analyst**. I learned how alerts are generated, how to prioritize them, and how to investigate them using information from the SIEM. The practical dashboard work helped connect these concepts to a realistic SOC workflow.
