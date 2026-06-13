## technique breakdown T1621

multi-factor authentication request generation


Adversaries may attempt to bypass multi-factor authentication (MFA) mechanisms and gain access to accounts by generating MFA requests sent to users.

Adversaries in possession of credentials to Valid Accounts may be unable to complete the login process if they lack access to the 2FA or MFA mechanisms required as an additional credential and security control. To circumvent this, adversaries may abuse the automatic generation of push notifications to MFA services such as Duo Push, Microsoft Authenticator, Okta, or similar services to have the user grant access to their account. If adversaries lack credentials to victim accounts, they may also abuse automatic push notification generation when this option is configured for self-service password reset (SSPR).[1]

In some cases, adversaries may continuously repeat login attempts in order to bombard users with MFA push notifications, SMS messages, and phone calls, potentially resulting in the user finally accepting the authentication request in response to "MFA fatigue.


## AN0451
Detect repeated failed login events followed by MFA challenges triggered in rapid succession, especially if originating from service accounts or anomalous IP addresses.


## Log source 

user account authentication(DC0002) -> WinEventLog: Security  -> EventCode = 4625

## Mutable elements
serviceaccountexclusion ->  exclude specific accounts where automated MFA requests are legitimate 


```
title: MFA Fatigue - Repeated Failed Logon Attempts (AN0451)
id: a3f1b2c4-9d8e-4f7a-b6c5-2e1d0f9a8b7c
status: experimental
description: >
  Detects potential MFA fatigue attacks by identifying repeated failed
  authentication attempts against the same account within a short
  timeframe. Adversaries with valid credentials repeatedly trigger
  logon failures to bombard users with MFA push notifications until
  accepted (T1621).
author: Krishna Gupta
date: 2026-06-12
logsource:
  product: windows
  service: security          # Windows Security Event Log
detection:
  selection_failed_logon:
    EventID:
      - 4625                 # Failed logon (all types)
      - 4771                 # Failed Kerberos pre-authentication
      - 4776                 # Failed NTLM authentication
  filter_legitimate:
    SubjectUserName|endswith: '$'    # Exclude machine accounts
    TargetUserName|contains:
      - 'ANONYMOUS'
      - 'anonymous'
  condition: selection_failed_logon and not filter_legitimate |
             count(TargetUserName) by TargetUserName > 10
timeframe: 5m
fields:
  - TargetUserName
  - IpAddress
  - LogonType
  - FailureReason
  - WorkstationName
  - EventID
falsepositives:
  - Legitimate users forgetting passwords and repeatedly retrying
  - Service accounts with expired credentials
  - Misconfigured applications hitting auth endpoints repeatedly
  - Tune threshold based on environment baseline
level: high
tags:
  - attack.credential_access
  - attack.t1621
  - analytic.an0451
  - detection.det0160
```
### false postivie


as the log and access or normal use we have the work can be different and all
