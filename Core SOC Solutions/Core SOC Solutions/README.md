# Elastic Stack (ELK)

## Overview

This TryHackMe room introduced me to the **Elastic Stack (ELK)** and how it can be used for log analysis and security investigations.

Although ELK is not traditionally a SIEM, it is widely used by SOC teams for SIEM-like activities because of its ability to collect, search, analyze, and visualize large amounts of log data.

The room focused on understanding the main ELK components, using **Kibana** to search and filter logs, investigating VPN activity, creating visualizations, and building dashboards.

---

## What I Learned

### Elastic Stack Components

The main components covered were:

* **Beats**: Lightweight agents that collect and ship data from endpoints.
* **Logstash**: Processes, filters, normalizes, and forwards data.
* **Elasticsearch**: Stores, searches, and analyzes the ingested data.
* **Kibana**: Provides the interface for searching, investigating, visualizing, and creating dashboards.

The basic workflow is:

```text
Data Sources
     ↓
   Beats
     ↓
 Logstash
     ↓
Elasticsearch
     ↓
  Kibana
```

### Kibana Discover

The **Discover** tab is the main workspace for exploring and investigating logs.

I learned how to work with:

* Index Patterns / Data Views
* Fields and field values
* Search queries
* Filters
* Time ranges
* Event timelines
* Tables

For this room, the VPN data was available through the `vpn_connections` data view.

The timeline was also useful for identifying unusual spikes in event activity.

---

## KQL

I learned the basics of **Kibana Query Language (KQL)**, which is used to search and filter Elasticsearch data through Kibana.

### Free-text search

```text
"United States"
```

### Wildcards

```text
United*
```

### Logical operators

```text
"United States" AND "Virginia"
```

```text
"United States" OR "England"
```

```text
"United States" AND NOT ("Florida")
```

### Field-based search

```text
Source_ip : 238.163.231.224
```

Multiple conditions can also be combined:

```text
Source_ip : 238.163.231.224 AND UserName : Suleman
```

These searches helped me narrow down large amounts of log data and focus on specific events during an investigation.

---

# Practical Lab

The practical part of the room involved using **Kibana to investigate VPN connection logs**, create visualizations, and build a dashboard.

### 1. Setting Up the Lab

I started the TryHackMe lab machine and waited for the Elastic environment to become available.

I then accessed the provided **Kibana dashboard** through the lab's web interface.

The main interface used throughout the practical work was **Discover**, where the ingested VPN logs could be searched and investigated.

---

### 2. Selecting the VPN Data

Inside the Discover tab, I selected the:

```text
vpn_connections
```

data view.

This allowed me to work with the VPN connection data stored in Elasticsearch.

I also made sure the **time picker included January 2022**, since that was the relevant period for the lab data.

A wide time range such as **Last 15 years** could also be used to ensure the required events were included.

---

### 3. Exploring the Logs

The Discover page displayed individual VPN events as log entries.

Each event contained different normalized fields that could be used during an investigation.

Some of the fields I worked with included:

```text
UserName
Source_ip
Source_Country
action
```

The **Fields Pane** on the left side of Discover made it possible to inspect available fields and their values.

I could also select field values and use the `+` or `-` options to include or exclude specific values from the results.

---

### 4. Searching VPN Logs with KQL

I used **Kibana Query Language (KQL)** to search through the VPN logs.

For example, I could search for activity associated with a particular IP address:

```text
Source_ip : 238.163.231.224
```

I could also combine multiple conditions:

```text
Source_ip : 238.163.231.224 AND UserName : Suleman
```

This allowed me to move from searching the entire dataset to investigating specific users and IP addresses.

I also practiced using logical operators such as:

```text
AND
OR
NOT
```

and wildcards such as:

```text
United*
```

This helped me understand how KQL can be used to progressively narrow down a large collection of security logs.

---

### 5. Using Filters

Instead of manually writing every query, I also used Kibana's **Add Filter** functionality.

Filters could be applied directly to fields and values.

For example, I could filter based on:

```text
Source_ip
UserName
Source_Country
action
```

This was useful when investigating a particular type of activity without having to construct the entire query manually.

The combination of **KQL searches and field-based filters** made it easier to isolate relevant VPN events.

---

### 6. Investigating the Timeline

I used the timeline in Discover to understand how the number of events changed over time.

The timeline displays the number of events during different periods.

This can help identify unusual spikes in activity.

For example:

```text
Normal activity
      ↓
Sudden increase in events
      ↓
Investigate the time period
      ↓
Examine the associated logs
```

The room demonstrated an unusual spike in activity around **11 January 2022**.

A spike by itself does not prove malicious activity, but it provides a useful starting point for further investigation.

---

### 7. Creating a Table

By default, Discover displays the logs in their raw form.

I learned how to select important fields and create a cleaner table containing only the information relevant to the investigation.

For example:

```text
Timestamp       UserName       Source_ip
-----------------------------------------
Event 1         User A        IP Address
Event 2         User B        IP Address
Event 3         User C        IP Address
```

Reducing the number of displayed fields makes the results easier to read and reduces unnecessary information.

The table configuration can also be saved for future use.

---

### 8. Creating a Failed Connection Visualization

I then created a visualization specifically for **failed VPN connection attempts**.

I used the:

```text
vpn_connections
```

data view and ensured that the time range included January 2022.

I filtered the events using:

```text
action : failed
```

The goal was to display **only failed VPN connection attempts**.

I selected the following fields for the table:

```text
UserName
Source_ip
```

This produced a more focused view of the users and IP addresses involved in failed connection attempts.

This type of visualization can be useful during investigations because repeated failed connections can be identified more easily than when looking through raw logs.

However, repeated failures alone do not automatically mean an attack. They provide activity that may require additional investigation.

---

### 9. Creating Data Visualizations

I also explored how different fields can be represented visually.

For example, I used:

```text
Source_IP
Source_Country
```

to explore the relationship between source IP addresses and countries.

Kibana allowed me to represent this information using different visualization types, including:

* Tables
* Pie charts
* Bar charts

Visualizations make large amounts of log data easier to interpret and can help reveal patterns that may not be obvious from individual events.

---

### 10. Saving Visualizations

After creating a visualization, I saved it to the Kibana library.

The process involved:

```text
Create Visualization
       ↓
Click Save
       ↓
Add Title
       ↓
Add Description
       ↓
Save and Add to Library
```

Saving the visualization made it possible to reuse it later when creating a dashboard.

---

### 11. Creating a Custom Dashboard

Finally, I created a custom Kibana dashboard to bring the saved searches and visualizations together.

I went to:

```text
Dashboard
     ↓
Create Dashboard
     ↓
Add from Library
```

I then selected the saved searches and visualizations I had created earlier.

After adding them, I arranged and resized the objects to create a useful layout and saved the dashboard.

The final idea was to create a **single view of VPN activity** rather than checking each search or visualization separately.

A dashboard can combine information such as:

```text
Failed Connections
        +
Source IP Information
        +
Country Distribution
        +
Other Saved Searches
        ↓
   VPN Dashboard
```

This provides a centralized view that can help a SOC analyst monitor activity and identify patterns more efficiently.

---

## Important Concepts

### Index Pattern / Data View

Defines which Elasticsearch data Kibana should explore.

### Discover

The main Kibana workspace for searching, filtering, and investigating logs.

### KQL

Kibana Query Language used to search and filter Elasticsearch data.

### Visualization

Represents log data using tables, charts, and other visual formats.

### Dashboard

Combines multiple saved searches and visualizations into a single monitoring view.

---

## Key Takeaways

* Learned the basic architecture of the **Elastic Stack**.
* Understood the roles of **Beats, Logstash, Elasticsearch, and Kibana**.
* Learned how SOC analysts can use Kibana for log analysis and investigation.
* Practiced searching and filtering VPN logs using **KQL**.
* Learned how to use field-based searches and logical operators.
* Used time-based analysis to identify unusual activity patterns.
* Created tables from relevant log fields.
* Created a visualization for failed VPN connection attempts.
* Explored relationships between source IP addresses and countries.
* Saved visualizations for reuse.
* Created a custom dashboard by combining saved searches and visualizations.
* Understood how ELK can support **SIEM-like security monitoring and investigations**.

## Conclusion

This room gave me practical experience with the **Elastic Stack from a SOC analyst's perspective**.

The practical investigation helped me understand how raw VPN logs can be searched, filtered, analyzed, and transformed into useful visualizations and dashboards.

The main workflow I took away from the room was:

```text
Collect
   ↓
Process
   ↓
Store
   ↓
Search
   ↓
Filter
   ↓
Investigate
   ↓
Visualize
   ↓
Monitor
```

This room also helped connect my previous **Splunk** experience with another commonly used security monitoring platform. While the tools and query languages are different, the underlying SOC investigation process remains similar.
