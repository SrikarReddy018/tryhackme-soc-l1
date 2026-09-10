# SOC Metrics and Objectives

## Overview

This TryHackMe room focused on how the performance of a Security Operations Center (SOC) can be measured using different metrics.

I learned about internal SOC metrics such as **Alerts Count, False Positive Rate, Alert Escalation Rate, and Threat Detection Rate**, along with performance metrics including **MTTD, MTTA, and MTTR**. I also learned how these metrics can be defined within a **Service Level Agreement (SLA)** and how L1 analysts can identify problems and contribute to improving SOC performance.

The practical part of the room involved working through three different SOC performance scenarios and assigning appropriate improvement tasks to address the issues presented.

## What I Learned

### SOC Performance Metrics

A SOC's main goal is to protect the **confidentiality, integrity, and availability** of an organisation's digital assets.

L1 analysts play an important role by receiving and triaging alerts and reliably identifying **True Positives** that need to be escalated to L2.

To evaluate how well this process is working, SOC teams use different metrics. I learned four important internal metrics:

| Metric                          | Formula                            | What it measures                |
| ------------------------------- | ---------------------------------- | ------------------------------- |
| **Alerts Count (AC)**           | `Total Count of Alerts Received`   | Overall SOC workload            |
| **False Positive Rate (FPR)**   | `False Positives / Total Alerts`   | Amount of alert noise           |
| **Alert Escalation Rate (AER)** | `Escalated Alerts / Total Alerts`  | L1 escalation behaviour         |
| **Threat Detection Rate (TDR)** | `Detected Threats / Total Threats` | Reliability of threat detection |

### Alerts Count

**Alerts Count (AC)** represents the total number of alerts received by the SOC.

```text
AC = Total Count of Alerts Received
```

I learned that both extremely high and extremely low alert volumes can be problematic.

A large number of unresolved alerts can overwhelm analysts and cause genuine threats to get buried among the noise. On the other hand, receiving very few alerts could indicate problems with SIEM visibility or detection rules.

The room gives **5 to 30 alerts per day per L1 analyst** as a generally good metric, although the appropriate number depends on the organisation.

### False Positive Rate

The **False Positive Rate (FPR)** measures how many alerts turn out to be false positives compared with the total number of alerts.

```text
FPR = False Positives / Total Alerts
```

For example, if 75 out of 80 alerts are false positives:

```text
FPR = 75 / 80 = 93.75%
```

I learned that a high FPR creates unnecessary work for analysts and can contribute to **alert fatigue**. When analysts repeatedly encounter harmless alerts, there is a greater risk that a genuine threat could be overlooked.

The room describes **0% as an unachievable ideal**, while an FPR of **80% or higher is considered a serious problem**.

One way to address this is through **False Positive Remediation**, such as tuning EDR or SIEM detection rules and excluding known trusted activities where appropriate. Common alerts can also potentially be automated using **SOAR or custom scripts**.

### Alert Escalation Rate

The **Alert Escalation Rate (AER)** measures the percentage of alerts that L1 analysts escalate.

```text
AER = Escalated Alerts / Total Alerts
```

L1 analysts are expected to filter out unnecessary noise and escalate actionable threats to L2.

At the same time, I learned that L1 analysts should not avoid escalation simply because they want to appear independent. If an alert is not fully understood, escalating it for senior analysis is safer than incorrectly closing a genuine threat.

The room gives a target of **below 50%**, with **below 20%** being an even better result.

### Threat Detection Rate

The **Threat Detection Rate (TDR)** measures how many actual threats are successfully detected.

```text
TDR = Detected Threats / Total Threats
```

For example, if four out of six attacks are detected:

```text
TDR = 4 / 6 = 67%
```

A 67% detection rate means two threats were missed, making it a serious security concern.

The room states that TDR should ideally be **100%**, because missed attacks can have serious consequences such as ransomware infections and data exfiltration.

I also learned that missed threats can have different causes. A detection rule could fail to identify an attack, or an L1 analyst could incorrectly classify a genuine breach as a False Positive.

### Service Level Agreements (SLA)

I learned that an alert itself does not stop an attack. The SOC needs to detect the threat, acknowledge the alert, investigate it, and respond before the attacker achieves their objective.

These expectations can be defined through a **Service Level Agreement (SLA)**.

An SLA can exist between an internal SOC and company management, or between a **Managed Security Service Provider (MSSP)** and its customers.

The room provided the following reference values:

| Metric   | What it measures                             |  Reference SLA |
| -------- | -------------------------------------------- | -------------: |
| **MTTD** | Time between an attack and its detection     |  **5 minutes** |
| **MTTA** | Time for L1 to begin triaging an alert       | **10 minutes** |
| **MTTR** | Time taken to stop the breach from spreading | **60 minutes** |

### Mean Time to Detect (MTTD)

**MTTD** measures the average time between an attack occurring and the SOC detecting it through its security tools.

For this room, the reference SLA is **5 minutes**.

A high MTTD means threats are being detected too slowly. This can be affected by detection rules and delays in collecting logs into the SIEM.

### Mean Time to Acknowledge (MTTA)

**MTTA** measures the average time between an alert being generated and an L1 analyst beginning its triage.

The reference SLA in the room is **10 minutes**.

MTTA is different from MTTD because detecting a threat and having an analyst begin investigating the resulting alert are two separate stages.

```text
Attack
   ↓
Detection
   ↓
Alert generated
   ↓
L1 begins triage
```

### Mean Time to Respond (MTTR)

For this room, **MTTR** measures the average time taken by the SOC to actually stop the breach from spreading.

The reference SLA is **60 minutes**.

Examples of response actions include isolating a compromised device or securing a breached account.

The overall timeline can therefore be viewed as:

```text
Attack
  ↓
Detection        → MTTD
  ↓
L1 acknowledgement → MTTA
  ↓
Investigation
  ↓
Response         → MTTR
  ↓
Breach contained
```

I also learned that different SOC teams may define these metrics differently. For the practical tasks in this room, the definitions and values provided by the room were used.

### Improving SOC Metrics

Understanding a metric is only useful if the SOC can act on it. I learned that different metric problems require different improvements.

#### Reducing False Positives

When the **FPR is above 80%**, the SOC is dealing with excessive alert noise.

Possible improvements include:

* Excluding trusted activities, such as legitimate system updates, from EDR or SIEM detection rules where appropriate.
* Tuning detection rules.
* Automating common alert-triage processes using SOAR or custom scripts.

#### Improving MTTD

When **MTTD is above 30 minutes**, threats are being detected too slowly.

The room recommends working with SOC engineers to improve detection rules and checking whether SIEM logs are being collected in real time.

A delay in log collection can result in the SOC receiving the information needed for detection too late.

#### Improving MTTA

When **MTTA is above 30 minutes**, L1 analysts are taking too long to begin triage.

Possible improvements include:

* Ensuring analysts receive real-time notifications for new alerts.
* Distributing alerts more evenly between analysts on shift.

This showed me that acknowledgement delays can be caused by the SOC's alert-handling process and workload distribution, rather than simply being an individual analyst performance issue.

#### Improving MTTR

When **MTTR is above four hours**, the SOC is taking too long to stop the breach.

As an L1 analyst, an important contribution is to **escalate genuine threats to L2 quickly** when deeper investigation or response is required.

The SOC should also have documented procedures for different attack scenarios so analysts know what actions to take during an incident.

### My Role as an L1 Analyst

Although metric tracking is generally handled by the SOC manager, L1 analysts are often among the first people to notice when something is wrong.

For example, an L1 analyst may notice:

* An unusually large number of alerts.
* A very high number of False Positives.
* Delays in receiving or acknowledging alerts.
* Problems that repeatedly require escalation.

I learned that an L1 analyst should not simply notice these problems and ignore them. They should be able to **communicate the issue and suggest an appropriate improvement**.

This makes the L1 role more than just processing alerts. Feedback from analysts can help improve the SOC's overall detection and response process.

## Practical Work / Lab

For the practical exercise, I took the role of a **SOC manager** and worked through **three different SOC performance scenarios**.

Each scenario presented a complaint or issue related to SOC performance. I had to identify the relevant problem and correctly assign an improvement task from the available options.

The exercise allowed me to apply the metrics I had learned to practical situations rather than only memorising their definitions.

The general decision-making process was:

```text
SOC Problem
     ↓
Identify the affected metric
     ↓
Understand the issue
     ↓
Select the appropriate improvement
     ↓
Improve SOC performance
```

This helped reinforce the relationship between a metric and the action required to improve it.

## Key Takeaways

* SOC metrics help measure the effectiveness of security operations.
* **Alerts Count** provides an indication of the workload handled by analysts.
* A high **False Positive Rate** creates alert noise and can contribute to alert fatigue.
* **Alert Escalation Rate** provides insight into how frequently L1 analysts escalate alerts to L2.
* **Threat Detection Rate** measures how reliably the SOC detects actual threats.
* **MTTD, MTTA, and MTTR** measure different stages of the detection and response process.
* **SLA** defines expected service levels and response times.
* Detection-rule tuning and automation can help reduce false positives.
* Real-time log collection and improved detection rules can help reduce MTTD.
* Better notifications and workload distribution can help reduce MTTA.
* Fast escalation and documented response procedures can help reduce MTTR.
* L1 analysts can contribute to improving SOC performance by identifying problems and communicating them to the appropriate teams.

## Conclusion

This room helped me understand that SOC performance is about more than simply handling alerts. The SOC needs to detect real threats reliably, minimise unnecessary alert noise, acknowledge alerts quickly, and respond before an attacker can cause significant damage.

Learning these metrics gave me a better understanding of how an L1 analyst's work fits into the wider SOC operation. The practical scenarios also helped me connect poor metric results with the actions that can be taken to improve them.

