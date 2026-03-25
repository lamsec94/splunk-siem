# Splunk SIEM Lab

Splunk Enterprise indexer deployed as LXC 102 on Proxmox node su1.
Ingests logs from 10+ sources across all VLANs. 7 dashboards built,
7 alerts defined.

## Stack

| Detail | Value |
|---|---|
| Host | LXC 102 on su1 |
| IP | 192.168.11.105 |
| Web UI | :8000 |
| Forwarder port | 9997 TCP |
| Syslog port | 5514 UDP (LXC cannot bind below 1024) |
| OPNsense sourcetype | opnsense:filterlog |

## Contents

- [Log Sources](log-sources.md)
- [Dashboards](dashboards.md)
- [Alerts](alerts.md)

## Forwarder Deployment

All Linux hosts provisioned via the `splunk_forwarder` Ansible role:
- Dedicated `splunk` system user and group on each host
- `outputs.conf` templated to 192.168.11.105:9997
- `inputs.conf` monitors `/var/log/syslog` and `/var/log/auth.log`
- Debian hosts: boot-start via built-in splunk command
- RHEL/AlmaLinux hosts: systemd unit deployed, ACLs set on
  `/var/log/secure`, `/var/log/messages`, `/var/log/audit/audit.log`
- Pi5: ARM64 build v10.2.1, installed manually outside the role

Proxmox nodes forward via rsyslog:

*.* @192.168.11.105:5514

OPNsense forwards via System → Settings → Logging → Remote, UDP 5514.
