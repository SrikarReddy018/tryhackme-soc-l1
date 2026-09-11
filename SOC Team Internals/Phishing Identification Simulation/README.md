# Phishing Identification Simulation

## Overview

I completed this phishing identification simulation separately from the SOC L1 module because I wanted to understand how phishing attacks are actually identified and investigated in a security environment.

Instead of only studying phishing from a theoretical perspective, I wanted to see how an analyst would work with suspicious email alerts, examine the available information, identify phishing indicators, and determine whether an alert is malicious or benign.

The simulation provided a SOC-style alert queue containing email-related alerts. I had to analyse the alerts, classify the relevant activity correctly, and prevent the simulated security breach.

## What I Learned

### Phishing Alert Analysis

I learned that identifying phishing is not simply about seeing a suspicious-looking email. The analyst needs to examine the information available in the alert and look for multiple indicators that support the classification.

Some of the information I reviewed included:

- Sender address
- Recipient
- Email subject
- Email content
- External links
- Timestamp
- Alert severity
- Alert type

Looking at these details together provides better context for deciding whether an email is suspicious.

### Suspicious External Links

One of the alerts I investigated was:

`Inbound Email Containing Suspicious External Link`

The alert was classified as:

- Severity: Medium
- Type: Phishing

The email claimed that an unusual sign-in had been detected on a Microsoft account and contained an external link asking the recipient to review the activity.

This demonstrated how phishing emails can use account-security notifications and urgency to encourage a user to click a link.

### Sender and Email Content

The simulation also showed why the sender address and actual content of an email should be examined together.

An email can attempt to appear legitimate by using familiar branding or a believable security scenario. However, the sender information, link, wording, and other details can provide clues that something isn't right.

This reinforced the importance of not trusting an email simply because it looks professional or mentions a familiar service.

## Practical Investigation

### Reviewing the Alert Queue

I worked through the simulated SOC alert queue and reviewed the available alert information before making classification decisions.

The environment provided details such as:

- Alert ID
- Alert rule
- Severity
- Alert type
- Date
- Status
- Event information

One of the phishing alerts I reviewed contained:

`Alert: Inbound Email Containing Suspicious External Link`

`Severity: Medium`

`Type: Phishing`

The email referenced an unusual Microsoft account sign-in and included an external login link.

I used the information provided in the alert to determine the appropriate classification.

### Phishing Identification

The objective of the simulation was to correctly identify the True Positive alerts while avoiding incorrect classifications.

After completing the scenario, the simulation displayed:

`Victory! Security breach prevented!`

It also confirmed that the True Positive alerts had been correctly identified.

### Results

The final results showed:

| Metric | Result |
|---|---:|
| Closed alerts | 4 |
| Mean time to resolve | 5 minutes |
| Mean dwell time | 16 minutes |
| True Positive identification rate | 100% |
| False Positive identification rate | 100% |

The results also showed individual phishing alerts being correctly classified, including resolution times of 8.78 minutes and 3.85 minutes for the displayed alerts.

The simulation noted that the phishing alert took slightly longer to resolve, while the overall scenario was successfully completed.

## Investigation Workflow

The exercise gave me practical experience with a workflow similar to:

```text
Email alert received
        ↓
Review alert details
        ↓
Examine sender and recipient
        ↓
Review subject and email content
        ↓
Look for suspicious links and other indicators
        ↓
Determine whether the activity is malicious
        ↓
Classify the alert
        ↓
Take the appropriate action
