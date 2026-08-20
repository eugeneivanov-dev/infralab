# Rack Layout

Current lab rack configuration.

## Top of Rack

Synology DS720+ (2 × 14 TB, RAID 1)
Active NAS: NFS backup target and QDevice host for the Proxmox cluster.

## Top to Bottom Layout

1U Patch Panel
Structured cabling termination.

1U UniFi Switch
Main network switch connecting internal devices.

1U Brush Panel
Cable management for internal rack routing.

1U UDM Pro Max
Router, firewall and network gateway.

1U PDU
Rack power distribution.

1U Blank Panel
Used for airflow control.

Shelf (Lab Compute Area)
2 × Dell Pro Micro Plus — Proxmox VE cluster nodes.

2U Synology RS1221+
Rack-mounted, no drives installed — not yet in service.

2U APC Rack UPS
Provides power protection and graceful shutdown capability.

## Notes

The rack is organized to separate:

- Network infrastructure
- Power distribution
- Compute resources
- Storage