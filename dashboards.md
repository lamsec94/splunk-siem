# Dashboards

7 dashboards built across authentication, security, network, DNS, and lab health.

| Dashboard | Data Sources | Key Panels |
|---|---|---|
| Auth Overview | Linux auth.log, Windows Security log | Failed/successful logins, sources, lockouts |
| Windows Security | LAB-DC Security event log | Event IDs 4624/4625/4720/4728/4732/4740/4756 |
| Linux Security | /var/log/auth.log all Linux hosts | SSH logins, sudo usage, failed auth |
| FreeIPA | Kerberos + LDAP logs | Auth failures, HBAC denies, password changes |
| Lab Health | All hosts via forwarders | Forwarder heartbeat, system errors, index storage |
| DNS Intelligence | AdGuard logs from Pi5 | Top domains, blocked queries, top clients |
| Network Traffic | OPNsense firewall logs | Denied connections, inter-VLAN flows, traffic by interface |

---

## Screenshots

### Auth Overview
![Auth Overview](images/auth overview.png)

### DNS Intelligence
![DNS Intelligence](images/dns intelligence.png)

### Lab Health
![Lab Health](images/lab health.png)

### Linux Security
![Linux Security](images/linux security.png)

### Network Traffic
![Network Traffic](images/network traffic.png)
