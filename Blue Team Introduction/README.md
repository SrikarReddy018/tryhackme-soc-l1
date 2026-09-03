# Blue Team Introduction 🛡️

## Overview

This module introduced the defensive side of cybersecurity and the role of a Security Operations Center (SOC) in protecting an organization.

The rooms covered the structure of security teams, the responsibilities of Blue Team members, common attack vectors against humans and systems, and the different ways organizations detect, mitigate, and respond to threats.

---

## What I Learned

### Security Operations Center

A SOC is responsible for monitoring an organization's environment, investigating security alerts, and responding to threats.

The main roles covered were:

- **SOC L1 Analyst:** Performs initial alert triage and investigation.
- **SOC L2 Analyst:** Handles more advanced investigations.
- **SOC Engineer:** Maintains and configures security tools such as SIEM and EDR.
- **SOC Manager:** Oversees the SOC team and its operations.

I also learned that the SOC is only one part of a larger security structure.

### Security Teams

In larger organizations, security responsibilities can be divided between different teams:

- **Red Team:** Offensive security and penetration testing.
- **GRC:** Governance, risk, and compliance.
- **Blue Team:** Defensive security.
- **CIRT:** Responds to major or critical security incidents.

The exact structure depends on the organization's size and requirements.

---

## Humans as an Attack Vector

One of the main concepts in this module was that employees can become an entry point for attackers.

Instead of exploiting a technical vulnerability, attackers can manipulate people through **social engineering**.

Common techniques covered included:

- Phishing
- Malware delivery
- Deepfakes
- Impersonation
- Malicious USB devices
- Insider threats
- Fake job offers

Social engineering generally relies on making the attacker appear **trustworthy** while creating an **emotional response**, such as urgency or fear.

From a SOC perspective, this means detecting and responding to attacks even when the initial compromise happened because of human interaction.

---

## Systems as an Attack Vector

The module also looked at attacks that target systems directly.

Examples of systems that can be valuable to attackers include:

- User computers
- Servers
- Mail servers
- Databases
- Cloud platforms
- Industrial systems

The impact of a compromise depends heavily on what the system provides access to.

### Main attack methods covered

**Software vulnerabilities**

Security flaws in software can be exploited to gain access to systems. Publicly known vulnerabilities are assigned CVE identifiers.

A **zero-day** is a vulnerability that is unknown or has no available patch when it is discovered or exploited.

**Misconfigurations**

Unlike vulnerabilities, misconfigurations are caused by an insecure system setup.

Examples include weak passwords, exposed databases, and incorrect access controls.

**Supply chain attacks**

Attackers can compromise trusted software or dependencies and use them to reach the organizations that depend on them.

---

## Mitigation and Detection

A major distinction covered in the module was between **mitigation** and **detection**.

### Mitigation

Mitigation attempts to prevent attacks or reduce their impact.

Examples include:

- Patch management
- Anti-phishing solutions
- Antivirus / EDR
- Network restrictions
- Security awareness training
- Configuration audits

### Detection

Detection focuses on identifying attacks that get past preventive controls.

This is where the SOC plays an important role by monitoring alerts, investigating suspicious activity, and escalating or responding to incidents.

The overall idea can be summarized as:

**Mitigate → Detect → Investigate → Respond**

---

## Internal SOC vs MSSP

The module also introduced two common SOC environments.

| Internal SOC | MSSP |
|---|---|
| Protects its own organization | Provides security services to multiple customers |
| Usually works with a smaller set of tools | May work with many different tools and platforms |
| Analysts develop deep knowledge of one environment | Analysts gain exposure to multiple environments |
| Workload can be more predictable | Can be faster-paced and higher-pressure |

An MSSP can therefore provide a lot of exposure to different attacks, while an internal SOC allows analysts to develop deeper knowledge of a particular organization.

---

## SOC Career Path

SOC L1 can be used as an entry point into cybersecurity.

A possible progression is:

**SOC L1 → SOC L2 → Senior / Specialized Role**

From there, different paths are possible, including:

- Security Engineering
- Incident Response
- Threat Intelligence
- Digital Forensics
- Management
- Other specialized security roles

The module emphasized using the first years of experience to build practical skills and determine which area of cybersecurity is the best fit.

---

## Practical Work

The module included practical scenarios where I worked from the perspective of a SOC analyst.

### Human Attack Scenario

I worked with a security dashboard to:

- Identify employees at risk
- Apply appropriate protections
- Work with security policies

### System Attack Scenario

I also worked with systems at risk and had to:

- Investigate the affected systems
- Determine appropriate actions
- Select suitable remediation measures

### Security Role Challenge

The final challenge required matching different security roles to incidents based on the responsibilities of each role.

This helped reinforce the differences between SOC analysts, engineers, incident responders, and other security roles.

---

## Key Takeaways

- The **SOC** is a major part of an organization's defensive security.
- **L1 analysts** focus heavily on alert triage and initial investigation.
- Attackers can use both **humans and systems** as attack vectors.
- Social engineering takes advantage of human trust and emotions.
- Vulnerabilities and misconfigurations are different problems and require different responses.
- Security requires both **mitigation and detection**.
- SOC analysts work with other teams rather than operating in isolation.
- SOC L1 experience can lead to several different cybersecurity career paths.

---

## Conclusion

This module gave me a better understanding of where a SOC analyst fits within an organization's security structure and what the defensive side of cybersecurity looks like.

The practical scenarios also helped connect the concepts to the decisions a SOC analyst may have to make when dealing with employees, vulnerable systems, and security incidents.
