# TODO

## Playbook: 00-bootstrap.yml

- [ ] **WireGuard host_key_checking prevents successful completion.**

Task \[Wait for SSH over tunnel\] currently fails if host_key_checking is
enabled on control machine.

### Planned Fix

Automate accepting the fingerprint on first run **before** the task \[Wait...\]

### Current State/Workaround

- Expect one failure on cold-build
- SSH through tunnel manually once to accept fingerprint
- Run again to show `changed=0`
