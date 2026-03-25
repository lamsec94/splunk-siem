# Dashboards

7 of 8 planned dashboards built. The 8th (RPi AP) was permanently
skipped — Pi5 has no hostapd running.

| Dashboard | Data Sources | Key Panels | Status |
|---|---|---|---|
| Auth Overview | Linux auth.log + Windows Security log | Failed/successful logins, sources, lockouts | ✅ Built |
| Windows Security | LAB-DC Security event log | Event IDs 4624/4625/4720/4728/4732/4740/4756 | ✅ Built |
| Linux Security | /var/log/auth.log all Linux hosts | SSH logins, sudo usage, failed auth | ✅ Built |
| FreeIPA | Kerberos + LDAP logs | Auth failures, HBAC denies, password changes | ✅ Built |
| Lab Health | All hosts via forwarders | CPU, memory, disk, uptime | ✅ Built |
| DNS Intelligence | AdGuard logs from Pi5 | Top domains, blocked queries, top clients | ✅ Built |
| Network Traffic | OPNsense firewall logs | Denied connections, inter-VLAN flows | ✅ Built |
| RPi AP | Pi5 hostapd + DHCP logs | Client connects, DHCP leases | ❌ Skipped permanently |

## Screenshots

Dashboard screenshots stored in `screenshots/`. Take these directly
from the Splunk UI at http://192.168.11.105:8000.
