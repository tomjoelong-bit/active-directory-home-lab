# Active Directory & Splunk SIEM Home Lab

A virtualized cybersecurity lab built to practice Windows domain administration, centralized log collection, and security investigations using Splunk Enterprise.

## Overview

This project uses four virtual machines in an isolated VirtualBox network to monitor Windows authentication activity, analyze endpoint events, and investigate controlled attack simulations.

## Lab Setup

**DC01 — Domain Controller**
- Windows Server 2025
- Active Directory Domain Services
- DNS and Group Policy

**PC01 — Windows Client**
- Windows 11
- Joined to the Active Directory domain
- Splunk Universal Forwarder

**Ubuntu — SIEM Server**
- Ubuntu Server 24.04.4 LTS
- Splunk Enterprise
- Centralized Windows log collection

**Kali Linux — Testing Machine**
- Used to generate controlled security-testing activity
- Used for failed-login and Kerberoasting simulations

**Network:** VirtualBox host-only network (`192.168.56.0/24`)

## Technologies

- **SIEM:** Splunk Enterprise, Splunk Universal Forwarder, SPL
- **Windows Security:** Active Directory, Group Policy, DNS, Windows Security Event Logs
- **Endpoint Monitoring:** Sysmon
- **Security Testing:** Kali Linux, failed-login testing, Kerberos service-ticket investigation
- **Virtualization:** Oracle VirtualBox

## Security Investigations

### Failed Login Analysis

- Investigated Windows Security Event ID `4625`.
- Extracted usernames and source IP addresses from raw XML event data using SPL `rex`.
- Aggregated failed-login events by account and source IP using `stats`.
- Applied a threshold of five or more failures using `where`.
- Recorded test results included six failures for `FakeLabUser` and five for `Administrator` from the Kali test IP.
  
**Findings:** The investigation identified 6 failed login attempts for `FakeLabUser` and 5 for `Administrator`, originating from the Kali Linux test IP (`192.168.56.105`).
**Response:** Investigate the source IP and targeted accounts, review surrounding authentication events, and consider account lockout policies if the activity is unauthorized.

### Kerberos Service-Ticket Investigation

- Investigated Windows Security Event ID `4769`.
- Conducted a controlled Kerberoasting simulation involving the `SQLService` account.
- Extracted the source IP address from raw event data.
- Identified three matching service-ticket events associated with Kali Linux.
- Investigated the results in Splunk Search & Reporting.

### Sysmon Monitoring

- Collected Sysmon Operational event data.
- Extracted event IDs from XML-formatted logs.
- Aggregated event counts using SPL.
- Visualized endpoint activity in a custom dashboard.

## Splunk Dashboard

Created a four-panel dashboard named **Security Monitoring Dashboard**.

- Failed Login Attempts Over Time
- Kerberoasting Activity by Source IP
- Sysmon Events by Event ID
- Failed Login Attempts by Account

## Saved Searches

Created and enabled two reusable Splunk reports:

- `Failed Login Investigation by Source IP and Account`
- `Kerberoasting - SQLService Ticket Activity`

## Skills Demonstrated

- Active Directory and Windows Server administration
- Centralized log collection and SIEM configuration
- SPL query development and XML field extraction
- Windows authentication event analysis
- Kerberos service-ticket investigation
- Sysmon endpoint monitoring
- Security dashboard development
- Virtual machine networking and troubleshooting

## Future Improvements

- Expand monitoring to account creation and privileged-group changes.
- Implement automated alerting if using a Splunk license that supports it.
- Refine dashboard panels to make investigation results easier to interpret.

## Disclaimer

All security testing was performed in an isolated, self-managed lab for educational purposes. Results represent controlled test activity, not a real-world incident.

## Screenshots

### Failed Login Attempts Over Time

![Failed Login Attempts Over Time](screenshots/failed-login-timeline.png)

### Kerberoasting Activity by Source IP

![Kerberoasting Activity by Source IP](screenshots/kerberoasting-source-ip.png)

### Sysmon Events by Event ID

![Sysmon Events by Event ID](screenshots/sysmon-event-counts.png)

## Project Files

- [Splunk investigation queries](queries/README.md)
- [Failed-login SPL search](queries/failed-login-investigation.spl)
- [Kerberos investigation SPL search](queries/kerberoasting-investigation.spl)
- [Lab screenshots](screenshots/)
