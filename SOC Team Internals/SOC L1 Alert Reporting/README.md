# SOC L1 Alert Reporting

## Overview

This TryHackMe room introduced me to what happens **after an L1 analyst triages an alert**. I learned how to properly document investigation findings, when an alert should be escalated to L2, and how communication fits into the SOC workflow.

The practical work was done using a **SOC dashboard** where I practiced reporting and escalating alerts in a simulated environment.

## What I Learned

### Alert Reporting

I learned that simply marking an alert as a **True Positive or False Positive** is not always enough. L1 analysts may need to write an alert report containing the relevant investigation details.

A good report helps:

* Give **context to L2** when an alert is escalated.
* Preserve investigation findings for future reference.
* Improve my own investigation skills by making me clearly explain what happened and why.

This is especially important for True Positives that require escalation.

Raw SIEM logs may only be stored for **3–12 months**, while alerts can be kept indefinitely. Because of this, important investigation context should be recorded in the alert itself.

### The Five Ws

I learned to structure alert reports using the **Five Ws**:

| Question  | Information to Include                         |
| --------- | ---------------------------------------------- |
| **Who**   | Which user performed the activity              |
| **What**  | What action or sequence of events occurred     |
| **When**  | When the suspicious activity started and ended |
| **Where** | Which device, IP, or website was involved      |
| **Why**   | The reasoning behind the final verdict         |

The **Why** is particularly important because it explains the reasoning behind the analyst's final classification.

A well-written report should give an L2 analyst, DFIR team member, or IT professional enough context to understand the investigation without having to start completely from scratch.

### Alert Escalation

After reaching a verdict and writing the report, an L1 analyst needs to determine whether the alert should be escalated to L2.

I learned that escalation may be appropriate when:

* The alert indicates a **major cyberattack** requiring deeper investigation or DFIR.
* **Remediation actions** are required, such as malware removal, host isolation, or password reset.
* Communication with customers, partners, management, or law enforcement is required.
* I do not fully understand the alert and need assistance from a more senior analyst.

The exact escalation process can differ between SOC teams.

### Escalation Workflow

In a typical workflow, an L1 analyst can reassign the alert to the **L2 analyst on shift** and notify them through the organization's communication channel.

Some teams may instead require a formal written escalation request.

After receiving the alert, L2 can use the L1 report to understand the initial investigation, investigate further, validate the verdict, communicate with other departments if necessary, and start a formal **Incident Response** process for major incidents.

I also learned that requesting senior support is normal when something is unclear. It is better to ask L2 for help than to incorrectly close an alert that I do not understand.

### Communication

SOC analysts may need to communicate with departments outside the SOC to obtain additional information or confirm whether activity is legitimate.

For example:

* **IT** can confirm whether administrative privileges were intentionally granted.
* **HR** can provide additional information about a newly hired employee.

Communication therefore becomes an important part of validating alerts and continuing an investigation.

### Handling Unexpected Situations

The room also covered several situations where the normal workflow may not be enough.

If an urgent critical alert requires escalation but L2 is unavailable, the recommended escalation path is to contact **L2, then L3, and finally the manager**, using the organization's emergency contacts.

If a **Slack or Teams account** may be compromised, I should not use the potentially compromised account to contact the affected user. An alternative method, such as a phone call, should be used.

If there is a sudden spike in alerts, the alerts should be prioritized according to the workflow while informing the L2 analyst on shift.

If I later discover that I incorrectly classified an alert and may have missed malicious activity, I should immediately inform L2 and explain my concerns.

If SIEM logs cannot be properly parsed or searched, the alert should not simply be skipped. I should investigate whatever information is available and report the issue to L2 or the SOC engineer.

## Practical Work / Lab

I worked with the **TryHackMe SOC dashboard** to practice the reporting and escalation workflow.

The general workflow I learned was:

`In Progress → Investigate → Write Report → Set Verdict → Escalate to L2 if Required`

The dashboard allowed me to work with alerts, investigate their available information, write analyst comments, assign verdicts, and escalate alerts to the L2 analyst on shift.

The practical work helped me understand how the information collected during L1 triage is turned into a useful report that another analyst can continue working from.

## Key Takeaways

* L1 analysts need to **document their investigations**, not just assign a verdict.
* The **Five Ws** provide a useful structure for writing clear alert reports.
* Good reports give L2 the context needed to continue an investigation efficiently.
* True Positives requiring deeper investigation, remediation, or additional expertise should be escalated.
* Asking L2 for help is appropriate when an alert is unclear.
* SOC analysts may need to communicate with IT, HR, management, or other parties during an investigation.
* Unexpected situations such as alert spikes, unavailable analysts, compromised communication accounts, and SIEM problems require clear communication and escalation.

## Conclusion

This room helped me understand what happens **after the initial L1 alert triage process**. I learned how to document investigation findings, explain my verdict using the Five Ws, recognize when an alert needs to be escalated, and handle communication during unexpected situations.

The practical SOC dashboard work helped me connect alert triage with the larger SOC workflow, where proper reporting and communication allow investigations to move smoothly from **L1 to L2 and beyond**.
