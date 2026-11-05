# Rocky Linux Homelab

## Overview

**This repository documents my development from being a proficient Arch Linux
CLI user into a Linux systems administrator as I learn the industry-standard
tools and practices of modern infrastructure engineering. Failures are kept and
documented as much as possible to showcase the ongoing learning process.**

## Learning Objectives

- Git version control and GitHub
- Idempotent Bash scripting
- Architecture design and development
- Ansible
- Terraform
- CI/CD pipelines and GitHub Actions
- Enterprise-level security and secret management
- Containerization
- Kubernetes orchestration
- Monitoring, alerts, and triage
- Backup and recovery protocols

I began this project with a good understanding of CLI tools that are ubiquitous
to Linux systems, OS installation, troubleshooting, and a basic understanding
of networking. I plan on learning these professional tools and concepts through
self-directed study and by trial and error. An actively maintained table of my
learning progress is at the end of this section. The levels are delineated by
these standards:

- **Not Started:** I have not worked with it yet.
- **Basic:** I understand the purpose, but need substantial guidance.
- **Intermediate:** I can write the required configuration by following
  generalized examples.
- **Advanced:** I can configure it independently and only need occasional
  reference material.

| Tool/Concept | Not Started | Basic | Intermediate | Advanced |
| ------------ | ----------- | ----- | ------------ | -------- |
| Git | | | X | |
| Bash | | | X | |
| Architecture | | X | | |
| Ansible | | | X | |
| Terraform | X | | | |
| CI/CD | | X | | |
| Security | | | X | |
| Containerization | X | | | |
| Kubernetes | X | | | |
| Monitoring | X | | | |
| Recovery | | X | | |

## Documentation

The [docs](docs/) directory lays out the changes, failures and successful
implementations as the repository grows. The ansible_run_log.sh script found at
[scripts](scripts/) captures detailed logs of playbook runs and `systemd`
service verification. An overview index is as follows:

- [adr](docs/adr/) Explains architecture design decisions as they're made.
- [ansible](docs/ansible/) Shows the output from the script mentioned above.
  Each subdirectory has notes on failure troubleshooting and patching.
- [manual](docs/manual/) The manual build history is preserved in
  [docs/manual/README.md](docs/manual/README.md). It records the changes made
  to rhel-lab00 before Ansible automation was introduced.

## Architecture

The design of this project is geared towards replicating enterprise systems as
closely as possible, given my hardware constraints. Rocky Linux is chosen
because it is a free, RHEL-compatible distribution that provides a practical
environment for learning RHEL administration. Tools are chosen to be as close
as possible or identical to what is used in the industry. The lab currently
consists of:

- One physical node with Rocky on bare metal
- One persistent staging VM
- One ephemeral VM for testing playbooks against cold-built nodes.

### Constraints

- All machines are on WLAN until cabling can be routed to their location.
- The workstation machine currently only has enough compute power to run one
  VM at a time.
- There is currently no NAS or shared storage.
- All machines are on a power grid that suffers from frequent power outages.
