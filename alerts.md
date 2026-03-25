# Alerts

7 alerts defined. None built yet — configure at:
http://192.168.11.105:8000 → Settings → Searches, reports, and alerts → New Alert

Thresholds are starting points — tune after the first week based on
actual baseline noise.

## Brute Force — Linux

Schedule: Every 5 min
Trigger: count > 5

SPL:

index=main sourcetype=syslog "Failed password"
| stats count by src_ip
| where count > 5

## Brute Force — Windows

Schedule: Every 5 min
Trigger: count > 5

SPL:

index=main sourcetype=WinEventLog:Security EventCode=4625
| stats count by Source_Network_Address
| where count > 5

## AD Privileged Group Change

Schedule: Real-time
Trigger: Any event

SPL:

index=main sourcetype=WinEventLog:Security
(EventCode=4728 OR EventCode=4732 OR EventCode=4756)

## AD New Admin Account

Schedule: Real-time
Trigger: Any event

SPL:

index=main sourcetype=WinEventLog:Security EventCode=4720

## FreeIPA Kerberos Spikes

Schedule: Every 10 min
Trigger: count > 10

SPL:

index=main sourcetype=ipa_krb "KRB5KDC_ERR"
| stats count
| where count > 10

## Firewall Deny Spike

Schedule: Every 5 min
Trigger: count > 100

SPL:

index=main sourcetype=opnsense "block"
| stats count
| where count > 100

## New IoT Device

Schedule: Real-time
Trigger: Any event

SPL:

index=main sourcetype=adguard_dhcp "new lease" subnet=192.168.30
