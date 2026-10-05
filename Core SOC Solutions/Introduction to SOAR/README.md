# Introduction to SOAR

## Overview

I completed the **Introduction to SOAR** room on TryHackMe to understand how Security Orchestration, Automation, and Response fits into a modern SOC environment.

Before this room, I had already worked with concepts such as SIEM, EDR, threat intelligence, and security monitoring. This room helped connect those concepts together and showed me what happens when a SOC has to deal with a large number of repetitive investigations.

The main focus was understanding how SOAR can connect security tools, automate repetitive investigation steps, and execute response actions through predefined workflows called **playbooks**.

---

## What I Learned

### Understanding the Traditional SOC

A traditional SOC depends on several different technologies and teams working together.

For example, an investigation might involve:

* SIEM for log collection and detection
* EDR for endpoint investigation and response
* Firewall for network-level blocking
* IAM for account and access management
* Threat Intelligence platforms for checking indicators
* Ticketing systems for tracking incidents

The problem is that an analyst may have to manually move between these tools during an investigation.

For a single alert, an analyst might have to check the SIEM, copy an IP address into a threat intelligence platform, check the endpoint in EDR, verify the user through IAM, create a ticket, and then communicate the findings.

Doing this repeatedly can become a significant workload.

The room identified four major challenges:

* **Alert fatigue**
* **Disconnected security tools**
* **Manual and inconsistent processes**
* **Shortage of skilled security personnel**

This helped me understand why simply having many security tools doesn't automatically make a SOC efficient.

---

# What SOAR Adds to the SOC

SOAR stands for:

**Security Orchestration, Automation, and Response**

The easiest way I understood it was as a layer that connects the different security tools and coordinates what happens after an alert.

For example:

```text
SIEM detects alert
       ↓
      SOAR
       ↓
 ┌─────┼─────┐
 ↓     ↓     ↓
 TI   EDR   IAM
       ↓
  Response
       ↓
 SOC Analyst
```

The important part is that SOAR doesn't replace these tools.

Instead, it can **coordinate them**.

---

## Orchestration

Orchestration is about connecting different security products and making them work together as part of one workflow.

For example, consider a VPN brute-force alert.

Instead of manually opening several applications, a SOAR workflow can coordinate:

1. Checking the user's previous login activity in the SIEM.
2. Checking the source IP against threat intelligence.
3. Looking for successful logins.
4. Interacting with IAM if the account needs action.
5. Updating the incident ticket.

This made the difference between **having security tools** and **having those tools work together** much clearer to me.

---

## Automation

Automation is where SOAR executes the predefined workflow without requiring the analyst to manually perform every repetitive action.

For example:

```text
SIEM Alert
    ↓
SOAR Playbook
    ↓
Check SIEM
    ↓
Check Threat Intelligence
    ↓
Check EDR
    ↓
Create/Update Case
    ↓
Notify SOC
```

Instead of an analyst performing each step manually, SOAR can execute these actions through integrations and APIs.

This is particularly useful when the SOC is dealing with hundreds of alerts or repeated types of incidents.

---

## Response

SOAR can also coordinate response actions through connected security tools.

For example, after an indicator has been confirmed as malicious, a playbook could potentially:

* Block an IP through a firewall
* Block a malicious domain
* Disable a compromised account
* Isolate an endpoint through EDR
* Update the incident ticket
* Notify the appropriate team

The exact actions depend on how the organization has designed its playbooks and integrations.

---

# Understanding SOAR Playbooks

One of the most useful concepts from this room was the idea of a **playbook**.

I think of a playbook as a predefined decision workflow for a particular type of security incident.

It isn't necessarily a simple list of steps.

It can contain conditions and different paths:

```text
Alert
  ↓
Check information
  ↓
Is it malicious?
 ┌───────┴───────┐
 │               │
Yes              No
 │               │
 ↓               ↓
Response       Close
```

The result of one step can determine what happens next.

This allows the same playbook to handle different outcomes instead of blindly performing the same actions every time.

---

# Phishing Playbook

The room used phishing as an example of an investigation that contains many repetitive tasks.

A phishing investigation may require checking:

* URLs
* Attachments
* Threat intelligence
* Reputation
* Potentially affected users

A playbook can automate the repetitive parts of this investigation.

For example:

```text
Suspicious Email
       ↓
Create Case
       ↓
URL or Attachment?
      /       \
    URL     Attachment
     ↓           ↓
Analyze       Analyze
  URL           File
     \           /
      \         /
       ↓       ↓
       Determine Risk
             ↓
          Response
```

The important thing I learned here was that playbooks can contain **branches**.

The workflow doesn't have to follow one fixed path. It can make decisions based on the results collected during the investigation.

---

# CVE Patching Playbook

The room also demonstrated how SOAR can be used for vulnerability management.

When a new CVE is disclosed, the organization needs to determine whether the vulnerability affects its environment and whether a patch is available.

The workflow can include:

```text
New CVE
  ↓
Check vulnerability details
  ↓
Is it applicable?
  ↓
Identify affected systems
  ↓
Check for patch
  ↓
Test patch
  ↓
Deploy
  ↓
Verify
  ↓
Still vulnerable?
```

I found this example useful because it showed that SOAR isn't limited to responding to malware alerts.

It can also automate structured security processes such as vulnerability management.

If a patch doesn't completely resolve the problem, mitigation measures can be used to reduce the risk until a proper fix is available.

---

# Practical Lab: Threat Intelligence Workflow

The main hands-on part of the room was a **Threat Intelligence workflow configuration exercise**.

Instead of simply reading about SOAR, I had to configure different parts of a workflow as either **automated** or **manual**.

The lab covered several areas of a typical threat intelligence workflow.

### Case Management

I configured how cases should be:

* Created
* Assigned
* Communicated
* Updated
* Deleted

This demonstrated how SOAR can integrate with case-management and ticketing platforms.

### Threat Intelligence Feeds

The workflow also handled threat intelligence feeds, including:

* Fetching new incident information
* Setting fetch intervals
* Handling failed feed retrieval
* Managing older alerts

This showed how routine threat intelligence collection can be incorporated into an automated workflow.

### Incident Data Extraction

The practical workflow included extracting indicators such as:

* IP addresses
* Domains
* URLs

These indicators can then be used for further threat intelligence investigation.

### Reputation and Analysis

The workflow also incorporated reputation checks and analysis using external security services.

This demonstrated how SOAR can take an indicator from an incident, send it to an external intelligence or analysis platform, and bring the resulting information back into the investigation.

An important part of this stage was **analyst validation**, showing that automated results still need to be interpreted when a decision requires human judgment.

### Course of Action

The final part involved response actions such as:

* Blocking malicious domains
* Blocking malicious IP addresses
* Blocking malicious URLs
* Updating the incident case

The workflow demonstrated how SOAR can coordinate these actions through connected security tools.

---

# What the Practical Taught Me

The practical made the difference between **automation and human decision-making** much clearer.

Not every action in a SOC should require an analyst to manually perform it.

For example:

```text
Extract IP
     ↓
Check reputation
     ↓
Search threat intelligence
     ↓
Gather results
```

These are repetitive and predictable tasks that are good candidates for automation.

However, deciding what the collected evidence actually means can require human judgment.

```text
Collected Evidence
       ↓
   SOC Analyst
       ↓
"Is this actually malicious?"
       ↓
Response decision
```

This is why SOAR is not simply an "automatic SOC analyst."

It is an automation and orchestration layer that follows workflows designed by the security team.

---

# SOAR vs Other SOC Tools

The room also helped me connect SOAR with the tools I had previously studied.

| Tool                    | Main purpose                                                      |
| ----------------------- | ----------------------------------------------------------------- |
| **SIEM**                | Collect, correlate, search, and detect security events            |
| **EDR**                 | Monitor and respond to activity on endpoints                      |
| **Threat Intelligence** | Provide context about suspicious indicators                       |
| **Firewall**            | Control and block network traffic                                 |
| **IAM**                 | Manage identities and access                                      |
| **SOAR**                | Connect these tools and automate investigation/response workflows |

A simplified SOC workflow would look like:

```text
             Security Events
                    ↓
                  SIEM
                    ↓
             🚨 Alert
                    ↓
                  SOAR
                    ↓
               Playbook
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
       EDR          TI          IAM
        ↓           ↓           ↓
        └───────────┼───────────┘
                    ↓
             Response Actions
                    ↓
              SOC Analyst
```

This helped me understand that SOAR isn't a replacement for SIEM or EDR. It works **with them**.

---

# Key Takeaways

* SOAR stands for **Security Orchestration, Automation, and Response**.
* Traditional SOCs can become inefficient because of alert fatigue, disconnected tools, repetitive processes, and limited personnel.
* **Orchestration** connects different security tools and coordinates their actions.
* **Automation** allows predefined workflows to run without requiring manual execution of every step.
* **Response** allows SOAR to perform actions through connected security products.
* **Playbooks** define how recurring security incidents should be investigated and handled.
* Playbooks can contain conditions and multiple branches depending on investigation results.
* Threat intelligence workflows can automate indicator extraction, enrichment, reputation checks, and other repetitive tasks.
* SOAR can also be used for workflows such as phishing investigation and CVE patching.
* Automation doesn't eliminate the need for SOC analysts.
* Analysts are still important for complex investigations, validation, decision-making, and maintaining playbooks.

---

# Conclusion

This room helped me understand where SOAR fits into the bigger SOC picture.

I had previously learned about individual technologies such as SIEM, EDR, and threat intelligence. The main thing I gained from this room was understanding **how those technologies can be coordinated into a single investigation workflow**.

The practical Threat Intelligence workflow was particularly useful because I had to think about which tasks should be automated and where human involvement should remain.

My main takeaway is:

> **SOAR doesn't replace the SOC analyst. It removes repetitive work, connects security tools, and allows analysts to spend more time on the parts of an investigation that actually require human judgment.**

Overall, this room gave me a much clearer picture of how automation fits into a modern SOC and how playbooks can turn repetitive security procedures into structured, repeatable workflows.
