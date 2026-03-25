# Log Sources

## Source Inventory

| Source | Method | Port | Status |
|---|---|---|---|
| All Linux VMs (7 hosts) | Universal Forwarder via Ansible role | 9997 TCP | ✅ Done |
| LAB-DC (Windows Server 2022) | Universal Forwarder MSI | 9997 TCP | ✅ Done |
| Pi5 / AdGuard DNS logs | UF ARM64 v10.2.1, manual install | 9997 TCP | ✅ Done |
| OPNsense firewall logs | Remote syslog | 5514 UDP | ✅ Done |
| su1, su2 Proxmox | rsyslog forward | 5514 UDP | ✅ Done |
| NetBox | UF | 9997 TCP | ❌ Excluded — SSH key auth broken |
| Splunk indexer itself | — | — | ❌ Permanently excluded (self-forward) |
| ER7206 | Remote syslog | 514 UDP | ⚠️ In plan, not confirmed done |
| NPM / Docker host | UF | 9997 TCP | ⚠️ In plan, not confirmed done |
| Guacamole | UF | 9997 TCP | ❌ Host deleted — irrelevant |

## Port Note

Syslog runs on 5514 UDP instead of the standard 514 because LXC
containers cannot bind ports below 1024 without elevated privileges.
OPNsense and Proxmox rsyslog are both configured to forward to 5514.
The ER7206 is the only source still targeting 514 — this needs to be
updated or confirmed if it is ever finalized.
