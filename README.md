Active Directory & Splunk SIEM Home Lab

Overview

Built a virtualized cybersecurity lab to practice Windows domain administration, centralized log collection, security event analysis, and controlled attack simulations. Integrated Windows Security logs and Sysmon telemetry with Splunk Enterprise to investigate authentication activity and visualize security events.

Lab Architecture

Virtual Machine

Role

Technologies

DC01

Domain controller

Windows Server 2025, Active Directory, DNS

PC01

Domain-joined endpoint

Windows 11, Splunk Universal Forwarder

Ubuntu / Splunk

SIEM server

Ubuntu Server 24.04.4 LTS, Splunk Enterprise

Kali Linux

Security testing

Kali Linux, controlled attack simulations

Network: Isolated VirtualBox host-only network (192.168.56.0/24)

Technologies Used

Identity and Access Management: Active Directory Domain Services, domain users and groups, Group Policy, DNS

SIEM and Log Management: Splunk Enterprise, Splunk Universal Forwarder, SPL

Endpoint Telemetry: Windows Security Event Logs, Sysmon

Security Testing: Kali Linux, controlled failed-login testing, Kerberoasting simulation

Virtualization and Operating Systems: Oracle VirtualBox, Windows Server 2025, Windows 11, Ubuntu Server

What I Built

Configured a Windows Server domain controller and Active Directory domain.

Joined a Windows 11 endpoint to the domain.

Configured DNS and worked with domain users, groups, and Group Policy.

Installed Splunk Enterprise on Ubuntu Server.

Configured Universal Forwarders to send Windows logs to Splunk.

Collected Windows Security events and Sysmon telemetry.

Created SPL searches to investigate failed authentication and Kerberos service-ticket activity.

Built a four-panel Splunk Dashboard Studio dashboard.

Saved reusable searches for failed-login and Kerberos investigations.

Security Investigations

1. Failed Authentication Analysis

Investigated Windows Security Event ID 4625.

Extracted account names and source IP addresses from raw XML event data using SPL rex.

Aggregated failed-login events using stats.

Applied a threshold of five or more failures to identify repeated failures.

In recorded test results, identified six failures for FakeLabUser and five for Administrator from the Kali test IP.

2. Kerberos Service-Ticket Investigation

Investigated Windows Security Event ID 4769.

Conducted a controlled Kerberoasting exercise involving the lab's SQLService account.

Extracted source IP information from event data.

Identified three matching service-ticket events associated with the Kali test machine.

Investigated the activity through Splunk Search & Reporting.

3. Sysmon Endpoint Monitoring

Collected Sysmon Operational events.

Extracted event IDs from XML-formatted logs.

Aggregated events by event ID to summarize endpoint activity.

Visualized Sysmon event counts in Splunk Dashboard Studio.

Splunk Dashboard

The custom Security Monitoring Dashboard contains four panels:

Failed Login Attempts Over Time

Kerberoasting Activity by Source IP

Sysmon Events by Event ID

Failed Login Attempts by Account

Saved Searches

Failed Login Investigation by Source IP and Account

Kerberoasting - SQLService Ticket Activity

Both saved reports are enabled in Splunk.

Skills Demonstrated

Active Directory and Windows Server administration

Centralized log collection and SIEM configuration

SPL query development and raw XML field extraction

Windows authentication event analysis

Kerberos service-ticket investigation

Endpoint telemetry analysis with Sysmon

Security dashboard development

Virtual machine networking and troubleshooting

Limitations and Future Improvements

Configure automated alerting when using a Splunk license that supports it.

Expand detection coverage to include account creation and privileged-group changes.

Add documented screenshots of the dashboard and investigation results.

Continue refining detection searches and documenting test methodology.

Disclaimer

All attack simulations were conducted in an isolated, self-managed virtual lab for educational purposes. The findings represent controlled test activity, not a real-world incident.
