[![eugeneivanov.dev — Infrastructure Engineering](assets/eugeneivanov-dev-logo_1280.webp)](https://eugeneivanov.dev)

# Infrastructure Lab — Engineering Journal

The working record of a permanent infrastructure lab — implementation logs, troubleshooting cases, and technical decisions captured during actual work. The polished version of the journal is published on [eugeneivanov.dev](https://eugeneivanov.dev); this repository is the raw record.

---

## The lab

Two-node Proxmox VE high-availability cluster on ZFS with bidirectional replication and an external QDevice for quorum. RHEL 10 and Ubuntu Server fleet managed by Ansible ([public repo](https://github.com/eugeneivanov-dev/ansible)). Internal DNS on BIND 9 (primary/secondary), private PKI on step-ca alongside Let's Encrypt, Prometheus and Grafana observability, seven VLANs with deny-by-default firewall policy on UniFi, off-node backups verified by real restores — all on a wall-mounted rack with structured cabling, a Synology NAS, and UPS-backed power.

Full environment: [eugeneivanov.dev/infra](https://eugeneivanov.dev/infra)

---

## Journal

- **Raw journal (latest entries):** [journal/README.md](journal/README.md)
- **Published journal:** [eugeneivanov.dev/journal](https://eugeneivanov.dev/journal)

---

## Documentation

- [Rack Layout](docs/rack-layout.md)
- [Network topology](docs/network-topology.svg)

---

## The build

Physical build of the infrastructure rack.

![Rack Installation](photos/rack-installation-start.webp)

![Network Stack](photos/network-stack-install.webp)

![Rack Layout](photos/rack-final-layout.webp)

---

## Links

- **Website:** [eugeneivanov.dev](https://eugeneivanov.dev)
- **Practice:** [proveninfra.com](https://proveninfra.com)
- **LinkedIn:** [linkedin.com/in/eugeneivanov-dev](https://www.linkedin.com/in/eugeneivanov-dev)