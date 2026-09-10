# SOC Team Internals

## Module Overview

This TryHackMe module introduced me to the workflow and responsibilities of a **SOC L1 analyst**.

Across four rooms, I learned how security events become alerts, how an L1 analyst should understand and triage those alerts, how investigation workbooks and lookups can make investigations faster and more consistent, and finally how SOC performance can be measured using operational metrics.

The four rooms covered were:

1. **SOC L1 Alert Reporting**
2. **SOC L1 Alert Triage**
3. **SOC Workbooks and Lookups**
4. **SOC Metrics**

Together, the rooms helped me understand that SOC L1 work is not just about looking at an alert and deciding whether it is malicious. There is a larger workflow involving **understanding the alert, gathering context, making a decision, reporting or escalating it correctly, and continuously improving the process**.

---

# 1. SOC L1 Alert Reporting

## What I Learned

### The Role of Alert Reporting

I learned that reporting is an important part of SOC operations because the information gathered during alert investigation needs to be communicated clearly to other analysts and teams.

An analyst may investigate an alert, determine what happened, collect relevant evidence, and then document the result so that the next person handling the incident can understand the situation without having to repeat the entire investigation.

### Communicating Security Findings

A useful security report should communicate the important information surrounding an alert rather than simply stating that something is "malicious" or "safe".

The investigation needs to provide enough context for the next level of the SOC to understand what happened and what action is required.

This is particularly important when an L1 analyst escalates a **True Positive** to L2.

### Why Accurate Reporting Matters

I understood that inaccurate or incomplete reporting can create problems further down the incident-response process.

If important information is missing, L2 analysts may need to repeat work that has already been performed. Clear reporting therefore helps maintain continuity between analysts and makes the overall investigation more efficient.

---

# 2. SOC L1 Alert Triage

## What I Learned

### From Events to Alerts

This room helped me understand how security activity becomes something that an analyst actually needs to investigate.

A security event by itself does not necessarily mean that an attack is taking place. Security tools collect events and use detection logic to generate alerts when activity matches conditions considered suspicious.

The L1 analyst then has to determine what the alert actually represents.

### Understanding Alert Properties

I learned that an alert contains information that helps an analyst understand and prioritise the event.

Important properties include things such as:

* **Severity**
* **Verdict**
* Relevant event information
* Context surrounding the activity

These properties provide an initial starting point for investigation rather than being the final answer.

### Alert Triage

The main responsibility of L1 during triage is to quickly determine whether an alert represents something that requires further action.

The basic thought process can be represented as:

```text
Alert received
      ↓
Understand the alert
      ↓
Review available context
      ↓
Determine whether activity is legitimate or suspicious
      ↓
Make a triage decision
      ↓
Close or escalate
```

I learned that the goal of L1 is not to perform every possible investigation. Instead, L1 acts as the first filtering layer, separating normal activity and false positives from alerts that require deeper investigation.

### True Positives and False Positives

A major part of triage is distinguishing between genuine threats and harmless activity.

A **True Positive** represents a genuine security event that requires action, while a **False Positive** is an alert that initially appears suspicious but turns out to be legitimate.

This distinction is important because both incorrect closure and unnecessary escalation can affect the efficiency of the SOC.

### L1 and L2

I also understood the relationship between L1 and L2 analysts more clearly.

L1 is responsible for the initial investigation and filtering of alerts. When an alert requires deeper analysis or represents a genuine threat, it can be escalated to **L2**.

The objective is therefore not to escalate everything, but also not to close something simply because the analyst is uncertain.

## Practical Work / Lab

The room involved working with a **SOC dashboard/SIEM environment** to understand and triage alerts.

The practical work helped connect the alert properties and triage concepts to the type of workflow an L1 analyst would follow when handling security alerts.

---

# 3. SOC Workbooks and Lookups

## What I Learned

### Investigation Workbooks

I learned that an **investigation workbook** is essentially a structured collection of resources that an analyst can use while investigating alerts.

Instead of searching for the same resources and queries every time an alert appears, a workbook provides a consistent starting point.

A workbook can contain resources such as:

* Asset inventory
* Identity information
* SIEM and EDR platforms
* Threat intelligence resources
* Internal documentation
* Network diagrams
* Standardised investigation queries

This makes the investigation process more organised and repeatable.

### Why Workbooks Matter

One of the main things I understood from this room is that a good SOC investigation should not depend entirely on an individual analyst remembering every useful resource.

Workbooks help analysts follow a consistent investigation process and reduce the time spent looking for basic information.

They can also make **knowledge transfer** easier because experienced analysts can document useful investigation resources and queries for other members of the team.

### Lookups

Lookups provide additional context that can help an analyst understand an alert.

For example, when investigating an IP address, hostname, user, or other indicator, an analyst may need to determine whether it is known, trusted, suspicious, or associated with previous activity.

This additional context helps the analyst make a more informed triage decision instead of relying only on the original alert.

### Combining Workbooks and Lookups

I understood that workbooks and lookups complement each other.

The workbook provides the **structured investigation path**, while lookups help the analyst **gather additional context** during that investigation.

A simplified workflow is:

```text
Alert
  ↓
Open investigation workbook
  ↓
Follow relevant investigation steps
  ↓
Perform lookups
  ↓
Gather context
  ↓
Make a better triage decision
```

This can make investigations both faster and more consistent.

---

# 4. SOC Metrics

## What I Learned

### Why SOC Metrics Matter

The final room moved from individual alert handling to measuring the performance of the SOC as a whole.

I learned that metrics can help identify problems such as excessive alert noise, delayed detection, slow acknowledgement, or delayed response.

They are not just management statistics. The actions of L1 analysts can directly affect several of these measurements.

### Alerts Count

**Alerts Count (AC)** measures the total number of alerts received.

```text
AC = Total Count of Alerts Received
```

A very high alert volume can overwhelm analysts and make genuine threats harder to identify.

However, an unusually low alert volume can also indicate a potential visibility or SIEM problem.

The room gives **5 to 30 alerts per day per L1 analyst** as a general target, although the appropriate volume depends on the organisation.

### False Positive Rate

The **False Positive Rate (FPR)** measures the amount of alert noise.

```text
FPR = False Positives / Total Alerts
```

A high FPR means analysts are spending a large amount of time dealing with alerts that do not represent genuine threats.

The room considers **80% or higher** a serious problem.

I learned that reducing false positives can involve tuning detection rules, excluding trusted activity where appropriate, and automating repetitive triage using tools such as **SOAR or custom scripts**.

### Alert Escalation Rate

The **Alert Escalation Rate (AER)** measures how frequently L1 analysts escalate alerts.

```text
AER = Escalated Alerts / Total Alerts
```

L1 analysts should filter out unnecessary noise while escalating alerts that require deeper investigation.

The room gives **below 50%** as a general target and notes that **below 20%** can be even better.

### Threat Detection Rate

The **Threat Detection Rate (TDR)** measures how reliably threats are detected.

```text
TDR = Detected Threats / Total Threats
```

The room gives **100%** as the desired target because every missed threat has the potential to cause significant damage.

A missed threat could result from a broken detection rule or from an analyst incorrectly classifying a genuine breach as a False Positive.

---

## SLA and Response Metrics

### Service Level Agreement

I learned that detecting an attack is only the beginning. The SOC must also acknowledge, investigate, and respond to the threat.

These expectations can be defined through a **Service Level Agreement (SLA)** between an internal SOC and its organisation or between an MSSP and its customers.

### MTTD

**Mean Time to Detect (MTTD)** measures the average time between an attack occurring and its detection by SOC tools.

The reference value used in the room was:

```text
MTTD = 5 minutes
```

### MTTA

**Mean Time to Acknowledge (MTTA)** measures the average time taken for an L1 analyst to begin triaging a newly generated alert.

The room's reference value was:

```text
MTTA = 10 minutes
```

### MTTR

For this room, **Mean Time to Respond (MTTR)** measures the average time taken by the SOC to actually stop the breach from spreading.

The reference value was:

```text
MTTR = 60 minutes
```

The three metrics represent different stages:

```text
Attack
  ↓
Detection       → MTTD
  ↓
Alert
  ↓
L1 triage       → MTTA
  ↓
Response        → MTTR
  ↓
Breach contained
```

---

## Improving SOC Performance

### Reducing Alert Noise

If the FPR becomes too high, the SOC can investigate the detection rules producing unnecessary alerts.

Trusted activities can be excluded where appropriate, and repetitive investigations can potentially be automated.

### Improving Detection

A high MTTD can indicate problems with detection rules or delays in SIEM log collection.

L1 analysts can identify these problems and communicate them to the relevant SOC engineering team.

### Improving Alert Acknowledgement

A high MTTA can indicate that analysts are not being notified quickly enough or that alerts are not being distributed effectively.

Real-time notifications and better workload distribution can help address this.

### Improving Response

A high MTTR means the SOC is taking too long to contain threats.

For L1 analysts, quickly escalating genuine threats to L2 is important. Documented procedures for different attack scenarios can also help the team respond more efficiently.

---

# Practical Work Across the Module

Across the four rooms, I worked through the SOC workflow from **alert handling to performance improvement**.

The progression of the module can be summarised as:

```text
Alert Reporting
      ↓
Communicate investigation results
      ↓
Alert Triage
      ↓
Understand and classify alerts
      ↓
Workbooks & Lookups
      ↓
Gather context efficiently
      ↓
SOC Metrics
      ↓
Measure and improve SOC performance
```

The practical exercises helped me connect these concepts to the responsibilities of an L1 analyst rather than treating them as isolated definitions.

The module also reinforced that SOC work is a continuous process. An analyst needs to investigate alerts correctly, document useful information, use available resources efficiently, and recognise when the wider SOC process needs improvement.

# Overall Key Takeaways

* An L1 analyst is the first layer of investigation for many security alerts.
* **Alert triage** is about understanding an alert and deciding whether it should be closed or escalated.
* **Severity and verdict** are important alert properties that help with triage decisions.
* **True Positives** need appropriate action, while excessive False Positives create unnecessary workload.
* **Investigation workbooks** provide structured resources and standardised investigation paths.
* **Lookups** provide additional context that can help analysts make better decisions.
* Good documentation and reporting help maintain continuity between SOC analysts.
* **Alerts Count, FPR, AER, and TDR** provide insight into the SOC's internal performance.
* **MTTD, MTTA, and MTTR** measure different stages of the detection and response process.
* **SLAs** establish expected service levels and response times.
* L1 analysts can contribute to improving SOC performance by identifying problems and communicating them to the appropriate teams.
* Reducing alert noise, improving detection, distributing alerts effectively, and escalating genuine threats quickly can make the SOC more efficient.

# Conclusion

Completing these four rooms gave me a much clearer picture of what happens inside a SOC at the L1 level.

I started with the fundamentals of **alert reporting and triage**, then learned how **workbooks and lookups** can make investigations more structured and efficient. Finally, SOC Metrics showed me how the effectiveness of these processes can be measured using metrics such as **FPR, TDR, MTTD, MTTA, and MTTR**.

The biggest takeaway for me was that SOC analysis is not just about responding to individual alerts. It is also about **making informed decisions, communicating findings clearly, using available investigation resources effectively, and continuously improving the overall security operation**.
