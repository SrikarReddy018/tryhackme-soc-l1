# Introduction to EDR

## Overview

This TryHackMe room introduced me to **Endpoint Detection and Response (EDR)** and its role in protecting endpoints from advanced cyber threats.

I learned how EDR differs from traditional antivirus, how EDR agents collect telemetry from endpoints, how that telemetry is analyzed for suspicious activity, and how SOC analysts use the information provided by an EDR during investigations.

The room also covered the main capabilities of EDR, including **visibility, detection, and response**, followed by a practical exercise where I investigated detections using a simulated EDR dashboard.

---

## What I Learned

### What is EDR?

**Endpoint Detection and Response (EDR)** is a security solution focused on monitoring, detecting, investigating, and responding to threats on endpoints.

Endpoints can include devices such as:

* Windows systems
* Linux systems
* macOS systems
* Servers
* Other network-connected devices

EDR provides detailed visibility into what is happening on these systems and helps security analysts investigate suspicious activity.

---

## The Three Pillars of EDR

The room introduced three main capabilities of EDR:

### 1. Visibility

EDR collects detailed information from endpoints, including:

* Process activity
* Network connections
* File and folder modifications
* Registry modifications
* User activity
* Command-line activity

It can also provide process trees, activity timelines, and historical endpoint information.

This visibility helps analysts understand the sequence of events surrounding a detection.

### 2. Detection

EDR can identify threats using several detection techniques, including:

* Behavioral detection
* Anomaly detection
* IOC matching
* Machine learning
* MITRE ATT&CK mapping

This allows EDR to detect suspicious behavior rather than relying only on known malware signatures.

### 3. Response

After detecting a threat, EDR can provide response capabilities such as:

* Isolating an endpoint
* Terminating a process
* Quarantining files
* Remote access
* Collecting forensic artefacts

Some EDR solutions also support automated responses through configured policies.

---

## EDR vs Antivirus

One of the important concepts I learned was the difference between traditional antivirus and EDR.

Traditional antivirus can detect known threats using signatures and other detection methods. However, advanced attacks can use legitimate applications and previously unknown techniques to avoid simple signature-based detection.

EDR provides deeper visibility into endpoint behavior.

For example, an attack could involve:

```text
Word Document
      ↓
Malicious VBA Macro
      ↓
PowerShell
      ↓
Obfuscated Command
      ↓
Payload Download
      ↓
Process Injection
      ↓
Outbound Connection
```

Instead of looking at each event independently, EDR can use telemetry and behavioral analysis to understand the larger attack chain.

Modern antivirus products can also have advanced detection capabilities, so the distinction is not simply that AV detects malware while EDR does not. The important difference covered in the room is the **depth of endpoint visibility, investigation context, and response capabilities provided by EDR**.

---

## EDR Architecture

I learned about the two main components involved in collecting and analyzing endpoint information.

### EDR Agent

The EDR agent, sometimes called a **sensor**, is installed on the endpoint.

It acts as the eyes and ears of the EDR by:

* Monitoring endpoint activity
* Collecting telemetry
* Performing some local detection
* Sending information to the central EDR console

### EDR Console

The EDR console receives information from the agents and provides a centralized place for analysis.

It can:

* Correlate endpoint activity
* Analyze telemetry
* Use detection logic and machine learning
* Use threat intelligence
* Generate alerts
* Provide investigation details
* Provide response capabilities

A simplified architecture looks like:

```text
Endpoint
    ↓
EDR Agent
    ↓
Telemetry
    ↓
EDR Console
    ↓
Detection / Alert
    ↓
SOC Analyst
    ↓
Investigation / Response
```

---

## EDR Telemetry

Telemetry is the detailed data collected from an endpoint by the EDR agent.

I learned that telemetry is important because individual activities may appear legitimate, while a combination of activities can reveal an attack.

Examples of telemetry include:

### Process Activity

EDR tracks process executions and terminations. This helps identify suspicious parent-child relationships and malicious processes.

### Network Connections

EDR monitors endpoint network connections, which can help identify:

* Command and Control activity
* Unusual port usage
* Data exfiltration
* Lateral movement

### Command-Line Activity

EDR can record commands executed through tools such as CMD and PowerShell.

This can help identify suspicious or obfuscated command execution.

### File and Folder Changes

EDR monitors modifications to files and folders, which can be useful for identifying activity such as:

* Malicious file drops
* Data staging
* Ransomware activity

### Registry Changes

EDR monitors registry modifications, which can provide useful information during investigations of suspicious Windows activity.

---

## Advanced Detection Techniques

The room introduced several techniques used by EDR to identify threats.

### Behavioral Detection

EDR examines how a process behaves instead of relying only on known signatures.

For example, `winword.exe` spawning `powershell.exe` can be considered suspicious because of the unusual parent-child relationship.

### Anomaly Detection

EDR can establish a baseline of normal endpoint behavior and flag activity that deviates from that baseline.

This can sometimes produce false positives, so analyst investigation and context are important.

### IOC Matching

EDR can compare endpoint activity against known **Indicators of Compromise (IOCs)** from threat intelligence sources.

For example, a known malicious file hash can be matched against threat intelligence.

### MITRE ATT&CK Mapping

EDR detections can be mapped to MITRE ATT&CK tactics and techniques.

For example:

```text
Tactic: Persistence
Technique: Scheduled Task/Job
```

This gives the analyst additional context about the activity.

### Machine Learning

Modern EDR solutions can use machine learning to identify complex patterns involving multiple events.

This can help identify attacks where individual actions may not appear malicious on their own.

---

## EDR Response Capabilities

I also learned about several actions that can be taken after a threat is identified.

### Isolate Host

An infected endpoint can be isolated from the network to help prevent further spread or lateral movement.

### Terminate Process

A malicious process can be terminated without necessarily isolating the entire endpoint.

This needs to be done carefully because terminating a legitimate process could disrupt normal operations.

### Quarantine

A suspicious or malicious file can be moved to an isolated location so that it cannot execute.

### Remote Access

Analysts can remotely access an endpoint through capabilities such as CrowdStrike Falcon's **Real Time Response (RTR)** and perform investigation or response actions.

### Artefact Collection

Analysts can remotely collect information for forensic investigation, such as:

* Memory dumps
* Event logs
* Specific folder contents
* Registry hives

---

## EDR and SIEM

Another important concept was that EDR normally operates as part of a larger security ecosystem.

Organizations may use multiple security technologies, including:

* Firewalls
* DLP
* Email Security Gateways
* IAM
* EDR
* Other security solutions

These systems can send information to a **SIEM (Security Information and Event Management)** platform.

The SIEM can act as a central point for investigation by bringing information from different security sources together.

```text
Firewall ───────┐
EDR ────────────┤
IAM ────────────┤
Email Security ─┤
DLP ─────────────┤
                ↓
               SIEM
                ↓
          SOC Analyst
```

The main distinction I learned is that **EDR provides deep endpoint visibility and response**, while **SIEM provides centralized visibility and correlation across multiple security sources**.

---

# Practical Lab

## EDR Detection Triage

For the practical part of the room, I worked with a simulated **EDR Dashboard** as a SOC analyst at **TECH THM**.

The scenario provided multiple **medium- and high-severity detections**.

The objective was to perform **triage** using the information available within the EDR.

During the investigation, the focus was on understanding the information provided by each detection and using that visibility to answer questions about the activity.

The practical exercise reinforced the importance of examining the context around an alert rather than looking at a single event in isolation.

### Practical Workflow

```text
EDR Detection
      ↓
Review Alert Information
      ↓
Examine Endpoint Activity
      ↓
Understand the Context
      ↓
Triage the Detection
      ↓
Determine What Happened
```

The room specifically stated that **acknowledging alerts and taking response actions were outside the scope of this practical exercise**. The focus was on understanding the visibility provided by the EDR.

---

## Key Takeaways

* EDR provides **deep visibility into endpoint activity**.
* EDR agents collect **telemetry** and send it to a central console.
* Telemetry can include process, network, command-line, file, folder, and registry activity.
* EDR can detect threats using **behavioral detection, anomaly detection, IOC matching, machine learning, and other techniques**.
* Process trees and event timelines are useful for understanding an attack chain.
* EDR can map detections to **MITRE ATT&CK** techniques.
* EDR provides response capabilities such as **host isolation, process termination, quarantine, remote access, and artefact collection**.
* EDR focuses on **endpoint security**, while SIEM provides broader centralized security event collection and correlation.
* A SOC analyst needs to investigate the **context and chain of events** surrounding an alert rather than relying on a single event.
* EDR is an important part of a larger security ecosystem and commonly works alongside other security solutions and SIEM platforms.

---

## Conclusion

This room gave me a solid introduction to how EDR works from a SOC analyst's perspective. I learned how endpoint telemetry is collected, how different detection techniques are used to identify suspicious activity, and how analysts can investigate and respond to threats using an EDR platform.

The practical detection-triage exercise also helped me understand how the visibility provided by EDR can be used to investigate security alerts and understand the activity occurring on an endpoint.
