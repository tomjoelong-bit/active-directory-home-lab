# Splunk Investigation Queries

These SPL searches were developed for my Active Directory and Splunk SIEM home lab.

## Failed Login Investigation

**File:** `failed-login-investigation.spl`

- Searches Windows Security Event ID `4625`.
- Extracts account names and source IP addresses from raw XML event data.
- Counts failed logins by account and source IP.
- Sorts results by the highest number of failures.

**Goal:** Investigate repeated authentication failures and identify the accounts and sources involved.

## Kerberos Service-Ticket Investigation

**File:** `kerberoasting-investigation.spl`

- Searches Windows Security Event ID `4769` for activity involving `SQLService`.
- Extracts the source IP address.
- Counts matching events by source IP.

**Goal:** Investigate service-ticket activity associated with a controlled Kerberoasting exercise.

**Note:** Event ID `4769` alone does not prove Kerberoasting. The surrounding activity and account context must also be investigated.
