# Cyber Kill Chain

## Overview

The Cyber Kill Chain is a cybersecurity framework developed by Lockheed Martin in 2011. It describes the stages an attacker may follow to achieve their objectives during a cyberattack.

Understanding these stages helps security professionals recognize attack activity, identify weaknesses in their defenses, and determine where an attack can be interrupted.

The framework consists of seven phases:

1. Reconnaissance
2. Weaponization
3. Delivery
4. Exploitation
5. Installation
6. Command and Control
7. Actions on Objectives

## What I Learned

### 1. Reconnaissance

Reconnaissance is the information-gathering phase in which an attacker researches a target before launching an attack.

The information collected may include employee details, email addresses, domain information, exposed services, and technologies used by the organization.

**Open-Source Intelligence (OSINT)** involves gathering information from publicly available sources, including search engines, social media, online forums, public records, and technical databases.

Reconnaissance can be divided into two types:

* **Passive Reconnaissance:** Collecting information without directly interacting with the target, such as reviewing public records or performing WHOIS lookups.
* **Active Reconnaissance:** Interacting directly with the target, such as through port scanning, banner grabbing, or probing exposed services.

Tools explored in this context include:

* **theHarvester:** Collects information such as email addresses, names, subdomains, IP addresses, and URLs from public sources.
* **Hunter.io:** Helps identify email addresses associated with a domain.
* **OSINT Framework:** Organizes OSINT tools and resources into categories.

Reconnaissance helps attackers understand their targets, while defenders can use similar techniques to identify exposed information and potential security weaknesses.

### 2. Weaponization

Weaponization involves preparing the tools and components required for an attack using information gathered during reconnaissance.

Attackers may create custom malware, use existing exploits, or obtain previously developed malicious payloads.

Important concepts include:

* **Malware:** Software designed to damage systems, disrupt operations, or gain unauthorized access.
* **Exploit:** Code or a program that takes advantage of a vulnerability.
* **Payload:** The code or component intended to perform a particular action on the target system.

Weaponization techniques may include preparing malicious Office documents, developing or obtaining payloads, setting up Command and Control infrastructure, preparing backdoors, and creating convincing phishing templates.

Attackers may also abuse legitimate technologies, such as Office macros or OAuth authorization requests, to make their attacks appear trustworthy.

The main objective of this phase is to prepare the components needed to carry out the attack.

### 3. Delivery

Delivery is the phase in which the attacker transmits the malicious payload to the target.

Common delivery methods include:

* **Phishing Emails:** Messages containing malicious attachments or links. Spear phishing targets a specific individual or organization.
* **USB Drops:** Malicious USB devices are left in public locations or distributed to targeted individuals.
* **Watering Hole Attacks:** Attackers compromise websites frequently visited by their intended victims to expose them to malicious content.

A watering hole attack may result in a drive-by download, where visiting or interacting with compromised web content causes unwanted or malicious software to be downloaded.

The delivery method depends on the target, the attacker's objectives, and the available opportunities.

### 4. Exploitation

Exploitation occurs when an attacker takes advantage of a vulnerability or another opportunity to execute malicious code or perform an unauthorized action.

Common techniques include:

* **Malicious Macro Execution:** Malicious code embedded in an Office document may execute when the victim opens the document and enables or triggers the macro.
* **Zero-Day Exploitation:** Taking advantage of a vulnerability for which an effective patch is not yet available.
* **Known Vulnerability Exploitation:** Exploiting publicly documented vulnerabilities in software or systems that remain unpatched.

A CVE, or Common Vulnerabilities and Exposures identifier, identifies a publicly documented cybersecurity vulnerability.

After gaining access, attackers may attempt privilege escalation to obtain higher permissions or lateral movement to reach other systems within the network.

Potential indicators of exploitation include unexpected process creation, suspicious command-line arguments, registry modifications, and the creation of unfamiliar services.

These indicators require investigation and should not automatically be treated as proof of compromise.

### 5. Installation

The Installation phase focuses on maintaining access to a compromised system.

Attackers may establish persistence so that they can regain access even after losing their initial connection or restarting the system.

Common persistence techniques include:

* **Web Shells:** Malicious scripts installed on web servers to maintain access and interact with the compromised server.
* **Backdoors:** Mechanisms that allow attackers to regain access to a compromised system.
* **Windows Services:** Creating or modifying services to execute malicious programs or scripts. Attackers may disguise malicious services using legitimate-looking names.
* **Registry Run Keys and Startup Folders:** Configuring a malicious program to execute automatically when a user logs in.

Meterpreter is a Metasploit payload that provides an interactive session for remote interaction with a compromised system.

Attackers may also use **masquerading** to make malicious files or services appear legitimate.

Another technique is **timestomping**, which involves modifying file timestamps to make forensic investigations more difficult.

Understanding persistence helps security analysts investigate suspicious services, unexpected startup entries, unfamiliar web-server scripts, and unusual file metadata.

### 6. Command and Control

Command and Control (C2) is the communication channel through which an attacker interacts with a compromised system.

After establishing access and persistence, malware may communicate with an external server controlled by the attacker.

**C2 beaconing** refers to repeated communications between an infected system and its C2 infrastructure.

Common communication methods include:

* **HTTP:** Often uses port 80 and may blend with legitimate web traffic.
* **HTTPS:** Often uses port 443 and encrypts traffic between communicating systems.
* **DNS:** Attackers may abuse DNS requests to carry hidden communications, a technique known as DNS tunneling.
* **IRC:** Internet Relay Chat has historically been used for C2 communication.

Security analysts can investigate unusual external connections, repetitive communication patterns, suspicious DNS activity, and unexpected network traffic.

However, repeated connections alone do not prove malicious activity. Their destinations, timing, frequency, and associated endpoint activity must also be examined.

### 7. Actions on Objectives

Actions on Objectives is the final phase of the Cyber Kill Chain. At this stage, the attacker attempts to achieve the original goals of the attack.

Possible objectives include:

* **Credential Collection:** Obtaining usernames, passwords, or other authentication information.
* **Privilege Escalation:** Gaining higher permissions, potentially including administrator or domain administrator access.
* **Internal Reconnaissance:** Exploring internal systems, applications, and network resources.
* **Lateral Movement:** Moving between compromised systems within an organization's environment.
* **Data Exfiltration:** Collecting sensitive information and transferring it outside the organization.
* **Backup Deletion:** Deleting backups or Windows Shadow Copies to make recovery more difficult.
* **Data Destruction:** Overwriting, corrupting, or deleting important information.

Not every attack involves all these activities. An attacker may focus on stealing data, disrupting operations, destroying information, or achieving another objective.

For defenders, identifying these activities early can help limit the impact of an attack.

## Practical Analysis: Target Data Breach

The room includes a practice scenario based on the 2013 Target data breach.

Target announced that approximately 40 million credit and debit card accounts were affected between November 27 and December 15, 2013.

The exercise involves mapping six supplied items to the appropriate Cyber Kill Chain phases:

* Spearphishing attachment
* Exploit public-facing application
* Dynamic linker hijacking
* Fallback channels
* Data from local system
* PowerShell

This exercise demonstrates how attack techniques can be associated with different phases of an intrusion.

The placement of a technique depends on its role in the specific attack. Some techniques, such as PowerShell, can be used during multiple phases, so context is important when analyzing an incident.

## Limitations of the Cyber Kill Chain

Although the Cyber Kill Chain is useful for understanding attacks, it has limitations.

* **Limited coverage:** The traditional framework focuses heavily on malware delivery and attacks involving the network perimeter.
* **Evolving threats:** Modern attackers combine multiple tactics, techniques, and procedures (TTPs) to achieve their objectives.
* **Changing indicators:** Attackers can modify file hashes, IP addresses, and other indicators to evade detection based on known threat intelligence.
* **Insider threats:** The traditional model may not adequately represent threats involving authorized users who misuse their access.
* **Not every attack follows the same sequence:** Real-world attacks may skip phases, repeat activities, or use different techniques.

The Cyber Kill Chain should therefore be used alongside other frameworks and security technologies.

### Other Frameworks

* **MITRE ATT&CK:** Provides a knowledge base of real-world adversary tactics and techniques.
* **Unified Kill Chain:** Offers a broader model for analyzing intrusion and attack activities.

Combining these frameworks helps defenders develop a more comprehensive understanding of adversary behavior.

## Key Takeaways

* The Cyber Kill Chain divides an attack into seven phases.
* Reconnaissance helps identify information about a target.
* Weaponization prepares the components required for an attack.
* Delivery transmits the payload to the target.
* Exploitation takes advantage of a vulnerability or another opportunity to execute malicious code.
* Installation establishes persistence or maintains access.
* Command and Control enables communication with compromised systems.
* Actions on Objectives represents the attacker's ultimate goals.
* Security analysts can use these phases to investigate suspicious activity and identify opportunities to interrupt an attack.
* The framework has limitations and works best as part of a broader security strategy that includes MITRE ATT&CK and other defensive approaches.

## Conclusion

This room helped me understand how cyberattacks can progress from initial information gathering to achieving an attacker's objectives. It also highlighted the importance of recognizing attacker behavior, investigating suspicious activity, and identifying opportunities to interrupt an attack.

Understanding the Cyber Kill Chain provides a useful foundation for security monitoring, incident investigation, and threat analysis.

