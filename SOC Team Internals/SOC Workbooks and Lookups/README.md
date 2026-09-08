# SOC Workbooks and Lookups

## Overview

This TryHackMe room focused on how SOC analysts gather additional context during **alert triage** and use that information to determine whether activity is expected or suspicious.

I learned how **identity inventories, asset inventories, and network diagrams** can help provide context about users, systems, and IP addresses. The room also introduced **SOC workbooks**, which provide structured investigation steps to help analysts follow a consistent process and avoid missing important evidence.

The practical work involved building investigation workflows using an interactive interface.

## What I Learned

### Identity Inventory

An **identity inventory** is a catalogue of identities within an organisation, including employee accounts and service accounts.

It can provide information such as:

* Username and email
* Role
* Location
* Access permissions
* Privileges
* Contact information

This information is useful when investigating an alert involving a particular user. For example, knowing the role and access of **G.Baker** and **R.Lund** can provide additional context when investigating activity involving financial records.

Identity information can come from sources such as **Active Directory, Entra ID, SSO providers, HR systems, and custom solutions**.

### Asset Inventory

An **asset inventory** provides information about computing resources within an organisation, particularly **servers and workstations**.

Useful information can include:

* Hostname
* Location
* IP address
* Operating system
* Owner
* Purpose

For example, looking up `HQ-FINFS-02` showed that it is a **Windows Server 2022 file server for financial records** located in the UK Datacenter.

This helped me understand that a hostname in an alert is not enough by itself. Knowing what the system is used for and where it is located provides important context for the investigation.

Asset information can be obtained from **Active Directory, SIEM/EDR platforms, MDM solutions, or custom asset inventories**.

### Network Diagrams

Network diagrams provide a visual representation of an organisation's **locations, subnets, services, and network connections**.

They are particularly useful when an investigation involves multiple IP addresses or suspicious network activity.

In the example scenario, an external IP `103.61.240.174` repeatedly connected to the corporate firewall over **TCP/10443**. The activity was later associated with the internal IP `10.10.0.53`.

The network diagram showed that:

* TCP/10443 was used for the corporate VPN.
* `10.10.0.0/16` was the VPN subnet.
* `172.16.15.0/24` was the Database subnet.
* `172.16.23.0/24` was the Office subnet.

This allowed the activity to be understood as an attack path rather than just a collection of unrelated IP addresses.

The threat actor first performed a **VPN brute-force attack**. After successfully logging in, the VPN assigned the session the internal address `10.10.0.53`. The attacker then attempted to scan the Database subnet but was likely blocked by firewall rules before moving on to the Office subnet.

This also helped me understand that an attacker using a VPN does not necessarily become physically present on the company's LAN. Instead, the VPN can provide the remote connection with an **internal VPN address and access to permitted parts of the internal network**.

### SOC Workbooks

A **SOC workbook**, also known as a playbook, runbook, or workflow, is a structured set of investigation and response steps for a particular type of threat.

Workbooks are especially useful for **L1 SOC analysts**, since they provide a defined process for investigations that may otherwise require significant experience.

Instead of relying entirely on memory or judgement, an analyst can follow the required steps and reduce the chance of missing important evidence.

I learned that workbooks can vary significantly between SOC teams. Some organisations may maintain hundreds of detailed workbooks for specific detections, while others may use a smaller number of high-level workbooks and rely more on the experience of their L1 analysts.

### Workbook Investigation Flow

The example workbook for an **Unusual Login Location** alert was divided into three main stages:

1. **Enrichment**
   Gather additional information using resources such as identity inventory and Threat Intelligence.

2. **Investigation**
   Use the gathered information and SIEM logs to determine whether the activity is expected. This can include analysing the IP and checking user behaviour.

3. **Escalation**
   Based on the findings, escalate the alert to L2, communicate with the user when necessary, or close the alert.

The overall process can be represented as:

`Enrichment → Investigation → Escalation`

This structure helps ensure that the analyst gathers enough evidence before making a final decision.

## Practical Work / Lab

I practiced building a **SOC investigation workbook** using the interactive interface provided by the room.

The task involved taking the available investigation steps and **dragging and dropping them into the correct positions** in the workflow.

Correctly placed steps remained in position, allowing me to build the investigation workflow step by step.

This practical exercise helped reinforce the idea of breaking an investigation into **modular blocks** and placing those blocks in a logical order.

## Key Takeaways

* **Identity inventories** provide context about users, service accounts, roles, and access.
* **Asset inventories** help identify what systems are involved in an alert and what those systems are used for.
* **Network diagrams** help analysts understand how IP addresses, subnets, and services relate to each other.
* VPN connections can give remote users an **internal VPN address** and access to permitted internal network resources.
* Combining different sources of context makes it easier to understand suspicious activity and reconstruct attack paths.
* **SOC workbooks** provide a consistent structure for investigating and responding to alerts.
* Workbooks can range from simple analyst guides to highly detailed processes similar to SOAR playbooks.
* Breaking investigations into **modular steps** makes them easier to follow and standardise.

## Conclusion

This room helped me understand how SOC analysts go beyond the information contained in an initial alert by using **identity, asset, and network lookups** to build additional context.

I also learned how **SOC workbooks** turn investigation processes into structured workflows. This is particularly useful for L1 analysts because it provides a repeatable process for gathering evidence, making a verdict, and deciding whether an alert should be escalated or closed.

The practical workbook exercise helped me connect these concepts to the way an investigation can be structured in a real SOC environment.
