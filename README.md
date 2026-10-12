# Active Directory & Splunk SIEM Home Lab

A virtualized cybersecurity lab for practicing Windows domain administration, centralized log collection, SIEM investigations, and controlled attack simulations.

## Overview

Built an isolated, four-VM environment using VirtualBox to monitor Windows authentication and endpoint activity through Splunk Enterprise.

## Lab Architecture

| Virtual Machine | Role | Technologies |
|---|---|---|
| **DC01** | Domain controller | Windows Server 2025, Active Directory, DNS |
| **PC01** | Domain-joined endpoint | Windows 11, Splunk Universal Forwarder |
| **Ubuntu / Splunk** | SIEM server | Ubuntu Server 24.04.4 LTS, Splunk Enterprise |
| **Kali Linux** | Security testing | Kali Linux, controlled attack simulations |

**Network:** Isolated VirtualBox host-only network (`192.168.56.0/24`)

## Technologies Used

- **Identity:** Active Directory, Group Policy, DNS, domain users and groups
- **SIEM:** Splunk Enterprise, Splunk Universal Forwarder, SPL
- **Endpoint monitoring:** Windows Security Event Logs, Sysmon
- **Security testing:** Kali Linux, failed-login testing, Kerberoasting simulation
- **Virtualization:** Oracle VirtualBox

## Security Investigations

### 1. Failed Login Analysis

- Investigated Windows Security Event ID **4625**.
- Used SPL `rex` to extract account names and source IP addresses from raw XML.
- Aggregated events using `stats` and filtered repeated failures using `where`.
- Recorded test results included 6 failures for `FakeLabUser` and 5 for `Administrator` from the Kali test IP.

### 2. Kerberos Service-Ticket Investigation

- Investigated Windows Security Event ID **4769**.
- Conducted a controlled Kerberoasting simulation involving the `SQLService` account.
- Extracted source IP information and identified 3 matching service-ticket events associated with Kali Linux.

### 3. Sysmon Monitoring

- Collected Sysmon Operational event data.
- Extracted event IDs from XML logs and aggregated event counts using SPL.
- Visualized endpoint activity in Splunk Dashboard Studio.

## Splunk Dashboard

Created a four-panel **Security Monitoring Dashboard**:

1. Failed Login Attempts Over Time
2. Kerberoasting Activity by Source IP
3. Sysmon Events by Event ID
4. Failed Login Attempts by Account

## Saved Searches

- `Failed Login Investigation by Source IP and Account`
- `Kerberoasting - SQLService Ticket Activity`

Both saved reports are enabled in Splunk.

## Skills Demonstrated

- Active Directory and Windows Server administration
- SIEM deployment and centralized log collection
- SPL query development and XML field extraction
- Windows authentication event analysis
- Kerberos service-ticket investigation
- Sysmon endpoint telemetry analysis
- Dashboard development and troubleshooting

## Future Improvements

- Add screenshots of the dashboard and investigation results.
- Expand detection coverage to account creation and privileged-group changes.
- Explore automated alerting with a Splunk license that supports it.

## Disclaimer

All security testing was performed in an isolated, self-managed lab for educational purposes. Findings represent controlled test activity, not a real-world incident.
