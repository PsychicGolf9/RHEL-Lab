# Documentation Index

This index links to every Markdown document in the repository, grouped by its
purpose.

## Project Overview

| Document | Description |
| --- | --- |
| [Project overview](README.md) | Explains the lab’s purpose, learning objectives, documentation layout, architecture, and constraints. |

## Architecture Decisions

| Document | Description |
| --- | --- |
| [LAN bootstrap decision](docs/adr/lan_shoehorn.md) | Records why the bootstrap role temporarily overrides `ansible_host` while establishing reachability. |

## Ansible Documentation

| Document | Description |
| --- | --- |
| [Service-user setup](docs/ansible/Service%20User/Creating%20Service%20User.md) | Documents the manual creation and SSH setup of the Ansible service user. |
| [Bootstrap failure post-mortem](docs/ansible/runs/rhel-lab00/00-bootstrap/failed-attempts/2026-10-25T18:57:10Z-first_POST-MORTEM.md) | Analyzes an early bootstrap idempotence failure, its root cause, and the corrective process. |
| [Baseline failure analysis](docs/ansible/runs/rhel-lab00/01-base/README.md) | Summarizes failed TPM2 and baseline automation attempts against the existing staging node. |

## Node Run Evidence

### `rhel-lab01`

| Document | Description |
| --- | --- |
| [Bootstrap follow-up note](docs/ansible/runs/rhel-lab01/00-bootstrap/NOTE.md) | Records the remaining first-run WireGuard host-key verification issue and its planned fix. |
| [Reboot validation](docs/ansible/runs/rhel-lab01/Reboot_Test.md) | Records that the promoted node returned after reboot and remained reachable over WireGuard SSH. |

### `rhel-lab02`

| Document | Description |
| --- | --- |
| [Cold-build procedure](docs/ansible/runs/rhel-lab02/README.md) | Explains the fresh-node build process, required input, SSH enrollment, and helper-script workflow. |
| [First cold-build failure](docs/ansible/runs/rhel-lab02/failed-attempts/first-failure/NOTE.md) | Records the initial cold-build problems and the changes planned before the next attempt. |
| [Second-run overview](docs/ansible/runs/rhel-lab02/failed-attempts/second-failure/01-base/NOTE.md) | Explains the separate TPM-disabled and TPM-enabled test runs and their evidence directories. |
| [TPM-disabled failure hypothesis](docs/ansible/runs/rhel-lab02/failed-attempts/second-failure/01-base/tpm_false/NOTE.md) | Records the host-key verification failure and the expected behavior before rerunning the playbook. |
| [TPM enrollment failure analysis](docs/ansible/runs/rhel-lab02/failed-attempts/second-failure/01-base/tpm_true/NOTE.md) | Documents TPM availability, invalid enrollment syntax, and the initramfs filename issue found during testing. |

## Manual Build History

| Document | Description |
| --- | --- |
| [Manual build history](docs/manual/README.md) | Preserves the original day-by-day Rocky Linux installation, hardening, networking, and Ansible transition notes. |

## Manual Troubleshooting Records

| Document | Description |
| --- | --- |
| [Wireless network recovery](docs/manual/troubleshooting/Lab01%20Network%20Failure/Lab01%20Network%20Failure.md) | Documents recovery from missing wireless packages and restoring network access on the physical node. |
| [Wireless idle disconnect](docs/manual/troubleshooting/Lab01%20Network%20Disconnect/Lab01%20Network%20Disconnect.md) | Documents the investigation and resolution of intermittent WLAN disconnects after idle periods. |
| [TPM boot failure](docs/manual/troubleshooting/TPM%20Boot%20Failure/TPM%20Boot%20Failure.md) | Documents recovery from a failed TPM-backed LUKS boot configuration. |
| [Firewalld reconfiguration](docs/manual/troubleshooting/firewalld/Reconfiguring%20Firewalld.md) | Documents the firewall and WireGuard interface configuration issue that could have caused SSH lockout. |

## Helper Scripts

| Document | Description |
| --- | --- |
| [Helper-script guide](scripts/README.md) | Explains the repository scripts used to prepare variables, configure nodes, and capture Ansible run evidence. |
