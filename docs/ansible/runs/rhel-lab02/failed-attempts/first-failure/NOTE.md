# Issues On First Run

- WG is broken.
  - I think it's a key thing with making the service user.
  - SSH works over LAN IP. Check wg0.conf to make sure it was configured
    correctly. Might also be firewall.
  - wg0.conf didn't have the \[Peer\] listed in the control node's config.
  - firewall-cmd --list-all doesn't show the WG port and UDP.
  - Both are corrected and connection is successful.
  - Turned out to be a firewall problem with not allowing the
    WireGuard port on UDP. The WireGuard role will be ammended to correct this.
  - 00-bootstrap.yml should also be ammended to check for successful connection
    over the tunnel before exiting 0.

## Going Forward

After the WireGuard role is updated to fix the firewall bug, rhel-lab02 will be
wiped, re-installed, and the playbooks will be run again. When all playbooks
complete successfully and idempotently, they will be promoted to rhel-lab01.
