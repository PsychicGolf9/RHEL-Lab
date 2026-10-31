# Notes for Cold-Build

## Process Summary

- Boot Rocky/RHEL ISO as VM or on bare metal.
- Take specific note of WLAN interface name when setting hostname. This is
  literally the only variable that is mandatory and can't be found afterwards
  without SSH.
- Defaults for everything, except:
  - Select "Encrypt My System" or whatever to enable LUKS. If you want TPM,
    You must do that now, because it's a pain later.
  - Choose minimal install... Unless you really want a GUI for a headless
    system.
- Make sure to lock the root account
- Whatever username you type in, make sure it's in your group_vars for
  later. Make them an administrator by hitting the toggle and set a
  password that you don't mind entering a bunch of times and will remember.
- Do the VERY EXTREMELY IMPORTANT PART now. See below.
- Fill out the bash_inventory found in scripts/
- Run the scripts/ directory in this order:
  1. wg_setup.sh
  2. luks_passphrase.sh
  3. ansible_run_log.sh

**Note:** You don't have to us the ansible_run_log.sh script, it's just a good
      thing to have for the docs.

## THE VERY EXTREMELY IMPORTANT PART

Make sure you run ssh-keygen for at very least the ansible user. You can run
it for yourself too, but managing a cluster with a ton of different keys for
your admin user is a huge pain.

You MUST ssh-copy-id or scp your human user keys to the node now! You'll
probably get locked out later if you don't. No one likes going into the console
without needing to.

You need to add the \[Peer\] section in your control machine's WireGuard
config.

Make note of the location for the ansible user's public key and put it in
host_vars.

Also make sure you ssh in manually at least once to confirm the fingerprint.

As much of this as possible will be automated in the future.

### Issues On First Run

- WG is broken.
  - I think it's a key thing with making the service user. Try again tomorrow.
  - SSH works over LAN IP. Check wg0.conf to make sure it was configured
    correctly. Might also be firewall.
  - wg0.conf didn't have the \[Peer\] listed in the control node's config.
  - firewall-cmd --list-all doesn't show the WG port and UDP.
  - Both are corrected and connection is successful.
  - Turned out to be a firewall problem with not ansible-lab02_ed25519owing the
    WireGuard port on UDP. The WireGuard role will be ammended to correct this.
  - 00-bootstrap.yml should also be ammended to check for successful connection
    over the tunnel before exiting 0.

## Going Forward

After the WireGuard role is updated to fix the firewall bug, rhel-lab02 will be
wiped, re-installed, and the playbooks will be run again. When all playbooks
complete successfully and idempotently, they will be promoted to rhel-lab01.
