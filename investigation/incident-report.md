# Windows Security Event Investigation Report

## 1. Investigation Overview

**Investigation Type:** Windows Authentication and Privileged Logon Analysis
**Environment:** Windows 11 Personal Lab
**Log Source:** Windows Security Event Logs
**Tools:** Windows Event Viewer and PowerShell
**Investigation Date:** October 2026

### Objective

To investigate Windows authentication activity, identify failed login attempts, analyse privileged logon sessions, and assess whether observed events require further security investigation.

---

## 2. Investigation A — Failed Authentication

**Event ID:** 4625
**Event Description:** An account failed to log on.

### Observed Evidence

| Field      | Value                        |
| ---------- | ---------------------------- |
| Account    | mamga                        |
| Domain     | SATVIK                       |
| Timestamp  | 25 October 2026, 10:48:22 PM |
| Logon Type | 2                            |
| Status     | 0xc000006d                   |
| SubStatus  | 0xc000006a                   |
| Process    | msedgewebview2.exe           |
| Source IP  | Not available                |

### Analysis

Event ID 4625 records an unsuccessful authentication attempt.

The status code 0xc000006d indicates a general logon failure.

The substatus code 0xc000006a indicates an incorrect password.

Logon Type 2 represents an interactive logon attempt.

The associated process was msedgewebview2.exe.

### Assessment

The event indicates an unsuccessful authentication attempt involving an incorrect password.

Possible explanations include incorrect credentials supplied by an application or a legitimate user authentication failure.

The available evidence does not establish malicious activity.

### Recommended SOC Actions

1. Review nearby authentication events.
2. Check whether the same account generated additional failed logons.
3. Examine related successful logons.
4. Investigate the associated process if unusual behaviour is observed.
5. Correlate with endpoint and application logs where available.

**Investigation Status:** Requires contextual investigation. No confirmed security incident.

---

## 3. Investigation B — Privileged Logon Activity

**Event ID:** 4672
**Event Description:** Special privileges assigned to a new logon.

### Observed Evidence

A total of 463 Event ID 4672 records were identified.

Key observations:

* 440 records were associated with SYSTEM.
* The predominant Logon ID was 0x3e7.
* Most of these entries used Logon Type 5.
* Observed privileges included SeAssignPrimaryTokenPrivilege and SeSecurityPrivilege.

### Analysis

Event ID 4672 indicates that special privileges were assigned to a logon session.

The SYSTEM account routinely requires elevated privileges to perform operating system operations.

Logon Type 5 represents a service logon.

Therefore, the observed SYSTEM-related service activity is consistent with normal Windows operating system behaviour.

### Assessment

The event count alone does not indicate malicious privilege escalation.

However, unexpected privileged sessions or unusual account activity should be investigated.

### Recommended SOC Actions

1. Identify the account associated with the event.
2. Examine the Logon ID.
3. Review the assigned privileges.
4. Correlate the event with Event ID 4624.
5. Investigate unexpected privileged sessions.

**Investigation Status:** No confirmed malicious privilege escalation identified.

---

## 4. Overall Investigation Findings

| Event ID | Activity                    | Count |
| -------- | --------------------------- | ----: |
| 4624     | Successful Logon            |   485 |
| 4625     | Failed Logon                |     1 |
| 4634     | Logoff                      |    44 |
| 4648     | Explicit Credentials        |    23 |
| 4672     | Special Privileges Assigned |   463 |

### Key Observations

* Successful authentication events were identified.
* One failed authentication event was investigated.
* The failed login contained an incorrect-password substatus.
* Privileged logon activity was predominantly associated with SYSTEM service sessions.
* No confirmed malicious activity was established from the available evidence.

---

## 5. Final Conclusion

This investigation demonstrated the use of Windows Security Event Logs to analyse authentication activity and privileged logon sessions.

The investigation involved identifying relevant Event IDs, interpreting authentication failure codes, examining logon types, and evaluating privileged account activity.

The findings demonstrate foundational SOC investigation skills, including evidence collection, event analysis, security triage, and incident documentation.

Further correlation with additional endpoint and network telemetry would be required to establish whether any observed activity represents a genuine security threat.

---

## 6. Skills Demonstrated

* Windows Security Event Log Analysis
* Authentication Investigation
* Failed Login Analysis
* Privileged Account Monitoring
* Windows Event ID Interpretation
* PowerShell Log Analysis
* Security Event Correlation
* Incident Triage
* Technical Documentation

---

## 7. Investigation Limitations

* Analysis was conducted using logs from a personal Windows 11 environment.
* The investigation was limited to the available exported Security Event Logs.
* No enterprise SIEM or centralised endpoint detection platform was used.
* Individual events were not sufficient to establish malicious intent.
* Additional telemetry would be necessary for deeper investigation.

**Disclaimer:** This project was conducted in a controlled personal lab environment for educational and cybersecurity portfolio purposes.

