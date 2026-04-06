# Splunk SIEM Lab

Splunk Enterprise indexer deployed as an LXC container on a two-node Proxmox cluster. Ingests logs from 10+ sources across all VLANs. 7 dashboards built covering authentication, network traffic, DNS intelligence, Linux/Windows security, FreeIPA, and lab health.

---

## Stack

| Detail | Value |
|---|---|
| Deployment | LXC container, Proxmox node su1 |
| Web UI | Port 8000 |
| Forwarder port | 9997 TCP |
| Syslog port | 5514 UDP |
| OPNsense sourcetype | `opnsense:filterlog` |

---

## Contents

- [Log Sources](log-sources.md)
- [Dashboards](dashboards.md)

---

## Forwarder Deployment

All Linux hosts provisioned via the `splunk_forwarder` Ansible role:

- Dedicated `splunk` system user and group on each host
- `outputs.conf` templated to indexer IP and port 9997
- `inputs.conf` monitors `/var/log/syslog` and `/var/log/auth.log`
- Debian hosts: boot-start via built-in splunk command
- RHEL/AlmaLinux hosts: systemd unit deployed, ACLs set on `/var/log/secure`, `/var/log/messages`, `/var/log/audit/audit.log`
- Pi5: ARM64 build v10.2.1, installed manually outside the role

Proxmox nodes forward via rsyslog to the indexer syslog port. OPNsense forwards via System → Settings → Logging → Remote, UDP 5514.
