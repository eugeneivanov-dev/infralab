# Engineering Journal

Short notes about infrastructure work, lab experiments, and physical network setup.

---

## 2026-08-10 — Writing Ansible Roles for an Ubuntu Server Baseline

Restructured the Ansible repository for a second fleet — fleet-prefixed roles, lab facts as a single source, one bootstrap play — and wrote all eight Ubuntu baseline roles, proven idempotent on a disposable test VM: changed=0 across the full play.

More details: https://eugeneivanov.dev/journal/labnotes/ubuntu-baseline-ansible-roles/

---

## 2026-08-03 — Auditing the Ubuntu Fleet Before Ansible Touches It

A read-only audit of all seven live Ubuntu VMs before writing their baseline roles: the core standard held, but cloud-init had silently re-opened password SSH on every host, unattended-upgrades was patching the fleet daily, and the monitoring host ran with its firewall off.

More details: https://eugeneivanov.dev/journal/labnotes/ubuntu-fleet-audit-before-ansible/

---

## 2026-08-02 — App Services on Let's Encrypt: Public Certificates for Internal Names

Issued public Let's Encrypt certificates for internal-only lab names via Cloudflare DNS-01 with acme.sh, terminating TLS on an nginx edge in the monitoring Docker stack — Grafana and Prometheus now serve trusted HTTPS with no private root installed anywhere.

More details: https://eugeneivanov.dev/journal/security/app-services-lets-encrypt-dns01/

---

## 2026-08-02 — Attaching Consumers to the Internal CA: Proxmox, Synology, and Device Trust

Both Proxmox nodes and the Synology DSM moved to certificates from the internal chain, the root landed on the administrative devices, certificate lifetimes got matched to the renewal machinery, and revocation turned out to mean renewal denial, not recall.

More details: https://eugeneivanov.dev/journal/security/internal-ca-consumers-proxmox-synology/

---

## 2026-08-02 — Building a Private Certificate Authority with step-ca on RHEL

Stood up the lab's internal CA: a RHEL VM provisioned by playbook, a step-ca PKI with an offline root and an online intermediate, the daemon under systemd, and an ACME endpoint verified end to end with a test certificate issued across the network.

More details: https://eugeneivanov.dev/journal/security/private-ca-with-step-ca-on-rhel/

---

## 2026-07-31 — Going Public: the Ansible Repo Transition, Step by Step

The hands-on half of opening the repo: sanitizing secrets and usernames, moving the vault out of git, building a single-commit public history — and the origin trap that could have pushed private history into the public repo.

More details: https://eugeneivanov.dev/journal/labnotes/going-public-ansible-repo-transition/

---

## 2026-07-31 — Going Public: the Decisions Behind Opening My Ansible Repo

Why the public Ansible repo became the working repo instead of a sanitized snapshot: real inventory, secrets outside git, clean history, and the reasoning behind each call.

More details: https://eugeneivanov.dev/journal/labnotes/going-public-ansible-repo-decisions/

---

## 2026-07-30 — Ansible Baseline — Part 6: Adopting the Live Fleet

Final article of the series: the playbook meets the four hand-built hosts — a drift report that had to earn the right to run, a one-host-at-a-time rollout with reboots, and the fleet at changed=0.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-adopting-live-fleet/

---

## 2026-07-30 — Ansible Baseline, Part 5 — The Clean-VM Proof

Published Part 5 of the Ansible Baseline series: a fresh RHEL 10 VM taken from installer defaults to the full lab standard by one uninterrupted site.yml run (2:11, including a mid-run kernel reboot), a second run reporting changed=0, and an eleven-point diff against the hand-built reference machine — which caught one real difference, a file mode invisible to the eye.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-clean-vm-proof/

---

## 2026-07-29 — Ansible Baseline — Part 4: Seven Roles to a Full Baseline

The first secret lands in Vault, seven roles codify the remaining layers — registration through a version-pinned node_exporter — and the full nine-role playbook holds changed=0 across two consecutive runs.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-seven-roles-full-baseline/

---

## 2026-07-29 — Ansible Baseline — Part 3: A Lint Gate and an Automation User

Two linters gate every push, force_handlers closes a lesson from Part 2, and a dedicated automation user with locked password and NOPASSWD sudo retires the -K prompt across the fleet.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-lint-gate-automation-user/

---

## 2026-07-28 — Ansible Baseline — Part 2: First Roles and the changed=0 Rule

Second article of the Ansible Baseline series: a throwaway test VM, the site.yml skeleton, chrony and ssh_hardening roles, idempotency as the acceptance criterion — and a burned handler that taught me not to infer service state from file state.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-first-roles-idempotency/

---

## 2026-07-28 — Ansible Baseline — Part 1: The Control Side

First article of the Ansible Baseline series: a dedicated control VM, Ansible via pipx on RHEL 10 (no EPEL), a repository with a one-way Git boundary, and an inventory answering ping on all eleven hosts.

More details: https://eugeneivanov.dev/journal/labnotes/ansible-baseline-control-side/

---

## 2026-07-25 — Commissioning a YubiKey from the CLI

Brought a pair of YubiKeys into service as a personal authenticator: verified with ykman, FIDO2 PIN set, both keys registered per service in one session, recovery paths written down before anything was tightened.

More details: https://eugeneivanov.dev/journal/security/commissioning-a-yubikey-from-the-cli/

---

## 2026-07-23 — New project: Ubuntu Baseline for the Lab

Planned the extension of the Ansible Baseline discipline to the seven Ubuntu VMs — parallel roles on native mechanisms (apt, UFW, AppArmor, netplan), same repository and workflow, adoption as a fleet-wide diff of hosts built from evolving manual notes.

More details: https://eugeneivanov.dev/projects/ubuntu-baseline-for-the-lab/

---

## 2026-07-23 — Ansible Baseline for the Lab: complete

Codified the lab's RHEL baseline as idempotent Ansible roles and adopted it across the fleet — five phases from control VM to fleet-wide check mode reading changed=0; the standard now lives in Git and drift is readable in one command.

More details: https://eugeneivanov.dev/projects/ansible-baseline-for-the-lab/

---

## 2026-07-21 — Secrets for the Lab (HashiCorp Vault)

Planned and published the secrets project: one Vault server on RHEL with a single KV v2 store, taking over the credentials the previous three projects parked as temporary — Ansible's subscription credentials, FreeIPA's admin material, Keycloak's client secrets. Manual unseal by design (Shamir 5/3), hypervisor HA with restore-verified raft snapshots, OIDC login through Keycloak with a hardware key, audit log from day one. The PKI engine stays off — four singular authorities: names, certificates, identity, secrets.

More details: https://eugeneivanov.dev/projects/hashicorp-vault-for-the-lab/

---

## 2026-07-21 — SSO for the Lab (Keycloak)

Planned and published the web SSO project: one Keycloak server on RHEL, federating users from the FreeIPA directory over LDAPS and issuing OIDC logins with TOTP as the second factor — Grafana as the first consumer, every future web service joining the same door. Deliberately a reader of the directory, not a second user store — and the first service in the redundancy series where hypervisor HA is the right answer, not the protocol.

More details: https://eugeneivanov.dev/projects/keycloak-sso-for-the-lab/

---

## 2026-07-19 — Identity for the Lab (FreeIPA)

Planned and published the identity project: a FreeIPA replica pair on RHEL, one server per Proxmox node in multi-master replication — centralized users, Kerberos, directory-served SSH keys, and sudo/HBAC policy for every enrolled guest, with redundancy by replication rather than hypervisor HA, the same design call the DNS pair made. Deliberately a consumer of the existing DNS and PKI layers: no DNS role, no CA role.

More details: https://eugeneivanov.dev/projects/identity-for-the-lab/

---

## 2026-07-19 — Internal DNS for the Lab: BIND Primary/Secondary on RHEL

Deployed the lab's name resolution layer: two BIND servers on RHEL across both Proxmox nodes — authoritative forward and reverse zones, scoped recursion, replication by zone transfer, and the whole network migrated in three waves. Closed with a live failover test: primary down, nobody noticed.

More details: https://eugeneivanov.dev/journal/labnotes/internal-dns-bind-primary-secondary-rhel/

---

## 2026-07-19 — Ansible Baseline for the Lab

Planned and published the Ansible baseline project: the lab's hand-built RHEL standard — networking, SSH hardening, SELinux, firewalld posture, monitoring agent — codified as idempotent, version-controlled playbooks, so every future VM reaches the lab standard by running a play instead of following a document.

More details: https://eugeneivanov.dev/projects/ansible-baseline-for-the-lab/

---

## 2026-07-12 — Internal CA for the Lab (step-ca)

Planned and published the internal CA project: a private PKI on step-ca with an offline root and online intermediate, issuing certificates over ACME to the infrastructure interfaces a public CA cannot cover — Proxmox and NAS management UIs first — while the lab's web services stay on publicly trusted certificates.

More details: https://eugeneivanov.dev/projects/internal-ca-for-the-lab/

---

## 2026-07-12 — ITSM for the Lab (GLPI)

Planned a new foundation project: GLPI on RHEL as the lab's permanent ITSM layer — real monitoring alerts becoming incidents, maintenance running as planned changes with rollback plans, recurring failures tracked as problems, and every VM and node inventoried by agent.

More details: https://eugeneivanov.dev/projects/itsm-for-the-lab/

---

## 2026-07-12 — Internal DNS for the Lab (BIND Primary/Secondary)

Planned and published the internal DNS project: two BIND servers on RHEL, a primary and a secondary on separate Proxmox nodes, serving forward and reverse zones for the lab domain with redundancy handled by the DNS protocol instead of hypervisor HA.

More details: https://eugeneivanov.dev/projects/internal-dns-for-the-lab/

---

## 2026-07-11 — Planned a mini-HPC cluster lab: Slurm, LDAP, and NFS on Proxmox

Scoped a new lab project: a three-node Slurm cluster on RHEL 10 VMs — one controller, two compute nodes — with LDAP-based central authentication and NFS-backed home directories automounted through autofs, running isolated on the production Proxmox cluster.

More details: https://eugeneivanov.dev/projects/mini-hpc-cluster-lab-slurm-ldap-nfs/

---

## 2026-07-11 — Nested vSphere Cluster Lab on Proxmox

Planned a new project: a second hypervisor stack in the lab — a nested vSphere cluster (two ESXi host VMs on separate Proxmox nodes, vCenter, shared NFS datastore from the NAS) with vMotion, HA, and DRS proven by live tests, run in 60-day evaluation-mode cycles where teardown and redeployment are part of the practice.

More details: https://eugeneivanov.dev/projects/nested-vsphere-cluster-lab-on-proxmox/

---

## 2026-07-02 — Installing Cisco Modeling Labs on Proxmox from the OVA

Deployed CML 2.10 as an on-demand VM on the Proxmox cluster from the Personal-license OVA: extracted the VMDK, built a UEFI VM with nested virtualization, imported the disk, ran the setup wizard, registered the 20-node license, and expanded lab storage the supported way through Cockpit.

More details: https://eugeneivanov.dev/journal/labnotes/installing-cml-on-proxmox-from-ova/

---

## 2026-06-29 — Cisco Modeling Labs (CML) Network Lab

Scoped out a CML project — running real Cisco IOS as an on-demand VM on Proxmox to build live Layer 3 by hand, train across the certification ladder, and practice design validation the way an architect does.

More details: https://eugeneivanov.dev/projects/cisco-modeling-labs-network-lab/

---

## 2026-06-27 — A Reinstalled Node Brought Back an Old NIC Hang, and HA Caught It

A node's e1000e NIC hung and the node self-fenced; HA failed its VMs over to the surviving node automatically. The cause was an old offloading fix that a full reinstall had dropped from the network config — re-applied and made persistent, with the layout restored and a previously unprotected VM brought under HA.

More details: https://eugeneivanov.dev/journal/troubleshooting/proxmox-ha-failover-nic-hang-after-reinstall/

---

## 2026-06-25 — A Deny-by-Default WireGuard Server on RHEL 10

Built a road-warrior WireGuard server where access control lives on the server in firewalld policies — a dedicated zone with forwarding off by default, deny-by-default policies, and per-peer authorization by source address.

More details: https://eugeneivanov.dev/journal/networking/deny-by-default-wireguard-firewalld-policies/

---

## 2026-06-24 — IPv6-Only Network Segment on the Home Lab — project planned

Scoped a planned project to run an isolated segment with IPv4 turned off entirely — NAT64/DNS64 translation for reaching IPv4-only resources, per-service IPv6-readiness auditing, and diagnosing what breaks once the IPv4 fallback is gone; the advanced follow-on to the dual-stack build.

More details: https://eugeneivanov.dev/projects/ipv6-only-segment-home-lab/

---

## 2026-06-24 — Dual-Stack IPv4/IPv6 Home Lab Network — project planned

Scoped a planned project to layer IPv6 alongside the existing IPv4 network as a dual-stack deployment — internal addressing, IPv6 firewalling on the RHEL hosts, AAAA records in the internal DNS, and verified dual-stack connectivity; an IPv6-only segment follows as a separate project.

More details: https://eugeneivanov.dev/projects/dual-stack-ipv4-ipv6-home-lab/

---

## 2026-06-24 — Reusable RHEL 10 Baseline

Installed RHEL 10.2 Minimal on a Proxmox VM and brought it to a clean, reusable baseline — static networking, subscription, updates, key-only SSH, SELinux enforcing, and a deny-by-default firewall — so every future service starts from the same known-good foundation.

More details: https://eugeneivanov.dev/journal/linux/reusable-rhel-10-baseline/

---

## 2026-06-22 — Ceph Storage Cluster Lab on Proxmox — project planned

Scoped a planned project to stand up a correct, fully isolated Ceph cluster in lab VMs — to understand Ceph hands-on (monitors, OSDs, placement groups, replication, recovery) without touching the production HA cluster; the ZFS-vs-Ceph findings will follow as a separate writeup.

More details: https://eugeneivanov.dev/projects/ceph-storage-cluster-lab-on-proxmox/

---

## 2026-06-22 — Two-Node Proxmox HA Cluster — project published

Rebuilt the lab's single Proxmox node into a two-node HA cluster on ZFS replication, with external QDevice quorum and a verified failover — now documented as a completed project with a full implementation series.

More details: https://eugeneivanov.dev/projects/two-node-proxmox-ha-cluster/

---

## 2026-06-22 — Rebuilding the lab's compute layer into a two-node Proxmox HA cluster

A capstone overview of turning a single Proxmox node into a two-node, ZFS-replicated HA cluster — the decisions behind it, the trade-offs, the verified failover, and where it sits in the wider lab.

More details: https://eugeneivanov.dev/journal/labnotes/two-node-proxmox-ha-cluster-rebuild/

---

## 2026-06-22 — Two-Node Proxmox HA with ZFS Replication and a Verified Failover

Made the two-node cluster genuinely highly available — rebalanced the guests across both nodes, set up bidirectional ZFS replication, enabled HA, and proved automatic failover with a real power-off test.

More details: https://eugeneivanov.dev/journal/labnotes/proxmox-2-node-ha-zfs-replication-failover/

---

## 2026-06-22 — The Proxmox Alert That Never Reached Me

A "spoofed" backup email led me to a node that had silently dropped a ZFS alert for fifteen hours — and to routing cluster notifications and system mail through an authenticated relay so the alerts that matter actually arrive.

More details: https://eugeneivanov.dev/journal/troubleshooting/proxmox-notifications-authenticated-email/

---

## 2026-06-21 — In-Place Reinstall of a Live Proxmox Cluster Node Without Losing Quorum

Reinstalled a live Proxmox cluster member in place on a ZFS mirror — evict, rebuild, rejoin, and restore the QDevice client a fresh install drops — without losing quorum.

More details: https://eugeneivanov.dev/journal/labnotes/in-place-reinstall-proxmox-cluster-node/

---

## 2026-06-21 — Live-migrating Proxmox VMs from LVM-thin to ZFS (and the thin-provisioning trap)

Emptied one node of my two-node Proxmox cluster by live-migrating all ten VMs from LVM-thin onto ZFS — and flipped the one storage flag that keeps the migrated disks thin instead of ballooning to full provisioned size.

More details: https://eugeneivanov.dev/journal/labnotes/proxmox-live-migrate-lvm-thin-to-zfs/

---

## 2026-06-20 — Off-node backups for Plausible (PostgreSQL + ClickHouse)

Added daily, off-node, restore-verified backups for Plausible CE — PostgreSQL via pg_dump and ClickHouse via native BACKUP/RESTORE, synced to a Synology NAS — then used that safety net to upgrade Plausible to v3.2.1.

More details: https://eugeneivanov.dev/journal/linux/backup-plausible-postgresql-clickhouse-synology-nas/

---

## 2026-06-20 — Cat6 camera run stuck at 100 Mbps: the crimper, not the cable

A garage camera linked at 100 Mbps with pins 7/8 open across three re-crimps per end and a full cable swap, but the cable tested perfect on bare copper — the culprit was a copper offcut jammed in the pass-through crimper die, blocking the 7/8 contacts.

More details: https://eugeneivanov.dev/journal/troubleshooting/cat6-stuck-100mbps-crimper-debris/

---

## 2026-06-15 — Off-Node Proxmox Backups to Synology, Verified by Restore

Backed up every guest in my two-node Proxmox cluster to a Synology over NFS and proved it by restoring a VM on the other node, before wiping anything.

More details: https://eugeneivanov.dev/journal/labnotes/offnode-proxmox-backups-synology-verified-restore/

---

## 2026-06-15 — An Independent, Restore-Tested DB-Dump Layer for Homelab VMs

Added a second backup layer — logical PostgreSQL and MariaDB dumps shipped off-node to a Synology — and verified each engine restores into a throwaway container.

More details: https://eugeneivanov.dev/journal/linux/offnode-db-dump-layer-homelab-vms/

---

## 2026-06-15 - A systemctl shim for non-systemd containers

Worked around "System has not been booted with systemd" by swapping systemctl for a stub script so pvecm qdevice setup runs inside a Docker container.

More details: https://eugeneivanov.dev/journal/linux/systemctl-shim-non-systemd-container/

---

## 2026-06-15 - External Proxmox QDevice on Synology in Docker

Ran corosync-qnetd in a custom container on the DS720+ over macvlan to give a 2-node cluster a third quorum vote.

More details: https://eugeneivanov.dev/journal/networking/proxmox-qdevice-synology-corosync-qnetd-docker/

---

## 2026-06-15 - Building a 2-node Proxmox cluster: FQDN and storage.cfg

Formed the pve1/pve2 cluster and hit two traps — set the FQDN before clustering, and join overwrites storage.cfg on the joining node.

More details: https://eugeneivanov.dev/journal/labnotes/proxmox-2-node-cluster-fqdn-storage-cfg/

---

## 2026-06-14 - Bootable ZFS RAID1 mirror across mismatched NVMe drives

Turned pve2's single-disk ZFS root into a bootable two-way mirror across mismatched drives (a 1 TB and a matching slice of a 2 TB), reclaiming the leftover space as a second pool.

More details: https://eugeneivanov.dev/journal/hardware/proxmox-zfs-raid1-mirror-mismatched-disks/

---

## 2026-06-14 - Second Proxmox node ready to join the cluster

Commissioned the second Dell Micro as node pve2 and turned its two mismatched NVMe drives into a bootable ZFS mirror, leaving it ready to join the cluster.

More details: https://eugeneivanov.dev/journal/hardware/proxmox-dell-cluster-node-prep/

---

## 2026-06-08 — New-Subscriber Email Notifications for Self-Hosted Listmonk

A cron-driven poller that emails you on every Listmonk signup, plus the API permissions that stop list names showing as *Unknown.

More details: https://eugeneivanov.dev/journal/linux/listmonk-new-subscriber-email-notifications/

---

## 2026-06-07 — A Self-Hosted Phone System (PBX) on a Multi-Node Home Lab

Planned a self-hosted PBX on Proxmox — a FreePBX brain with PoE Cisco IP phones, one shared SIP trunk, a dedicated voice VLAN, central provisioning, and monitoring — and wrote it up as a project with an architecture diagram.

More details: https://eugeneivanov.dev/projects/self-hosted-pbx-home-lab/

---

## 2026-06-06 — Fixing a Phantom “Unknown Error” on a Cisco 8861 MPP Phone

Tracked down a misleading firmware upgrade failure and cleared the phone’s first-boot activation prompt.

More details: https://eugeneivanov.dev/journal/troubleshooting/cisco-8861-mpp-firmware-upgrade-unknown-error/

---

## 2026-06-05 — Self-hosted newsletter is live

Stood up a self-hosted listmonk newsletter end to end — double opt-in signups from the site, authenticated delivery via Resend, public access through a Cloudflare Tunnel with the admin behind Zero Trust, plus local backups and monitoring.

More details: https://eugeneivanov.dev/journal/linux/self-hosted-newsletter-listmonk-resend-cloudflare-tunnel/

---

## 2026-06-01 — Private AI Inference Platform

Designed a multi-node local AI platform on Proxmox with a LiteLLM control plane, observability, NetBox, and WireGuard, and wrote it up as a site project.

More details: https://eugeneivanov.dev/projects/private-ai-inference-platform-home-lab/

---

## 2026-06-01 - Self-Hosted Website Audits with SiteOne Crawler and systemd

Built a dedicated Linux VM to run repeatable website audits with SiteOne Crawler, systemd automation, local reports, and optional Uptime Kuma monitoring.

More details: https://eugeneivanov.dev/journal/linux/self-hosted-website-audits-siteone-crawler-systemd/

---

## 2026-05-31 - Improved Proxmox Grafana dashboard readability

Fixed the Proxmox monitoring dashboard by replacing qemu VM IDs with readable VM names and correcting percentage scaling for storage and memory panels.

More details: https://eugeneivanov.dev/journal/troubleshooting/improving-proxmox-dashboard-readability-grafana/

---

## 2026-05-25 — Fixed Recurring GitHub Authentication Prompts with SSH

Resolved constant GitHub credential prompts across four repositories by diagnosing the root cause with git log and git remote, then replacing per-repo personal access tokens with a single dedicated SSH key, a scoped SSH config, and SSH-based remotes.

More details: https://eugeneivanov.dev/journal/troubleshooting/fixing-github-auth-with-ssh/

---

## 2026-05-24 — Planned a Self-Hosted Website Audit Crawler

Planned a dedicated SiteOne Crawler VM to run repeatable technical audits of the Hugo engineering journal, checking links, redirects, sitemap output, canonical rules, noindex behavior, and crawl quality.

More details: https://eugeneivanov.dev/projects/self-hosted-website-audit-crawler-for-hugo/

---

## 2026-05-23 - Planned a Self-Hosted Newsletter and RSS Automation System

Outlined a new infrastructure project to connect my Hugo engineering journal and project updates with a self-hosted listmonk VM, PostgreSQL, Amazon SES delivery, DNS authentication, backups, and monitoring.

More details: https://eugeneivanov.dev/projects/self-hosted-newsletter-and-rss-automation-system-for-hugo/

---

## 2026-05-22 - Updated Proxmox VE to 9.2.2

Completed a controlled Proxmox VE home lab maintenance window by upgrading from 9.1 to 9.2.2, rebooting the node, and validating that all VMs, storage targets, and package updates were healthy.

More details: https://eugeneivanov.dev/journal/linux/updating-proxmox-ve-from-9-1-to-9-2-2/

---

## 2026-05-22 — Applied RHCSA Linux Administration

Added a planned RHCSA-based project to build practical Linux administration depth after the networking foundation, focusing on operating, configuring, troubleshooting, and validating Linux systems in an infrastructure environment.

More details: https://eugeneivanov.dev/projects/applied-rhcsa-linux-administration/

---

## 2026-05-22 — Linux Networking for Infrastructure Troubleshooting

Added a planned follow-up project to deepen Linux networking skills after the CCNA foundation, focusing on server-side troubleshooting across interfaces, routes, DNS, ports, firewalls, Proxmox networking, and packet evidence.

More details: https://eugeneivanov.dev/projects/linux-networking-for-infrastructure-troubleshooting/

---

## 2026-05-21 - Planned Enterprise Linux Administration Lab on Proxmox

Defined a new Proxmox-based enterprise Linux lab project focused on RHEL administration, Oracle Linux comparison, SELinux, firewalld, systemd services, monitoring, and storage mount practice.

More details: https://eugeneivanov.dev/projects/enterprise-linux-administration-lab-on-proxmox/

---

## 2026-05-21 — Microsoft 365 Identity and Endpoint Administration Lab

Added a project to study Microsoft 365 as an enterprise platform for identity, access, collaboration services, security basics, and endpoint management.

More details: https://eugeneivanov.dev/projects/microsoft-365-identity-and-endpoint-administration-lab/

---

## 2026-05-20 — CCNA Foundation for Infrastructure Engineering

Defined a focused project to use CCNA not as a checkbox certification, but as a structured path for building networking thinking, packet-flow understanding, and stronger infrastructure troubleshooting skills.

More details: https://eugeneivanov.dev/projects/ccna-foundation-for-infrastructure-engineering/

---

## 2026-05-20 — Building a Cross-Platform Unity Workspace for a Beginner C# Programmer

Set up a clean Windows and macOS development workflow for a beginner Unity/C# programmer using GitHub as the source of truth, a proper Unity .gitignore, and a structured first project repository.

More details: https://eugeneivanov.dev/journal/labnotes/building-cross-platform-unity-workspace-for-beginner-csharp-programmer/

---

## 2026-05-16 - Planned Windows Server 2025 Infrastructure Lab

Planned a staged Windows Server 2025 infrastructure lab on Proxmox with Active Directory, DNS, Windows 11 domain clients, Group Policy, file services, and future Domain Controller redundancy.

More details: https://eugeneivanov.dev/projects/windows-server-2025-infrastructure-lab-on-proxmox/

---

## 2026-05-16 - Wireshark Packet Analysis Workflow

Defined a practical packet capture workflow for the home lab using Wireshark, tcpdump, and UniFi port mirroring to support evidence-based network troubleshooting.

More details: https://eugeneivanov.dev/projects/wireshark-packet-analysis-workflow/

---

## 2026-05-15 — Planned NetBox Source of Truth Implementation

Defined a project to deploy NetBox as the internal source of truth for documenting network devices, VLANs, IPAM, cabling, Proxmox virtualization, services, monitoring, and backup expectations in the home infrastructure lab.

More details: https://eugeneivanov.dev/projects/netbox-source-of-truth-implementation/

---

## 2026-05-12 - Troubleshooting Noisy Grafana Memory Alerts in a Proxmox Home Lab

Investigated noisy Grafana memory alerts, confirmed the VM had no real Linux memory pressure, and replaced the Proxmox memory-percentage alert with a more accurate node_exporter MemAvailable-based rule.

More details: https://eugeneivanov.dev/journal/troubleshooting/troubleshooting-noisy-grafana-memory-alerts-proxmox/

---

## 2026-05-11 — Building a Self-Hosted Observability Stack for a Home Lab

Published a high-level overview of the self-hosted observability stack, linking the full series covering Ubuntu VM preparation, Prometheus, Grafana, Node Exporter, Blackbox Exporter, Proxmox monitoring, dashboards, and alerting.

More details: https://eugeneivanov.dev/journal/labnotes/building-self-hosted-observability-stack-for-home-lab/

---

## 2026-05-11 — Configuring Grafana Alerts and Email Notifications with Proton SMTP

Configured Grafana alert rules and Proton SMTP email notifications for HTTP service availability, Proxmox objects, Node Exporter targets, disk usage, memory usage, and controlled DOWN/UP alert validation.

More details: https://eugeneivanov.dev/journal/labnotes/configuring-grafana-alerts-and-email-notifications-with-proton-smtp/

---

## 2026-05-11 — Organizing Grafana Dashboards for Home Lab Observability

Organized the Grafana dashboard layer into focused views for Linux VM metrics, HTTP service availability, Proxmox infrastructure health, and alert visibility across the home lab monitoring stack.

More details: https://eugeneivanov.dev/journal/labnotes/organizing-grafana-dashboards-for-home-lab-observability/

---

## 2026-05-10 — Adding Proxmox Monitoring with Prometheus PVE Exporter

Integrated Proxmox into the monitoring stack with a dedicated API user and token, Prometheus PVE Exporter, pve_up validation, and Grafana panels for node, VM, storage, disk, and memory metrics.

More details: https://eugeneivanov.dev/journal/labnotes/adding-proxmox-monitoring-with-prometheus-pve-exporter/

---

## 2026-05-10 — Monitoring HTTP Service Availability with Blackbox Exporter

Added HTTP service availability monitoring with Blackbox Exporter, Prometheus probe_success checks, Grafana UP/DOWN status panels, and validation for self-hosted lab services.

More details: https://eugeneivanov.dev/journal/labnotes/monitoring-http-service-availability-with-blackbox-exporter/

---

## 2026-05-10 — Monitoring Linux VMs with Node Exporter and Prometheus

Expanded the monitoring stack from a single monitoring VM to multiple Linux VMs using Node Exporter, UFW access control, Prometheus scrape targets, readable instance labels, and Grafana validation.

More details: https://eugeneivanov.dev/journal/linux/monitoring-linux-vms-with-node-exporter-and-prometheus/

---

## 2026-05-09 — Deploying Prometheus and Grafana on an Ubuntu Monitoring VM

Deployed the initial monitoring core with Prometheus, Grafana, and Node Exporter on an Ubuntu Server VM using Docker Compose, persistent volumes, Prometheus target validation, and a working Grafana datasource.

More details: https://eugeneivanov.dev/journal/labnotes/deploying-prometheus-and-grafana-on-ubuntu-monitoring-vm/

---

## 2026-05-09 — Preparing an Ubuntu Server VM for Docker-Based Infrastructure Services

Documented a repeatable Ubuntu Server VM baseline for Docker-based infrastructure services, including system validation, Docker installation, Docker Compose checks, project directory structure, and basic operational readiness.

More details: https://eugeneivanov.dev/journal/linux/preparing-ubuntu-server-vm-for-docker-infrastructure/

---

## 2026-05-08 - Custom 404 Page with Correct Nginx Error Handling

Built a branded Hugo 404 page and configured production Nginx behavior so missing routes preserve HTTP 404 status while displaying the custom error page.

More details: https://eugeneivanov.dev/journal/troubleshooting/custom-404-page-hugo-nginx-cloudways/

---

## 2026-05-07 - Self-Hosted Matomo Analytics with Docker and Cloudflare Tunnel

Deployed Matomo on a dedicated Ubuntu VM with Docker Compose and MariaDB, exposed it through Cloudflare Tunnel, added the tracking code to the site, and configured both VM-level and database-level backups.

More details: https://eugeneivanov.dev/journal/linux/matomo-self-hosted-docker-cloudflare-tunnel/

---

## 2026-05-07 - Self-Hosted Plausible Analytics Deployment

Deployed Plausible Community Edition on Ubuntu Server using Docker Compose and Cloudflare Tunnel with realtime analytics successfully tracking live traffic.

More details: https://eugeneivanov.dev/journal/linux/plausible-self-hosted-docker-cloudflare-tunnel/

---

## 2026-05-06 — Updated Umami Analytics Stack to Version 3.1

Updated the self-hosted Umami analytics stack on Ubuntu with Docker Compose, verified database migrations, validated realtime tracking, and confirmed analytics collection across multiple devices and operating systems.

More details: https://eugeneivanov.dev/journal/linux/updating-umami-to-version-3-1/

---

## 2026-05-06 — Fixed Proxmox Enterprise Repository Update Errors

Investigated repeated apt update failures in Proxmox, identified unauthorized enterprise repositories as the root cause, migrated the node to the no-subscription repository, and restored normal package update operation.

More details:  https://eugeneivanov.dev/journal/troubleshooting/fixing-proxmox-enterprise-repository-errors/

---

## 2026-04-25 - Defining My CCNA Preparation Stack

A short lab note on how I structured my CCNA preparation around a primary path, delayed reinforcement, and practical lab work without turning the process into unnecessary duplication.

More details: https://eugeneivanov.dev/journal/labnotes/defining-my-ccna-preparation-stack/

---

## 2026-04-24 - Protecting the First Cognitive Block of the Day

A short note on why I now keep the first work block of the day for learning and move heavier operational and execution tasks later.

More details: https://eugeneivanov.dev/journal/labnotes/protecting-the-first-cognitive-block-of-the-day/

---

## 2026-04-17 - The real goal of automation

The goal is not simply moving from GUI to CLI, but moving from touching one thing at a time toward controlling the whole estate.

More details: https://eugeneivanov.dev/journal/labnotes/follow-up-that-clarified-the-real-goal-of-automation/

---

## 2026-04-16 - Rethinking VLANs, automation, and the next stage of my home lab

A useful conversation with a Senior Systems Engineer helped me sharpen how I think about VLAN boundaries, reproducible infrastructure, automation, cloud, and the right build order for the next stage of my lab.

More details: https://eugeneivanov.dev/journal/labnotes/rethinking-vlans-automation-and-home-lab/

---

## 2026-04-15 - DNS, CCNA, and a better learning loop

Returned to Google IT Support, saw the need for a dedicated DNS server in my lab, and confirmed that pairing structured study with deeper CCNA reading is the best fit for how I learn and turn new knowledge into infrastructure decisions.

More details: https://eugeneivanov.dev/journal/labnotes/from-dns-to-ccna-a-better-learning-loop/

---

## 2026-04-12 - Tailscale ACL for Minecraft Access Control

Implemented controlled remote access to a private Minecraft server using Tailscale ACLs, transitioning from open network trust to explicit, group-based access rules.

More details: https://eugeneivanov.dev/journal/networking/tailscale-acl-minecraft-access-control/

---

## 2026-04-11 - Stabilizing a Proxmox Host That Stayed Powered On but Dropped Off the Network

Documented how I diagnosed an intermittent Proxmox network hang, confirmed a temporary fix by disabling NIC offloading, and then made the solution persistent after 120 hours of stability.

More details: https://eugeneivanov.dev/journal/troubleshooting/proxmox-host-powered-on-but-offline-nic-offloading-fix/

---

## 2026-04-11 - Roadmap Expanded with Certifications and Reading

I updated my infrastructure roadmap to include a focused certification path and a core technical reading library to support deeper systems thinking and long-term architectural growth.

More details: https://eugeneivanov.dev/roadmap/

---

## 2026-04-10 - Roadmap Reframed

I restructured my infrastructure engineering roadmap to reflect a clearer long-term direction from hands-on systems work toward architecture, resilience, and complex environment design.

More details: https://eugeneivanov.dev/roadmap/

---

## 2026-04-06 — Fixed Umami tracking issue caused by invalid HTML in Hugo

Resolved a silent analytics failure by identifying a missing closing script tag that broke tracking despite a fully working backend and tunnel.

More details: https://eugeneivanov.dev/journal/troubleshooting/umami-not-tracking-hugo-cloudflare-tunnel/

---

## 2026-04-06 - Minecraft Server with Python Integration

Built and validated a self-hosted Minecraft server with remote access, systemd management, backups, and Python control via RaspberryJuice.

More details: https://eugeneivanov.dev/journal/linux/minecraft-server-proxmox-tailscale-python/

---

## 2026-04-04 - Synology NAS VLAN Migration Troubleshooting

Diagnosed and resolved NAS inaccessibility after VLAN migration, identifying improper shutdown as the root cause rather than a network issue.

More details: https://eugeneivanov.dev/journal/troubleshooting/troubleshooting-synology-nas-vlan-unifi/

---

## 2026-04-03 — Productionizing Umami Analytics with Backup and Recovery

Deployed a self-hosted analytics stack with Cloudflare Tunnel and automated Proxmox backups, turning it into a secure and fully recoverable system.

More details: https://eugeneivanov.dev/journal/linux/umami-cloudflare-tunnel-proxmox-backup/

---

## 2026-03-30 — From Linux to System Thinking

Moved from “learning Linux” to designing a role-based home lab architecture with analytics, monitoring, access, and identity.

More details: https://eugeneivanov.dev/journal/labnotes/home-lab-architecture-from-linux-to-system-thinking/

---

## 2026-03-29 — First Ubuntu Server Deployment in Home Lab

Deployed my first Ubuntu Server VM on Proxmox with static IP, SSH key authentication, and initial system validation.

More details: https://eugeneivanov.dev/journal/linux/first-linux-server-ubuntu-proxmox-installation/

---

## 2026-03-29 — Proxmox First Node Installation Completed

Deployed my first Proxmox VE node on a Dell Micro system with proper BIOS update, storage configuration, and VLAN-based network integration.

More details: https://eugeneivanov.dev/journal/hardware/proxmox-first-node-installation/

---

## 2026-03-28 - Philips Hue VLAN Troubleshooting

Restored Hue after VLAN move by renewing DHCP, assigning fixed IPs, adding a targeted firewall rule, and enabling mDNS.

More details: https://eugeneivanov.dev/journal/troubleshooting/troubleshooting-philips-hue-iot-vlan-unifi/

---

## 2026-03-24 - Correction: Why I Abandoned the Upgrade Path for My First Compute Node 
 
Validated hardware limitations of a Dell Micro system, abandoned upgrade-based strategy, and shifted to a fixed 64GB baseline configuration.  

More details: https://eugeneivanov.dev/journal/hardware/compute-node-upgrade-correction/


---

## 2026-03-20 - Troubleshooting UniFi 10G Link: SFP+ to RJ45

Diagnosed a 1GbE fallback caused by an SFP+ to 2.5G RJ45 negotiation mismatch and restored a stable 10GbE link using SFP+ modules on both ends.

More details: https://eugeneivanov.dev/journal/troubleshooting/unifi-10g-sfp-rj45-mismatch/

---

## 2026-03-19 — Quarantine Network & Port Isolation (UniFi)

Designed and implemented a quarantine VLAN with Layer 3 firewall rules to isolate untrusted devices and convert unused switch ports into controlled, low-trust entry points.

More details: https://eugeneivanov.dev/journal/networking/quarantine-network-unifi/

---

## 2026-03-18 — Home Network Segmentation (VLANs, WiFi, Firewall)

Implemented VLAN-based segmentation with UniFi, configured multiple WiFi networks and firewall rules to isolate traffic and secure the home lab

More details: https://eugeneivanov.dev/journal/networking/home-network-segmentation/

---

## 2026-03-18 — Troubleshooting UniFi WAN Failover After Switching to SFP+  

Resolved a false WAN failover event caused by incorrect WAN role assignment after moving the primary connection to SFP+.  

More details: https://eugeneivanov.dev/journal/troubleshooting/unifi-wan-failover-after-sfp-switch/

---

## 2026-03-18 — Role-Based Access in UniFi

Implemented and documented role-based access in my UniFi home lab by separating Owner and Site Admin responsibilities to apply least privilege in daily operations.

More details: https://eugeneivanov.dev/journal/labnotes/role-based-access-unifi/

---

## 2026-03-18 — 8 Gbps Home Network Validation

Validated an 8 Gbps home network build using Google Fiber and UniFi stack. Achieved near line-rate performance with low latency after physical layer adjustments and manual tuning.

More details: https://eugeneivanov.dev/journal/networking/8gbps-home-network-unifi-google-fiber/

---

## 2026-03-18 - Umami

Planned deployment of Umami (self-hosted analytics) on the Dell node after completing the Linux setup. Chosen for its lightweight, privacy-focused design and to gain hands-on experience deploying a real service. It will serve as the first production-like service in the home lab.

More details: https://eugeneivanov.dev/journal/labnotes/role-based-access-unifi/

---

## 2026-03-17 — Selecting a Compute Node for the Home Infrastructure Lab

Documented compute node selection for home lab. Prioritized architecture and scalability over maximum initial specs.

More details: https://eugeneivanov.dev/journal/hardware/compute-node-selection/

---

## 2026-03-10 — Assembling the Home Lab Rack

Assembled the rack and revised the layout to properly fit the NAS, UPS, and rack shelves.

More details: https://eugeneivanov.dev/journal/hardware/home-lab-rack-assembly/

---

## 2026-03-07 — Installing Home Lab Rack and Patch Panel

Installed the rack patch panel and terminated the house Ethernet cabling.

More details: https://eugeneivanov.dev/journal/hardware/home-lab-rack-patch-panel-installation/

---

## 2026-03-06 — Installing Wall-Mounted Rack

Installed a StarTech 12U wall-mounted rack with a plywood backboard anchored to wall studs.  
Prepared mounting surface for switches, NAS, and UPS.

More details: https://eugeneivanov.dev/journal/hardware/network-rack-backboard/

---

## 2026-03-05 — Planning Home Lab Rack Equipment

Designed the rack layout and selected networking, compute, and power infrastructure components.

More details: https://eugeneivanov.dev/journal/hardware/home-lab-rack-equipment-planning/

---

## 2026-03-05 — Testing Home Ethernet Cabling

Tested existing Ethernet wiring using a Klein Tools VDV501-851 cable tester.  
Verified cable map, continuity, and wiring order for multiple wall ports.

More details: https://eugeneivanov.dev/journal/networking/home-network-cable-testing/
